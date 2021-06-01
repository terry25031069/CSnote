---
title: CMP Arch Chapter 3
---
# Arithmetic for Computers
## Interger 
### addition
#### Overflow
* Overflow if result out of range
* Adding +val and –val operands, no overflow
* Adding two +val operands
    * Overflow if result sign is 1
* Adding two –ve operands
    * Overflow if result sign is 0
![](https://i.imgur.com/QFplbJc.png)
#### Example 2
* adding the numbers 7 and 6 represented in 2’s complement using 4 bits.
* ![](https://i.imgur.com/ooSeeTO.png)
* overflow!!!
### Multiplication
#### long-multiplication approach
* 1000 * 1001
![](https://i.imgur.com/3rOjwg6.png)
![](https://i.imgur.com/h5nQ92n.png)
*  The Multiplicand register, ALU, and Product register are all 64 bits wide, with only the Multiplier register containing 32 bits.  The 32-bit multiplicand starts in the right half of the Multiplicand register and is shift ed left 1 bit on each step. Th e multiplier is shift ed in the opposite direction at each step. Th e algorithm starts with the product initialized to 0. Control decides when to shift the Multiplicand and Multiplier registers and when to write new values into the Product register.
##### Explain
multiplicand(left shift) * multiplier(right shift)
1000 * 1001
* 1 * 1000 +
* 0 * 10000 +
* 0 * 100000 +
* 1 * 1000000
![](https://i.imgur.com/D9QyqEz.png)
#### Refined
* Add and shift at the same time
![](https://i.imgur.com/Z1jEwlb.png)
##### example
* 2*3 or 0010 * 0011
![](https://i.imgur.com/LsJ7yAu.png)
#### Fast multiplication hardware
![](https://i.imgur.com/AjcQNwx.png)
* Rather than use a single 32-bit adder 31 times, this hardware “unrolls the loop” to use 31 adders and then organizes them to minimize delay
#### MIPS multiplication
* Two 32-bit registers for product
    * HI: most-significant 32 bits
    * LO: least-significant 32-bits
* Instructions
    * mult rs, rt / multu rs, rt
        * 64-bit product in HI/LO
    * mfhi rd / mflo rd
        * Move from HI/LO to rd
        * Can test HI value to see if product overflows 32 bits
    * mul rd, rs, rt
        * Least-significant 32 bits of product –> rd 

### Division
#### Long division approach
![](https://i.imgur.com/SScmZtW.png)
* Check for 0 divisor
* Long division approach
    * If divisor ≤ dividend bits
        * 1 bit in quotient, subtract
    * Otherwise
        * 0 bit in quotient, bring down nextdividend bit
* Restoring division
    * Do the subtract, and if remainder goes < 0, add divisor back
* Signed division
    * Divide using absolute values
    * Adjust sign of quotient and remainder as required 
#### Division Hardware
![](https://i.imgur.com/wJ9s0q1.png)
![](https://i.imgur.com/vWrl7hR.png)
##### Explain1
![](https://i.imgur.com/rLi5PMl.png)
#### improved
![](https://i.imgur.com/Ru3qDSt.png)
* The Divisor register, ALU, and Quotient register are all 32 bits wide, with only the Remainder register left at 64 bits
* Can’t use parallel hardware as in multiplier
    * Subtraction is conditional on sign of remainder
#### MIPS
* Use HI/LO registers for result
    * HI: 32-bit remainder
    * LO: 32-bit quotient
* Instructions
    * div rs, rt / divu rs, rt
    * No overflow or divide-by-0 checking
        * Software must perform checks if required
    * Use mfhi, mflo to access result
        * E.g.
        ```mfhi $s3```
        ```mflo $s2```
## Floating Point
* Single precision
![](https://i.imgur.com/oIFZiGH.png)
* double precision
![](https://i.imgur.com/w5czkoV.png)

* Generally $(-1)^{Sign} \times (1+Fraction) \times 2^{exponent -bias}$
* Sign: 正負
* Fraction:數值。因為第一個位置一定是１所以從第二位才開始算
* exponent：　次方，需要加１２７或是１０２３（最高位元以外都是一）
### example –0.75
* 負　0.11　
* Sign　＝　１
* Fraction　＝　1000... (記得要過第一位)
* exponent = -1 + 127 or 1023

### Infinities and NaNs
* Exponent = 111...1, Fraction = 000...0
    *  ±Infinity
    *  Can be used in subsequent calculations, avoiding need for overflow check 
* Exponent = 111...1, Fraction ≠ 000...0
    * Not-a-Number (NaN)
    * Indicates illegal or undefined result
        * e.g., 0.0 / 0.0
    * Can be used in subsequent calculations
### Addition 
* Now consider a 4-digit binary example
* 0.5 + –0.4375
* $1.000_2 × 2^{–1} + –1.110_2 × 2{–2} $
* 1. Align binary points
    * Shift number with smaller exponent
    * $1.00_2 × 2^{–1} + –0.111_2 × 2^{–1}$
* 2. Add significands
    * $1.000_2 × 2^{–1} + –0.111_2 × 2^{–1} = 0.001_2 × 2^{–1}$
* 3. Normalize result & check for over/underflow
    * $1.000_2 × 2^{–4}$, with no over/underflow
* 4. Round and renormalize if necessary
    * $1.000_2 × 2^{–4}$ (no change) = $0.0625$
![](https://i.imgur.com/oT6Tdi4.png)
#### hardware
* complicate
* ![](https://i.imgur.com/Yhu5JZY.png)
* Th e steps of Figure in addition correspond to each block, from top to bottom. First, the exponent of one operand is subtracted from the other using the small ALU to determine which is larger and by how much. Th is difference controls the three multiplexers; from left to right, they select the larger exponent, the significand of the smaller number, and the significand of the larger number. Th e smaller significand is shift ed right, and then the significands are added togetherusing the big ALU. Th e normalization step then shift s the sum left or right and increments or decrements the exponent. Rounding then createsthe final result, which may require normalizing again to produce the actual final result
### Multiplication
![](https://i.imgur.com/pqXSniv.png)
* Now consider a 4-digit binary example
* 0.5 $\times$ –0.4375
1. Add exponents
    * Unbiased: –1 + –2 = –3
    * Biased: (–1 + 127) + (–2 + 127) = –3 + 254 – 127 = –3 + 127
* 2. Multiply significands
    * 1.000_2 × 1.110_2 = 1.110_2 ⇒ 1.1102 × 2^{–3}
* 3. Normalize result & check for over/underflow
    * 1.110_2 × 2^{–3} (no change) with no over/underflow
* 4. Round and renormalize if necessary
    * 1.110_2 × 2^{–3} (no change)
* n 5. Determine sign: +ve × –ve ⇒ –ve
    * –1.1102 × 2^{–3} = –0.21875 
![](https://i.imgur.com/oT6Tdi4.png)
### MIPS
* Floating-point addition, single (add.s) and addition, double (add.d)
* Floating-point subtraction, single (sub.s) and subtraction, double (sub.d)
* Floating-point multiplication, single (mul.s) and multiplication, double (mul.d)
* Floating-point division, single (div.s) and division, double (div.d)
* Floating-point comparison, single (c.x.s) and comparison, double (c.x.d),where x may be equal (eq), not equal (neq), less than (lt), less than or equal(le), greater than (gt), or greater than or equal (ge)
* Floating-point branch, true (bc1t) and branch, false (bc1f)
###### tags: `Computer Architecture` `CSnote`