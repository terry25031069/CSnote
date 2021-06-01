---
title: Alg chapter 9
---
# Medians and Order Statistics(期中考範圍)
* Selection problem
	* Input: A set A of n (distinct) numbers and an integer i, with 1  i  n.
	* Output: The element $x \subset A$ that is larger than exactly i - 1 other elements of A
## 9.1 Minimum and maximum
* Let S denote the input set of n items  
* To find the maximum of S, we can:
  * Step 1:  Set max = item 1
  * Step 2:  for k = 2, 3, …, n
    * if (item k is larger than max) 
	* Update max = item k;
  * Step 3:  return max;
```
MAXIMUM(A)
1 max = A[1]
2 for i = 2 to A.length // A.length is the length of arrat
3     if max < A[i]
4     max = A[i]
5 return max
```
* This takes n-1 comparisons
## Better method
* Define a function Find-Max as follows:
    Find-Max(R, k) \\ (R is a set with k items)
  1.  if (k $\leq$ 2)  return maximum of R;
  2.  Partition items of R into $\lfloor k/2\rfloor$ pairs;  
  3.  Delete smaller item from R in each pair;
  4.  return Find-Max(R, k - $\lfloor k/2\rfloor$); 
### Running time
* Let T(n) be number for comparisons for Find-Max with problem size n
* $T(n)=T(n- \lfloor n/2 \rfloor)+\lfloor n/2 \rfloor$ for $n\geq 3$, T(2) = 1
* ㄋㄟlving the recurrence (by substitution),  we get T(n) = n - 
### Lower bound
* Question:  Can we find the maximum using fewer than n – 1 comparisons?
* Answer:  No !  Every element except the winner must drop at least one match
* So, we need to ensure n-1 items not max -> at least n – 1 comparisons are needed
## Selection in expected linear time
```
Randomized-Select(A, p, r, i)
if p==r return A[p]
q = Randomized-Partition(A, p, r)
k = q – p + 1
if i ==k //the pivot value is the answer
    return A[q]
else if i < k 
    return Randomized-Partition(A, p, q-1, i)
6. else return Randomized-Partition(A, q+1, r, i-k)
```
### Running time
![](https://i.imgur.com/YNfhxCE.png)
![](https://i.imgur.com/FvUi5oP.png)
![](https://i.imgur.com/UQ8blns.png)
## Selection in expected linear time
we describe a recursive call 
				Select(S, k) 
	which supports finding the kth smallest element in S
Recursion is used for two purposes:
    (1) selecting a good pivot (as in Quicksort)
    (2) solving a smaller sub-problem
![](https://i.imgur.com/iEjF4X3.png)
![](https://i.imgur.com/mai09W4.png)
### Running time
In our selection algorithm, we choose m, which is the median of medians, to be a pivot and partition S into two sets X and Y
A closer look reviews that the worst-case running time depends on |X| and |Y|

Precisely, if T(|S|) denote the worst-case running time of the algorithm on S, then
		
   T(|S|) =  T(|S|/5) + Q(|S|) 
                 + max {T(|X|),T(|Y|) } 
Later, we show that if we choose m, the “median of medians”, as the pivot, 

both |X| and |Y| will be at most 7|S|/10 + 6 

Consequently,

    T(n) = T(n /5) + Q(n) + T(7n/10 + 6)  
	     T(n) = O(n)    (obtained by substitution)
* Substitution
![](https://i.imgur.com/K961ZRo.png)
## Median of medians
###### tags: `Algorithm` `CSnote`