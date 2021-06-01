---
title: 	Embedded System Mid term
---
* Progress: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11*,12, 13
# 1. What is Embedded System? Please simply describe the “Embedded System”.
## Appeared in
99, 01, 02, 03, 04, 05, 06
## Answer
* Any device that includes a programmable computer but not a general purpose computer
* It includes input and output and control logic. It has to have a specific function.
# 2. Please simply describe the boot control flow according the below figure. And you have to explain the functionality of bootloader and bootstrap loader. 
![](https://i.imgur.com/BE2rlGM.png)
## Appeared in
99, 01, 04, 05, 06
## Answer 
### Boot control flow
1. Boot loader initiates low level hardware.
2. bootsrap loader locates, decompress and loads the kernel image into the memory.
3. vmlinux head.o initializes CPU and virtual memory.
4. Main.c:  Architecture setup. Identify CPU and initialize it's advanced capability. 
### boot-loader and bootstrap loader
* Boot-loader: Boot loader initiates low level hardware including memory. Doesn't depend on Linux image.
* Bootstrap loader: Locate,decompress and loads the kernel image into memory. Real address mode. 
# 3. The below picture shows the relationship between processor and chipset. Please describe the functions of Northbridge and Southbridge. And Northbridge and Southbridge connect which kinds of devices? 
![](https://i.imgur.com/fd4cXSw.png)
## Appeared in
99,02
## answer
### Northbridge
* Northbridge connects directly to the  high-speed front-side bus (FSB). It connects DRAM and graphics
* South bridge: IO controller. Hardware for interfacing IOs

# 4. Please describe how to obtain a Linux kernel of an embedded system and building process of a Linux kernel
## Appeared in
99, 01, 02, 05, 06
## Answer
### obtain
* Download or purchase. Download from official website and Port kernel to your device
### building process
* Download the kernel.
* configure kernel features and modules
* use make to configure the kernel
* use make to compile the kernel
# 5. The below picture shows how to composite kernel image construction. Please explain overall processes and the objects in each process. 
![](https://i.imgur.com/35brIaY.png)
## Appeared in 
99, 01, 02, 04, 05, 06
## Answer
### vmlinux
* Kernel proper, in ELF format, including symbols, comments,debug info (if compiled with -g ) and architecture-generic components.
* objcopy generates a binary file
### image
* Binary kernel module, stripped of symbols, notes, and comments.
* compress with gzip.
### piggy.gz
* compressed image
### piggy.o
* The file piggy.gz in assembly language format so it can be
linked with a subsequent object, misc.o 
#### misc.o
* Routines used for decompressing the kernel image
(piggy.gz ), and the source of the familiar boot message:
"Uncompressing Linux … Done" on some architectures.
#### headxscale.o
Processor initialization specific to the XScale processor
family.
#### bigendian.o
Tiny assembly language routine to switch the XScale
processor into big-endian mode.
#### head.o
ARM-specific startup code generic to ARM processors. It is
this object that is passed control by the bootloader.

# 6 Please simply describe the bootloader of an embedded Linux. And how it works? 
## Appeared in
01, 02, 03, 05, 06
## Answer
* basic processor and platform initialization
* locating, loading, and passing execution to the primary operating system.
# 7. Please list four popular processors in an embedded system? And describe the main features of these processors.
## Appeared in
01, 05, 06
## Answer
* Intel pentium M
	* popular x86 architecture
	* Advanced power-management features
	* Dynamic clock speed capability
	* automatic transition to lower power modes
	* Multiple frequency and voltage operating points
* Freescale MPC7448
	* Forth gen PowerPC
	* Advanced power-management capabilities
	* AltiVec to enable very fast algorithmic computations and other data-crunching applications o enable very fast software computations commonly found in signalprocessing and network elements.
* Intel ARM XScale
	* ARM v5TE
	* coupled with one or more dedicated processing engines
	*  NPEs are dedicated to specific data-path manipulation in real time at wire speeds
* TI OMAP3530(arm)
	*  ARM core
	*  interfaces commonly found on integrated processors, such as UARTs and I2C
	*  Integrated 2D or 3D graphics accelerators
	*  Integrated DSPs for video and audio processing 49
# 8. Please describe the Initial RAM Disk? And discuss the difference between initrd and initramfs.
## Appeared in
03, 04, 05, 06
## Ans
* Initial ramdisk is a Linux kernel feature to allow further startup behavior customization before mounting a final root file system and spawning init. We presented the mechanism and example configuration for using this powerful feature.
* initrd
	* initrd is loaded before at prepare_namespace()
	* Initrd requires at least one file system driver be compiled into the kernel
	*  initrd is a gzipped file system image
* initramfs
	* initramfs is loaded before the call to do_basic_setup()
	* provides a mechanism for loading firmware for devices before its driver has been loader
	* cpio archive
# 9.There are some functions of embedded Linux driver as follows. Please explain the functionalities of listed functions.
(1)	static int XXX_open(struct inode *inode, struct file *file)
(2)	static ssize_t XXX_write(struct file *file, const char *buf, size_t count, loff_t * ppos)
(3)	static int XXX_ioctl(struct inode *inode, struct file *file, unsigned int cmd, unsigned long arg)
(4)	register_chrdev(XXX_MAJOR, "xyz", &xyz_fops);
(5)	static void __exit XXX_exit(void)
## Appeared in
03
## ANS
1. Open device
2. write device
3. I/O control
4. Register a char device and connect fops(file operation) to kernel.
5. remove module
# 10. When you plan to build a Linux kernel image, you can find three files in the kernel source code, including .config, Makefile, Kconfig. Please attempt to explain the roles of .config, Makefile, Kconfig.
## Appeared in
04, 05
## ANS
* .config:  configuration blueprint for building a Linux kernel image
* Makefile: specify build target
* kconfig: Kconfig drives the configuration process for the features contained within its subdirectory.
# 11. Please explain the booting embedded board in NOR boot mode and NAND boot mode (Stepping Stone) respectively. And compare the difference of these two modes
## Appeared in
04, 05, 06
## Answer
* Nand: Need initialize(stepping stone) to load u-boot. 4KB data will copy from NAND flash to internal SRAM(stepping stone). init clock, memory controller, copy bootloader image from NAND to SDRAM). Bootloader then loads linux kernel .
* Nor: Non volatile. Don't need to initialize Can boot with u-boot directly. oot from flash, init RAM,copy kernel to RAM. 
# 12. A simple Linux root file system might contain the following top-level directory entries as below figure.
Please describe the general contents in the directory of (1) bin, (2) dev, (3) etc, (4) lib, (5) usr.
```
|
|--bin
|--dev
|--etc
|--lib
|--sbin
|--usr
|--var
|--tmp
```
## Appeared in
05,06
## Answer
* bin: Binary executable
* dev: Device nodes.
* etc: Local system-configuration file
* lib: System libraries
* usr: Secondary file system hierarchy for application programs.

# 13. The below picture shows a typical embedded Linux system. Please describe the functionalities of (1) Host Development System, (2) Ethernet Hub, (3) RS-232 
![](https://i.imgur.com/4vWYCq0.png)
## Appeared in
06
## Answer
* RS-232: receive the message on board, burns code slowly
* Ethernet: upload code faster.
* Host Development System:  Development tools and utilities along with target files




# 上機考(過時)
```
# 9.請設計一個系統，請用電腦端的鍵盤輸入你學號的最後1個數字，然後透過UART傳到你的嵌入式板子，當它收到字元後，會依序用LED array顯示你的學號，每個數字的delay time約0.5秒。例如：你的學號是49881234，在電腦端的鍵盤輸入你學號的最後1個數字4，然後LED Array會依序顯示4->9->8->8->1->2->3->4 (不含顯示->)
## Appeared in
01
```

```
6.	(上機考：50%，安裝全部所需的driver得25%，全部完成50%) 
請開發一套DC Motor控制系統，如圖一所示。可以讓使用者在電腦端透UART去控制DMA2440XP上的DC Motor的轉速，使用者可以下幾個指令(在電腦端按數字鍵)來控制DC Motor的轉速，電腦端的操作畫面如圖二所示。
1.	Start =>此時DC Motor會開始用最低的轉數轉，4顆的LED會亮最左邊一顆。
2.	Stop=>此時DC Motor會停止，4顆的LED會全暗。
3.	Speed Up=>此時DC Motor會加速，使用者每按一次，會多亮一顆LED，最多亮到4顆。
4.	Speed Down=>此時DC Motor會減速，使用者每按一次，會多滅一顆LED，最少會亮到1顆。
5.	Exit=>離開主程式
```

```
6.	(上機考：50%，安裝全部所需的driver得25%，全部完成50%) 
請開發一套嵌入式無線電壓監控系統，如圖一所示。BBB會每200ms透過藍芽(Bluetooth, BT)依序地傳出你的學號，ADC直接讀進來可變電阻(Variable Resistor, VR) 10bits的數位值(0~1023)，以及轉換之後的電壓值(0~3.3V或0~5V)至電腦端。在電腦端你可以直接使用TeraTerm顯示或是自行撰寫程式顯示，完成後請demo給老師或助教檢查，老師或助教會順便問你程式碼的內容。
```


###### tags: `Embedded system` `CSnote`