---
title: CMP Arch Chapter 1
---



# Chapter 1 Computer Abstractions and Technology
## 1.1 Intro
### Algorithm
* Determines both the number of source-level statements and the number of I/O operations executed
* Not in this class
### Programming language, compiler, and architecture
* Determines the number of computer instructions for each source-level statement
* Chapter 2, 3
### Processor and memory system
* Determines how fast instructions can be executed
* Chapter 4, 5, 6
### I/O system (hardware and operating system)
* Determines how fast I/O operations may be executed
* Chapter 4, 5, 6
## 1.2 Eight great ideas
* Design for Moore’s Law
    * integrated circuit resources double every 18–24 months
* Use abstraction to simplify design
    *  lower-level details are hidden to offer a simpler model at higher levels
* Make the common case fast
    * Making the common case fast will tend to enhance performance better than optimizing the rare case
* Performance via parallelism
* Performance via pipelining
* Performance via prediction
    *  it can be faster on average to guess and start working rather than wait until you know for sure
* Hierarchy of memories
    * cache, main memory, secondary memory
* Dependability via redundancy
    * we make systems dependable by including redundant components that can take over when a failure occurs and to help detect failures
## 1.3 Below your program
* Application software
    * Written in high-level language.
* System software
    * OS: Service code
        * Handle I/O
        * Manage memory and storage
        * schedule tasks and share resources
    * Compiler: Translates high-level language to assembly code.
* Hardware
    * Processor, memory, I/O controllers
## 1.4 Under the Covers
* Skip
## 1.5 Technologies for Building Processors and Memory
* Electronics technology continues to evolve.
![](https://i.imgur.com/3wczI98.png)
![](https://i.imgur.com/twMvUvV.png)
### Integrated Circuit(IC) cost 
$cost\ per\ die = \frac{cost\ per\ wafer}{dies\ per\ wafer\ \times yeld}$
$dies\ per\ wafer \approx \frac{wafer\ area}{die\ area}$
$yield = \frac{1}{(1+defects\ per\ area \times die\ area/2)^2}$
* Nonlinear relation to area and defect rate
    * Wafer cost and area are fixed.
    * Defect rate determined by manufacturing process
    * Die area determined by architecture and circuit design
## 1.6 Performance(Important) 
### Defining performance
* Response time(aka execution time): the time between the start and completion of a task
* throughput(aka bandwidth): the total amount of work done in a given time
$performance = \frac{1}{execution\ time}$
* Computer X is $n$ times faster than Y.
$\frac{performance_X}{performance_Y}=\frac{execution\ time_Y}{execution\ time_X} = n$
### Measuring performance
* Response time, elapsed time or wall clock time
    * Total time to complete a task
    * System performance
* CPU(execution) time
    * The actual time the CPU spends computing a task
    * Comprise user CPU time and system CPU time.
    * CPU performance
* Operation of digital hardware governed by a constant-rate CPU clock
    * Clock period(週期): duration of a clock cycle
        * time per cycle
    * Clock frequency(頻率): cycles per second
        * Hz
![](https://i.imgur.com/g2pyA90.png)
### CPU Performance and its factors
$\ CPU time = CPU\ clock\ cycles \times clock\ cycle\ time\\ =\frac{CPU\ clock\ cycles}{clock\ rate}$
* Performance improved by 
    * Reduce number pof clock cycles
    * Increase clock rate
    * Hardware designer must trade off clock rate against clock cycle
### The Classic CPU Performance Equation(102期中)
$clock\ cycles = instruction\ count \times CPI$
$CPU\ time = instruction\ count \times CPI\ times clock cycle time \\ =\frac{instruction\ count \times CPI}{clock\ rate}$
* Instruction count for a program
    * Determined by program, ISA and compiler
* Clock cycles per instruction (CPI)
    * Determined by CPU hardware
    * If different instructions have different CPI, average CPI is affected by instruction mix.
### CPI in More Detail
* If different instruction classes take different number of cycles
$clock\ cycles = \mathop{\sum_{i=1}^{n}}(CPI_i \times instruction\ count_i)$
* Weighted average CPI
$CPI=\frac{clock/ cycles}{instruction\ count}= \mathop{\sum_{i=1}^{n}}(CPI_i \times \frac{instruction\ count_i}{instruction\ count})$
### Performance Summary
$CPU\ time =\frac{instructions}{program} \times \frac{clock\ cycles}{instructions} \times \frac{seconds}{clock\ cycle}$
* Performance depends on
    * Algorithm: affects instruction count (IC), possibly CPI
    * Programming language: affects IC, CPI
    * Compiler: affects IC, CPI
    * Instruction set architecture: affects IC, CPI, clock rate
## 1.7 The power Wall
* Skip
## 1.8 The Sea Change: The Switch from Uniprocessors to Multiprocessors
* More than one processor per chip
* Require explicitly parallel programming
    * Compare with instruction-level parallelism
        * Hardware executes multiple instructions at once.
        * Hidden from the programmer
    *　Hard to do
        * Programming for performance
        * Load balancing
        * Optimizing communication and synchronization
## 1.9 Real Stuff: Benchmarking the Intel Core i7
* Skip
## 1.10 Fallacies and Pitfalls
### Improve an aspect of a computer and expect a proportional improvement in overall performance.
* Admahl's Law
$T_{improved} = \frac{T_{addected}}{improvement\ factor}+ T_{unaffected}$
* collary: make the common case fast
### Use a subset of the performance equation as a performance metric.
* MIPS (millions of instructions per second) does not account for
    * Differences in ISAs between computers
    * Differences in complexity between instructions
$MIPS = \frac{instruction\ count}{execution\ time \times 10^6}\\ =\frac{instruction\ count}{\frac{instruction\ count \times CPI}{clock\ rate}\times 10^6} = \frac{clock\ rate}{CPI \times 10^6}$
* CPI varies between programs on a given CPU. CPI varies between programs on a given CPU.
## 1.11 Concluding Remarks
* Cost/performance is improving.
    * Due to underlying technology development
* Hierarchical layers of abstraction
    * In both hardware and software
* Instruction set architecture
    * The hardware/software interface
* Execution time: the best performance measurement
* Power is a limiting factor (skipped)
    * Use parallelism to improve performance.
# QE
## 1.3
![](https://i.imgur.com/Okcypy0.png)
![](https://i.imgur.com/qOCc3sC.png)
## 1.5
![](https://i.imgur.com/Cm1cfrg.png)
![](https://i.imgur.com/fLvWUZO.png)
## 1.6
![](https://i.imgur.com/TgeZD6N.png)
![](https://i.imgur.com/0Xo1Gew.png)
## 1.7
![](https://i.imgur.com/DzWJKFF.png)
![](https://i.imgur.com/toLxGsL.png)
## 1.9
![](https://i.imgur.com/P1Ze5oX.png)
![](https://i.imgur.com/JbjBzxc.png)
## 1.12
![](https://i.imgur.com/ZaAdiE8.png)
![](https://i.imgur.com/saBp1cH.png)
## 1.13
![](https://i.imgur.com/XKPFGjA.png)


## 1.14
![](https://i.imgur.com/kkhPfkX.png)
![](https://i.imgur.com/QokM153.png)

## 1.15 
![](https://i.imgur.com/A5UikB4.png)
![](https://i.imgur.com/Sl9RAe3.png)







###### tags: `Computer Architecture` `CSnote`