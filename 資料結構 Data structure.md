# 資料結構 Data structure
>程式=資料結構+演算法

## 資料儲存層次的分類(由低到高)
1. 基本資料型態(實質資料型態)
2. 結構型資料型態(虛擬資料型態)
3. 抽象資料型態

## 抽象資料型態
* 是指定義一些結構型資料型態所具備的數學運算關係，也就是說使用者無需考慮到ADT的製作細節，只要知道如何使用即可
* 指的是將物件的規格及其相關運算的規格，與物件的表示方式及其相關運算的實作方式分隔開來，以提供更便利的形式讓使用者存取資料，而不涉及資料的實際儲存細節或實做細節
>優點: 
1. 可以模組化 
2. 進行資訊隱藏

# Chapter algorithm
## 分割問題
>給予一個正整數的集合A={a1,a2,...,an}，是否可以將其分割成兩個子集合，而此**兩個子集合的個別總和相等**

## 0/1 knapsack
>n個東西有其個別價值跟重量，另有一個限重為M的袋子
如何選取某些東西，**使得總重量不超過M，且總價值最高**。

## 旅行推銷員問題(Traveling Salesman problem, TSP)
>尋找一條總距離(總花費)最小的路徑，並滿足：從公司出發，走訪所有城市且不重複，最後回到公司。

## 頂點覆蓋(Vertex cover)
>挑選最小的頂點集合，使得任何一邊的兩個頂點中，至少有一頂點在集合中。

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
1. Input
2. Output
3. Definiteness: clear and unambiguous
4. Finiteness: terminate after a finite number of steps
5. Effectivenss: instruction is basic enough to be carried out

## 凸包(Convex hull)
>找出最小的凸多邊形，將平面上所有點包在內部。

## 全世界所有問題可分為：
### Unsolvable problems
>e.g. Halting problem

### Solvable problems
1. Intractable problems
>e.g.列出一個集合的所有子集合

2. Tractable problems(Polynomial Time)
>e.g.排序問題

## Definition of the time complexity notation
* Worst-case: **upper bound**(defined by an **algorithm**)
* Average-case
* Best-case: **lower bound**(defined by a **proof**)

### Definition of Big-O
> f(n) = O(g(n)) if and only if exists two real constant c>0, and an integer constant n0>=1, 
> such that f(n) <= c * g(n), for all n >= n0

### Definition of Big-Omega
> f(n) = $\omega$(g(n)) if and only if exists real constant c>0, and an integer constant n0>=1, 
> such that f(n) >= c * g(n), for all n >= n0

### Defination of Big-theta
>f(n) = $\theta$(g(n)) if and only if exists real constants c1, c2 > 0, and an integer constant n0 >= 1,
>such that c1 * g(n) <= f(n) <= c2 * g(n), for all n >= n0

<img style="display: block; margin-left: 0; margin-right: auto" height="50%" width="50%" src="https://upload.cc/i1/2019/11/01/s7K6WH.png">
<div style="text-align:left">Big-O函數示意圖</div>
<img style="display: block; margin-left: 0; margin-right:auto" height="50%" width="50%" src="https://upload.cc/i1/2019/11/01/v4qECs.png">
<div style="text-align:left">Big-Omega函數示意圖</div>

## Definition of P, NP problem
>A decision problem is a problem where the answer is always "YES/NO"
* NP = Non-deterministic and polynomial

## Definition of Determinism and Non-determinism
### Deterministic 
>演算法中每一個步驟需備唯一定義，因此產生的結果也是唯一的。
### Non-deterministic
>允許一些步驟可以有可變動的執行選擇，因此運算結果不唯一，但需要限制在一組可能的結果之內。

# Chapter 1
## System Life cycle
1. Requirements
2. Analysis:
> Bottom-up or Top-down 
3. Design:
* Data objects: abstract data types
* Operations: specification & design of algorithms


# Chapter 2
## 稀疏矩陣(sparse matrix)
### Sparse matrix representation
using 3-tuple form(row, column, value)
### Transpose a sparse matrix
1. 跑所有 column
2. 對於每一個可能的 column 值，掃描所有 terms
3. 找出含有相對應的 column 的 terms，依序放進另一個陣列

Time complexity: **O(term * column)**
### Fast transpose a sparse matrix
* (比上一個做法多宣告兩個陣列 rowsize 和 rowstart)
1. 跑所有 terms
2. 統計每個 term 是屬於哪個 column，並記錄在 rowsize 裡面
3. 加總 rowsize (prefix sum, 因為要算相同 column 的 terms 在新陣列的起始位置)
4. 再跑一次所有 terms，按column在新陣列的相對應位置依序放入新陣列

Time complexity: **O(term + column)**
## KMP algorithm
### Definition of failure function
如果 p = p0p1p2....pn-1 是一個字串，則：
* f(j) = largest k < j, such that p[0 : k]=p[j-k : j], if k>=0 exists
* f(j) = -1, otherwise.

# Chapter 3
## Infix to postfix converion
1. Fully parenthesize expression
2. All operators replace their corresponding right parentheses 
(if to prefix, then turn into left parentheses)
4. Delete all parentheses 

# Storage Management Buddy System
## 記憶體分配方法
### 最先合適法(First-Fit)
1. 從可用的空間區段中，找到**第一塊大於n的閒置區段**，將其中一部份分配給使用者。
2. 回收時，將釋放的閒置區段插回**鏈結串列的開頭**。
### 最佳合適法(Best-Fit)
1. 從可用的空間區段中，找出**一塊大小最接近n的閒置區段**分配給使用者。(會先將區段自小到大排序)
2. 回收時，必須將釋放的閒置區段插入到**合適的位置**上去。
### 最差合適法(Worst-Fit)
1. 從可用的空間區段中，找出**最大的閒置區段**分配給使用者。(將閒置區段由大到小排序。)
2. 回收時，必須將釋放的閒置區段插入到**合適的位置**上去。
#### 比較圖
|          | First-Fit                          | Best-Fit                                         | Worst-Fit                                                              |
| -------- | ---------------------------------- | ------------------------------------------------ | ---------------------------------------------------------------------- |
| 適用時機 | 系統先不管執行時間分配跟回收的情況 | 分配記憶體範圍廣的系統                           | 分配記憶體範圍窄的系統                                                 |
| 分配方法 | 分配隨機，需先查可用空間區段       | 找出最接近請求的閒置區段，需搜尋連結串列(最費時) | 從記憶體最大的節點中分配，使連結串列中節大小趨向平衡，不須查詢連結串列 |
| 回收方法 | 插回串列開頭就好                   | 需先搜尋適當位置才能插入                         | 需先搜尋適當位置才能插入                                               |
| 優點     | 配置速度快                         | 配置後殘餘的空間最小，但不能給其他作業使用       | 配置後殘餘的空間最大，但可給其他作業使用                               |
## 邊界標示法(Boundary Tag Method)
在於每個記憶體區段的開頭部份和尾部兩個邊界上分別設有標籤，以標識該區域為占用區段或閒置區段，使得在回收使用者釋放的閒置區段時，易於判別物理位置上與其相鄰的記憶體區域是否為閒置區段，以便將所有位址中連續的閒置記憶體區組合成一個大的閒置區段。*配合最先合適法來管理記憶體，可減少搜尋時間。
## 夥伴系統(Buddy System)
*和邊界標識法類似*。使用者提出申請時，分配一塊大小“適當”的記憶體給使用者；反之，在使用者釋放記憶體時即回收。 
* A block of size 2^i is called an i-block and the list containing i-blocks is called the i-list
* If a request for a block of size n is made，an i-block is reserved where i is the smallest integer such that n <= 2^i.**會一直向上找直到有空閒區段可以切割。**
* If q|2^i+1, then it is the first half of an (i+1)-block and its buddy is at q+2^i.Otherwise, it is the second half of an   (i+1)-block and its buddy is at q-2^i.
>優點：演算法簡單，速度快\
>缺點：只合併夥伴，容易產生碎片
## 費氏夥伴系統(Fibonacci Buddy System)
* 重點在兩個具有共同父節的相鄰區塊，如何合併成較大的區塊。
* 為了記憶體釋回工作操作順利，設定counter變數，以記錄區塊的分裂關係
>步驟：
使用區塊中最大者，即節點counter = 0
當區塊分裂為二時，以遞迴方式定義counter的值：
    左區塊的counter = counter+1。
    右區塊的counter = 0 (歸零)。

# Chapter 5
## Definition of Tree
* a distinguished node r(root)
* zero or more nonempty (sub)trees T1, T2, ... , Tk, each of whose roots are connected by a directed edge from r
### Terminology of Tree
* degree: the number of subtrees of the node（i.e. degree = 節點有幾個子樹）, the node with degree 0 is a leaf(葉節點)
* parent（父節點）: the node that has subtrees is the parent of the roots of the subtrees.（如果某點有子樹，那麼此點為其所有子樹根的父節點）
* children（子節點）: the root of these subtrees are children of the node（反過來說，這些子樹根為此節的點的子節點）
* siblings: the nodes which have same parent.
* ancestors（祖先）: all the nodes long the path from the root to the node（某個點的祖先為從根節點到此節點路徑上的所有點）
 
### Representation of trees
* list
* left child-right sibling
* 
## Binary tree
### Definition of Binary tree
* A binary tree is a finite set of nodes that is either empty or consists of a root and two disjoint binary trees called the left and right subtree.（二元樹為含左右獨立子樹及根的有限點集合或空集合）
* 樹不能是空集合，但二元樹可以。
* 二元樹的子樹有左右順序，但樹沒有。

### Full binary tree vs Complete binary tree
* a full binary tree of depth k have 2^k-1 nodes.
* a complete binary tree of depth k and n nodes iff its nodes correspond to the nodes numbered from 1 to n in the full binary tree of depth k.
* 完美(full)二元樹全部塞滿，完滿(complete)二元樹的每個節點都能對應完美二元樹的編號

### Binary Tree Traversals
* inorder: LVR
* preorder: VLR
* postorder: LRV

## SAT problem
* satisfiability problem: is there an assignment to make an expression true?



# Chapter 6
## Eular's graph（尤拉圖）
* degree of a vertex（邊的度數）：此點有幾條邊
* 只有每點都有偶數條邊（偶點），才會存在恰好遍歷所有邊一次，且起點終點相同的走法，且此種走法稱為 Eulerian walk。
* 七橋問題不存在 Eulerian walk，因為每個點都有奇數條邊。
## Definition of a graph
* A graph, G=(V,E), consists of two sets, V and E, V is finite and nonempty set of vertices, and E is a set of edges.
* The vertices of a graph G can be repersented as V(G), and E(G) means the edges of a graph.
* 圖有分有向圖 (directed graphs) 跟無向圖 (undirected graph).
* (u,v)跟(v,u)在無向圖是相同的邊，但在有向圖分別是由u開始跟由v開始的邊。
### Graph restrictions
* 圖不能有自環跟重邊。（但中文精確點叫做簡單圖，英文還是叫graph）
### Terminology of graph
以下列我覺得重要的，要的自己寫，我懶。
* Acyclic graph (Directed Acyclic Graph, DAG)：a directed graph with no cycle.（有向無環圖）。
* connected graph：an undirected graph if there is a path from every vertex to every vertex.（沒孤點的無向圖稱為連通圖）。
* strongly connected graph：a directed graph if there is a path from every vertex to every vertex.(每個點都存在一條路徑連往其他點的「有向圖」，為強連通圖。)
* complete graph： graph in which there is an edge between every pair of vertices.(圖上任兩點均有邊的圖為完全圖)
### Subgraph(子圖)
* subgraph of G is a graph G’ such that V(G’)⊆V(G) and E(G’)⊆E(G).
### Strongly Connected Component(SCC, 強連通元件)
* A SCC is a maximal subgraph that is strongly connected.（強連通元件）
## Graph representation
* Matrix: space complexity:O(vertex^2), good for dense but bad for sparse.
* undirected graph is symmetric matrix
* List: space:O(vertex+edge) good for sparse.
* sequential: 前面陣列位置0~end，為周圍鄰居索引的起始點，後方array[i]至array[i+1]-1為vertex i的鄰居。
* adjacency list:紀錄離開那個點的頂點(out-degree)
* Inverse adjacency list: 記錄能到那個點的頂點(in-degree)
* Multilist: 這有點難解釋
## Weighted edge
* 有時候邊上面有所謂的「權重」(weight)
* 權重可能代表兩點間「距離」(distance)，或者某點經由某條邊至另一點的「代價」(cost，暫譯)
* 如果要表示權重，我們需要額外的值以記錄它，有權重的圖稱為網路(network)
## Graph operations
* 如果要拜訪圖G上所有點V能到的點，那有兩種做法，分別是深度優先搜尋(Depth-first search, DFS)跟廣度優先搜尋(Breadth-first search, BFS)
* 此兩種做法都可以支援有向圖跟無向圖
### DFS
### BFS
## Connected component
## Spanning tree
* Any tree consisting solely of edges in G and including all vertices in G is called a spanning tree.
## Biconnected component
## Depth-first spanning tree
## Minimal cost spanning tree
* 這我他媽很有爭議，明明minimum spanning tree(MST，最小生成樹)比較多人叫
* 叫最小擴充樹的，我一樣跟你拼命(X
* 生成樹上所有邊的權重和，即為此樹的cost
* 生成生成樹有三種greedy algorithm，分別是Kruskal, Prim 跟 Borůvka's(Sollin's) algorithm
### Constraints of Minimum spanning tree
* 只能用圖上的n-1條邊，且這些邊不能構成環
### Kruskal algorithm
* 此演算法的做法為依序將邊加入生成樹的集合內
* 先將所有邊的cost由小到大排序O((edge)log(edge))，然後檢查所有邊O(edge)是否與之前被選入的邊構成環O(constant)
* Time complexity: O((edge)log(edge))

### Prim algorithm
* 此演算法的做法為依序將「點」加入生成樹的集合內
* 先選一個起始點，然後選擇集合內所有點的連到的最小權重邊，檢查此邊的另一點是否在點集合內，若沒有則加入點集合
* Time complexity: O(edge^2) when using adjacency list or matrix
* with fibonachi heap or priority queue: O(edge+(vertex)log(vertex))
  
### Borůvka's(Sollin's) algorithm
* 此演算法於每階段會一次選取多邊
* 剛開始時，所有n個點形成最小生成子樹森林
* 每個階段，對於每一棵最小生成子樹，選擇此子樹上最小權重且索引值最小的邊，有可能與先前的邊重複，無妨
* 直到生成最小生成樹為止
* Time complexity: O((edge)log(vertex))
## Single source shortest path 
### with nonnegative edge(Dijkstra algorithm)
### with negative edge(Bellmen ford) 
## All-pairs shortest paths(Floyd wareshll)
## Activity-on-vertex(AOV) network


# Chapter matrix chain multiplicaion

###### tags: `CSnote`