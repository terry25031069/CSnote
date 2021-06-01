---
title: CMP Arch Chapter 2
---
# Instructions:Language of the Computer
## 2.1 Introduction
* instruction set
	* Command understood by a given architecture
	* Different in different architecture
* MIPS Instruction set
	* Large share in commercial market
	* Typical of many modern ISAs
		* E.G. ARMv7, intel x86, ARMv8
## 2.2 Operations of the Computer Hardware
![](https://i.imgur.com/vs68wY0.png)
## 2.3 Operands of the Computer Hardware
*  MIPS has 32 registers
*  2^30 memory words
![](https://i.imgur.com/ecqAiS1.png)
![](https://i.imgur.com/rNjsG6I.png)
* Data transfer instructions
	* Load(lw)
	* Store(sw)
![](https://i.imgur.com/PIqx6eS.png)
* Memory is byte addressed
	* Each address identifies an 8-bit byte
* Alignment restriction
	* Words must start at addresses that are a multiple of 4
* MIPS is Big Endian
	* Most significant byte at least significant address of a word
		* start from lower address
* Registers v.s. memory
	* Registers are faster to access than memory
* Operating on memory data requires load and store
	* more instructions
* MIPS register 0($zero) is the constant 0
	* cannot be overwritten
* Useful for common operation
	* E.G. move between registers
`add $t2 $s1 $zero`
## 2.4 Signed and Unsigned Numbers
* skip 
## 2.5 Representing Instructions in the Computer
* symbolically
	* add $t0,\$s1,$s2
* Decimal 
![](https://i.imgur.com/wZ6KD8d.png)

* binary 
	![](https://i.imgur.com/PLXkxUV.png)
	
### R-type
* the format is called R-type (for register) or R-format. 
![](https://i.imgur.com/7Mc0saT.png)
* Mips field
	* op: Basic operation of the instruction, traditionally called the opcode.
	* rs: The first register source operand.
	* rt: The second register source operand.
	* rd: The register destination operand. It gets the result of the operation.
	* shamt: Shift amount. (Section 2.6 explains shift instructions and this term; it will not be used until then, and hence the field contains zero in this section.)
	* funct: Function. Th is field, oft en called the function code, selects the specific variant of the operation in the op field
![](https://i.imgur.com/gsgalRn.png)
#### I-type
* I-format and is used by the immediate and data transfer instructions.

![](https://i.imgur.com/ThkcID0.png)
* rt destination or source he second register source operand.
* constant $-2^{15} \sim 2^{15}-1$
![](https://i.imgur.com/bcgtNZN.png)

## 2.6 Logical Operations
* Bit-wise operation
	* ![](https://i.imgur.com/wLnLtkL.png)
	* Useful for extracting and inserting groups of bits in a word
## 2.7 Instructions for Making Decisions
* Conditional branch
	* Branch to a labeled statement if a conditon is true
	* beq rs,rt, L1
		* if( rs == rt) branch to statement label l1
		* * Branch to a loabeled statement if a conditoin is rie
	* bne rs,rt, L1
		* if( rs != rt) branch to statement label l1
	* Set result to 1 if a condition is true, otherwise set to 0
		* slt rd,rs,rt
			* if(rs<rt)rd =1; else rd =0
		* slti rt,rs,constant
			* if(rs<constant)rt =1,else rt =0
* Unconditional branch
	* j L1
		* jump to statement labeled L1
![](https://i.imgur.com/nW5xzLI.png)
* A basic block is a sequence of instructions with
	* No embedded branches
	* no branch target
		* A compiler identifies basic blocks optimization
		* an advanced processor can accelerate execution of basic blocks
### Branch  instruction design
* why not blt(lt stands for less then), bge(ge = greater or equal),...?
* hardware for $\geq , \le$ slower than $=,!=$
	* combining with branch involves more work per instruction, requiring a slower clock
	* all instruction will be slower
* beq and bne are the common case, thus this is a good compromise
### signed vs unsigned
* signed comparison slt, slti
* unigned comparison sltu, sltiu
### case/switch
* a chain of if-then-else statements
* jump address table or jump table
	* a table of addresses of alternative instruction sequence
	* a program loads the appropriate entry from the jump table into a register
	* jump to the address in the register using jump register instruction(ir)
## 2.8 Supporting Procedures in Computer hardware
### Steps required for procedure calling
1. Put parameters in a place where the procedure can access them.
2. Transfer control to the procedure.
3. Acquire the storage resources needed for the procedure.
4. Perform the desired task.
5. Put the result value in a place where the calling program can access it.
6. Return control to the point of origin, since a procedure can be called from several points in a program
*  registers are the fastest place to hold data in a computer
*  MIPS soft ware follows the following convention for procedure calling in allocating its 32 registers:
	*  $a0–a3$: four argument registers in which to pass parameters
	* $v0–v1$: two value registers in which to return values
	*  $ra$ : one return address register to return to the point of origin
	
### Procedure call instructions
* jump-and-link instruction (jal) 
	* writen:` jal ProcedureAddress`
	* follwing instruction is stored in $ra
* jump to target address
	* jump register
	* writen:` jr $ra`
	* copy $ra to program counter
	* can also be used to computed jumps
		* e.g. for case/switch statements
### Leaf procedure
#### Example
* C code
```
int leaf_example (int g, int h, int i, int j)
{
 int f;
 f = (g + h) – (i + j);
 return f;
}
```
* Equivalent MIPS code
![](https://i.imgur.com/oTDLWap.png)

* To avoid saving and restoring a register whose value is never used, which might happen with a temporary register, MIPS soft ware separates 18 of the registers into two groups:
* $t0–$t9: temporary registers that are not preserved by the callee (called procedure) on a procedure call
* $s0–$s7: saved registers that must be preserved on a procedure call (if used, the callee saves and restores them)
* Only code
* ![](https://i.imgur.com/NZH46iX.png)
* ![](https://i.imgur.com/iiZr0Kz.png)
#### Non-leaf procedure
* Procedures that call other procedures
* For nested call, caller needs to save on the
	* stack:
		* Its return address
		* Any arguments and temporaries needed after the call
		* Restore from the stack after the call
		* 
		* 
##### Example
Let’s tackle a recursive procedure that calculates factorial:
```
int fact (int n)
{
 if (n < 1) return (1);
 else return (n * fact(n – 1));
}
```
What is the MIPS assembly code?
![](https://i.imgur.com/Tap6nFq.png)
![](https://i.imgur.com/1VmrwqT.png)
### Allocating Space for New Data on the Stack
![](https://i.imgur.com/8LwibIc.png)

* local data on the stack
	* Local data allocated by callee
		*  e.g., C automatic variables
	* Procedure frame (activation record)
		* Used by some compilers to manage stack storage
### Allocating Space for New Data on the Heap
* Text: program code
	* Static data: global variables
		* e.g., static variables in C,constant arrays and strings
		* $gp initialized to address allowing ±offsets into this * segment
* Dynamic data: heap
	* E.g., malloc in C, new in Java
	* Stack: automatic storage
![](https://i.imgur.com/aaQE8uO.png)
![](https://i.imgur.com/907drLg.png)
## Communicating with people
### Character Data
* Byte-encoded character sets
	* ASCII: 128 characters
		* 95 graphic, 33 control
	* Latin-1: 256 characters
		* ASCII, +96 more graphic characters
* Unicode: 32-bit character set
	* Used in Java, C++ wide characters, …
	* UTF-8, UTF-16: variable-length encodings
### byte half word
* Could use bitwise operations
* MIPS byte/halfword load/store
	* String processing is a common case
* `lb rt, offset(rs) lh rt, offset(rs)`
	* Sign extend to 32 bits in rt
* `lbu rt, offset(rs) lhu rt, offset(rs)`
	* Zero extend to 32 bits in rt
* `sb rt, offset(rs) sh rt, offset(rs)`
	* Store just rightmost byte/halfword
### String Copy
* C code (naïve):
	* Null-terminated string
* The procedure strcpy copies string y to string x using the null byte
* termination convention of C:
```
void strcpy (char x[], char y[])
{
 int i;
 i = 0;
 while ((x[i] = y[i]) != ‘\0’) /* copy & test byte */
 i += 1;
}
```
What is the MIPS assembly code?
![](https://i.imgur.com/a8wOxVw.png)
![](https://i.imgur.com/2jCSVdP.png)
## 2.10 MIPS Addressing for 32-bit Immediates and Addresses
* Most constants are small
	* 16-bit immediate is sufficient
* For the occasional 32-bit constant
	* `lui rt, constant`
	* Copies 16-bit constant to left 16 bits of rt
	* Clears right 16 bits of rt to 0
#### example
What is the MIPS assembly code to load this 32-bit constant into register $s0?
0000 0000 0011 1101 0000 1001 0000 0000
First, we would load the upper 16 bits, which is 61 in decimal, using lui:
lui $s0, 61 # 61 decimal = 0000 0000 0011 1101 binary
Th e value of register $s0 aft erward is
0000 0000 0011 1101 0000 0000 0000 0000
Th e next step is to insert the lower 16 bits, whose decimal value is 2304:
ori $s0, $s0, 2304 # 2304 decimal = 0000 1001 0000 0000
Th e fi nal value in register $s0 is the desired value:
0000 0000 0011 1101 0000 1001 0000 0000


![](https://i.imgur.com/rHspgKA.png)
### Addressing in Branches and Jumps
* Branch instructions specify
	* Opcode, two registers, target address
* Most branch targets are near branch
	* Forward or backward
	* op, rs, rt, constant or address
![](https://i.imgur.com/LVTCnzD.png)

* PC-relative addressing
	* Target address = PC + offset × 4
	* PC already incremented by 4 by this time
Jump Addressing
* Jump (j and jal) targets could be
anywhere in text segment
* Encode full address in instruction
op address 6 bits 26 bits
* (Pseudo) Direct jump addressing
* Target address = PC31…28 : (address
× 4)

![](https://i.imgur.com/0oqLMfW.png)

Branching Far Away
Given a branch on register $s0 being equal to register $s1,
`beq $s0, $s1, L1`
replace it by a pair of instructions that off ers a much greater branching distance.
Th ese instructions replace the short-address conditional branch:
```
bne $s0, $s1, L2
j L1
L2:
```
![](https://i.imgur.com/tdP6ECC.png)
## 2.11 Parallelism and Instructions: Synchronization
Two processors sharing an area of memory
 P1 writes, then P2 reads
 Data race if P1 and P2 don’t synchronize
 Result depends of order of accesses
 Hardware support required
 Atomic read/write memory operation
 No other access to the location allowed between the read and
write
 Could be a single instruction
 E.g., atomic swap of register
↔ memory
 Or an atomic pair of instructions
![](https://i.imgur.com/VApm2mq.png)
# QE
## 2.2
![](https://i.imgur.com/DTz6DOa.png)
![](https://i.imgur.com/USXk3WA.png)
## 2.4
![](https://i.imgur.com/GN2o3zq.png)
![](https://i.imgur.com/l5rVryE.png)
## 2.6
![](https://i.imgur.com/Q04fAJB.png)
![](https://i.imgur.com/8r2pouG.png)
## 2.8
![](https://i.imgur.com/IJnXcyc.png)
![](https://i.imgur.com/f5EaXZg.png)
## 2.10
![](https://i.imgur.com/Rm5UrzE.png)
![](https://i.imgur.com/K7xVDR4.png)
## 2.12
![](https://i.imgur.com/beu02IU.png)
![](https://i.imgur.com/EUnYeo8.png)
## 2.14
![](https://i.imgur.com/1DoqsF5.png)
![](https://i.imgur.com/8W1UuCs.png)
## 2.16
![](https://i.imgur.com/PR6hqo6.png)
![](https://i.imgur.com/ywbIUwR.png)
## 2.18
![](https://i.imgur.com/wqMnGxk.png)
![](https://i.imgur.com/EgMjPHs.png)
## 2.20
![](https://i.imgur.com/Gd006dc.png)
![](https://i.imgur.com/WanZU7K.png)
## 2.22
![](https://i.imgur.com/7A3Rkt6.png)
![](https://i.imgur.com/6kpuy8H.png)
## 2.24
![](https://i.imgur.com/WFrXlPZ.png)
![](https://i.imgur.com/RhOIGyY.png)
## 2.26
![](https://i.imgur.com/JtIRkF7.png)
![](https://i.imgur.com/aG4N36Z.png)
## 2.28
![](https://i.imgur.com/5boLDyv.png)
![](https://i.imgur.com/3mwfnXd.png)
## 2.29
![](https://i.imgur.com/JD3Zg8F.png)
![](https://i.imgur.com/31nhG6R.png)
## 2.31
![](https://i.imgur.com/G72NTVy.png)
![](https://i.imgur.com/n8T7Y1C.png)
## 2.34
![](https://i.imgur.com/GavsjXU.png)
![](https://i.imgur.com/kOsbpES.png)
## 2.36
![](https://i.imgur.com/klLtPpm.png)
![](https://i.imgur.com/gQRtvCC.png)
## 2.38
![](https://i.imgur.com/7gYLdI7.png)
![](https://i.imgur.com/Dm5aNNv.png)
## 2.40
![](https://i.imgur.com/4Nu2NIe.png)
![](https://i.imgur.com/ApFhYRV.png)
## 2.42
![](https://i.imgur.com/ePcxuZR.png)
![](https://i.imgur.com/g6Hr8OK.png)
## 2.43
![](https://i.imgur.com/eSwvJZL.png)
![](https://i.imgur.com/65YSuPy.png)
## 2.44
![](https://i.imgur.com/m2mYyWg.png)
![](https://i.imgur.com/sKYU29J.png)
## 2.46
![](https://i.imgur.com/EQ4vkCt.png)
![](https://i.imgur.com/LinCf6y.png)
## 2.47
![](https://i.imgur.com/Ra2hjsd.png)
![](https://i.imgur.com/Uu0SFxc.png)

###### tags: `Computer Architecture` `CSnote`