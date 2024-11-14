# EC200A SDK build based on Docker


We will provide customers with a guide.
Quectel_EC200A&ECx00R_Series_QuecOpen(SDK)_Quick_Start_Guide_V1.1.pdf
However, customers may still encounter some compilation errors. We provide customers with guidance based on docker.

## Prerequisites

- Install the docker on Ubuntu


```    
    sudo apt update
    sudo apt install docker.io
    sudo apt install docker
```    

- Add the current user to the docker group

```
    sudo groupadd docker
    sudo usermod -aG docker $USER
    sudo gpasswd -a ${USER} docker
    newgrp docker
```

If you do not try this, you can only use docker with root.

- Add the linux kernel headers

```
    sudo apt install -y linux-headers-`uname -r`
```

By default, we should be able to see it in the /usr/src/linux-headers-`uname -r`.


## Generate the docker image based on Dockerfile

    docker build -t asr_linux_env  .

And then with  `docker images` you can see the asr_linux_env. 

Dockerfile:


    FROM ubuntu:18.04
    RUN apt-get update
    RUN apt-get upgrade --assume-yes
    RUN apt-get install --assume-yes perl  mc re2c g++ g++-multilib wget  sudo  python3 python3-pip

    ARG user=test

    RUN useradd --create-home --no-log-init --shell /bin/bash ${user} \
        && adduser ${user} sudo \
        && echo "${user}:1" | chpasswd

    RUN apt-get install --assume-yes   \
                bison gcc make build-essential libc6-dev-i386 libncurses-dev \
                coreutils diffstat  chrpath cpio  gawk sed  texi2html texinfo unzip flex bc  \
                python3-setuptools rsync swig unzip zlib1g-dev file wget \
                gcc-multilib g++-multilib gettext git libncurses5-dev   \
                libssl-dev  clang g++  dos2unix python  python-pip  curl 

    RUN update-alternatives --install /usr/bin/python  python /usr/bin/python2   3

    RUN python -m pip install   --upgrade  pip

    RUN pip install pyhocon

    USER  ${user}


The default user is test and the password is 1.
It is based on Ubuntu 18.04.


## Run the command to start the docker container.

For example, we put the quectel_asr_linux in the folder /data/quectel_asr_linux.


    docker run -it -v /data/quectel_asr_linux:/home/test/asr_linux  \
            -v /usr/src/linux-headers-`uname -r`:/usr/src/linux-headers-`uname -r`  \
            -v /lib/modules/`uname -r`:/lib/modules/`uname -r`  \
            --name=asr_build  \
            asr_linux_env  \
            /bin/bash


Notes:
    
- -v /data/quectel_asr_linux:/home/test/asr_linux means that mount the sdk folder on the host machine at the /home/test/asr_linux in the container.
-  -v /usr/src/linux-headers-\`uname -r\`:/usr/src/linux-headers-\`uname -r\`  and -v /lib/modules/\`uname -r\`:/lib/modules/\`uname -r\`  means that the container shares the linux kernel headers and kernel modules with the host.
-   --name=asr_build means that asr_build is the docker container name of the docker container we run.


If you want to enter the container, you can use the command

    docker exec -it  asr_build /bin/bash

## How to build the SDK

Here is an example to compile the EC200A_EUAB.

    source package/quectel/compile/ql_build_config \
            &&   buildversion  EC200A_EUAB  EC200AEUABR03A01M1G V01 FFF EC200AEUABR03A01M1G 01 01.001  \
        && buildconfig  EC200A_EUAB  EC200AEUABR03A03M1G STD	\
        && build_fw



buildconfig \<project\> \<version\> STD

- \<project\>  Module model. For example: EC200A_CNAA

- \<version\> Firmware version. For example: EC200ACNAAR01A01M1G


The target firmware is in the bin/target.

