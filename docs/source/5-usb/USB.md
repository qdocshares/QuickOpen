# USB Driver

      Can be mapped into several different functional interfaces.
       - USB-AT port
       - USB-DM port
       - USB-NMEA port
       - USB-Modem port
       - USB-Network adapter 

In QuecOpen, the GNSS NMEA is outputted to applications through a virtual serial port  (/dev/smd7).

USB Design Suggestions:
- For downloading → DM port
- For Capturing system log→ DM port
- For debugging → ADB port
- For USB data channel→ /dev/ttyGS0


## Add USB virtual port


    diff -uprN ql-ol-sdk_ori/ql-ol-kernel/drivers/usb/gadget/android.c ql-ol-sdk/ql-ol-kernel/drivers/usb/gadget/android.c
    --- ql-ol-sdk_ori/ql-ol-kernel/drivers/usb/gadget/android.c	2019-02-22 15:04:37.000000000 +0800
    +++ ql-ol-sdk/ql-ol-kernel/drivers/usb/gadget/android.c	2019-06-04 18:53:04.325676077 +0800
    @@ -2020,7 +2020,7 @@ static struct android_usb_function qdss_
     };
     
     /* SERIAL */
    -#define MAX_SERIAL_INSTANCES 4
    +#define MAX_SERIAL_INSTANCES 5
     struct serial_function_config {
        int instances_on;
        struct usb_function *f_serial[MAX_SERIAL_INSTANCES];
    diff -uprN ql-ol-sdk_ori/ql-ol-kernel/drivers/usb/gadget/function/f_serial.c ql-ol-sdk/ql-ol-kernel/drivers/usb/gadget/function/f_serial.c
    --- ql-ol-sdk_ori/ql-ol-kernel/drivers/usb/gadget/function/f_serial.c	2019-02-22 15:04:37.000000000 +0800
    +++ ql-ol-sdk/ql-ol-kernel/drivers/usb/gadget/function/f_serial.c	2019-06-04 18:56:52.535903240 +0800
    @@ -44,7 +44,7 @@
     #define GSERIAL_SET_XPORT_TYPE_SMD 1
     
     #define GSERIAL_BUF_LEN  256
    -#define GSERIAL_NO_PORTS 3
    +#define GSERIAL_NO_PORTS 4
     
     struct ioctl_smd_write_arg_type {
        char		*buf;
    @@ -330,12 +330,16 @@ int gport_setup(struct usb_configuration
        pr_debug("%s: no_tty_ports: %u no_smd_ports: %u no_hsic_sports: %u nr_ports: %u\n",
            __func__, no_tty_ports, no_smd_ports, no_hsic_sports, nr_ports);
     
    +    /* add usb channel */
        if (no_tty_ports) {
    -		for (i = 0; i < no_tty_ports; i++) {
    -			ret = gserial_alloc_line(
    +		for (i = 0; i < GSERIAL_NO_PORTS; i++) {
    +            if (gserial_ports[i].transport == USB_GADGET_XPORT_TTY)
    +            {
    +			    ret = gserial_alloc_line(
                        &gserial_ports[i].client_port_num);
    -			if (ret)
    -				return ret;
    +			    if (ret)
    +				    return ret;
    +            }
            }
        }
     
    diff -uprN ql-ol-sdk_ori/ql-ol-rootfs/sbin/usb/compositions/9025 ql-ol-sdk/ql-ol-rootfs/sbin/usb/compositions/9025
    --- ql-ol-sdk_ori/ql-ol-rootfs/sbin/usb/compositions/9025	2019-02-22 16:01:26.000000000 +0800
    +++ ql-ol-sdk/ql-ol-rootfs/sbin/usb/compositions/9025	2019-06-04 18:51:44.274980430 +0800
    @@ -107,6 +107,7 @@ run_9607() {
        QUEC_USB_VID=2C7C
        QUEC_ENABLE_USB=0
        QUEC_USB_NET_TYPE="rmnet"
    +    QUEC_USB_TTYGS1=1
        QUEC_MANUFCTURE="Quectel, Incorporated"
         QUEC_PRODUCTINFO="LTE Module"
        usb_dir="/data/usb"
    @@ -190,7 +191,12 @@ run_9607() {
        echo 239 > /sys/class/android_usb/android$num/bDeviceClass
        echo 2 > /sys/class/android_usb/android$num/bDeviceSubClass
        echo 1 > /sys/class/android_usb/android$num/bDeviceProtocol
    -	echo $SERIAL_FUNC > /sys/class/android_usb/android0/f_serial/transports
    +    #juson.zhang-2019/06/04:add usb channel
    +    if [ $QUEC_USB_TTYGS1 -eq 0 ];then
    +	    echo $SERIAL_FUNC > /sys/class/android_usb/android0/f_serial/transports
    +    else
    +        echo $SERIAL_FUNC,tty > /sys/class/android_usb/android0/f_serial/transports
    +    fi
        echo QTI,BAM_DMUX > /sys/class/android_usb/android0/f_rmnet/transports
        echo BAM_DMUX > /sys/class/android_usb/android0/f_usb_mbim/mbim_transports
        echo $USB_FUNC,ffs > /sys/class/android_usb/android$num/functions




