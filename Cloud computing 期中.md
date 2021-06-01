---
title: Cloud computing 期中
---
# 1.	根據NIST，雲端計算的定義為何? 雲端有那些重要的特性？
## definition
* A model for enabling ubiquitous, convenient, on-demand network access to a shared pool of configurable computing resources (e.g., networks, servers, storage, applications, and services) that can be rapidly provisioned and released with minimal management effort or service provider interaction. 
## Essential Characteristics 
* On-demand self-service 
* Broad network access. 
* Resource pooling 
* Rapid elasticity 
* Measured service

# 2.	請說明雲端的服務模型有那些？雲端的佈建模型有那些？
## Service Models 
* Software as a Service (SaaS) 
* Platform as a Service (PaaS) 
* Infrastructure as a Service (IaaS)
## Deployment Models 
* Private cloud 
*  Community cloud 
* Public cloud 
* Hybrid cloud 

# 3.	請說明何謂SOA？OASIS的定義為何？
## SOA
* Service oriented architecture
* It logically represents a repeatable business activity with a specified outcome.
* It is self-contained.
* It is a black box for its consumers, meaning the consumer does not have to be aware of the service's inner workings.
* It may be composed of other services.
## OASIS
* A paradigm for organizing and utilizing distributed capabilities that may be under the control of different ownership domains. It provides a uniform means to offer, discover, interact with and use capabilities to produce desired effects consistent with measurable preconditions and expectations.
## 4.	請說明何謂Remote Method Invocation？他的基本原理為何？
## RMI
* A true distributed computing application interface for Java, written to provide easy access to objects existing on remote virtual machines Helps provide access to objects existing on remote virtual machines
## 原理
![](https://i.imgur.com/NoD7yEB.png)
* Stub/skeleton layer
    * Responsible for managing the remote object interface between the client and server
* Remote reference layer
    * Responsible for managing the "liveliness" of the remote objects
    * Manages the communication between the client/server and virtual machines
* Transport layer
    * Actual network/communication layer that is used to send the information between the client and server over the wire
    * Currently TCP/IP based
* Uses serialization and remote procedure call to send information back and forth between remote objects

# 5.	何謂Web Service？Web Service的特性為何？
* A software application available via internet based protocols that supports to use xml based messages to communicate with other software applications
## 特性
* XML based everywhere
* Message-based
* Programming language independent
* Could be dynamically located
* Could be dynamically assembled or aggregated
* Accessed over the internet
* Loosely coupled
* Based on industry standards

# 6.	請以圖簡單的說明Web Service的架構。並說明何謂SOAP？何謂WSDL？
![](https://i.imgur.com/fXPmcqm.png)

## SOAP
* Simple Object Access Protocol
* Message Protocol for web services
## WSDL 
* Web Services Description Language
* XML language for describing web services

# 7.	請說明RESTful Web Service與一般的Web Service有何不同？
* Representational State Transfer是個設計架構。
* 藉由CRUD、Resourcename、resourceID進行訪問，將控制細節抽向化，使伺服器端與客戶端更為獨立，就算兩端都經過了極大的變動，只要傳訊方式不變就不會影響運作
# 8.	Google的GFS有那些特性?
* High fail tolerance by chunk replication
* Larger chunk size -> reduce meta data size and client master interaction
* most files are mutated by appending new data rather than overwriting existing data
* Is a user-space library
# 9.	請繪圖說明GFS的動作原理?
* ![](https://i.imgur.com/j625S0U.png)
# 10.	Google的GFS的複本配置的策略為何? 
* 預設為3個複本，並放入複數不同伺服器當中
# 11.	Google的GFS中寫入資料到複本的原理為何?
![](https://i.imgur.com/p5XiHV7.png)
![](https://i.imgur.com/QXKTHRE.png)
![](https://i.imgur.com/UurhMeV.png)
![](https://i.imgur.com/HzL8CK4.png)

# 12.	請繪圖說明Google的MapReduce的動作原理?
![](https://i.imgur.com/dlSOSie.png)
# 13.	請說明Spark的目標。Spark比MapReduce有何優點？
* Provide distributed memory abstractions for clusters to support apps with working sets retaining the properties of mapreduce
    * Or simply, Better for applications that repeatedly reuse a working set of data
## 優點
* MapReduce is built for batch processing, Spark has an interactive mode
* by caching partial/complete results across distributed nodes spark is faster than MapReduce, which is disk based
# 14.	Spark上的RDD為何？RDD在Spark中的重要性為何？
* An RDD is an immutable, partitioned, logical collection of records.
* RDD是SPARK的基本數據結構

# 15.	何謂虛擬化(Virtualization)？虛擬化的理由為何？
* 將電腦的各種實體資源（CPU、記憶體、磁碟空間、網路適配器等），予以抽象、轉換後呈現出來並可供分割、組合為一個或多個電腦組態環
## 理由
*　合併伺服器->增加使用率
*　容易控制、更改配置
*　不需預先購買硬體
*　容易轉移
*　較能從災難中恢復
# 16.	虛擬化的型態中，請說明何謂 Hardware Virtualization？Software Virtualization？Desktop Virtualization？
## Hardware Virtualization
* It hides the physical characteristics of a computing platform from users, instead showing another abstract computing platform
## Software Virtualization
* Application virtualization and workspace virtualization, the hosting of individual applications in an environment separated from the underlying OS
## Desktop Virtualization
* separates a personal computer desktop environment from a physical machine using the client–server model of computing

# 17.	何謂Full Virtualization？ 它的主要挑戰為何？
* provide a certain kind of virtual machine environment, namely, one that is a complete simulation of the underlying hardware. 
## challenge
* interception and simulation of privileged operations, such as I/O instructions. 
* The effects of every operation performed within a given virtual machine must be kept within that virtual machine 

# 18.	何謂Paravirtualization？Paravirtualization的主要目標為何？
* a virtualization technique that presents a software interface to virtual machines that is similar but not identical to that of the underlying hardware
## goal
* Modified OS, unmodified applications
* Leverage OS knowledge of virtualization to provide high-performance VM
* Enable hosting of 10’s-100’s of VM’s on a single machine

# 19.	Full Virtualization與Paravirtualization差異為何？
* Paravirtualization uses hypercall for system call, while full virtualization uses Binary Translation and Direct Execution
* Full virtualization guest OS don't have to be similar to host OS, but Paravirtualization guest OS is heavily dependent on Host OS
# 20.	何謂Hypervisor？Hypervisor可以分成那二類？
## what is ?
* aka virtual machine manager 
* technique that allow multiple operating systems, to run concurrently on a host computer. 
## types
* native, bare metal: 
    * hypervisors run directly on the host's hardware to control the hardware and to manage guest operating systems.
* hosted:
    * hypervisors run within a conventional operating system environment. With the hypervisor layer as a distinct second software level, guest operating systems run at the third level above the hardware
# 21.	何謂Docker？Docker跟Virtual Machine的差異為何？
## what is?
* Docker is a software platform that packages software into containers. It binds application and its dependencies inside a container.
## Difference
* All docker containers share the same host os, while VMs all has their own guest OS to run on.
# 22.	何謂Kubernetes？Kubernetes的功能為何？Kubernetes的基本單元為何？
## what is 
* Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. 
## Pod
* Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.
* a Pod is similar to a group of Docker containers with shared namespaces and shared filesystem volumes

###### tags: `Cloud computing` `CSnote`








