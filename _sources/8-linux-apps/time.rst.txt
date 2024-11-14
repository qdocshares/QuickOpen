=======================================
System Time
=======================================


QuecOpen supports an automatic system time synchronization and time source supports 
NITZ, GNSS and NTP. 
 
NITZ: NITZ is a timing service provided by the operators specialized for mobile communication devices. 
Operator base station takes the initiative to send this service to mobile devices. At present, Operators are 
still not able to confirm whether all base stations support NITZ timing service. The premise condition for 
obtaining this time is that there are supports from the base station and the device can make a normal 
network registration. 
 
GNSS: UTC time can be obtained after a successful GNSS positioning. The premise condition for 
obtaining this time is to call API related to GNSS within QuecOpen and successful positioning  
 
NTP: NTP is a network protocol used to synchronize computer clocks on the Internet. It allows devices to 
synchronize its time with that of NTP servers. The prerequisite for obtaining this time is that the device 
can access the Internet. When performing NTP time synchronization, it will access the Internet and 
generate a little amount of traffic. 
 
The module contains a hardware RTC (device file /dev/rtc0). Power will not be supplied to 
RTC separately. When the module is powered off, it can continue to work for a short time (Its power was 
supplied by an external capacitor. The working time depends on the capacitor capacity and usually it will 
last less than one minute time. When the capacitor capacity is exhausted, the RTC will reset). Both 
system soft restart and hard restart can ensure that RTC continues to work. The RTC is a restricted RTC 
and it should not be manipulated.



Set the time manually
----------------------

.. code-block:: 

    /var/volatile/tmp # echo "user: 1514768470000" > ql_time_set_pipe
    /var/volatile/tmp # date
    Mon Jan  1 09:01:12 CST 2018

Set the time via NTP
---------------------


/etc/ql_time_conf.json



.. code-block::

    {
            "sync_accuracy_ms":2000,
            "modem_sync_enable":1, // NITZ time from modem
            "gnss_sync_enable":1,  // UTC time from GNSS
            "ntp_sync_policy":"assist", // valid policy: assist, normal
            "ntp_server_probe_interval_ms":2000,
            "ntp_server_probe_retry_count":2,
            "ntp_failed_retry_interval_s":300,
            "ntp_resync_interval_s":86400, // one day
            "ntp_server_list" : [
                "pool.ntp.org",
                "0.pool.ntp.org",
                "1.pool.ntp.org",
                "cn.ntp.org.cn",
                "cn.pool.ntp.org",
                "us.ntp.org.cn",
                "de.ntp.org.cn"
            ]
        }



Time Zone
---------------

Timezone is set according to the GLIBC. So the timezone is set in /etc/localtime by default.

Copy the timezone file, eg, /usr/share/zoneinfo/Asia/Shanghai, from the Ubuntu to the device /etc/localtime.







