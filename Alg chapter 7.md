---
title: Alg chapter 7
---
# Quicksort
* Worst case: $\theta (n^2)$
* Average case: $\theta(n logn)$
* Partition(A,p,r)     /* to partition array A[p..r]  */
	1. Pick an element, say A[t]  (called pivot) 
	2. Let q = #elements less than pivot
	3. Put elements less than pivot to A[p..p+q-1]
	4. Put pivot to A[p+q] 
	5. ut remaining elements to A[p+q+1..r] 
	6. Return q
* Quicksort(A,p,r)
	1. if($p\geq r$) return
	2. q=Partition(A,p,r)
	3. Quicksort(A,p,p+q-1);
	4. Quicksort(A,p+q+1,r);
## Randomized quicksort
```
Randomized-Partition(A, p, r)
i = Random(p, r)
Exchange A[r] with A[i]
Return Partition(A, p, r)
```

```
Randomized-Quicksort(A, p, r)
If p < r
q = Randomized-Partition(A, p, r)
Randomized-Quicksort(A, p, q-1)
Randomized-Quicksort(A, q+1, r)
```

## Worst Case
* $T(n)= max_{q=0\to\ n-1}(T(q)+T(n-q-1))+\theta(n)$
	* We prove T(n) = 0($n^2$) by substitution method:
		1. Guess $T(n) \le cn^2$ for some constant c
		2. Next, verify our guess by induction Basis: n=1 hold, Assume $n \le k\  hold$
## Balanced partitioning
* if PARTITION always produces a 9-to-1 split. Get recurrence
	* T(n) = T(9n/10)+T(n/10)+ cn
![](https://i.imgur.com/yXdgT0X.png)
## Average running time
* Let X = number  of comparisons in all partition
* We find 
	* running time = O(n+X)
		* Find average of X gives average running time
### Average number of comparisons
* Let $X_ij$ = number comparisons between $a_i$ and $a_j$ in all Partition calls, and $X$ = number of comparisons in all Partition calls
* X= $X_{12} + X_{13} + … + X{n-1,n}$
* Average number comparisons 
	$\begin{aligned} 
	& = E[X]\\
	& = E[X_{12} + X_{13} + … + X_{n-1,n}]\\
	& = E[X_{12}] + E[X_{13}] + … + E[X_{n-1,n}]
	\end{aligned}$
	* Using this result, 
	$\begin{aligned} 
	E[X] & = \mathop{\sum_{i=1\ to\ n-1}^{}} \mathop{\sum_{j=i+1\ to\ n}^{}} 2/(j-i+1) \\
	& = \mathop{\sum_{i=1\ to\ n-1}^{}} \mathop{\sum_{k=1\ to\ n-i}^{}} 2/(k+1) (let\ k\ = j-1) \\
	& < \mathop{\sum_{i=1\ to\ n-1}^{}} \mathop{\sum_{k=1\ to\ n}^{}} 2/k \\
	& = \mathop{\sum_{i=1\ to\ n-1}^{}} O(logn) = O(nlogn)
	\end{aligned}$
###### tags: `Algorithm` `CSnote`