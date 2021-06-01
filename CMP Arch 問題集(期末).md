---
title: CMP Arch 問題集(期末)
---
# Chapter 3
## 3.5
### Question
* What is 4365 - 3412 when these values represent signed 12-bit octal numbers stored in sign-magnitude format? The result should be written in octal. Show your work.
### Answer
* http://bit.ly/2MtqyLX
* 7777(-3777)
## 3.9 
### Question
* http://bit.ly/3rUoXiH
* Assume 151 and 214 are signed 8-bit decimal integers stored in two’s complement format. Calculate 151 + 214 using saturating arithmetic. The result should be written in decimal. Show your work.
### Answer
* -105 -42 = -128 (-147)
## 3.12 
### Question
* Using a table similar to that shown in Figure 3.6, calculate the product of the octal unsigned 6-bit integers 62 and 12 using the hardware described in Figure 3.3. You should show the contents of each register on each step.
#### fig 3.6
![](https://i.imgur.com/4scpGRR.png)
#### fig 3.3
![](https://i.imgur.com/ZLzH7WK.png)
### Answer
* $62 \times 12$
* ![](https://i.imgur.com/AuAINDu.png)
## 3.16 
### Question
* Calculate the time necessary to perform a multiply using the approach given in Figure 3.7 if an integer is 8 bits wide and an adder takes 4 time units.
#### fig 3.7
* ![](https://i.imgur.com/fLh653k.png)
### Answer
![](https://i.imgur.com/0NF82Yd.png)
## 3.19 
### question
* Using a table similar to that shown in Figure 3.10, calculate 74 divided by 21 using the hardware described in Figure 3.11. You should show the contents of each register on each step. Assume A and B are unsigned 6-bit integers. Th is algorithm requires a slightly different approach than that shown in Figure 3.9. You will want to think hard about this, do an experiment or two, or else go to the web to figure out how to make this work correctly. (Hint: one possible solution involves using the fact that Figure 3.11 implies the remainder register can be shifted either direction.)
#### fig 3.9
![](https://i.imgur.com/J8W1qi3.png)
#### fig 3.10
![](https://i.imgur.com/XupNuy0.png)
#### fig 3.11
![](https://i.imgur.com/MceJQhm.png)
### Answer
![](https://i.imgur.com/TP0H9Wq.png)

## 3.22
### question
* What decimal number does the bit pattern 0×0C000000 represent if it is a floating point number? Use the IEEE 754 standard.
### Answer
![](https://i.imgur.com/aiV8WmA.png)

## 3.26
### question
* Write down the binary bit pattern to represent $-1.5625 \times 10^{-1}$ assuming a format similar to that employed by the DEC PDP-8 (the left most 12 bits are the exponent stored as a two’s complement number, and the rightmost 24 bits are the fraction stored as a two’s complement number). No hidden 1 is used. Comment on how the range and accuracy of this 36-bit pattern compares to the single and double precision IEEE 754 standards.
### Answer
![](https://i.imgur.com/mL498j5.png)

## 3.27
### question
* IEEE 754-2008 contains a half precision that is only 16 bits wide. Th e left most bit is still the sign bit, the exponent is 5 bits wide and has a bias of 15, and the mantissa is 10 bits long. A hidden 1 is assumed. Write down the bit pattern to represent $-1.5625 \times 10^{-1}$ assuming a version of this format, which uses an excess-16 format to store the exponent. Comment on how the range and accuracy of this 16-bit floating point format compares to the single precision IEEE 754 standard.
### Answer
![](https://i.imgur.com/eaMn4rk.png)

## 3.28
### question
* The Hewlett-Packard 2114, 2115, and 2116 used a format with the left most 16 bits being the fraction stored in two’s complement format, followed by another 16-bit field which had the left most 8 bits as an extension of the fraction (making the fraction 24 bits long), and the rightmost 8 bits representing the exponent. However, in an interesting twist, the exponent was stored in sign magnitude format with the sign bit on the far right! Write down the bit pattern to represent $-1.5625 \times 10^{-1}$ assuming this format. No hidden 1 is used. Comment on how the range and accuracy of this 32-bit pattern compares to the single precision IEEE 754 standard.
### Answer
![](https://i.imgur.com/FrQ5DFP.png)

## 3.29
### question
* Calculate the sum of $2.6125 \times 10^{1}$ and $4.150390625 \times 10^{-1}$ by hand, assuming A and B are stored in the 16-bit half precision described in Exercise 3.27. Assume 1 guard, 1 round bit, and 1 sticky bit, and round to the nearest even. Show all the steps.
### answer
![](https://i.imgur.com/Fz2ck6H.png)

## 3.32
### question
* > Calculate $3.984375 \times 10^{-1} + 3.4375 \times 10^{-1} + 1.771 \times 10^3$ by hand, assuming each of the values are stored in the 16-bit half precision format described in Exercise 3.27 (and also described in the text). Assume 1 guard, 1 round bit, and 1 sticky bit, and round to the nearest even. Show all the steps, and write your answer in both the 16-bit floating point format and in decimal.
### answer
![](https://i.imgur.com/Fkz9U4L.png)

## 3.36
### question
* Calculate $3.41796875 \times 10^3 \times (6.34765625 \times 103 \times 1.05625 \times 10^2)$ by hand, assuming each of the values are stored in the 16-bit half precision format described in Exercise 3.27 (and also described in the text). Assume 1 guard, 1 round bit, and 1 sticky bit, and round to the nearest even. Show all the steps, and write your answer in both the 16-bit floating point format and in decimal.
### Answer
![](https://i.imgur.com/nLkzFCH.png)

## 3.38
### question
* Calculate $1.666015625 \times 10^0\times (1.9760 \times 10^4 -1.9744 \times 10^4)$ by hand, assuming each of the values are stored in the 16-bit half precision format described in Exercise 3.27 (and also described in the text). Assume 1 guard, 1 round bit, and 1 sticky bit, and round to the nearest even. Show all the steps, and write your answer in both the 16-bit floating point format and in decimal.
### Answer
![](https://i.imgur.com/IXNVjJb.png)

## 3.42
### question
* What do you get if you add -1/4 to itself 4 times? What is $1/4 \times 4$? Are they the same? What should they be?
### Answer
![](https://i.imgur.com/eEgX76L.png)

## 3.44
### question
* Write down the bit pattern in the fraction 1/3 assuming a floating point format that uses Binary Coded Decimal (base 10) numbers in the fraction instead of base 2. Assume there are 24 bits, and you do not need to normalize. Is this representation exact?
### Answer
![](https://i.imgur.com/UZfmal1.png)

## 3.46
### question
* Write down the bit pattern assuming that we are using base 30 numbers in the fraction instead of base 2. (Base 16 numbers use the symbols 0–9 and A–F. Base 30 numbers would use 0–9 and A–T.) Assume there are 20 bits, and you do not need to normalize. Is this representation exact?
### Answer
![](https://i.imgur.com/6rfPggy.png)

# chapter  4
## 4.2
### Question
* The basic single-cycle MIPS implementation in Figure 4.2 can only implement some instructions. New instructions can be added to an existing Instruction Set Architecture (ISA), but the decision whether or not to do that depends, among other things, on the cost and complexity the proposed addition introduces into the processor datapath and control. Th e first three problems in this exercise refer to the new instruction:
* Instruction: LWI Rt,Rd(Rs)
* Interpretation: Reg[Rt] = Mem[Reg[Rd]+Reg[Rs]]
#### fig 4.2
![](https://i.imgur.com/NkChxWd.png)
#### 4.2.1  
##### Q
* Which existing blocks (if any) can be used for this instruction?
##### A
![](https://i.imgur.com/eRhNXdR.png)

#### 4.2.2
##### Q
* Which new functional blocks (if any) do we need for this instruction?
##### A
![](https://i.imgur.com/mOPZLAj.png)
#### 4.2.3 
##### Q
* What new signals do we need (if any) from the control unit to support this instruction?
##### A
![](https://i.imgur.com/dFRsrlJ.png)

## 4.4
### Question
* Problems in this exercise assume that logic blocks needed to implement a processor’s datapath have the following latencies:
* ![](https://i.imgur.com/VBQudAw.png)
#### 4.4.1  
* If the only thing we need to do in a processor is fetch consecutive instructions (Figure 4.6), what would the cycle time be?
##### fig 4.6
![](https://i.imgur.com/MHgMKw3.png)
##### A
![](https://i.imgur.com/q1WOCmO.png)

#### 4.4.2 
* Consider a datapath similar to the one in Figure 4.11, but for a processor that only has one type of instruction: unconditional PC-relative branch. What would the cycle time be for this datapath?
##### fig 4.11
![](https://i.imgur.com/XlmQ1YI.png)
##### A
![](https://i.imgur.com/OuRgolR.png)

#### 4.4.3 
* Repeat 4.4.2, but this time we need to support only conditional PC-relative branches. The remaining three problems in this exercise refer to the datapath element Shift - left -2:
##### A
![](https://i.imgur.com/4IxaF09.png)

#### 4.4.4
* Which kinds of instructions require this resource?
##### A
![](https://i.imgur.com/No9rLzN.png)

#### 4.4.5
* For which kinds of instructions (if any) is this resource on the critical path?
##### A
![](https://i.imgur.com/QsG7EhZ.png)

#### 4.4.6 
* Assuming that we only support beq and add instructions, discuss how changes in the given latency of this resource affect the cycle time of the processor. Assume that the latencies of other resources do not change.
##### A
![](https://i.imgur.com/4gQ3aQh.png)

## 4.7
### Question
* In this exercise we examine in detail how an instruction is executed in a single-cycle datapath. Problems in this exercise refer to a clock cycle in which the processor fetches the following instruction word:
10101100011000100000000000010100.
* Assume that data memory is all zeros and that the processor’s registers have the following values at the beginning of the cycle in which the above instruction word is fetched:
![](https://i.imgur.com/mWH5GBT.png)
#### 4.7.1 
* What are the outputs of the sign-extend and the jump “Shift left 2” unit (near the top of Figure 4.24) for this instruction word?
##### figure 4.24
![](https://i.imgur.com/37KJpNZ.png)
##### A
![](https://i.imgur.com/qmbvStd.png)
#### 4.7.2 
* What are the values of the ALU control unit’s inputs for this instruction?
##### A
![](https://i.imgur.com/dC1NHhm.png)
#### 4.7.3
*  What is the new PC address aft er this instruction is executed? Highlight the path through which this value is determined.
##### A
![](https://i.imgur.com/alsU8S5.png)

#### 4.7.4
* For each Mux, show the values of its data output during the execution of this instruction and these register values.
##### A
#### 4.7.5
* For the ALU and the two add units, what are their data input values?
##### A
![](https://i.imgur.com/DcreXxA.png)
#### 4.7.6 
*  What are the values of all inputs for the “Registers” unit?
##### A
*  ![](https://i.imgur.com/HgqILZN.png)
## 4.9
### question
* In this exercise, we examine how data dependences aff ect execution in the basic 5-stage pipeline described in Section 4.5. Problems in this exercise refer to the
* following sequence of instructions:
```
or r1,r2,r3
or r2,r1,r4
or r1,r1,r2
```
* Also, assume the following cycle times for each of the options related to forwarding:
![](https://i.imgur.com/m3zehZK.png)
#### 4.9.1
* Indicate dependences and their type.
##### A
![](https://i.imgur.com/dSFRRWT.png)

#### 4.9.2
* Assume there is no forwarding in this pipelined processor. Indicate hazards and add nop instructions to eliminate them.
##### A
![](https://i.imgur.com/QB5jxSi.png)

#### 4.9.3
* Assume there is full forwarding. Indicate hazards and add NOP instructions to eliminate them
##### A
![](https://i.imgur.com/1rlsANH.png)

#### 4.9.4
* the total execution time of this instruction sequence without forwarding and with full forwarding? What is the speedup achieved by adding full forwarding to a pipeline that had no forwarding?
##### A
![](https://i.imgur.com/HbDQHDg.png)

#### 4.9.5
* Add nop instructions to this code to eliminate hazards if there is ALU-ALU forwarding only (no forwarding from the MEM to the EX stage).
##### A
![](https://i.imgur.com/7D8PYCz.png)
#### 4.9.6
* What is the total execution time of this instruction sequence with only ALU-ALU forwarding? What is the speedup over a no-forwarding pipeline?
##### A
![](https://i.imgur.com/0mzDasW.png)

## 4.11
### Question
* Consider the following loop.
```
loop:	lw r1,0(r1)
 		and r1,r1,r2
 		lw r1,0(r1)
 		lw r1,0(r1)
		beq r1,r0,loop
```
* Assume that perfect branch prediction is used (no stalls due to control hazards), that there are no delay slots, and that the pipeline has full forwarding support. Also assume that many iterations of this loop are executed before the loop exits.
#### 4.11-1
* Show a pipeline execution diagram for the third iteration of this loop, from the cycle in which we fetch the first instruction of that iteration upto (but not including) the cycle in which we can fetch the first instruction of the next iteration. Show all instructions that are in the pipeline during these cycles (not just those from the third iteration).
##### A
![](https://i.imgur.com/4gGNOK4.png)

#### 4.11-2
*  How oft en (as a percentage of all cycles) do we have a cycle in which all five pipeline stages are doing useful work?
##### A
![](https://i.imgur.com/VxVK7u6.png)

## 4.12
### Question
* This exercise is intended to help you understand the cost/complexity/performance trade-off s of forwarding in a pipelined processor. Problems in this exercise refer to pipelined datapaths from Figure 4.45. These problems assume that, of all the instructions executed in a processor, the following fraction of these instructions have a particular type of RAW data dependence. Th e type of RAWdata dependence is identified by the stage that produces the result (EX or MEM) and the instruction that consumes the result (1st instruction that follows the one that produces the result, 2nd instruction that follows, or both). We assume that the register write is done in the first half of the clock cycle and that register reads aredone in the second half of the cycle, so “EX to 3rd” and “MEM to 3rd” dependences are not counted because they cannot result in data hazards. Also, assume that the CPI of the processor is 1 if there are no data hazards.
* ![](https://i.imgur.com/4y6bFBu.png)
* Assume the following latencies for individual pipeline stages. For the EX stage, latencies are given separately for a processor without forwarding and for a processor with different kinds of forwarding.
![](https://i.imgur.com/1lxqAlW.png)
#### figure 4.45
![](https://i.imgur.com/Rl9eYVk.png)

#### 4.12-1
* If we use no forwarding, what fraction of cycles are we stalling due to data hazards?
##### A
![](https://i.imgur.com/KhPq2Cs.png)

#### 4.12-2
* If we use full forwarding (forward all results that can be forwarded), what fraction of cycles are we staling due to data hazards?
##### A
![](https://i.imgur.com/pz2iHIe.png)
#### 4.12-3
* > Let us assume that we cannot afford to have three-input Muxes that are needed for full forwarding. We have to decide if it is better to forward only from the EX/MEM pipeline register (next-cycle forwarding) or only from the MEM/WB pipeline register (two-cycle forwarding). Which of the two options results in fewer data stall cycles?
##### A
![](https://i.imgur.com/Zp61tnP.png)
#### 4.12-4
* For the given hazard probabilities and pipeline stage latencies, what is the speedup achieved by adding full forwarding to a pipeline that had no forwarding?
##### A
![](https://i.imgur.com/KPfHKEA.png)
#### 4.12-5
* What would be the additional speedup (relative to a processor with forwarding) if we added time-travel forwarding that eliminates all data hazards? Assume that the yet-to-be-invented time-travel circuitry adds 100 ps to the latency of the full-forwarding EX stage.
##### A
![](https://i.imgur.com/aFjcCiR.png)
#### 4.12-6
* Repeat 4.12.3 but this time determine which of the two options results in shorter time per instruction.
##### A
![](https://i.imgur.com/1AnVLoh.png)
## 4.13
### Question
* Th is exercise is intended to help you understand the relationship between forwarding, hazard detection, and ISA design. Problems in this exercise refer to the following sequence of instructions, and assume that it is executed on a 5-stage pipelined datapath:
```
add r5,r2,r1
lw r3,4(r5)
lw r2,0(r2)
or r3,r5,r3
sw r3,0(r5)
```
#### 4.13.1
* If there is no forwarding or hazard detection, insert nops to ensure correct execution.
##### A
![](https://i.imgur.com/Fbeeeg4.png)

#### 4.13.2
* Repeat 4.13.1 but now use nops only when a hazard cannot be avoided by changing or rearranging these instructions. You can assume register R7 can be used to hold temporary values in your modified code.
##### A
![](https://i.imgur.com/fXzE2S9.png)

#### 4.13.3
* If the processor has forwarding, but we forgot to implement the hazard detection unit, what happens when this code executes?
##### A
![](https://i.imgur.com/Z6vNChD.png)

#### 4.13.4
* If there is forwarding, for the first five cycles during the execution of this code, specify which signals are asserted in each cycle by hazard detection and forwarding units in Figure 4.60.

##### figure 4.60
![](https://i.imgur.com/tVyOtUE.png)
##### A
![](https://i.imgur.com/RjtlS6r.png)

#### 4.13.5
* If there is no forwarding, what new inputs and output signals do we need for the hazard detection unit in Figure 4.60? Using this instruction sequence as an example, explain why each signal is needed.
##### A
![](https://i.imgur.com/17qSmir.png)

#### 4.13.6
* For the new hazard detection unit from 4.13.5, specify which output signals it asserts in each of the first five cycles during the execution of this code.
##### A
![](https://i.imgur.com/GexrI8l.png)

## 4.14
### Question
* Th is exercise is intended to help you understand the relationship between delay slots, control hazards, and branch execution in a pipelined processor. In this exercise, we assume that the following MIPS code is executed on a pipelined processor with a 5-stage pipeline, full forwarding, and a predict-taken branch predictor:
```
 	lw r2,0(r1)
label1: beq r2,r0,label2 # not taken once, then taken
 	lw r3,0(r2)
 	beq r3,r0,label1 # taken
 	add r1,r3,r1
label2: sw r1,0(r2)
```
#### 4.14.1
* Draw the pipeline execution diagram for this code, assuming there are no delay slots and that branches execute in the EX stage.
##### A
![](https://i.imgur.com/B6EQjqe.png)

#### 4.14.2
* Repeat 4.14.1, but assume that delay slots are used. In the given code, the instruction that follows the branch is now the delay slot instruction for that branch
##### A
![](https://i.imgur.com/eRdlK6d.png)

#### 4.14.3
* One way to move the branch resolution one stage earlier is to not need an ALU operation in conditional branches. The branch instructions would be “bez rd,label” and “bnez rd,label”, and it would branch if the register has and does not have a zero value, respectively. Change this code to use these branch instructions instead of beq. You can assume that register R8 is available for you to use as a temporary register, and that an seq (set if equal) R-type instruction can be used. Section 4.8 describes how the severity of control hazards can be reduced by moving branch execution into the ID stage. Th is approach involves a dedicated comparator in the ID stage, as shown in Figure 4.62. However, this approach potentially adds to the latency of the ID stage, and requires additional forwarding logic and hazard detection.
##### A
![](https://i.imgur.com/1uzYQkT.png)

#### 4.14.4
* Using the first branch instruction in the given code as an example, describe the hazard detection logic needed to support branch execution in the ID stage as in Figure 4.62. Which type of hazard is this new logic supposed to detect?
##### fig 4.62
![](https://i.imgur.com/0PsLIwT.png)
##### A
![](https://i.imgur.com/VVAuY2A.png)

#### 4.14.5
* For the given code, what is the speedup achieved by moving branch execution into the ID stage? Explain your answer. In your speedup calculation, assume that the additional comparison in the ID stage does not affect clock cycle time.
##### A
![](https://i.imgur.com/KDjXx7E.png)

#### 4.14.6
* Using the fi rst branch instruction in the given code as an example, describe the forwarding support that must be added to support branch execution in the ID stage. Compare the complexity of this new forwarding unit to the complexity of the existing forwarding unit in Figure 4.62.
##### A
![](https://i.imgur.com/WpEkFL1.png)

## 4.15
### Question
* The importance of having a good branch predictor depends on how often conditional branches are executed. Together with branch predictor accuracy, this will determine how much time is spent stalling due to mispredicted branches. In this exercise, assume that the breakdown of dynamic instructions into various instruction categories is as follows:
* ![](https://i.imgur.com/2mdNINd.png)
* Also, assume the following branch predictor accuracies:
* ![](https://i.imgur.com/lHjEulG.png)
#### 4.15.1 
* Stall cycles due to mispredicted branches increase the CPI. What is the extra CPI due to mispredicted branches with the always-taken predictor? Assume that branch outcomes are determined in the EX stage, that there are no data hazards, and that no delay slots are used.
##### A
![](https://i.imgur.com/GwKegxh.png)

#### 4.15.2 
* Repeat 4.15.1 for the “always-not-taken” predictor.
##### A
![](https://i.imgur.com/QbmJkld.png)

#### 4.15.3 
* Repeat 4.15.1 for for the 2-bit predictor.
##### A
![](https://i.imgur.com/tWbLIKw.png)

#### 4.15.4 
* With the 2-bit predictor, what speedup would be achieved if we could convert half of the branch instructions in a way that replaces a branch instruction with an ALU instruction? Assume that correctly and incorrectly predicted instructions have the same chance of being replaced.
##### A
![](https://i.imgur.com/Y0topUD.png)

#### 4.15.5 
* With the 2-bit predictor, what speedup would be achieved if we could convert half of the branch instructions in a way that replaced each branch instruction with two ALU instructions? Assume that correctly and incorrectly predicted instructions have the same chance of being replaced.
##### A
![](https://i.imgur.com/wVCnVD2.png)

#### 4.15.6 
* Some branch instructions are much more predictable than others. If we know that 80% of all executed branch instructions are easy-to-predict loop-back branches that are always predicted correctly, what is the accuracy of the 2-bit predictor on the remaining 20% of the branch instructions?
##### A
![](https://i.imgur.com/k6BKiBN.png)

## 4.16
### Question
* This exercise examines the accuracy of various branch predictors for the following repeating pattern (e.g., in a loop) of branch outcomes: T, NT, T, T, NT
#### 4.16.1 
* What is the accuracy of always-taken and always-not-taken predictors for this sequence of branch outcomes?
##### A
![](https://i.imgur.com/4yuW2Vn.png)

#### 4.16.2 
* What is the accuracy of the two-bit predictor for the first 4 branches in this pattern, assuming that the predictor starts off in the bottom left state from Figure 4.63 (predict not taken)?
##### fig 4.63
![](https://i.imgur.com/38s5dhT.png)
##### A
| State | 左下 | 右下 | 左下 | 右下 |
| -------- | -------- | --- | --- | -------- |
| Perdict  |    NT    |  NT |  NT |  NT      |
| Outcome  |    T     |  NT |  T  |  T       |
* Accuracy: 1/4 = 25% 

#### 4.16.3 
* What is the accuracy of the two-bit predictor if this pattern is repeated forever?
##### A
![](https://i.imgur.com/Fn5zvBU.png)

#### 4.16.4 
* Design a predictor that would achieve a perfect accuracy if this pattern is repeated forever. You predictor should be a sequential circuit with one output that provides a prediction (1 for taken, 0 for not taken) and no inputs other than the clock and the control signal that indicates that the instruction is a conditional branch.
##### A
![](https://i.imgur.com/fpmCH24.png)

#### 4.16.5
* What is the accuracy of your predictor from 4.16.4 if it is given a repeating pattern that is the exact opposite of this one?
##### A

![](https://i.imgur.com/wiKWdRO.png)

#### 4.16.6 
* Repeat 4.16.4, but now your predictor should be able to eventually (after a warm-up period during which it can make wrong predictions) start perfectly predicting both this pattern and its opposite. Your predictor should have an input that tells it what the real outcome was. Hint: this input lets your predictor determine which of the two repeating patterns it is given.
##### A
![](https://i.imgur.com/4URjW7Z.png)

###### tags: `Computer Architecture` `CSnote`