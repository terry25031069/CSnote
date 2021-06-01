---
title: Alg chapter 6
---
# Heapsort
## Heaps
* A heap (or binary heap) is a binary tree that satisfies both:
	* Shape Property:
		* All levels, except deepest, are fully filled Deepest level is filled from left to right 
	* Heap Property
		* Value of a node $\le$ Value of its children
### Min heap
* Each node is smallest in it's subtree
#### Operations
* n = number of nodes in the heap

* Find-Min :  find the minimum value
	* Q(1) time
* Extract-Min :  delete the minimum value
	* O(log n) time  (how??)
* Insert :  insert a new value into heap
	* O(log n) time  (how??)
#### Heapsort
* How to use heap to sort in ascending order?
	* Call Insert to insert n numbers into heap Call Extract-Min n times
		*  numbers are output in sorted order
* Runtime: n x O(log n) + n x O(log n) = O(n log n)
#### Heapify(make binary tree a heap)
* for any tree T, we can make T satisfy the heap property as follows:
   1.   h = node_height(T) ;
   2.  for k = h, h-1, …, 1   
	             for each node u at level k
			   Heapify(u) ;
* tIME COMPLEXIRTY 
	* Let h = node-height of a tree
	So, 2h-1 ≤ n ≤ 2h - 1 	(why??)
	For a tree with shape property, 
	at most 2h-1 nodes at level h, 
	exactly 2h-2 nodes at level h-1, 
	exactly 2h-3 nodes at level h-2, …
	2h-1 x 1 + 2h-2 x 2 + 2h-3 x 3+ … + 1 x h   [why??]
	= 2h ( 1x½ + 2x(½)2 + 3x(½)3 + … + hx(½)h )
	≤ 2h Sk=1 to ∞ k x (½)k  = 2h x 2 ≤  4n
	* Thus, total time is O(n)
### Array Representation of Heap
Given a heap.
Suppose we mark the position of root as 1, and mark other nodes in a way as shown in the right figure.  (BFS order)
Anything special about this marking? 
![](https://i.imgur.com/oNyv2i8.png)
Something special:
If the heap has n nodes, the marks are from 1 to n
Children of x, if exist, are 2x and 2x+1
Parent of x is $\lfloor x/2\rfloor$

The special properties of the marking allow us to use an array A[1..n] to store a heap of size n
# Exercises 
## Exercise
### 6.2-3
![](https://i.imgur.com/gWISwHk.png)

### 6.2-6
![](https://i.imgur.com/5dT1gNR.png)
### 6.3-3
![](https://i.imgur.com/9nLOIUq.png)
### 6.4-3
![](https://i.imgur.com/LyL5raP.png)
### 6.5-7
![](https://i.imgur.com/AGlXz8i.png)
### 6.5-9
![](https://i.imgur.com/sl6MdxW.png)
## problem
### 6.3
![](https://i.imgur.com/QEiqsaC.png)

###### tags: `Algorithm` `CSnote`