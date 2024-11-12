# usbmon



The name “usbmon” in lowercase refers to a facility in kernel which is used to collect traces of I/O on the USB bus. This function is analogous to a packet socket used by network monitoring tools such as tcpdump(1) or Ethereal. Similarly, it is expected that a tool such as usbdump or USBMon (with uppercase letters) is used to examine raw traces produced by usbmon.

The usbmon reports requests made by peripheral-specific drivers to Host Controller Drivers (HCD). So, if HCD is buggy, the traces reported by usbmon may not correspond to bus transactions precisely. This is the same situation as with tcpdump.

Two APIs are currently implemented: “text” and “binary”. The binary API is available through a character device in /dev namespace and is an ABI. The text API is deprecated since 2.6.35, but available for convenience.



## reference

https://docs.kernel.org/usb/usbmon.html


