---
title: Alg chapter 4
---
# Divide and Conquer(分治)
* 將問題切割成多個相同類型的子問題
* 利用遞迴(recursive)處理子問題，如果子問題規模夠小，則直接將子問題解掉。將所有子問題答案結合起來，以解出原問題的答案。
## Recurrence
* Three methods to obtain asymptotic $\theta$ or $O$ bounds on the solution.
    * Substitution method: Guess a bound and then use mathematical induction to prove our guess.
    * Recursion-tree method: Converts the recurrence into a tree whose nodes represent the costs incurred at various levels of recursion. 
        * We use techniques for bounding summations to solve the recurrence
    *  The master method provides bounds for recurrences of the form
     $T(n) = aT(n/b)+f(n)$
         * where $a \geq 1, b>1$ and $f(n)$ is a given function
         * A recurrence of the form characterizes a divideand-conquer algorithm that creates $a$ subproblems, each of which is $1/b$ the size of the original problem, and in which the divide and combine steps together take $f(n)$ time
         * master method has three cases
         * We will use the master method to determine the running times of the divide-and-conquer algorithms for the maximum-subarray problem and for matrix multiplication
### Merge sort worst case:
$T(n)= 
\begin{cases}{} 
\theta(1)   &\text{if n=1}\\
T(\lceil n/2 \rceil)+ T(\lceil n/2 \rceil) + \theta(n) &\text{if n>1}
\end{cases}$
## Substitution method(替換法)
1. 猜Bound (經驗法則)
2. 假設子問題符合此Bound
	證明母問題符合此bound
### 適用時機 
* 單邊(不能是$\theta$)，分數(fraction)少
### Examples
#### EX.1
* Solve $T(n) = 2T(\lfloor n/2\rfloor )+n$
1. Guess
	* $T(n) = O(nlgn)$
2. prove there exists a $c$ and $n_0$ for $all\ n>n_0$
	for $n = 1,2,...k$, prove $n = k+1$ is true

$\begin{aligned}
T(n) &=2T(\lfloor n/2\rfloor )+n\\
&\leq 2C\lfloor n/2\rfloor lg\lfloor n/2\rfloor +n\\
&= cnlgn+(1-c)n\\
&\leq cnlgn
\end{aligned}$
$\rightarrow T(n) = O(lg(n))$
#### EX.2
* Solve $T(n) = 2T( \sqrt{n})+lgn$
1. Set $m=lgn$, we get $T(2^m) = 2T( 2^{m/2})+m$
2. rename $S(m) = 2S(m/2)+m$
3. We solve $\begin{aligned} 
S(m) &= O(mlgm)\\
\rightarrow T(n) &= O(lgnlglgn)
\end{aligned}$
## Recursion tree method(遞迴樹法)
* Term
$\underbrace{T(n)}_{母問題} = \underbrace{T(\frac{n}{2})}_{子問題}+\underbrace{T(\frac{2n}{3})}_{子問題}+\underbrace{n}_{cost}$
$r = \frac{1}{2}+\frac{2}{3}=\frac{7}{6} \leftarrow 子問題係數相加$
### 適用時機
子問題個數$\geq 2$個
### 類型
#### 類型1: r>1
* EX: $T(n) = T(n/2)+T(n/4)+T(n/8)+n$
* SOL:
	* Step 1 : create a recursive tree
$r = n/2+n/4+n/8 = 7/8 < 1$
$\begin{array}{lllllllll}
&&&&n&&&&\\
& n/2 &&& n/4 &&& n/8& \\
n/4&n/8&n/16&n/8&n/16&n/32&n/16&n/32&n/64
\end{array}$
	* step 2: 求bound
		* 求upper-bound(O)
		$T(n) = n+7/8n+49/64n+.....C_e\\
		\le n+7/8n+49/64n+.....\\
		=\frac{1}{1-7/8}n = 8n \\ \rightarrow T(n) = O(n)$
		* 求lower-bound($\Omega$)
		$T(n) = n+7/8n+49/64n+......\\
		\ge n \\ \rightarrow T(n) = \theta(n)$
		* by O and $\theta \rightarrow T(n) = \theta(n)$
#### 類型2: r=1
* EX: $T(n) = T(n/3)+ T(\frac{2n}{3})+n$
* SOL: $r = 1/3+2/3 =1$
* $\begin{array}{lllllllll}
&&n&\\
& n/3 && 2n/3 &\\
n/9&2n/9&&2n/9&4n/9
\end{array} \\
\rightarrow T(n) = n+n+n+n+... +C_e$
* 求bound
* Tree depth: $n \rightarrow \frac{2n}{3}  \rightarrow \frac{2}{3}^2n \rightarrow ... \rightarrow1\\
 Since\ (2/3)^kn =1, when\ k = log_{\frac{3}{2}}n$
 Height of tree is $log_{\frac{3}{2}}n$
* 求Upper bound
	* $T(n) = n+n+....+C_e\\
  n \times tree\ height = O(nlogn)$
* 求  lower  bound
$T(n) = n+n+....+C_e\\
\geq n \times h'\\
=n(log_3n+1)\\
\rightarrow T(n) = \Omega(nlogn)$
* $T(n) = \theta(nlogn)$
### Master method
* 令$T(n) =aT(n/b)+f(n), a\geq 1,b>1$ 
* Case 1: If $f(n) = O(n^{log_ba-\epsilon}) for\ some\ \epsilon>0$, then $T(n) = \theta(N^{log_ba})$
* Case 2: if $f(n) = \theta(N^{log_ba})$, then $\theta(N^{log_ba}logn)$
* Case 3: If $f(n) = O(n^{log_ba+\epsilon}) for\ some\ \epsilon>0$, then $T(n) = \theta(f(n))$
## Maximum-subarray( in construction)
![](https://i.imgur.com/ANADOV0.png)
* examine all $\left(\begin{array}{l}2\\n \end{array} \right)$ possible $S[i,j]$
### Three implementations
#### Brute
* compute each S[i, j] in O(n) time  O(n3) time
	*compute each S[i, j+1] from S[i, j] in O(1) time
	(S[i, i] = A[i] and S[i, j+1] = S[i, j] + A[j+1])
* Time complexity: O($n^2$)
![](https://i.imgur.com/iz9waOh.png)
#### A divide-and-conquer solution
* Possible locations of a maximum subarray A[i..j] of A[low..high], where mid = (low+high)/2
* Time complexity: 
    * FIND-MAX-CROSSING-SUBARRAY : O(n), where n = high - low + 1
    * FIND-MAXIMUM-SUBARRAY: T(n) = 2T(n/2) + O(n) = O(nlg n) 
        * T(1) = O(1), similar to merge-sort
entirely in A[low..mid] (low < i < j < mid)
entirely in A[mid+1..high] (mid < i < j < high)
crossing the midpoint (low < i < mid < j < high)
![](https://i.imgur.com/GWRutZW.png)
* pseudocode
![](https://i.imgur.com/WVmYn0K.png)
#### A Dynamix programming solution(HW 4.1-5)
* Time complexity: O(n)
* pseudocode(簡單測試過，不見得全對)
* 詳情請去看CLRS solution
``` cpp
int currentlow = 0, currenthigh = 0;
int maxsubarray(vector<int>nums){
    int sum = nums[0], maxsum = nums[0];
    int tmplow = 0, tmphigh = 0;
    for(int i = 1; i < nums.size(); i++){
        if(nums[i] > sum){
            tmplow = tmphigh = i;
            sum = nums[i];
            continue;
        }else{
            tmphigh = i;
            sum += nums[i];
        }
        if(sum > maxsum){
            currentlow = tmplow;
            currenthigh = tmphigh;
            maxsum = sum;
        }
    }
    return maxsum;
}
```
## Matrix Multiplication
* Input: two n x n matrices A and B
Output:	C = AB
$c_{ij}=\mathop{\sum_{k=1}^{n}}a_{ik}b_{kj}$
### two method
#### Divide and conquer

![](https://i.imgur.com/pM5G7jO.png)
##### Simplified
Suppose that we partition each of A, B, and C into four $n/2 \times n/2$ matrices
![](https://i.imgur.com/N6nQPYC.png)
Each of these four equations specifies two multiplications of $n/2 \times n/2$ matrices and the addition of their $n/2 \times n/2$products. We can use these equations to create a straightforward, recursive, divide-and-conquer algorithm:
![](https://i.imgur.com/w2Yx14A.png)
* Time complexity 
* $T(n)= 
\begin{cases}{} 
\theta(1)   &\text{if n=1}\\
8T(\lceil n/2 \rceil)+ \theta(n^2) &\text{if n>1}
\end{cases}$
	* by master theorem case 1, time complexity is $\theta(n^3)$ 
#### Strassen’s method
![](https://i.imgur.com/i6IwkkR.png)
![](https://i.imgur.com/XHILYmc.png)
Step 1: Divide each of A, B, and C into four sub-matrices as in (4.1)
Step 2: Create 10 matrices S1, S2, …, S10  as in (4.2)
Step 3: Recursively, compute P1, P2, …, P7 as in (4.3)
Step 4: Compute                             according to (4.4) 

#### Time complexity
T(n) = 7T(n/2) + O(n2)
	    = O(nlg7 ) (why?)
	    = O(n2.81)
* master method case2

# Exercises
## Exercise
### 4.3-2
![](https://i.imgur.com/ECETTBf.png)
* Answer: $T(n) = clgn/2+1 = clgn-c+1 \leq clgn$. O(lgn)
### 4.3-3
![](https://i.imgur.com/4nKsZTY.png)
### 4.3-6
![](https://i.imgur.com/f86ymsN.png)

### 4.3-8
![](https://i.imgur.com/OpGRbfD.png)


### 4.4-2
![](https://i.imgur.com/98Hxcgp.png)

### 4.4-6
![](https://i.imgur.com/7P754E1.png)

### 4.4-8
![](https://i.imgur.com/RDwfCyp.png)

### 4.5-1
![](https://i.imgur.com/bP4EULC.png)

### 4.5-2
![](https://i.imgur.com/UzThZ3o.png)

### 4.5-4
![](https://i.imgur.com/XA8DsPt.png)

## Problem
### 4.1 b,f
![](https://i.imgur.com/Hu4hh8x.png)
### 4.3 b,f,h
![](https://i.imgur.com/TtpUAto.png)

###### tags: `Algorithm` `CSnote` `Book`