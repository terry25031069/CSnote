---
title: Alg chapter 15
---
# Dynamic programming
* Applied to optimization problems.
* Steps to develop a dynamic-programming algorithm
    1. Characterize the structure of an optimal solution
    2. recursively define the value of an optimal solution
    3. compute the value of an optimal solution, typically in a bottom-up fashion
    4. construct an optimal solution from computed information
## 1. Rod cutting
* Given a rod of length $n$ inches, and a table of prices $p_i$ for $i  = 1,2,...,n$ , determine the maximum revenue $r_n$ obtained by cutting the rod and sell it.
* Price: 
![](https://i.imgur.com/S9JfvNe.png)
* example of cutting(n=4):
    * cut into 2 rods of length 2. Price is 2 $\times$ 5 = 10
* Recursive solution
    * ![](https://i.imgur.com/JfXNSXP.png)
    * running time $T(n)=2^n$, very slow

## Dynamic programming of optimal rod cutting
* two solutions
    * top down with memoization
    * bottom up
* Save solution of sub-problems, so we don't have to recompute it again and again. Dynamic programming use additional memory to save computation time. **time-memory trade-off**. 
* time complexity$/theta(n^2)$
### Memoized-cut-rod
![](https://i.imgur.com/yxssyN5.png)
* ***MEMOIZED-CUT-ROD*** initializes a new auxiliary array $r[n]$ with the value $-\infty$.
* ***MEMOIZED-CUT-ROD-AUX*** is  the memoized version of recursive ***CUT-ROD***. 
    * It first checks in line 1 to see whether the desired value is  known and, if it is, line 2 returns it. Otherwise, lines 3–7 compute the desired value q in the usual manner, line 8 saves it in $r[n]$, and line 9 returns it
### Button-up-cut-rod
![](https://i.imgur.com/YeFbr2A.png)
* BOTTOM-UP-CUT-ROD uses the natural ordering of the subproblems: a problem of size i is “smaller” than a subproblem of size j if i<j . Thus, the procedure solves subproblems of sizes j = 0, 1, ... ,n in that order.
    * Line 1 of procedure BOTTOM-UP-CUT-ROD creates a new array $r[0...n]$ to save the results of the subproblems, and line 2 initializes $r[0]$ to 0
    *  Lines 3–6 solve each subproblem of size j , for j = 1, 2,..., n, in order of increasing size.
    *  Line 7 saves in $r[j]$  the solution to the subproblem of size j . Finally, line 8 returns $r[n]4, which equals the optimal value $r_n$.
## 2. Matrix chain multiplication
* Let A be a matrix of dimension p x q and B be a matrix of dimension q x r 
* By multiplying A and B, we obtain C = AB. Which takes  pqr operaions.
* $((A_1A_2)A_3)=(A_1(A_2A_3))$ so matrix multiplication is **Associative**

# homework
4.1-15*
15.4-4
15.4-5
15.5-2
15.5-3*
###### tags: `Algorithm` `CSnote`