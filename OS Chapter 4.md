---
title: OS Chapter 4
---
# Chapter 4 Threads and Concurrency
* Thread runs within program.
* Process creation is heavy-weight, thread creation is light-weight.
* Simplify code, increase efficiency
 
Multi-threaded server architecture:
![](https://i.imgur.com/ErZ5m5y.jpg)


#### Benefits
* Responsiveness: Even if a part of program is slow or blocked, other parts of the program can continue to run.
* Resource sharing: Threads shares memory and resources within process by default.
* Economy: Cheaper to create than process.
* Scalability: Runs in parallel in different cores.
##### Context switch VS thread switch
![](https://i.imgur.com/LkAy47S.png)
* Context switch will have to reload everything currently in memory space.
* Threads in the process shares the same code, data section and OS resources. 
## Multicore programming
#### Parallel
* Perform more than one task simultaneously.
##### Types of parallelism
* Data parallelism: Same data and operation on multiple core.
* Task parallelism: Distribute threads across cores, each performing an unique operation.
##### Amdahl's law
* S is serial portion of program.
* N processing cores

![](https://i.imgur.com/y2o8aul.png)

* As N approaches infinite, speedup approaches 1/S.
#### Concurrency 
* Supports more than one task making progress.
* Single core multitask. Use a scheduler.
## Multi-threading Models
* User threads: Management done by user-level thread library.
    * POSIX thread
    * Windows thread
    * Java thread
* Kernel threads: Supported by the Kernel
### Models
* Many-to-one
    * Many user-level threads mapped to single kernel thread
    * One thread blocking causes all to block
    * May not run in parallel on multi-core system because only one thread can be in the kernel at a time.
* One-to-One
    * Each user-level thread maps to kernel thread
    * More concurrency than many-to-one
    * Number of threads per process sometimes restricted due to overhead
* Many-to-many
    * Allows many user level threads to be mapped to many kernel threads
    * Allows the  operating system to create a sufficient number of kernel threads
* Two level model
    * Hybrid One-to-One and Many-to-many. Allows a user thread to be bound to kernel thread.
## Thread Libraries
* Use thread libraries to create and and manage threads.
### Pthreads
* Provided either as user-level or kernel-level.
* A POSIX standard (IEEE 1003.1c) API for thread creation and synchronization
* Is a spec. not implementation.
* API specifies behavior, implementation is up to library.
* Common in UNIX.
#### Example
![](https://i.imgur.com/EwmvysN.png)
![](https://i.imgur.com/GRLxSIr.png)
### Windows multi-thread C program
* Similar to POSIX
#### Example
![](https://i.imgur.com/eimoTRr.png)
![](https://i.imgur.com/byV4ZUo.png)
### JAVA Threads
* Managed by the JVM
* JVM is available on any OSs, including Windows, Linux, MacOS.
* JAVA thread is created by:
    * Extending the thread class
    * implementing the runnable interface(Used most of the time)
```
public interface Runnable
{
    public abstract void run();
}
```
##### Codes
* Implement runnable interface

![](https://i.imgur.com/bpF43Pw.png)
* Create thread

![](https://i.imgur.com/kMQUua5.png)
* waiting on a thread 

![](https://i.imgur.com/NeZytvq.png)

#### Java executor framework
* Java also allows thread creation around the Executor interface:

![](https://i.imgur.com/gayBzjp.png)
* The Executor is used as follows:

![](https://i.imgur.com/1dGaRym.png)
![](https://i.imgur.com/skRF4do.png)

### Implicit threading
* Growing in popularity as number of thread increase. 

* Creation and management of threads done by compilers and run-time libraries rather than programmers
* Five methods explored
    * Thread Pools
    * Fork-Join
    * OpenMP
    * Grand Central Dispatch
    * Intel Threading Building Blocks
#### Thread pool
* Creates threads in a pool waiting for work.
###### Advantages
* Usually slightly faster than creating thread on request.
* Number to threads is bound to the size of pool 
* task can start run by mechanics rather than create thread.
##### Windows API supports thread pool
![](https://i.imgur.com/dijLWCT.png)

##### Three methods to create thread pool for JAVA
![](https://i.imgur.com/rQep2Ed.png)
![](https://i.imgur.com/YsuMZbG.png)
### Fork Join
* Threads are forked, and then joined.
    * ![](https://i.imgur.com/nKWsZYm.jpg)
* General algorithm for fork-join strategy
    * ![](https://i.imgur.com/OjL9z5x.png)
#### Fork join parallelism in JAVA
![](https://i.imgur.com/46qvaBw.png)
![](https://i.imgur.com/AERKONM.png)

* The ForkJoinTask as an abstract task.
* RecursiveTask and RecursiveAction classes extend ForkJoinTask.
* RecursiveTask returns a result (via the return value from the compute() method) 
* RecursiveAction does not return a result

![](https://i.imgur.com/j0ctoYD.jpg)
### OpenMP
* Identifies parallel regions as code blocks by `#pragma omp parallel ` .
![](https://i.imgur.com/iiBbYF6.png)
![](https://i.imgur.com/Bx6wABX.png)

### Grand Central Dispatch
* For MacOS and IOS.
* Extensions to C, C++ and Objective-C languages, API, and run-time library
* Allows identification of parallel sections by `^{}` .
* Blocks placed in dispatch queue. After task is removed from queue, assign the task to empty thread in thread pool.
* Two types of dispatch queues:
    * Serial: Blocks removed in FIFO order. Queue is per process, called main queue.
    * concurrent: Removed in FIFO order, several may be removed at a time.
### Intel Threading Building Blocks (TBB)
* Template library for designing parallel C++ programs
* For loop written using TBB with parallel_for statement
    * parallel_for(size_t(0),n, [=] (size_t i){apply(v[i])})

## Threading Issues
### The fork() and exec() System Calls
* Two versions of fork()
    * Only duplicate the called thread
    * Duplicate all threads
* Exec(). Replace all threads in process.
### Signal handling
* Signal is used to notify an event has occurred.
* A **signal handler** is used to process signals.
    * Signal is created by particular event.
    * Signal is delivered to a process.
    * Signal handlers can be default or user-defined.
*  Every signal has default handler that kernel runs. User-defined signal handler can override default.
* Four types of signal deliver:
    * Deliver the signal to the thread to which the signal applies
    * Deliver the signal to every thread in the process
    * Deliver the signal to certain threads in the process
    * Assign a specific thread to receive all signals for the process

### Thread Cancellation
* Terminate a thread before it has finished.
* Thread to be canceled is called the **target thread**.
#### Two general approaches
* Asynchronous cancellation: Terminates the target thread immediately.
* Deferred cancellation: Target thread periodically check if it should be cancelled.
#### Pthread example to create and cancel a thread.
![](https://i.imgur.com/NJMDoem.png)
* `pthraed_cancel(tid)` sends a request to terminate only. Actual cancellation depends on thread state. 
* If thread has cancellation disabled, cancellation remains pending.
* Default type is deferred.
* Cancel only occurs when pthread_testcancel() is called, the cleanup handler is invoked.
#### JAVA
* Deferred cancellation uses the `interrupt()` method.

![](https://i.imgur.com/ZkBrC6Y.png)
* A thread checks if it is interrupted.

![](https://i.imgur.com/a0BddhC.png)
#### Thread-Local Storage(TLS)
* TLS allows each thread to have its own data.
* Useful when using thread pool.
#### Scheduler Activations
* Many-to-many and two-level models require communication to maintain the appropriate number of kernel threads allocated to the application.
* Lightweight process (LWP) is an intermediate data structure  between kernel and user thread.
    * Appears to be a virtual processor user thread could be scheduled to run on.
    * Each LWP is attached to kernel thread.
* The kernel informs an application about current event using upcalls provided by upcall handler in thread library.
* This communication allows an application to maintain the correct number kernel threads

![](https://i.imgur.com/OlJErxh.png)
## Operating System Examples
### Windows Threads
* Provided by windows API.
* Implements the one-to-one mapping.

* **Context** of thread:
    * thread id
    * Register set representing state of processor
    * Separate user and kernel stacks for when thread runs in user mode or kernel mode
    * Private data storage area used by run-time libraries and dynamic link libraries (DLLs)
* Primary data structures of a thread :
    * ETHREAD (executive thread block) – includes pointer to process to which thread belongs and toKTHREAD, in kernel space
    * KTHREAD (kernel thread block) – scheduling and synchronization info, kernel-mode stack, pointer to TEB, in kernel space
    * TEB (thread environment block) – thread id, user-mode stack, thread-local storage, in user space

[![](https://i.imgur.com/PFcvWcI.jpg)
](https://)

### Linux Threads
* Refers to as tasks not threads.
* Thread creation is done by `clone()`.
* `clone()` allows a task to share address space with process controlled by flags.
![](https://i.imgur.com/HvavpZA.jpg)
* `struct task_struct` points to process data structures (shared or unique)

# Review Questions
* 1. What resources are used when a thread is created and a process is created? 
    How do they differ from those used when a process is created? [Difference](#Context-switch-VS-thread-switch)
* 2. How does a multi-threaded web server work?
* 3. What are the benefits of multi-threaded programming? Explain each item. [Benefits](#Benefits)
* 4. What are the differences between the three multithreading models? [Models](#Models)
* 5. Implement creating a thread by the following thread library, 
    including the critical functions, parameters, and related procedures.
    a. [Pthread](#Pthreads) b. [Windows thread](#Windows-multi-thread-C-program) c. [Java Thread](#JAVA-Threads)
* 6. How does implicit threading work? 
    Describe the three types of implementations.[Thread pool, openMP and Grand Central Dispatch](#Implicit-threading)
* 7. How a signal can be delivered in a multi-threaded program.
    Describe the four options.[Signal handling](#Signal-handling)
* 8. How do the two types of thread cancellation work? [Thread Cancellation](#Thread-Cancellation)
* 9. How does the scheduler of kernel thread work, including the upcall procedure? [Scheduler](#Scheduler-Activations) 
* 10. What is the data structure of Windows thread?
      Describe the content of each block of data structure. [Window Thread](#Windows-Threads)
###### tags: `Operating System` `CSnote`