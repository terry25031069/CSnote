# Chapter algorithm
## 0/1 knapsack
>n個東西有其個別價值跟重量，另有一個限重為m的袋子
如何選取某些東西，**使得總重量不超過M，且總價值最高**。

## 旅行推銷員問題(Traveling Salesman problem, TSP)
>尋找一條總距離(總花費)最小的路徑，並滿足：從公司出發，走訪所有城市且不重複，最後回到公司。

## 頂點覆蓋(Vertex cover)
>挑選最小的頂點集合，使得任何一邊的兩個頂點中，其中一點在集合中。

## Dominating Set
>拿一些點，蓋住所有鄰點

## Using computer to solve problem>
1. 明確定義問題
2. 設計演算法，並估計所需時間
3. 撰寫程式，並加以測試

## Definition & Criteria of Algorithm
### Defination
>An algorithm is a finite set of instruction that accomplishes a particular task.
### Criteria
>Input, Output, Definiteness, Finiteness, Effectivenss

## 凸包(Convex hull)
>找出最小的凸多邊形，將平面上所有點包在內部。

## 全世界所有問題可分為：
### Unsolvable problems
>e.g. Halting problem
### Solvable problems
>Intractable problems, Tractable(Polynomial Time) problem

## Definition of the time complexity notation
### Definition of Big-O
> f(n) = O(g(n)) if and only if exists two real constant c>0, and an integer constant n0>=1, 
> such that f(n) <= c * g(n), for all n >= n0

### Definition of Big-Omega
> f(n) = $\omega$(g(n)) if and only if exists real constant c>0, and an integer constant n0>=1, 
> such that f(n) >= c * g(n), for all n >= n0

### Defination of Big-theta
>f(n) = $\theta$(g(n)) if and only if exists real constants c1, c2 > 0, and an integer constant n0 >= 1

<img style="display: block; margin-left: 0; margin-right: auto" height="50%" width="50%" src="https://upload.cc/i1/2019/11/01/s7K6WH.png">
<div style="text-align:left">Big-O函數示意圖</div>
<img style="display: block; margin-left: 0; margin-right:auto" height="50%" width="50%" src="https://upload.cc/i1/2019/11/01/v4qECs.png">
<div style="text-align:left">Big-Omega函數示意圖</div>

## Definition of P, NP problem
>A decision problem is a problem where the answer is always "YES/NO"
>NP = Non-deterministic and polynomial

## Definition of Determinism and Non-determinism
### Deterministic 
>演算法中每一個步驟需備唯一定義，因此產生的結果也是唯一的。
### Non-deterministic
>允許一些步驟可以有可變動的執行選擇，因此運算結果不唯一，但需要限制在一組可能的結果之內。

# Chapter 1
## 抽象資料型別(Abstract Data Type, ADT)
ADT is a data type that 
* is organized in such a way that spec. of objects, and
* the spec. of the operations on the objects is separated from the representaiton of the objects and the implementation of the operation

ADT is implementation-independent

# Chapter 2
## 稀疏矩陣(sparse matrix)
### sparse matrix representation
using 3-tuple (row, column, value)
### transpose a sparse matrix
1. 跑所有 column
2. 對於每一個可能的 column 值，掃描所有 terms
3. 找出含有相對應的 column 的 terms，依序放進另一個陣列

Time complexity:O(term * column)
### fast transpose a sparse matrix
* (比上一個做法多宣告兩個陣列 rowsize 和 rowstart)
1. 跑所有 terms
2. 統計每個 term 是屬於哪個 column，並記錄在 rowsize 裡面
3. 加總 rowsize (prefix sum, 因為要算相同 column 的 terms 在新陣列的起始位置)
4. 再跑一次所有 terms，按column在新陣列的相對應位置依序放入新陣列

Time complexity:O(term + column)
## KMP algorithm
### Definition of failure function
如果 p = p0p1p2....pn-1 是一個字串，則：
f(j) = largest k < j, such that p[0 : k]=p[j-k : j], if k>0 exists
f(j) = -1, otherwise.

# Chapter 3
## infix to postfix converion
1. Fully parenthesize expression
2. All operators replace their corresponding right parentheses. (if to prefix, then turn into left parentheses)
3. Delete all parentheses. 













