# SPI Flash


Configure macro definition of CONFIG_MTD_SERIAL_NAND to y in arch/armconfigs/mdm9607-perf
_defconfig and arch/arm/configs/mdm9607_defconfig. This option will open support function of SPI 
Nand

Add Toshiba spi flash driver under the premise of opening spi nand, this driver is provided by Toshiba 
(TC58CVG2S0HxS0HxAIx) manufacturer, and then integrated it into the Linux system to make Linux 
support this spi flash. Drivers of different spi flash models are different, but adding process keeps the 
same, perform the same adaptation according to different models. 

Add the related attributes of the spi flash sub-node to the device tree. Different types of spi flash have 
different attributes. User can modify the corresponding attributes according to the chip manual, as shown 
in the following figure. 



    &spi_1 {
            status = "okay";

            nand_flash: flash@0 {
                    compatible = "spi-nand";
                    reg = <0>;
                    spi-max-frequency = <50000000>;
                    partitions {
                            compatible = "fixed-partitions";
                            #address-cells = <1>;
                            #size-cells = <1>;

                            partition@0 {
                                    label = "applications0";
                                    reg = <0x00000000 0x04000000>; // 64 MB partition                        
                            };

                            partition@1 {
                                    label = "applications1";
                                    reg = <0x04000000 0x04000000>; // 64 MB partition                        
                            };

                            partition@2 {
                                    label = "sounds";
                                    reg = <0x08000000 0x04000000>; // 64 MB partition
                            };

                            partition@3 {
                                    label = "customer";
                                    reg = <0x0C000000 0x04000000>; // 64 MB partition
                            };
                    };
            };


Please also add

    CONFIG_MTD_SPI_NAND=y





