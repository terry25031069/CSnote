---
title: OS Chapter 6
---

# Chapter 6: Process Synchronization
## Background
* Processes can be executed concurrently
* Shared data may be changed by different process leading to data inconsistency
* Maintaining data consistency requires mechanisms to ensure the orderly execution of cooperating processes
#### Race condition
counter++ could be implemented as

     register1 = counter
     register1 = register1 + 1
     counter = register1

counter-- could be implemented as

     register2 = counter
     register2 = register2 - 1
     counter = register2

Consider this execution interleaving with “count = 5” initially:
```
S0: producer execute register1 = counter         {register1 = 5}
S1: producer execute register1 = register1 + 1   {register1 = 6} 
S2: consumer execute register2 = counter        {register2 = 5} 
S3: consumer execute register2 = register2 – 1  {register2 = 4} 
S4: producer execute counter = register1         {counter = 6 } 
S5: consumer execute counter = register2        {counter = 4}
```
* A situation like this, where several process access and manipulate data concurrently and the outcome of the execution depends on the particular order in which the access take place is called, **race condition**.
## The Critical-section problem 
* Each process has critical section segment of code
* When one process in critical section, no other may be in its critical section

* Each process must ask permission to enter critical section in entry section, may follow critical section with exit section, then remainder section
* General structure of typical process
![](https://i.imgur.com/XKb2u3z.png)

#### Solution requirement:
* 1. Mutual exclusion: If a process is executing in critical section, then other processes cannot access to its critical secion
* 2. Progress: If no process is executing in its critical section and there exist some processes that wish to enter their critical section, then the selection of the processes that will enter the critical section next cannot be postponed indefinitely
* 3. Bounded Waiting: A bound must exist on the number of times that other processes are allowed to enter their critical sections after a process has made a request to enter its critical section and before that request is granted

* two approaches are used to handle critical-sections in OS:
    * Preemptive – allows preemption of process when running in kernel mode
    * Non-preemptive – runs until exits kernel mode, blocks, or voluntarily yields CPU

## Peterson's Solution
* Two Process solution
* Assume that the load and store instructions are atomic i.e. cannot be interrupted
* The two processes share two variables:
    * int turn; 
        * turn indicates whose turn it is to enter the critical section
    * Boolean flag[2]
        * The flag array is used to indicate if a process is ready to enter the critical section. flag[i] = true implies that process Pi is ready
#### Structure of process in Peterson's solution

```
while (true) { 
    flag[i] = true; 
    turn = j; 
    while (flag[j] && turn == j); 
        "critical section" 
    flag[i] = false; 
        "remainder section"
}
```
* This solution is correct because:
    * Mutual exclusion is preserved
    * The progress requirement is  satisfied
    * The bounded-waiting requirement is met
## Hardware support for synchronization
### Memory Barriers
* How a computer architecture determines what memory guarantees it will provide to an application is called **memory model**.
* two categories of memory model
    * Strongly ordered: A memory modification on one processor is immediately visible to all other processors
    * Weakly ordered: A memory modification on one processor is not immediately visible to all other processors

* Memory barriers fences: Instructions to force any changes in memory to be propagated to all other processors.
### Hardware Instructions
#### Concepts
##### test_and_set()
* Shared boolean variable lock, initialized to FALSE
```
boolean test_and_set (boolean *target)
{
    boolean rv = *target;
    *target = TRUE;
    return rv:
}
```
##### using test_and_set()
```
do {
   while (test_and_set(&lock)) 
      ; /* do nothing */ 
   /* critical section */ 
   lock = false; 
   /* remainder section */ 
} while (true); 
```
##### Bounded-waiting Mutual Exclusion with test_and_set
```
do {
   waiting[i] = true;
   key = true;
   while (waiting[i] && key) 
      key = test_and_set(&lock); 
   waiting[i] = false; 
   /* critical section */ 
   j = (i + 1) % n; 
   while ((j != i) && !waiting[j]) 
      j = (j + 1) % n; 
   if (j == i) 
      lock = false; 
   else 
      waiting[j] = false; 
   /* remainder section */ 
} while (true); 
```
##### Bounded-waiting compare_and_swap Instruction
* Shared Boolean variable lock initialized to FALSE; Each process has a local Boolean variable key
```
int compare and swap(int *value, int expected, int new value) { 
   int temp = *value; 
   if (*value == expected) 
      *value = new value; 
   return temp; 
} 
```
```
do {
   while (compare and swap(&lock, 0, 1) != 0) 
      ; /* do nothing */ 
      /* critical section */ 
   lock = 0; 
      /* remainder section */ 
} while (true); 
```

## Mutex Locks(aka spinlock)
* mutex: short of mutual exclusion
* Simplest to implement
* Product critical regions with it by first acquire() a lock then release() it
* requires busy waiting 
```
acquire() {
   while (!available) 
      ; /* busy wait */ 
   available = false;; 
} 
release() { 
   available = true; 
} 

do { 
   acquire lock
      critical section
   release lock 
      remainder section 
} while (true);
```
## Semaphore
### Usage
* synchronization tool that does not require busy waiting
* Semaphore S – integer variable 
* Two standard operations modify S: wait() and signal()
* Consider P1  and P2 that require S1 to happen before S2
```
P1:
   S1;
   signal(synch);
P2:
   wait(synch);
   S2;
```
### implementation
* Must guarantee that no two processes can execute wait () and signal () on the same semaphore at the same time
* implementation is the critical section problem where the wait and signal code are placed in the critical section
* applications may spend lots of time in critical sections and therefore this is not a good solution
#### Semaphore without busy waiting
* With each semaphore there is an associated waiting queue
* Each entry in a waiting queue has two data items:
    * value (of type integer)
    * pointer to next record in the list
* Two operations:
    * block – place the process invoking the operation on the appropriate waiting queue
    * wakeup – remove one of processes in the waiting queue and place it in the ready queue
```
typedef struct{ 
   int value; 
   struct process *list; 
} semaphore; 
wait(semaphore *S) { 
   S->value--; 
   if (S->value < 0) {
      add this process to S->list; 
      block(); 
   } 
}
signal(semaphore *S) { 
   S->value++; 
   if (S->value <= 0) {
      remove a process P from S->list; 
      wakeup(P); 
   } 
} 
```
#### Use semaphore to solve bounding buffer
* n buffers, each can hold one item
* Semaphore mutex initialized to the value 1
* Semaphore full initialized to the value 0
* Semaphore empty initialized to the value n

![](https://i.imgur.com/1Gk7cZm.png)
![](https://i.imgur.com/zxzRNmY.png)




## Monitors
* A high-level abstraction that provides a convenient and effective mechanism for process synchronization
### Usage
* Is an Abstract data type, internal variables only accessible by code within the procedure
* Only one process may be active within the monitor at a time

```
monitor monitor-name
{
	// shared variable declarations
	procedure P1 (…) { …. }

	procedure Pn (…) {……}

    Initialization code (…) { … }
	}
}
```
#### Schematic view of a monitor
![](https://i.imgur.com/vNc0dFC.jpg)
* condition x, y;

* Two operations on a condition variable:
    * x.wait ()  – a process that invokes the operation is suspended until x.signal () 
    * x.signal () – resumes one of processes (if any) that  invoked x.wait ()
        * If no x.wait () on the variable, then it has no effect on the variable
* If process P invokes x.signal (), with Q in x.wait () state, then  Q is resumed, P must wait

* Options include
    * Signal and wait – P waits until Q leaves monitor or waits for another condition
    * Signal and continue – Q waits until P leaves the monitor or waits for another condition

* Both have pros and cons – language implementer can decide
* Monitors implemented in Concurrent Pascal compromise P executing signal immediately leaves the monitor, Q is resumed
### Implementing a monitor using semaphores
Each procedure F  will be replaced by

```
wait(mutex);
    …			 
    body of F;

    …
if (next_count > 0)
    signal(next)
else 
    signal(mutex);
```
* For each condition variable x, we  have:
```
semaphore x_sem; // (initially  = 0)
int x_count = 0;
```
* The operation x.wait can be implemented as:	
```
x-count++;
if (next_count > 0)
    signal(next);
else
    signal(mutex);
wait(x_sem);
x-count--;
```
* The operation x.signal can be implemented as:

```
if (x-count > 0) {
    next_count++;
    signal(x_sem);
    wait(next);
    next_count--;
}
```
* A Monitor to Allocate Single Resource

```
monitor ResourceAllocator 
{ 
	boolean busy; 
	condition x; 
	void acquire(int time) { 
		if (busy) 
			x.wait(time); 
		busy = TRUE; 
	} 
	void release() { 
		busy = FALSE; 
		x.signal(); 
	} 
initialization code() {
	 busy = FALSE; 
	}
}	
```

### Resuming Processes within a Monitor
* If several processes queued on condition x, and x.signal() executed, which should be resumed?
    * First-come, first-serve not adequate 
    * conditional-wait construct of the form x.wait(c)
        * c is priority number
        * Process with lowest number (highest priority) is scheduled next
### Readers-Writers Problem
* A data set is shared among a number of concurrent processes
    * Readers – only read the data set; they do not perform any updates
    * Writers   – can both read and write

* Problem – allow multiple readers to read at the same time Only one single writer can access the shared data at the same time
* Shared data: 
    1. Data set
    2. Semaphore rw_mutex initialized to 1
    3. Semaphore mutex initialized to 1
    4. Integer read_count initialized to 0
```
writer
do {
   wait(rw mutex); 
      ...
   /* writing is performed */ 
      ... 
   signal(rw mutex); 
} while (true)
```
```
reader
do {
wait(mutex);
read count++;
if (read count == 1) 
wait(rw mutex); signal(mutex); 
...
/* reading is performed */ 
... wait(mutex);
read count--;
if (read count == 0) 
signal(rw mutex); signal(mutex); 
} while (true);
```
### dining-philosophers problem
* don’t interact with their neighbors, occasionally try to pick up 2 chopsticks (one at a time) to eat from bowl
* Need both chopsticks to eat, then release both when done
```
structure of philosopher i
do  { 
          wait ( chopstick[i] );
	     wait ( chopStick[ (i + 1) % 5] );
	
	             //  eat

	     signal ( chopstick[i] );
	     signal (chopstick[ (i + 1) % 5] );
	
                 //  think

} while (TRUE);
```
#### Solution to Dining Philosophers
```
monitor DiningPhilosophers
   { 
	enum { THINKING; HUNGRY, EATING) state [5] ;
	condition self [5];

	void pickup (int i) { 
        state[i] = HUNGRY;
	    test(i);
	     if (state[i] != EATING) self [i].wait;
	}
	
    void putdown (int i) { 
        state[i] = THINKING;
        // test left and right neighbors
	    test((i + 4) % 5);
	    test((i + 1) % 5);
    }
    
    void test (int i) { 
	    if ( (state[(i + 4) % 5] != EATING) &&
	         (state[i] == HUNGRY) &&
	         (state[(i + 1) % 5] != EATING) ) {
	            state[i] = EATING ;
		        self[i].signal () ;
	         }
	 }

    initialization_code() { 
        for (int i = 0; i < 5; i++)
            state[i] = THINKING;
	}
}
```

#### avoid deadlock
1. Don't allow all philosophers to sit and eat/think at once.
2. Pick up both chopsticks in a critical section
3. Alternate choice of first chopstick
## Liveness
* Liveness refers to a set of properties that a system must satisfy to ensure that processes make progress during their execution life.
### Deadlock
* two or more processes are waiting indefinitely for an event that can be caused by only one of the waiting processes
### Starvation
* indefinite blocking
* A process may never be removed from the semaphore queue in which it is suspended
### Priority Inversion 
* Scheduling problem when lower-priority process holds a lock needed by higher-priority process
* Solved via priority-inheritance protocol
## Evaluation
* Not important

# Review Question
## 1. [What is race condition? Give an example to show how race condition happens.](#Race-condition)
出率高
### ANS
* several process access and manipulate data concurrently making the outcome depends on the order in which the access take place
* Consider this execution interleaving with “count = 5” initially:
```
S0: producer execute register1 = counter         {register1 = 5}
S1: producer execute register1 = register1 + 1   {register1 = 6} 
S2: consumer execute register2 = counter        {register2 = 5} 
S3: consumer execute register2 = register2 – 1  {register2 = 4} 
S4: producer execute counter = register1         {counter = 6 } 
S5: consumer execute counter = register2        {counter = 4}
```
## 2. [What are the three requirements of critical section solution? Explain them.](#Solution-requirement)
出率高
### ANS
 * Mutual exclusion: Only one process can access critical section by a time.
 * Progress: If there is no process in critical section, and some process wants in. A process will be selected in.
 * Bounded Waiting: Time waiting to get in critical section is limited
## 3.[ What is Peterson’s solution? How does it satisfy the three requirements of critical section?](#Peterson’s-Solution)
### ANS
* Two process solution
```
while (true) { 
    flag[i] = true; 
    turn = j; 
    while (flag[j] && turn == j); 
        "critical section" 
    flag[i] = false; 
        "remainder section"
}
```
 * Mutual exclusion: the second one will be stuck in while loop
 * Progress: once the first one gets out, the second one gets in.
 * Bounded Waiting: The second one gets in after the first one gets out.
## 4. [Implement bounded-waiting mutual exclusion with test_and_set(), including the implementation of TestAndSet() How does it satisfy the three requirements of critical section?](#Bounded-waiting-Mutual-Exclusion-with-test_and_set)
### ANS
* Test and set implement
```
boolean test_and_set (boolean *target)
{
    boolean rv = *target;
    *target = TRUE;
    return rv:
}
```
* bounded-waiting mutual exclusion
```
do {
   waiting[i] = true;
   key = true;
   while (waiting[i] && key) key = test_and_set(&lock); 
   waiting[i] = false; 
   /* critical section */ 
   j = (i + 1) % n; 
   while ((j != i) && !waiting[j]) j = (j + 1) % n; 
   if (j == i) 
      lock = false; 
   else 
      waiting[j] = false; 
   /* remainder section */ 
} while (true); 
```
* Mutual Exclusion: while (waiting[i] && key)
* Passing: 
* Bound waiting: 
## 5. [Implement mutual exclusion with compare_and_swap(). How does it work to satisfy the first two requirements of critical section?](#Bounded-waiting-compare_and_swap-Instruction)
### ANS
```
do{
   while (compare_and_swap(&lock, 0, 1) != 0);
   /* do nothing */
   /* critical section */
   lock = 0;
   /* remainder section */
}
while (true);
```
* mutual exclusion and progress. No bound waiting
* Mutual exclusion: Only one can get into critical section
* Progress: If a process gets out, other processes will be able to get in.
## 6. [What is spinlock and its implementation? What is busy waiting in spinlock ](#Mutex-Locksaka-spinlock)
### ANS
* Product critical regions with it by first acquire() a lock then release() it
```
acquire() {
   while (!available) 
      ; /* busy wait */ 
   available = false;; 
} 
release() { 
   available = true; 
} 

do { 
   acquire lock
      critical section
   release lock 
      remainder section 
} while (true);
```
* Spinlock will repeatedly ask for permission rapidly if it can't get into critical section.
## 7. [How does semaphore work? How does semaphore avoid busy waiting?](#Semaphore)
### ANS
* Synchronization tool that allow multiple process to access and don't require busy waiting.
* Incoming process is put into a queue to wait. Don't have to check repeatedly
## 8. [Use semaphore to solve bound-buffer problem.Explain how the implementation solves the problem.](#Use-semaphore-to-solve-boundibg-buffer)
### ANS
* n buffers, each can hold one item
* Semaphore mutex initialized to the value 1
* Semaphore full initialized to the value 0
* Semaphore empty initialized to the value n

![](https://i.imgur.com/1Gk7cZm.png)
![](https://i.imgur.com/zxzRNmY.png)
## 9. [Use semaphore to solve reader-writer problem.Explain how the implementation solves the problem..](#Readers-Writers-Problem)
### ANS
* Shared data: 
    1. Data set
    2. Semaphore rw_mutex initialized to 1
    3. Semaphore mutex initialized to 1
    4. Integer read_count initialized to 0
```
writer
do {
   wait(rw mutex); 
      ...
   /* writing is performed */ 
      ... 
   signal(rw mutex); 
} while (true)
```
```
reader
do {
wait(mutex);
read count++;
if (read count == 1) wait(rw mutex); 
signal(mutex); 
...
/* reading is performed */ 
... 
wait(mutex);
read count--;
if (read count == 0)signal(rw mutex); 
signal(mutex); 
} while (true);
```
## 10. [Use semaphore dining-philosophers problem.Show how this solution can avoid deadlock.](#dining-philosophers-problem)
### ANS
```
monitor DiningPhilosophers
   { 
	enum { THINKING; HUNGRY, EATING) state [5] ;
	condition self [5];

	void pickup (int i) { 
            state[i] = HUNGRY;
	    test(i);
	    if (state[i] != EATING) self [i].wait;
	}
	
    void putdown (int i) { 
        state[i] = THINKING;
        // test left and right neighbors
	test((i + 4) % 5);
	test((i + 1) % 5);
    }
    
    void test (int i) { 
	    if ( (state[(i + 4) % 5] != EATING) &&
	         (state[i] == HUNGRY) &&
	         (state[(i + 1) % 5] != EATING) ) {
	            state[i] = EATING ;
		     self[i].signal () ;
	         }
	 }

    initialization_code() { 
        for (int i = 0; i < 5; i++)
            state[i] = THINKING;
	}
}
```
# END 
###### tags: `Operating System` `CSnote`