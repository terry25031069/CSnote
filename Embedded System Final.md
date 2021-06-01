---
title: 	Embedded System Final
---

* Mid term questions are skipped
* Progress: 1,2,3,4,5,6,7,8,9,10,11,12,13 (total 13) 
# 1. Device drivers are broadly classified into two basic categories: character devices and block devices. Please individually describe them. (10%)
## Appeared in
99, 99_2, 101, 102, 104, 105_1, 105_2, 106, 108
## Derivation
* Please simply describe the Device Driver concepts. (10%)  103_2
## Answer 
### Character devices
* Character devices are accessed as stream of data.
* e.g. Serial port
### block devices
* Read and write blocks of data from random locations of an addressable.
* e,g, disks
# 2. Please refer to below example code of a Linux driver and then describe the functionalities of Section 1 and Section 2.

```
static int my_major = 0;
…
If (my_major) {
	// Section 1
	dev = MKDEV(my_major, my_minor);
	result = register_chrdev_region(dev, nr_devs, “mydev”);
} else {
	// Section 2
	result = alloc_chrdev_region(&dev, my_minor, nr_devs, “mydev”);
	my_major = MAJOR(dev);
}
If (result < 0){
	printk(KERN_WARNING “mydev: can’t get major %d\n”, my_major);
	return result;
}
```
## Appeared in
103, 105_1, 106, 108
## Answer
* if my_major!=0, register device by using the assigned ***mymajor, myminor***
* else, dynamically register device
# 3.What is the Proc File System? Please describe the functionalities of /proc file system. (10%)
## Appeared in
101, 103_2, 105_1, 105_2, 106, 108
## Answer
* Interface that allows the kernel to communicate information about each running process on a Linux system.
* Communication between kernel space and user space
# 4. What is Memory Technology Devices (MTD) subsystem? (10%)
## Appeared in
99, 99_2, 101, 102, 103, 103_2, 104, 105, 106, 108
## Answer
* A type of device file to interact with flash memory.
* The MTD layer architecture enables the separation of the lowlevel device complexities from the higher-layer data organization and storage formats that use memory devices.

# 5. Why the engineers usually mount a NFS to develop an embedded system? Please point out the advantages of NFS for building an embedded system. (10%)
## Appeared in
99_2, 101, 104, 105_1, 105_2, 106, 108
## Answer
* Network File System 
* NFS enables you to export a directory on an NFS server and mount that directory on a remote client machine as if it were a local file system. In other words, access file on a server machine like it is a local file system.
* developer can have access to a huge number of files, libraries, tools, and utilities during development and debugging, even if the target embedded system is resource constrained.
# 6. Please list the advantages of cramfs. (10%)
## Appeared in
102, 104, 105_1, 106, 108
## Answer
* A read-only ,compressed file system. Simple and small, ideal for boot ROMS
# 7. What is the BusyBox in an embedded system? How to add a new command into the embedded system except the commands that BusyBox provides. (10%)
## Appeared in
99, 99_2, 102,103, 103_2, 104, 105, 106, 108
## Answer
* BusyBox provides compact replacements for many traditional fullblown utilities found on most desktop and embedded Linux distributions.
* add a new command
    * 1
	    1. cross compile c then copy to bin 
	    2. 修改busybox設定
	
# 8. Please describe the functionalities and their advantages of DHCP server and NFS server. (10%)
## Appeared in
103
## Answer
#### DHCP
* A DHCP server controls the IP address assignments for IP subnets for which it has been configured, and for DHCP or BOOTP clients that have been configured to participate. A DHCP server listens for requests from a DHCP client (such as your target board), and assigns addresses and other pertinent information to the client as part of the boot process.
#### NFS
* Network File System 
* Your root file system is not size-restricted by your board's own limited resources, such as Flash memory.
* Changes made to your application files during development are immediately available to your target system.
* You can debug and boot your kernel before developing and debugging your root file
system.
# 9 Fig. 1 shows a typical DHCP exchange, please explain the each step (4 steps) in Fig. 1. (10%)
![](https://i.imgur.com/b2u9ByN.png)
## Appeared in
103_2, 105_1
## Answer
* The sequence starts with the client (target) transmitting a broadcast frame attempting to discover a DHCP server. This is shown by the DHCPDISCOVER message shown.
* The server responds (if it has been so configured and enabled) by offering an IP address for the client. This is evidenced by the DHCPOFFER message.
* The client then responds by testing this IP address locally. The testing includes sending the DHCPREQUEST packet to the DHCP server, as shown.
* Finally, the server responds by acknowledging the IP address assignment to the client, thus completing the automatic target configuration.
# 10. What advantages of Ext3 File System compared to Ext2 File System? How to convert an Ext2 File System to the Ext3 File System? (10%)
## Appeared in
103, 105_1, 106, 108
## Answer
### Advantage
* Availability: By journaling, after an unexpected power failure or system crash,  file system check is not necessary 
* Data complete: Journaling can prevent the data damage.
* speed: ext3's journaling optimizes hard drive head motion. 
* Easy to convert: Don't have to reformat to migrate from ext2 to ext3
### Convert
* mount ext2 file system
`mount /dev/sdb1/mnt/flash`
* create journal
`tune2fs -j /dev/sdb1`
# 11 How to build a simple EXT2 file system and modify its content (add and delete directories, make device nodes, and so on).
## Appeared in
105_1, 106, 108
## Answer
### Create file image
* mke2fs
### make directory
*　mkdir
### remove directory
* rmdir or rm 
### make device node
* mknod
# 12 Please describe the functionalities of below module utilities. (10%)
    (1) insmod
    (2) lsmod
    (3) modprobe
    (4) depmod
    (5) rmmod
## Appeared in
106, 108
## Answer
### insmod
* insert a module into a running kernel.
### lsmod
* displays a formatted list of the modules that are inserted into the kernel
### modprobe
* discover this relationship and load the dependent modules in the proper order.
### depmod
* When modprobe is executed, it searches for a file called modules.dep in the same location where the modules are installed
### rmmod
* It simply removes a module from a running kernel
# 13 Please list the advantages of JFFS2. (10%)
## Appeared in
99
## Answer
* Support for NAND flash devices
* Hard links
* Compression
* Better performance: JFFS treated the disk as a purelycircular log. This generated a great deal of unnecessary I/O. The garbage collection algorithm in JFFS2 makes this mostly unnecessary. 
###### tags: `Embedded system` `CSnote`