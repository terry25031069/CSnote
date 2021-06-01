# 微算機與組合語言 Microprocessor & Assembly language

# Chapter 2

## Internal architecture
### BIU (Bus Interface Unit)
* Performing external bus operations
* e.g. Fetch Instruction and data
### EU (Execution Unit)
* perform operations

![](https://i.imgur.com/WcF2c3t.jpg)
### BIU prefetch instructions into instruction queue
### Register
* segment
* pointer
* data
### ALU (Arithmetic logic unit)
### Flags
* status
* control
![](https://i.imgur.com/oNV2KYy.jpg)
## Register
32 bits: 80286 above
### Instruction Pointer
### Segment Register
* CS (Code Segment) + IP (Instruction Pointer)
* DS (Data Segment) + SI (Source Index)
* ES (Extra Segment) + DI (Destination Index)
* SS (Stack Segment) + SP (Stack Pointer)/BP (Base Pointer)
### Data Register
* AX (Accumulator)
* BX (Base)
* CX (Counter)
* DX (Data)
### Pointer & Index
* BP (Base Pointer)
* SP (Stack Pointer)
* SI (Source Index)
* DI (Destination Index)
### Status Register
#### Status flags
##### CF (Carry Flag): 
* is set if there is a carry-out or a borrow-in for the most significant bit of the result 
* 最高位借進位時，CF=1
##### PF (Parity Flag): 
* is set if the result produced by the instruction has even parity. 
* If the parity is odd, PF reset
* 結果有偶數個位元=1時，PF=1
##### AF (Auxiliary Flag): 
* Is set if there is a carry-out from the low nibble into the high nibble. Otherwise AF is reset.
* 將暫存器長度切為一半 (nibble)，若低 nibble 有進位至高 nibble，AF=1
* 比如 16-bit register，從第7位進位到第8位時(最低位為第0位)，AF=1
##### ZF (Zero Flag):
* Is set if the result produced by an instruction is zero. Otherwise, ZF is reset
* 結果是0，ZF=1
##### SF (Signed Flag):
* The MSB (Most Significant Bit) of the result is copied into SF. 
* Is set if the result is a negative, reset if it is positive
* 結果最高位(負數)=1，SF=1
##### OF (Overload Flag):
* Is set if the signed result out of range, otherwise remains reset
* 溢位時，OF=1
#### Control flags
##### TF (Trap Flag):
* If TF is set, 8088 goes into the single-step mode. 
* Very useful for debugging programs
* 開下去會逐步執行，所以常拿來除錯
##### DF (Direction Flag):
* Determine the direction in which string operations will occur. When set, the string instruction automatically decrements the address; 
* if reset the string address will be incremented 
* 如果 DF=1，將由高位元讀到低位元
##### IF (Interrupt Flag):
* For the 8088 to recognize maskable interrupt requests at its interrupt (INT) input, the IF must be set
* When IF is reset, requests at INT are ignored and the maskable interrupt interface is disabled.
* Maskable interrupt v.s. Non-maskable  interrupt (highest priority of interrupt)


# Chapter 3
 
## Native language is machine language 
### A program written in language is often called machine code 
* encoded using  0, 1
### An instruction can be divided into two parts (Operation code)
* operation code (opcode)
* operands
### Each opcode is assigned a unique letter combination called a menmonic
* MOV AX, BX
* move bx register to ax register

## Advantages of assembly program than high-level program
### Small code size
* Useful for limited memory space
### Short execution time
* Useful for real-time app. or time-sensitive app. 
### Low lever control 
* Device service routines

## Addressing mode 
Access different type of operands, the 8088 is provided with various addressing modes
### Specify an operand
* register addressing mode
* immediate addressing mode
* memory addressing mode (direct, register indirect, based, indexed, based-indexed)
### Register operand addressing mode
* 所指定的就是 register 裡面的內容
* MOV AX, BX
### Immediate operand addressing mode
* 後面那個就是值，帶進去前面的暫存器就好
* MOV AX, 12h
### Memory operand addressing mode
Physical address is computed from a segment base address and effective address   

Five memory operand addressing modes
* Displacement: direct addressing mode
* BX, BP, SI, DI: register indirect
* BX or BP + displacement: based
* SI or DI + displacement: Indexed
* BX, BP + SI, DI + displacement: Based-indexed
#### Direct addressing mode
* MOV CX, [1234h]
* Physical address(PA) = {CS, DS, SS, ES} * 16 + {Direct address} 
#### Register indirect addressing mode
* MOV AX, [SI]
* PA = {CS, DS, SS, ES} * 16 + {BX, BP, SI, DI} 
#### Based addressing mode
* MOV [BX]+1234H, AL
* PA = {CS, DS, SS, ES} * 16 + {BX, BP, SI, DI} + {8/16-bit displacement}
#### Indexed addressing mode
* MOV AL, [SI]+1234H
* PA = {CS, DS, SS, ES} * 16 + {SI, DI} + {8/16-bit displacement}
#### Based-Indexed addressing mode
* MOV AH, [BX][SI]+1234H
* PA = {CS, DS, SS, ES} * 16 + {BX, BP} + {SI, DI} + {8/16-bit displacement}

















































###### tags:`CSnote`