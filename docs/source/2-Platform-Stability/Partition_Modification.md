# Partition_Modification


The partition.mbn file is the partition table flashed to the module, located in the \update directory of the 
firmware package. To generate this file, use the partition_nand.xml configuration file found in the same 
directory. When adjusting partition(s), replace the XML file with the identical name in the SDK with the one
in the firmware package before making any modifications. The content of the configuration file is shown
below

    
    <nandboot>
            <magic_numbers>
                    <usr_part_magic1>0xAA7D1B9A</usr_part_magic1>
                    <usr_part_magic2>0x1F7D48BC</usr_part_magic2>
            </magic_numbers>
            <partition_version length="4">0x4</partition_version>
            <partitions>
            ...
                    <partition>
                            <name length="16" type="string">0:sys_back</name>
                            <size_kb length="4">58880</size_kb>
                            <pad_kb length="4">512</pad_kb>
                            <which_flash>0</which_flash>
                            <attr>0xFF</attr>
                            <attr>0x01</attr>
                            <attr>0x00</attr>
                            <attr>0xFF</attr>
                            <img_name type="string">mdm9607-perf-sysfs.ubi</img_name>
                    </partition>
            ...
            </partitions>
    </nandboot>


| Tag | Description | Description |
|--- | --- | --- |
|name | Partition name | |
| size_kb | Size of the Nand occupied by the partition | Unit: KB, Size: must be an interger multiple of 128KB |
| pad_kb  | Size of the partition used for redundancy  | Size generaly 128 512KB |
| which_flash |  - | Attributes of the five tags: <which_flash> and 4 <attr> 
shown in the above figure are configured 
according to that of system partition. | 
| img_name | UBI file system image | - |




