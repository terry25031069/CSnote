---
title: OS Chapter 2
---

# Chapter 2
## Operating system services 
* OS provide an environment for execution of programs and services to programs and users
* Helpful OS functions: User interface(CLI, GUI, batch), Program execution, I/O operation, File-system manipulation, Communications, Error detection.
* Another set of OS functions exists for ensuring the efficient operation of the system itself via resource sharing: Resource allocation, Accounting(追蹤用戶使用狀況), Protection(控制系統資源存取) and security(用戶授權跟外部惡意存取)
## Command Line Interface(CLI)
* Implemented by kernal or system program 
* Multiple flavor - shells(User interface for access to OS service)
## System calls
* programming interface to the services provided by the OS
* Typically written in a high-level language (C, C++)
* Mostly accessed by programs via a high-level API rather than system call
![](https://i.imgur.com/cOm2ptA.png)
### System class parameter passing
* pass the parameters in registers
* store in memory
* pushed onto stack
## System programs
* System programs provide a convenient environment for program development and execution. They can be divided into:
### File manipulation
* create, delete, copy, rename, print, dump, list and generally manipulate files and directories
### Status information
* Some ask for system info(time and date, amount of available memory, disk space...)
* Other provide detailed performance, logging, and debugging information
* Some systems implement a registry, used to store and retrieve configuration information.
### File modification
* Text editors to create ad modify files
* Special commands to search contents of files or perform transformations of the text.
### Programming language support
* Compiler, assemblers, debuggers and interpreters sometimes provided
### Program loading and execution
* Absolute loaders, relocatable loader, linkage editors and overlay-loaders, debugging systems for higher-level and machine language 
### Communications
* Provide the mechanism for creating virtual connections among processes, user and computer system
* Allow users to send messages to one another's screens, browse web pages, send e-mail, logging remotely, transfer files to another.
### Background services
* Launch at boot time, some for system startup and terminate, and some from system boot to shutdown
* Provide facilities like disk checking, process scheduling, error logging, printing
* Run in user context not kernel context
* Known as services, subsystems, daemons
### Application programs
* Not pertain to system, and not typically considered of OS
* Run by command line, mouse click and finger poke by user
## Ms-DOS vs UNIX
* MS-DOS is written to provide the most functionality in the least space, thus its levels of functionality aren't well separated
* UNIX is limited by hardware functionality, it consists of two separable part:
* System programs and The Kernel(包含各種在CLI底下的各種東西，如圖)
#### OSs
* MS-DOS(Simple)

![](https://i.imgur.com/Giwbz4z.png)
* UNIX(beyond simple not fully layered)

![](https://i.imgur.com/FZLYbxm.png)
* Solaris(modular)

![](https://i.imgur.com/rDgcExs.png)
## Microkernel System structure
* Move as much from the kernel into user space(剩下行程間通訊、記憶體管理跟執行緒管理在kernel，剩下的在user space跑)
* Mac OS X kernel (Darwin) partly based on Mach
* Communication takes place between user modules using message passing
* Benefits: Easier to extend a micro-kernel, port the OS to new architectures, More reliable(less code is running) and secure.
* Detriment: Performance overhead of user space to kernel space communication.
## Module
* Most modern OS implement loadable kernel modules
* Uses object-oriented approach
* Each core component is separate
* Each talks to the others over known interfaces
* Each is loadable as needed within their kernel
## Hybrid(=Mixed) system
* hybrid combines multiple approaches to address performance, security, usability needs.
#### MAC OS X
* COCOA Is the programming environment

![](https://i.imgur.com/RxjfTBx.png)
#### Android
* Based on Linux

![](https://i.imgur.com/AnSu0eN.png)
#### Dtrace
* Probes fire when code is executed within a provider. capturing state data and sending it to consumers of probes


## System Boot
* When power is initialized on system, the **bootstrap loader** is loaded from ROM. The bootstrap loader loads the kernel.
# Review Question 
* 1.  What is “shell” in Unix? Describe its usage. -[CLI](#Command-Line-InterfaceCLI)
* 2.  What is system call? -[System Call](#System-calls)
* 3.  What is API? -[API](#System-calls)
* 4.  What are differences between system call and API? -[API](#System-calls)
* 5.  How does user program pass a block of data by a system call? -[Parameter passing](#System-class-parameter-passing)
* 6.  What is system program? -[System Program](#System-programs)
* 7.  What is the structure of MS-DOS, UNIX, and Solaris?[OS](#OSs)
* 8.  How does Cocoa work? [MAC OS](#MAC-OS-X)
* 9.  How does Android work?[Android](#Android)
* 10. How does DTrace work?[DTrace](#Dtrace)
* 11. What is bootstrap program? How does it work? -[System boot](#System-Boot)
# END

###### tags: `Operating System` `CSnote`