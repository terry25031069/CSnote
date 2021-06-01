---
title: Alg chapter 2
---
# Getting Started
* Sorting problem
    * Input: A list of n numbers
    * Output: Arrange the numbers in increasing order
* If the list is already sorted, we can search a number in the list faster.
## 2.1 Insertion Sort
* A good algorithm for sorting a small number of elements. 
![](https://i.imgur.com/6DEFJxE.png)
![](https://i.imgur.com/GZ3SLer.png)
### Correctness of Insertion sort
* Loop invariant(insertion sort as an example):
	* Subarray $A[1..j-1]$ consists of elements originally from $A[1..j-1]$, but in sorted order$
* Three properties for Loop Invariant:
    * Initialization: It is true prior to the first iteration of the loop
    * Maintenance: If it is true before an iteration of the loop, it remains true before the next iteration
    * Termination: When the loop terminates, array is sorted.
* If the firs two properties hold, loop invariant is true prior to every iteration of the loop.r
### Analyzing the Running Times
* Standard assumption: Our computer is a RAM (Random Access Machine), so that each arithmetic (such as +, −, $\times$, $\div$), memory access, and control (such as conditional jump, subroutine call, return) takes constant amount of time
* Suppose that our algorithms are now described in terms of RAM operations
    * we can count # of each operation used
    *  we can measure the running time!
* Running time is usually measured as a function of the input size
    * E.g., n in our sorting problem
### Insertion sort(Running time)
* The following is a pseudo-code for Insertion Sort. Each line requires constant RAM operations.
![](https://i.imgur.com/S4IcfNC.png)
* Let T(n) denote the running time of insertion sort, on an input of size n.
* By combining terms, we have 
$T(n) = c_1n +(c_2+c_4+c_8)(n-1)+c_5\mathop{\sum_{}^{}}t_j+(c_6+c_7)\mathop{\sum_{}^{}}(t_j-1)$
* The values of $t_j$ are dependent on the input (not the input size) 
* Best: The input list is sorted, so that all $t_j=1$. Then,T(n) = $c_1n+(c_2+c_4+c_5+c_8)(n-1)=Kn+c -> linear function of n$
* worst: The input list is sorted in decreasing order, so that all $t_j = j-1$
* Then, T(n) = $k_1n^2+k_2n+k_3$
    * Quadratic function of n
### Worst-Case Running Time
* In our course (and in most CS research), we concentrate on worst-case time
## Divide and conquer
* Divide a big problem into smaller sub-problems
 * Solve (Conquer) smaller sub-problems recursively
* Combine the results to solve original one
### Merge sort
![](https://i.imgur.com/0QcOaiG.png)
1. Divide list to two halves, A and B
2. Sort A using Merge Sort
3. Sort B using Merge Sort
4. Merge sorted lists of A and B
![](https://i.imgur.com/5l8ISwh.png)
### Merge Sort (Running Time)

* Suppose we know that Merge( ) of two lists of total size n runs in $c_1n$ time
    * $T(n) = 2T(n/2) + c_1n$
        * when n>1
    * $T(n) = c_1$ 
        * when n=1
* Solving the recurrence, we have $T(n) = c_1\ nlogn + c_2n$
![](https://i.imgur.com/MNVLTW9.png)
#### Why? (補充) 
![](https://i.imgur.com/dxB10q3.png)
![](https://i.imgur.com/nzPdjKn.png)


### which is faster
*  if n is VERY large, worst-case time of Merge Sort must be smaller than that of Insertion Sort 

# Exercises ch1
## Exercise
### 1.2-2
* Question:
	* Suppose we are comparing implementations of insertion sort and merge sort on the same machine. For inputs of size n, insertion sort runs in $8n^2$ steps, while merge sort runs in $64n lg n$ steps. For which values of n does insertion sort beat merge sort?
* Answer
	* $8n^2<64nlgn$ -> $n<8lgn$
	* Largest n is 43
### 1.2-3
* Question
	* What is the smallest value of $n$ such that an algorithm whose running time is $100n^2$ runs faster than an algorithm whose running time is $2^n$ on the same machine?
* Answer
	* use $100n^2<2^n$ to find the largest n and plus 1 for the first $n$ to let $100n^2 > 2^n$
## problem
### 1.1
* Question:
	* For each function f(n) and time t in the following table, determine the largestsize n of a problem that can be solved in time t, assuming that the algorithm tosolve the problem takes f(n) microseconds.
![](https://i.imgur.com/arbokpd.png)
* answer
	* [Sladder Answer](https://www.slader.com/textbook/9780262033848-introduction-to-algorithms-3rd-edition/14/problems/1/)

# Exercises ch2
## Exercise
### 2.2-1
* Question
	* Express the function $n^3/1000 - 100n^2 - 100n + 3$ in terms of ‚$\theta$ notation
* Answer
	* $\theta(n^3)$
### 2.3-3
* Question
	* Use mathematical induction to show that when n is an exact power of 2, the solution of the recurrence
	$T(n)= 
\begin{cases}{} 
2   &\text{if n=2}\\
2T(n/2) + n&\text{if n>1}
\end{cases}$.
is $T(n)=nlgn$
* Answer
	* 假設 T(n) = nlgn
	* 讓 n = $2^k$ k=1 ,if n=2 T(2) = 2 = 2lg2
	* 證明$n=2^{k+1}成立$
		* $T(2^{K+1}) = 2T(2^{k+1}/2)+2^{k+1}\\
		=2(2^klg2^k)+2^{k+1}\\=k2^{k+1}+2^{k+1}\\
		=(k+1)2^{k+1}\\
		=2^{k+1}lg(2^{k+1}) = nlgn$
### 2.3-6
* question:
	* Observe that the while loop of lines 5–7 of the INSERTION-SORT procedure in Section 2.1 uses a linear search to scan (backward) through the sorted subarray A[1..j-1]. Can we use a binary search (see Exercise 2.3-5) instead to improve the overall worst-case running time of insertion sort to $\theta(nlgn)$?
* answer:
	* The linear search not only scans the sub-array, but also moves the element to it's position, the worst case is $\theta(j)$. Binary search only takes $\theta(lgj)$,but we still have to move the element, which takes$\theta(j)$, so this part still costs $\theta(j)$, therefore the worst case isn't improved 
## problem
### 2-1
* Although merge sort runs in $\theta(nlgn)$ worst-case time and insertion sort $\theta(n^2)$ worst-case time, the constant factors in insertion sort can make it faster in practice for small problem sizes on many machines. Thus, it makes sense to coarsen the leaves of the recursion by using insertion sort within merge sort when subproblems become sufficiently small. Consider a modification to merge sort in which n/k sublists of length k are sorted using insertion sort and then merged using the standard merging mechanism, where k is a value to be determined.
* a. Show that insertion sort can sort the n/k sublists, each of length k, in $\theta(nk)$ worst-case time
	* Sorting each of the sublists will take$\theta(k^2)$. Sorting n/k lists will take $\theta(n/k \times k^2) = \theta(nk)$
* b. Show how to merge the sublists in $\theta(nlg(k/n))$ worst-case time.
	* With a coarseness of k. Merge sort is conducted above the length k.The depth of the merge tree is $lg(n)-lg(k)=lg(n/k)$. Merging on each level still takes cn time, therefore the merge sort part takes $\theta(nlg(k/n))$
* c. Given that the modified algorithm runs in $\theta(nk+nlg(n/k))$ worst-case time, what is the largest value of k as a function of n for which the modified algorithm has the same running time as standard merge sort, in terms of $\theta$ notation?
	* if $k(n) \in \theta(lgn)$, time complexity will still be$\theta(nlgn)$
* d. How should we choose k in practice?
###### tags: `Algorithm` `CSnote`