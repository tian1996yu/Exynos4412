# linux-4.4.38-for-tiny4412
linux-4.4.38-for-tiny4412 made by FriendlyARM Corp.

- how to boot and flash the uboot
    
    * use the uboot modified by myself
    https://github.com/zczjx/uboot_tiny4412
    
    * do sign manually if you modify the uboot
    before flash it to gen bl2.bin
    cd sd_fuse/tiny4412
   ../mkbl2 ../../u-boot.bin bl2.bin 14336

    * follow this article to flash uboot.bin to emmc
    http://www.cnblogs.com/pengdonglin137/p/4161084.html

- how to build the linux-4.4.38-for-tiny4412 
    
    1. download the correct version of arm-linux-gcc
    I use arm-linux-gcc version 4.9.4 download from Linaro
		export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/work/uboot/gcc-linaro-4.9.4-2017.01-x86_64_arm-linux-gnueabihf/bin
		export CROSS_COMPILE=arm-linux-gnueabihf-

    2. cp tiny4412_linux_4_4_defconfig .config

    3. make LOADADDR=0x40008000 uImage

    4. make dtbs

- how to tftp the linux kernel and dtb image

	setenv ipaddr 192.168.31.40
	setenv serverip 192.168.31.192
	usb start
	usb reset
	tftp 0x46000000  exynos4412-tiny4412.dtb
	tftp 0x40008000  uImage
	tftp 0x41000000  ramdisk.img
	bootm 0x40008000 0x41000000 0x46000000
