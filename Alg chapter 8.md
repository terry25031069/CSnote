---
title: Alg chapter 8
---
# Sorting in linear time
## Lower bound of comparison sorts
* Lower bound of any comparison sorting algorithm 
	* applies to insertion sort, selection sort, merge sort, heapsort, quicksort, …
	* does not apply to counting sort, radix sort, bucket sort
* Based on Decision Tree Model
### Comparison sort
* Comparison sort only uses comparisons between items to gain information about the relative order of items
### Worst-case running time
* Merge sort and heapsort are the “smartest” comparison sorting algorithms we have studied so far:  Worst-case running time is Q(n log n)

* Question:  Do we have an even smarter algorithm? Say, runs in o(n log n) time?
	* Answer:  No!  (main theorem in this lecture)
### theorem
* Theorem: Any comparison sorting algorithm requires $\Theta(n log n)$ comparisons to sort  n distinct items in the worst case
* Corollary: Any comparison sorting algorithm runs in $\Theta(n log n)$  time in the worst case
* Corollary: Merge sort and Heapsort are (asymptotically) optimal comparison sorts
#### Proof
* The main theorem only counts comparison operations, so we may assume all other operations (such as moving items) are for free

* Consequently, any comparison sort can be viewed as performing in the following way:
	* Continuously gather relative ordering information between items
	* In the end, move items to correct positions
### Decision Tree of an Algorithm


* Consider the following algorithm to sort 3 items A, B, and C:

	Step 1:  Compare A with B
	Step 2:  Compare B with C
	Step 3:  Compare A with C if the result in Steps 1 and 2 are different 



* The previous algorithm always use 3 comparisons, and can sort the 3 items

* A cleverer algorithm may sort the 3 items, sometimes, using at most 2 comparisons:

	Step 1:   Check if A > B
	Step 2:  Check if B > C
	Step 3:  Compare A with C if the resul#
	![](https://i.imgur.com/HkglCTJ.png)
#### Properties of Decision Tree
In general, assume the input has n items Then, for ANY comparison sort algorithm:

Each of the n! permutations corresponds to a distinct leaf in the decision tree 
The height of the tree is the worst-case # of comparisons for any input 

Question:  What can be the height of the decision tree of the cleverest algorithm?

### Lower bound on height
There are n! leaves   [for any decision tree]
Degree of each node is at most 2
Let h = node-height of decision tree
	So,  n!  = total # leaves  ≤ 2h
       h  ≥ log (n!) = log n + log (n-1) + …
 		        ≥  log n + … + log (n/2)
		        ≥  (n/2) log (n/2) = W(n log n) 
#### Proof of Lower Bound
Conclusion:
    worst-case # of comparisons 
	= node-height of the decision tree
	= W(n log n)    [for any decision tree]
Any comparison sort, even the cleverest one, needs  W(n log n) comparisons in the worst case
Heapsort and merge sort are asymptotically optimal comparison sorts

## Sorting in Linear Time
Sorting algorithms we studied so far
Insertion, Merge,  Heapsort, Quicksort
	 determine sorted order by comparison 

We will look at 3 new sorting algorithms 
Counting Sort, Radix Sort, Bucket Sort
	 assume some properties on the input, and 	determine the sorted order by counting
### counting sort
Input:  Array A[1..n] of n integers,      		       each has value from [0,k]
Output:  Sorted array of the n integers
Idea 1:  Create B[1..n] to store the output
Idea 2:  Process A[1..n] from right to left
Use k + 2 counters:
 One for “which element to process”
 k + 1  for “where to place”
#### Counting Sort (Step 1)
Initialize c[0], c[1], …, c[k] to 0
    
2.  /* First, set c[j] = # elements with value j */
    For x = 1,2,…,n, increase c[A[x]] by 1

3. /* Set c[j] = the number of elements less than or equal to j  (iteratively) */
    For y = 1,2,…,k,  c[y] = c[y-1] + c[y] 
Time for Step 1 = O( n + k )
#### Counting Sort (Step 2)
   For x = n, n-1,…,2, 1 
	{   /* Process next element */
         B[c[A[x]]] = A[x]; 
 
           /* Update counter */
  	        Decrease c[A[x]] by 1;
    }
Time for Step 2 = O( n )
#### Counting sort (running time)
Conclusion:
Running time = O( n + k )
 if k = O( n ), time is (asymptotically) optimal
Counting sort is also stable : 
elements with same value appear in same order in before and after sorting
### Stable sort
*　elements with same value appear in same order in before and after sorting

### Radix sort
* Input:  Array A[1..n] of n integers, each has value from [0,k]
* Output:  Sorted array of the n integers
* Idea:  Sort in d rounds
	* At Round j,  stable sort A on digit j  (where rightmost digit = digit 1)
* Sort from most insignificant digit to the most significant digit
#### Radix sort (correctness)
* Question:  
  * “After r rounds, last r digits are sorted”
  Why ??
* Answer:  
  * his can be proved by induction :
  	The statement is true for r = 1
  	Assume the statement is true for r = k
  	Then …
* At Round k+1, 
	*if two numbers differ in digit “k+1”,  their relative order [based on last k+1 digits] will be correct after sorting digit “k+1” if two numbers match in digit “k+1”,  their relative order [based on last k+1 digits]  will be correct after stable sorting digit “k+1”  (why?)

-> Last “k+1” digits sorted after Round “k+1”
#### Conclusion:  

After d rounds, last d digits are sorted, so that the numbers in A[1..n] are sorted

There are d rounds of stable sort, each can be done in O( n + k ) time
    Running time = O( d (n + k) )
if d=O(1) and k=O(n), asymptotically optimal

### Bucket sort
Input:  Array A[1..n] of n elements,      		       each is drawn uniformly at 	        		       random from the interval [0,1)  
Output:  Sorted array of the n elements
Idea:  
	Distribute elements into n buckets, so that each bucket is likely to have fewer elements  easier to sort

#### Bucket Sort (Running Time)
Let X = # comparisons in all insertion sort
		Running time = Q( n + X )
	  worst-case running time = Q( n2 )
How about average running time?
Finding average of X (i.e. #comparisons) gives average running time

#### Average Running time
Let nj = # elements in Bucket j		
			X ≤ c(  n02   +  n12  + … + nn-12  )
So,    E[X] ≤ E[c(n02 + n12 + … + nn-12)]
                  = c E[n02 + n12 + … + nn-12]
                  = c (E[n02] + E[n12] + … + E[nn-12]) 
			   = cn E[n02]      (by uniform distribution)
Textbook (pages 202-203) shows that
	 E[n02]  =  2 – (1/n) 
	 E[X] ≤ cn E[n02] = 2cn – c 
In other words, E[X] = O( n ) 
 Average running time = Q( n ) 

###### tags: `Algorithm` `CSnote`