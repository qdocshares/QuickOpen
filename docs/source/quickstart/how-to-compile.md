# How to Compile


## Quectel Open SDK

SDKl.zip unzipped process must be done under non-root Ubuntu environment.
    
    tar xvf EC25EFAR06A12M4G_OCPU_20.200.20.200_SDK.tar.bz2
    $ tree -L 1
    .
    ├── Makefile
    ├── ql-ol-bootloader
    ├── ql-ol-crosstool
    ├── ql-ol-extsdk
    ├── ql-ol-kernel
    ├── ql-ol-rootfs
    ├── ql-ol-rootfs.tar.gz
    ├── ql-ol-usrdata
    ├── ql-ol-usrfs
    └── target




|     Directory    |     Content               |
|   ------         |       ------              |
| ql-ol-crosstool  | Cross tool chain               |
| ql-ol-bootloader | QTI bootloader source code     |
| ql-ol-kernel     | Linux kernel source code       |
| ql-ol-rootfs     | Root file system for platform runtime |
| ql-ol-extsdk     | Include API，example and tools        |



## Ubuntu Environment

It is better to try Quectel SDK on Ubuntu 16.04 or 18.04, and not try the SDK on Ubuntu later than 22.04.
    
    sudo apt-get install -y perl  mc re2c g++ g++-multilib wget  sudo  python
    sudo apt-get install -y bison gcc make build-essential libc6-dev-i386 libncurses-dev wget coreutils diffstat  chrpath cpio gawk  sed     texi2html texinfo unzip flex bc     libssl-dev
    sudo update-alternatives --install /usr/bin/python  python /usr/bin/python2  2700


## Compile 

### Enable the cross tool

    cd ql-ol-sdk 

    source ql-ol-crosstool/ql-ol-crosstool-env-init
    QUECTEL_PROJECT_NAME      =EC25E
    QUECTEL_PROJECT_REV       =EC25EFAR06A12M4G_OCPU_20.200
    Relocating ............done
    Extracting the rootfs...
    Done.

### Build the kernel    

    make kernel_menuconfig
    make kernel
    make kernel_module

### Build the rootfs

    make rootfs

### Build the userdata

    make usrsdata


