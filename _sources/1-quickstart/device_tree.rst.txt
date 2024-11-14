======================================
Device Tree
======================================


Given the correct device tree, the same compiled kernel can support different hardware configurations within a wider architecture family. This can be seen as a remedy to the vast number of forks (of Linux and Das U-Boot) that have historically been created to support (marginally) different ARM boards. The purpose is to move a significant part of the hardware description out of the kernel binary, and into the compiled device tree blob, which is handed to the kernel by the boot loader, replacing a range of board-specific C source files and compile-time options in the kernel.

It is specified in a Devicetree Source file (.dts) and is compiled into a Devicetree Blob or device tree binary (.dtb) file through the Devicetree compiler (DTC). Device tree source files can include other files, referred to as device tree source includes.

It has been customary for ARM-based Linux distributions to include a boot loader, that necessarily was customized for specific boards. This has created problems for the creators of Linux distributions as some part of the operating system must be compiled specifically for every board variant, or updated to support new boards. 
However, some modern SoCs have a vendor-provided boot loader with device tree on a separate chip from the operating system.


Device Tree API
-----------------------------------

https://elixir.bootlin.com/linux/v4.5/source/include/linux/of.h

.. code-block:: c
   :linenos:
   :emphasize-lines: 1, 4


    int of_property_read_u32_index(const struct device_node *np,
                                  const char *propname,
                                  u32 index,
                                  u32 *out_value);






Reference Doc
------------------------------------


[kernel doc device tree](https://elixir.bootlin.com/linux/v3.18.140/source/Documentation/devicetree)

