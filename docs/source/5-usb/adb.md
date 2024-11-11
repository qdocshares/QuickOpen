# ADB

## How To Enable ADB

ql-ol-rootfs/sbin/usb/compositions/9025

    echo "diag,serial,rmnet,ffs" > /sys/class/android_usb/android$num/functions

And need to make the rootfs.

Or you can set it with AT command

    AT+QCFG="usbcfg",0x2C7C,0x0125,1,1,1,1,1,1,0

It take effect after reboot.

## adb connect detect devices

~/.android/adb_usb.ini

Add the

    0x2C7C

It support for both Windows and Ubuntu.



## adb permissions 

 $ adb root
error: insufficient permissions for device

Solutions:

sudo vi /etc/udev/rules.d/70-android.rules

        SUBSYSTEM=="usb", ATTRS{idVendor}=="2c7c", ATTRS{idProduct}=="0125", MODE="0666"


sudo service udev restart
sudo udevadm control --reload-rules
sudo service udev restart
sudo udevadm trigger
adb kill-server
adb start-server



