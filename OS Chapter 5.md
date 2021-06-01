---
title: OS Chapter 5
---

# Chapter 5: Process scheduling\ CPU scheduling
## Basic concept
* CPU-I/O Burst Cycle: Process execution consists of a cycle of CPU execution and I/O wait
* CPU burst is followed by I/O burst 

![](https://i.imgur.com/wacBq5w.png)
* Distribution of CPU burst is the main concern

### CPU Scheduler
* When the CPU becomes idle, the OS must select one of the process in the ready queue to be executed.
* the selection process is done by the **CPU scheduler**

### Preemptitve and Nonpreemptive scheduling
* Preemptive scheduling allocates CPU for a limited time.
* Nonpreemptive once process allocates CPU for it's process. It will hold it until finishes burst or change to switches to wait state.
#### Nonpreemptive(cooperative)
* Process switches from running state to waiting state
* Terminates

#### Preemptive
* Process switches from running state to ready state
* Process switches from waiting state to ready state
* And all other

### Dispatcher 
* Dispatcher is the module that gives control of CPU to the process selected by the CPU scheduler.
#### Function
* Switching context between processes
* Switching to user mode
* jumping to the proper location in the user program to restart that program

* Dispatch latency: Time it takes for the dispatcher to stop one and restart another process.
## Scheduling criteria
* CPU utilization(max): Keep the CPU busy
* Throughput(max): number of processes that are completed per unit time
* Turnaround time(min): Time length to start and complete a particular process
* waiting time(min): Time spent waiting in the ready queue
* response time(min): Time length between request and response(time sharing environment)

## scheduling algorithms
* review Gnatt chart
### FIFO scheduling
* aka FCFS, first come first server.
* Do the job that comes in first.
#### CONS
* convoy effect: A large process may block the CPU. Results in long waiting time

### Shortest-Job-First Scheduling
* Do the shortest job
* Gives the lowest average waiting time
* Problem: difficult to know the length of the next CPU process

#### Determine the length of next CPU burst
* Can only estimate length (should be similar to last CPU burst)
* use exponential average
##### Exponential average
* 1. $t_n$ = actual length of $n^{th}$ CPU burst
* 2. $τ_{n+1}$ = predicted value of next CPU burst.
* 3. α , 0<=α<=1
* 4. Define: $τ_{n=1} = αt_n + (1-α)t_n$
* Commonly, α set to ½
* α =0
    * $τ_{n+1} = τ_n$
    * Recent history does not count
* α=1
     * $τ_{n+1} = ατ_n$
     * Only the actual last CPU burst counts
* Preemptive version is called shortest-remaining-time-first
#### Shortest remaining time
* Takes arrival time into consideration.
![](https://i.imgur.com/6u9uTys.png)
### Round robin Scheduling
* Process is given a small CPU time(i.e.time slice, time quantum). After that, the process is sent back into the ready queue.
* Higher average turnaround than SJF, but better response
#### Performance
* large time slice: close to FIFO
* Small time slice: time slice must be large with respect to context switch, otherwise overhead is too high

### priority scheduling
* A priority number (integer) is associated with each process
* The CPU is allocated to the process with the highest priority (smallest integer = highest priority)
* SJF is priority scheduling where priority is the inverse of predicted next CPU burst time
* Problem: Starvation – low priority processes may never execute
* Solution: Aging – as time progresses increase the priority of the process

### Multilevel queue scheduling
* Ready queue is partitioned into separate queues, e.g.:
    * foreground (interactive)
    * background (batch)
* Each queue can has its own scheduling algorithm. e.g.:
    * foreground – RR
    * background – FCFS 
* Scheduling must be done between the queues:
    * Fixed priority scheduling; (i.e., serve all from foreground then from background).  Possibility of starvation.
    * Time slice – each queue gets a certain amount of CPU time which it can schedule amongst its processes; i.e., 80% to foreground in RR
    * 20% to background in FCFS 
### Multilevel feedback  scheduling
* A process can move between the various queues; aging can be implemented this way
* Multilevel-feedback-queue scheduler defined by the following parameters:
    * number of queues
    * scheduling algorithms for each queue
    * method used to determine when to upgrade a process
    * method used to determine when to demote a process
    * method used to determine which queue a process will enter when that process needs service
## Thread scheduling
* Mapping User-level thread to associated kernel-level thread.
### Contention scope
* Many-to-one and many-to-many models, thread library schedules user-level threads to run on LWP
    * process-contention scope (PCS): scheduling threads within process
* system-contention scope (SCS): scheduling Kernel thread

### Pthread scheduling
* API allows specifying either PCS or SCS during thread creation
    * PTHREAD_SCOPE_PROCESS schedules threads using PCS scheduling
    * PTHREAD_SCOPE_SYSTEM schedules threads using SCS scheduling
* Linux and Mac OS X only allow PTHREAD_SCOPE_SYSTEM
```
#include <pthread.h> 
#include <stdio.h> 
#define NUM THREADS 5 
int main(int argc, char *argv[]) { 
   int i, scope;
   pthread t tid[NUM THREADS]; 
   pthread attr t attr; 
   /* get the default attributes */ 
   pthread attr init(&attr); 
   /* first inquire on the current scope */
   if (pthread attr getscope(&attr, &scope) != 0) 
      fprintf(stderr, "Unable to get scheduling scope\n"); 
   else { 
      if (scope == PTHREAD SCOPE PROCESS) 
         printf("PTHREAD SCOPE PROCESS"); 
      else if (scope == PTHREAD SCOPE SYSTEM) 
         printf("PTHREAD SCOPE SYSTEM"); 
      else
         fprintf(stderr, "Illegal scope value.\n"); 
   } 
      /* set the scheduling algorithm to PCS or SCS */ 
   pthread attr setscope(&attr, PTHREAD SCOPE SYSTEM); 
   /* create the threads */
   for (i = 0; i < NUM THREADS; i++) 
      pthread create(&tid[i],&attr,runner,NULL); 
   /* now join on each thread */
   for (i = 0; i < NUM THREADS; i++) 
      pthread join(tid[i], NULL); 
} 
/* Each thread will begin control in this function */ 
void *runner(void *param)
{ 
   /* do some work ... */ 
   pthread exit(0); 
}
```
## Multi-Processor Scheduling
### Approached to Multiple-Processor Scheduling
* Asymmetric multiprocessing – only one processor accesses the system data structures, alleviating the need for data sharing
* Symmetric multiprocessing (SMP) – each processor is self-scheduling, all processes in common ready queue, or each has its own private queue of ready processes
### Multicore Processors
* memory stall: When a processor access memory, a significant time is spent on waiting for the data to become available.
### Load Balancing
Load balancing attempts to keep workload evenly distributed
* Push migration – periodic task checks load on each processor, and if found pushes task from overloaded CPU to other CPUs
* Pull migration – idle processors pulls waiting task from busy processor
### Processor affinity 
* A process may have affinity on which processor it runs\
* soft affinity:OS attempts to keep a process on a single processor, but is still possible to migrate between processors due to load balancing 
* hard affinity: Specify a subset of processors to run on.
## Real-time CPU Scheduling
* Soft real-time systems: no guarantee as to when critical real-time process will be scheduled
* Hard real-time systems: task must be serviced by its deadline
### Minimizing latency
* Event latency : amount of time elapsed between an event occurs and serviced.
* two types of latencies:
    * Interrupt latency: time from arrival of interrupt to start of routine that services interrupt
    * Dispatch latency: time for schedule to take current process off CPU and switch to another 
* Conflict phase of dispatch latency has two components:
    * Preemption of any process running in kernel mode
    * Release by low-priority process of resources needed by high-priority processes
    *
![](https://i.imgur.com/Y7BYOgH.png)
### Priority-based Scheduling
* For real-time scheduling, scheduler must support preemptive, priority-based scheduling
* For hard real-time must also provide ability to meet deadlines
* Processes have new characteristics: periodic ones require CPU at constant intervals
    * Has processing time t, deadline d, period p
    * 0 ≤ t ≤ d ≤ p
    * Rate of periodic task is 1/p
### Rate Montonic Scheduling
* Shorter periods = higher priority;
* Longer periods = lower priority
### Earliest Deadline First Scheduling (EDF)
* the earlier the deadline, the higher the priority;
* the later the deadline, the lower the priority
### Proportional Share Scheduling
* T shares are allocated among all processes in the system
* An application receives N shares where N < T
* This ensures each application will receive N / T of the total processor time
### POSIX Real-Time Scheduling
* API provides functions for managing real-time threads
* Defines two scheduling classes for real-time threads:
    * SCHED_FIFO - threads are scheduled using a FCFS strategy with a FIFO queue. There is no time-slicing for threads of equal priority
    * SCHED_RR - similar to SCHED_FIFO except time-slicing occurs for threads of equal priority
* Defines two functions for getting and setting scheduling policy:
```
pthread attr getsched policy(pthread attr t *attr, int *policy) 
pthread attr setsched policy(pthread attr t *attr, int policy) 
```

## Operating-System Examples
### LINUX
### Windows
### Solaris


## Algorithm Evaluation
* How to select CPU-scheduling algorithm?
* Determine criteria, then evaluate algorithms
### Deterministic Modeling
* analytic evaluation
* Takes a particular predetermined workload and defines the performance of each algorithm  for that workload
### Queueing Models
* the arrival of processes, and CPU and I/O bursts probabilistically
    * Computes average throughput, utilization, waiting time, etc
* Computer system described as network of servers, each with queue of waiting processes
    * Knowing arrival rates and service rates
    * Computes utilization, average queue length, average wait time, etc
#### Little's formula
* n = average queue length
* W = average waiting time in queue
* λ = average arrival rate into queue
* Little’s law – in steady state, processes leaving queue must equal processes arriving, thus
    * n = λ x W
### Simulations
* Queueing models limited
* more accurate
    * Programmed model of computer system
    * Use Clock as variable
    * Gather statistics indicating algorithm performance
    * Data to drive simulation gathered via
        * Random number generator according to probabilities
        * Trace tapes record sequences of real events in real systems
### Implementation
* simulations have limited accuracy
* implement new scheduler and test in real systems
    * High cost, high risk
    * Environments vary
* Most flexible schedulers can be modified per-site or per-system 
* Use APIs to modify priorities
    * environments vary
# Review Question
## 1. [What does CPU scheduler do?](#CPU-Scheduler) [What does Dispatcher do?](#Dispatcher)
### ANS
* CPU scheduler selects a process in the ready queue to be executed when the CPU idle.
* Dispatcher is the module that gives control of CPU to the process selected by the CPU scheduler.
## 2. [What is the difference between preemptive and non-preemptive scheduling?](#Preemptitve-and-Nonpreemptive-scheduling)
### ANS
* Preemptive scheduling: allocates CPU for a limited time.
* Non-preemptive: once process allocates CPU for it's process. It will hold it until finishes burst or change to switches to wait state.
## 3. [What kinds of process switching are preemptive scheduling?](#Preemptive)[What kinds of process switching are non- preemptive scheduling?](#Nonpreemptivecooperative)Explain the reason.
### ANS
* Non-preemptive
    * Process switches from running state to waiting state
    * Terminates
* Preemptive
    * Process switches from running state to ready state
    * Process switches from waiting state to ready state
    * And all other
## 4. [What are optimization criteria of scheduling algorithm?](#Scheduling-criteria)Explain them.
### ANS
* CPU utilization: Keep the CPU busy
* Throughput: number of processes that are completed per unit time
* Turnaround time: Time length to start and complete a particular process
* waiting time: Time spent waiting in the ready queue
* response time: Time length between request and response
## 5. [How does FCFS scheduling work? When does FCFS become less efficient?](#FIFO-scheduling)
### ANS
* Do the job that comes in first.
* When a large process comes in. Processes that comes after will have long waiting time.
## 6. [How does SJF scheduling work? Why SJF is better than FCFS?](#Shortest-Job-First-Scheduling)
### ANS
* Do the shortest job
* Gives the lowest average waiting time
## 7. [How does Shortest-Remaining-Time-First scheduling work? What is the difference between this scheduling algorithm and SJF?](#Shortest-remaining-time)
### ANS
* Do the job with shortest remaining time.
* Takes arrival time into consideration.
## 8. [How does Round Robin (RR) work?What is the advantage of RR?](#Round-robin-Scheduling)
### ANS
* Process is given a small CPU time. After that, the process is sent back into the ready queue.
* Good response.
## 9. [What are the problem when time quantum(time slice) of RR becomes too short and too long?](#Performance)
### ANS
* large time slice: close to FIFO
* Small time slice: time slice must be large with respect to context switch, otherwise overhead is too high
## 10. [How does Multilevel Queue scheduling work?How does this algorithm avoid starvation problem?](#Multilevel-queue-scheduling)
### ANS
* Queues are separated into more queues with different priorities
* Time slice among the queues
## 11. [How does Multilevel Feedback Queue scheduling work?How does this algorithm implement aging?](#Multilevel-feedback-scheduling)
### ANS
* Much like Multilevel Queue scheduling, but processes can move between queues.
* Move a process that is waiting to long into a higher priority queue.
## 12. [In thread scheduling, what are the scopes and how do they work?](#Contention-scope)[How does Pthread implement them?](#Pthread-scheduling)
### ANS
*
    * process-contention scope (PCS): schedule User thread to run o LWP.
    * system-contention scope (SCS): scheduling Kernel thread.
*   
    * PTHREAD_SCOPE_PROCESS schedules threads using PCS scheduling
    * PTHREAD_SCOPE_SYSTEM schedules threads using SCS scheduling
# END
###### tags: `Operating System` `CSnote`