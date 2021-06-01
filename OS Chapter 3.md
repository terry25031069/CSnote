---
title: OS Chapter 3
---

# Chapter 3 Process
## Concept
### The Process
Process is a program in execution.

![](https://i.imgur.com/ByIIqVm.jpg)
#### Sections (Memory allocation of a process)
* Text section: Executable code
* Data section: Global variables
* Heap section: Memory that is dynamically allocated during run.
* Stack section: Data storage when invoking functions(e.g. function parameters,return addresses)
### Process state
* State is defined by current activity of the concept.
#### States
* New: The process is being created
* Running: Executing instructions
* Waiting: Waiting for events to occur
* Ready: Waiting to be assigned to a processor
* Terminated: Finished execution

![](https://i.imgur.com/S7VgqWq.jpg)
### Process control block(PCB)
Process is represented as a PCB in the OS.
#### Information contained
* Process state: As written above in process state.
* Program counter: Address of the next instruction to be executed
* CPU registers: Accumulators, index registers, stack pointers etc
* CPU scheduling: Process priority, pointer to scheduling queues, and other scheduling information. (Chap 5)
* Memory-management info: base and limit registers, page tables, segment tables etc
* Accounting info: Time spent, time limits, account numbers, job and process number.
* I/O status info: List of I/O device allocated, list of open files.![](https://i.imgur.com/y9EwQVE.jpg)

## Process scheduling
The objective of multiprogramming is to maximum CPU utilization. To achieve this, the **process scheduler** selects an available process to be executed by a core.
Number of processes currently in memory is known as the **degree of multiprogramming**.
### Scheduling queues
* Job queue : set of all processes in the system
* Ready queue: A process is created, waiting to be executed.
* Device queues: set of processes waiting for an I/O device
### schedulers
* Long-term scheduler(job scheduler): selects which processes should be brought into the ready queue
* Short-term scheduler(CPU scheduler): select processes in the ready queue and allocate a CPU core for it.
* Swapping: A kind of scheduling. Swapping is to move a process in-and-out memory. 
* Processes can be described as either:
    * I/O-bound process – spends more time doing I/O than computations, many short CPU bursts
    * CPU-bound process – spends more time doing computations; few very long CPU bursts

### Context switch
* When an interrupt occurs, the system has to save the current context of the process running on the CPU. **State save** is to save current state of the CPU, **state restore** is to resume operation.
* Context-switch time is overhead. the system does no useful work while switching
    * The more complex the OS and the PCB the longer the context switch
* Context switch should be as fast as possible

## Operations on Processes
### Process creation
* Most operating system identify processes according to a process identifier(PID).
#### UNIX process creating
* `fork()`: Creates a process.Returns 0 if it is the child process. Nonzero if it is the parent process.
* `exec()`: Replace process's memory space with a new program. Does not return unless error occurs.
* `wait()`: Move process into ready queue until child process terminates.
#### Windows.api
* `CreateProcess()`: Creates processes. Unlike fork, in requires many parameters.
* `STARTUPINFO`: Contains properties of new process.
* `PROCESS_INFORMATION`: Contains a handle and identifiers to the newly created process and its thread.
* `WaitForSingleObjct()`: Wait until the child process exits and return control to parent process.
### Process Termination
####  UNIX
* exit(): To terminate process.
#### Windows
* TerminateProcess()

Some system doesn't allow child process to exist if its parent process is terminated. In such systems, if a parent is terminated, its child will also be terminated. This is referred to as **cascade termination**. 

* A terminated process whose parent hasn't called wait() is a **zombie** process. 
* If a parent did not invoke wait() and instead terminated, its child processes will be left as **orphans**. UNIX systems address this system by assigning **init** process as the new parent of the process and periodically invokes wait().
### EXAMPLE
![](https://i.imgur.com/QVRiBxM.png)

#### Android process hierarchy
* Foreground process: The process on screen, the user is currently in interacting with.
* Visible process: A process that is not directly visible on the foreground, but performing an activity that the foreground process is referring to.
* Service process: Similar to a background process but is performing an activity that is apparent to the user(such as playing music)
* Background process: A process that is performing an activity but is not apparent to the user.
* Empty process: A process that holds no active components associated with any Apps.
## Interprocess Communication(IPC)
Reasons to allow process cooperation.
* Information sharing: Many Apps may be interested in the same piece of info.
* Computation speedup: Break up a task into subtasks and execute them parallelly.
* Modularity: Divide system function into separate processes or threads.

IPCs(two models):
* Shared memory: A region of memory is shared between cooperating processes.
* Message passing: Transfer messages between processes. Slower, but easier to implement. 
## IPC in Shared-Memory Systems
### Producer-Consumer problem
Producer process produces information that is consumed by consumer process.
Two variations:
* unbounded buffer: Buffer size is not limited. Producer never waits. Consumer waits if nothing is in the buffer.
* Bounded buffer. Buffer size is fixed. Producer must wait if the buffer is full.

## IPC in Message-Passing Systems
Message passing is done by two operations:
`send()` and `recieve()`
### Naming:
Direct communication:
* Send and receive between two processes.
* A **single** link is created between two processes. Processes only need each other's identity to communicate.

Symmetry/Asymmetry comm:
* Sender names the recipient, the recipient isn't required to name the sender.
* less desirable then techniques described next.

Indirect comm:
* Messages are sent and received by mailboxes or ports.
* A link is established only if they have shared mailbox.
* A link can be associated to more than two processes.
* Multiple links can may exist between two processes.

### Synchroniztion
Synchronous/asynchronous also known as blocking/nonblocking
* Blocking send/receive: Sending is blocked until a message is fully sent. Receive is blocked until a message is available. 
* Nonblocking send/receive: Sending process sends the message and resumes operation. Receiver retrieves a valid message or a NULL.
### Buffering
* Zero capacity: The queues max length is zero. Link cannot have any message waiting in it.
* Bounded capacity: Queue has a finite length for messages to reside in. If the queue is not full when a message is sent, the message will be placed inside the queue, and the sender can continue execution. If queue is full, the sender will be blocked.
* Unbounded capacity: Queue length is potentially infinite. The sender is never blocked.
## Examples of IPC Systems
### POSIX Shared Memory
Process first creates shared memory segment.
* `shm_fd = shm_open(name, O CREAT | O RDWR, 0666);`
* Also can be used to open an exsisting segment.

Set size of the object.
* `ftruncate(shm_fd, 4096);`

Use `mmap()` to memory-map a file pointer to the shared memory object.
Reading and writing to shared memory is done by using the pointer returned by `mmap()`.
### Mach communication Message based
* Even system calls are messages.
* Messages are sent and received using `mach_msg()`.
* Port needed for communication is created by `mach_port_allocate()`.
### Windows 0S
Message-passing centric via advanced local procedure call (LPC) facility.
* Only works between processes on the same system.
* Uses ports to communication.
#### Communicate using windows(Code is only to express how it works)
* First, Create a handle object. 

`HANDLE hComm;`
* Open a port. 
```
hComm = CreateFile(com,                //port name
			GENERIC_READ | GENERIC_WRITE, //Read/Write
			0,                            // No Sharing
			NULL,                         // No Security
			OPEN_EXISTING,// Open existing port only
			NULL,         // Non Overlapped 
			NULL);        // Null for Comm Devices
```
* Read and write.
```
ReadFile( hComm,              //Handle 
          &Buffer,            //buffer
          sizeof(Buffer),     //Size of Buffer
          &NoBytesRead,       //Number of bytes read
          NULL);              //Non Overlapped
```
```
WriteFile(hComm,               //Handle 
		  lpBuffer,            //buffer
		  temp.length(),       //Size of buffer
		  &dNoOfBytesWritten,  //Bytes written
		  NULL);               //Non Overlapped
```              
### Pipes
#### Ordinary Pipes
* Cannot be accessed from outside the proccess that created it.
* Parent proccess creates the to communicate with child processes.
* Allows communication in producer-consumer style.
* Is **unidirectional**. Only the the write-end(Producer) can send, the read-end(Consumer) can only read.
* Windows calls these **anonymous pipes**.

![](https://i.imgur.com/dIDqIjt.jpg)
#### Named Pipes
* Bidirectional.
* Not necesarry to be Parent-Child.
* Several processes can use the same pipe.
## Communication in Client-Server systems
### Sockets
* Endpoint for communication.
* IP position: **120.126.197.52:80**. 120.126.197.52 is the ip position. 80 is port.

Types of socket:
* TCP
* UDP
* Multicast



### Remote Procedure Calls(RPC)
* Abstracts procedure calls between processes on network.
* Use ports for service.

**Stubs** 
* Client side proxy for procedure on server.
* Locates the server and commands the parameters.
* Server uses a similar stub to interact with client.
* Transmits messages between client and server.
* On Windows, stub code compile from specification written in Microsoft Interface Definition Language (MIDL)
* By controlling the parameters, differences in data representation between client and server can be negated. (Big-endian/little-endian  i.e. Most significant Byte/LSB stored first)
* One data representation of RPC is **external data representation**(XDR)


# Review Questions
* 1. What is memory allocation of a process? Describe the meaning of each member in the memory. -[Process Sections](#Sections-Memory-allocation-of-a-process)
* 2. Draw the diagram of process state. Describe the meaning of each state. -[Process states](#States)
* 3. What is PCB of a process? Describe the content of PCB. -[PCB](#Process-control-blockPCB)
* 4. What are the scheduling queues, and their usage?  -[Scheduling queues](#Scheduling-queues)
* 5. What are difference between I/O-bound and CPU-bound process?  -[Schedulers](#schedulers)
* 6. What is context switch? What is the problem of context switch?  -[Context switch](#Context-switch)
* 7. Write the codes that create a child process, which calls “ls”. Parent process will terminate after child process is done. -[Code](#EXAMPLE)
* 8. What are the two IPC models and how do they work? -[DIrect and indirect](#Naming)
* 9. What are the two ways of IPC message-passing, and how do they work? How does the buffer size affect synchronization of message passing?[Buffer size](#Buffering)
* 10. How does IPC implementation work in:
   a. [POSIX](#POSIX-Shared-Memory) b. [Windows](#Windows-0S)
* 11. How does Remote Procedure Call work, including its execution procedure? -[RPC](#Remote-Procedure-CallsRPC)
* 12. How does the pipe work, including the fd array. [Pipe](#Pipes)
# END
###### tags: `Operating System` `CSnote`