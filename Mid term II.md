---
title: Mid term II
---
reference: nthu cs4311
# 1 Dynamic programming
* Basic idea: Remember the solution of sub-problems
## 1. Peter is an owner of a Japanese sushi restaurant. 
* Peter is an owner of a Japanese sushi restaurant and today he invites you for dinner at his restaurant. In front of you are $n$ sushi dishes that are arranged in a line. Each dish are different and they have different costs.
* Peter hopes that you can select the dishes you want, starting from the left to the right.However, there is a further restriction: when you select a dish, say $A$, the next dish you can select must cost higher than A. 
* Design an O($n^2$)-time algorithm to select the dishes so as to maximize the total costs.
### Answer
* Modified slightly to memorize where j comes from
* Use an 2d array $Best[1..n][2]$. $Best[i][0]$ stores the maximum total costs of dishes you can select by choosing i as the last dish taken. $Best[i][1]$ stores the last dish taken.
* $Best[i][0]$ = cost of $i$th dish + $\underset{j<i}{max}\{Best[j][0],cost\ of\ jth\ dish < cost\ of\ ith\ dish\}$
* $Best[i][1]$ = $j$;
* Keep tracking the  element with biggest $Best[i][0]$. 
* Computation will be done in $O(n^2)$ time.
* Result is the  element with biggest $Best[i][0]$, and use $Best[i][1]$ to find all the preceding selected dishes.
## 2. There is a stair with n stages
* There is a stair with n stages, and on each stage there is a coupon to your favorite restaurant. Each coupon has an associated value which may be different. 
* You can climb up 1, 2, or 3 stages in a step. Since you are in a hurry, you need to reach the top of the stair in at most L steps, where L ≤ n. When you visit a particular stage, you can collect the coupon on that stage.
* Find a way to climb the stair within L steps so that you can collect coupons with maximum total value. Your algorithm should run in O($n^2$) time.
### Answer
* Use an L x n x 2 array Best. $Best[i][j][0]$ is the maximum total costs of coupons possible at reaching stage j with i steps.$Best[i][j][1]$ stores the pointer to the last j.
* $Best[1][1][0]$,$Best[1][2][0]$ and $Best[1][3][0]$'s value is assigned with the values of coupon on stage 1,2,3. Others should have $-\infty$ assigned initially.
* for others $Best[i][j][0]$= value of $jth$ coupon + $max\{Best[i-1][j-1][0],Best[i-1][j-2][0],Best[i-1][j-3][0]\}$
	* Save the j selected in $Best[i][j][1]$
	* Keep tracking the  element with biggest $Best[i][n][0]$
* All the entries can be counted in $O(Ln) = O(n^2)$ time.
* Result is the element with biggest $Best[i][n][0]$, and use $Best[i][j][1]$ to find all the preceding steps.
## 3. You have newly obtained the right to invest at a strange city called Trellisland
* You have newly obtained the right to invest at a strange city called Trellisland. The shape of the city looks like a tree, such that each node in the tree has a building, and each edge in the tree is a road connecting two buildings. And in total, there are n buildings. 
* You want to open stinky tofu stores in this city. According to the  have at most one store, and each store cannot be adjacent to each other on the same road (otherwise, it becomes too stinky). 
* You have done some preliminary study, and can now tell the number of customers who will visit each building if a store is open there. Now, your target is to decide where to open the stores so as to maximize the total number of customers.
* Design an O(n)-time algorithm to achieve the above target.
### Answer
* Make the tree a rooted tree with root r, and process the tree in a bottom-up manner. Each node v stores a value M(v) containing the maximum customers possible if a store is opened at, and a value m(v) if a store is not opened at, and also the position of the selected next Node.
* M(v) = number of customers at v + $\underset{u\ is\ a\ child\ of\ v}{\sum}m(u)$
* m(v) = $\underset{u\ is\ a\ child\ of\ v}{\sum}max\{M(u,),m(u)\}.$
* Save the u selected.
* Each M(v) or M(u) can be calculated in O(n) time, total time is proportional to the number of edges thus time complexity is $O(n)$
* the result is the nodes with M(v) from the root and nodes by following the u selected.
## 4. After a lot of hard work, you have successfully opened the stinky tofu stores.(Maximum independent set)
* In order to celebrate, you go to a buffet restaurant to have a big dinner. 
* There are $n$ distinct dishes, each has a different volume (which is an integer). It is obvious that your stomach capacity, $V$ (which is also an integer), is not large enough to hold all the dishes. Also, some dish looks expensive and some looks so-so, so that each dish has a different value to you. 
* Now, you have decided the following strategy: 
	* (i) Never take the same dish twice, and 
	* (ii) do not overeat (so that total volume is at most V ).
* Design an O(nV)-time algorithm to select the dishes so as to maximize the total values.
### Answers
* Use a n x V x 2 array Best, $Best[i][j][0]$ indicates the maximum cost of food selected, from dishes 1 to i, whose volume is j. $Best[i][j][1]$ is j or (j - $Best[i][j][0]$), to remember the last dish. If $Best[i][j][1]$ == j, this dish is not picked, otherwise it is picked. 
* $Best[i][j][0]$=  $max\{Best[i-1][j][0],cost\ of\ dish\ i+ Best[i-1][j-volume(i)][0]\}$
* $Best[i][j][1]$ = j or j- volume depend on the result of max.
* All are computed row by row , total time is O(nV).
* The maximum cost of dishes can select is $Best[n][V][0]$, find the volume of last dish by using $Best[i][j][1]$, to check whether the last dish is selected

# 2 Greedy and Amortized cost
## 1. One day a camel asks for your help. 
* He wants to make a trip from Egypt to Turkey, but he can only travel 100km with his stomach filled with bananas. There are several oases on the road which supply bananas, but he wants to visit as few oases as possible. Suppose you already know the position of oases on the road from Egypt to Turkey, and assume that there is at least a way for the camel to travel from Egypt to Turkey. Design a greedy algorithm to help the poor camel finish his trip. 
* Requirements:
    * (a) The camel must visit minimum oases with your algorithm.
    * (b) The algorithm must be a greedy algorithm (with a brief proof).
    * (c) The camel must arrive Turkey.
### Answer
* Always pick the farthest oasis.
* Proving the greedy choice property. Let OPT = an optimal solution, Let Aj = activity with moving farthest. Let A' be the farthest moving activity, since Aj can't be shorter than A', we can replace A' with Aj. OPT contains Aj.
* Proving optimal substructure property, let k be the number of oasis to stop int OPT.
	* Let OPT – { Aj } = OPT', an optimal solution to reach Turkey from Aj.
	* To suppose that the lemma is incorrect. Then OPT' can use fewer stops than k-1. Since OPT -{Aj} is a solution to move from Aj to Turkey, and OPT'∪ {Aj} has at most k-1 oasis, reaching Turkey from Aj with less than k-1 stops is a contradiction
## 2. Bill has invented a strange data structure called Flipping Stack. 
* Flipping Stack supports only Flipping-Push() function. In each Flipping-Push(), an item is first pushed to the stack, and check if the number of items in the stack is a power of 2 (i.e., equals to 2i for some i). If so, all items in the stack will have to be fipped. For instance,suppose we use Flipping-Push() to push the items 1, 2, 3, 4 into the stack, the contents of the stack (viewed from bottom to top) after each push are as follows: (1) ⇒ (2, 1) ⇒ (2, 1, 3) ⇒ (4, 3, 1, 2) Bill asks you to analyze the amortized cost of Flipping-Push.Requirements:
    * (a) The cost for flipping of the stack is equal to the number of items currently in the stack.
    * (b) Analyze the amortized cost with all the three methods taught in class. (Aggregate,Accounting, Potential)
#### Aggregate
* Total cost to push n items is O(n).
* Total cost to flip is 1+2+4+...+n = O(n).
* So total time of n operations is O(n).
* Amortized cost is O(n)/n  = O(1).
#### Accounting
* Assign cost 3 for each operation
* Pushing an item costs 1, so we will gain 2 credits for each operation.
* for the $2^ith$ operation, we will accumulate $2\times 2^i = 2^{i+1}$, the cost at $2^ith$ has an $2^i$ extra, $2^{i+1}> 2^i$ . 
* For the $2^{i+1}th$ operation, we have  $2\times2^{i+1}= 2^{i+2}$ credits, and cost at $2^{i+1}th$ operation is $2^{i+1}$, $2^{i+2}>2^{i+1}$.
* By induction, for any n operations we have non-negative credits, thus the amortized cost for each operation is $O(1)$ 
#### Potential
* To ease the discussion, for any integer $i$, we define $i'$ to be the largest power of two that is smaller than or equal to $i$.
* Define the potential function$\Phi(D_0)=0, \Phi(D_i)= 2(i-i')$ for $i>0$.
* for operation 1
    * $c_i' = c_i+\Phi(D_i)-\Phi(D_{i-1}) = 2+2(0-0) -0 = 2$ 
* for operation $i>1$, if i is not power of 2
    * $c_i' = c_i+\Phi(D_i)-\Phi(D_{i-1}) = 1+2(i-i')- 2(i-1-i') = 3$
* for operation $i=2^j, j \in N$
    * $c_i' = c_i+\Phi(D_i)-\Phi(D_{i-1}) = 1 + 2^j + 2(i-i) - 2(2^{j}-1-2^{j-1}) = 1+2^j-2^{j+1} + 2 + 2^j = 3$
* Amortized cost is 3 = 0(1).
### Answer
## 3. A min-heap with n elements supports Insert and Extract-Min in O(log n) worstcase time. 
* Give a potential function Φ such that the amortized cost of Insert is O(log n)and the amortized cost of Extract-Min is O(1).Requirements:
    * (a) You have to describe your potential function Φ clearly.
    * (b) You must show that your potential function works.
*  Explain why it is impossible to have the amortized cost of Insert to be o(log n) and at the same time the amortized cost of Extract-Min is O(1).(Hint: Sorting lower bound.)
### Answer
* For each node u in the heap, Φ(u) = size of the subtree rooted at u. Then, for a heap H, $Φ(H) = \sum_{u∈H} Φ(u) = sum$ of potentials of all the nodes. It is easy to check that at any time, Φ(H) ≥ 0.
* When Insert is performed, at most log n nodes will increase each of their potential by 1, so that the potential of H will be increased by at most log n. Since the actual cost of insertion is also log n, the amortized cost of Insert is O(log n).
* When Extract-Min is performed, each ancestor of the last node of the heap will decrease their potential by 1, which is the same as the actual cost of Extract-Min. Thus, its amortized cost is O(1).
* However, it is impossible to have the amortized cost of Insert to be o(log n) and at the same time the amortized cost of Extract-Min is O(1). Assume on the contrary that thiscan be done. Then, we can sort n items using n Insert followed by n Extract-Min, with a total cost of n × o(log n) + n × O(1) = o(n log n). As each operation of Insert or Extract-Min requires only a series of comparisons, this shows that n items can always be sorted using o(n log n) comparisons. Now, we obtain a contradiction from the sorting lower bound, which states that sorting n items in the worst case needs Ω(n log n) comparisons.
# 3
## 1. There is a staircase with n steps. 
* Your friend, Jack, wants to count how many different ways he can walk up this staircase. Because John is quite tall, in one move, he can choose either to walk up 1 step, 2 steps, or 3 steps. Let Fk denote the number of ways John can walk up a staircase with k steps. So, F1 = 1, F2 = 2, F3 = 4, and F4 = 7. Derive a recurrence for Fk, and show that Fn can be computed in O(n) time.
### Answer
* For $k>3$, we can walk $k$ steps in three ways
	1. First reaching the $(n-1)$th step, and walk one step in the last move.
	2. First reaching the $(n-2)$th step, and walk two step in the last move.
	3. First reaching the $(n-3)$th step, and walk three step in the last move.
* Based on the above, the recurrence of Fk can be expressed as follows:
	* $F_1=1,F_2=2,F_3=4$
	* For $k>3, F_k=f_{k-3}+f_{k-2}+f_{k-1}$
* If we compute $F_k$ in a bottom-up manner (i.e., for k = 1, 2, . . . , n), each $F_k$ can be computed in O(1) time. Thus, F(n) can be found in O(n) time.
## 2. Consider the following coin-taking game between Tom and Jerry.
* We start with two piles of coins, with x coins in the first pile and y coins in the second pile. They will take turn to remove coins from the pile. In each turn, they have three options: (i) remove any number of coins from the first pile, (ii) remove any number of coins from the second pile, or (iii) remove the same number of coins from both piles. In this game, the person loses if he cannot get any coin during his turn. For instance, suppose it is Tom’s turn, and the coins in the current piles are (x, y) = (5, 5). In this case, if Tom now removes coins using the third option, he can make the piles (0, 0) so that Jerry loses by not getting any coin in his next turn. If both Tom and Jerry plays cleverly, some combinations of (x, y) are always losing. For instance, (0, 0) is a losing combination, and we can also show that (1, 2) is a losing combination as follows:
* Firstly, there are only 4 ways of removing the coins: 
    * (1) take 1 coin from pile 1; 
    * (2)take 1 coin from pile 2; 
    * (3) take 2 coins from pile 2; 
    * (4) take 1 coin from both piles;
    *  If we remove using (1), the remaining pile is (0, 2), so that the opponent player can force us to lose by taking 2 coins from pile 2.
* If we remove using (2), the remaining pile is (1, 1), so that the opponent player canforce us to lose by taking 1 coin from both piles.
* If we remove using (3), the remaining pile is (1, 0), so that the opponent player canforce us to lose by taking 1 coin from pile 1.
* If we remove using (4), the remaining pile is (0, 1), so that the opponent player canforce us to lose by taking 1 coin from pile 2.
* Suppose x and y are both at most n. For any i, j, let A(i, j) = L if (i, j) is a losing combination, and A(i, j) = W otherwise.(20%) Derive a recurrence for A(i, j) and show that we can determine if (x, y) is a losing combination in O($n^3$) time.
### Answer
* A combination is losing if every move leads to a winning combination (for our opponent). Conversely, a combination is winning if at least one of the moves leads to a losing combination, since we can take such a move and force our opponent to lose.
* Based on this observation, we can derive the recurrence for A(i, j) as follows:
	* A(0,0) = L
	* If every move of (i,j) leads  to a winning combination, that A(i,j) = L. Precisely , A(i,j) = L if
		* \begin{cases}
A(i',j)= W, &\text{for all}\ 0 \leq i'<i,\\
A(i,j')= W, &\text{for all}\ 0 \leq j'<j, and\\
A(i-k,j-k)= W, &\text{for all}\ 1 \leq k \leq min\{i,j\}\\
\end{cases}
		* otherwise, $A(i,j) = W$
* Since the value of A(i, j) depends only on the values of A(k, l) with (k + l) < (i + j), we can compute A(i, j) according to the increasing order of i + j. The time to compute each A(i, j) is O(i + j), which is O(n).
* As x and y are at most n, to obtain A(x, y), there are at most $O(n^2)$ entries of A to be computed. The total time to compute all such entries is thus $O(n^3)$.

## 3. John wants to drive from San Francisco to Seattle using his car.
* His car’s gas tank, when full, holds enough gas to travel exactly n km. John has already made up his route, and his only concern now is to plan where to refill his gas tank along the way.
* Suppose that there are k gas stations x1, x2, . . . , xk along the route, and the distance between any two of them are known. Also, for any two consecutive gas stations, the distance is at most n km.†
* To save time, John wants to stop for as few gas stations as possible. Give an efficient method to find out the gas stations for John to stop, and show that your method yields an optimal solution.
* †Assume that the distance between San Francisco and x1, and the distance between xk and Seattle, are both at most n km. So, John must be able to arrive Seattle.
### Answer
* Let s be the rightmost (farthest) gas station within the first n km from SF. Then, we can show the following:
* There exists an optimal solution n (using the fewest number of gas stations) whose first station is s.
	* Proof. (By cut-and-paste argument.) Consider an optimal solution OP T = $(s_1, s_2, . . . , s_k)$, with stations ordered from left to right. If $s_1 = s$, then the lemma is correct. Otherwise, we replace $s_1$ by s, and remove redundant gas stations (if any). It is easy to see that s1 must be on the left of s, since if not, the distance of s1 and SF is more than n km. Thus, after the replacement, we obtain another solution that can allow us to travel from SF to Seattle. The new solution uses at most the same number of gas stations as OP T, which must be optimal. Thus, the proof completes.
* Let OPT be an optimal solution that contains s. Suppose OP T has k gas stations.
* By removing s from OP T, the remaining k − 1 gas stations must form an optimal solution to travel from s to Seattle, starting with a full-tank at s.
    * Proof. (By contradiction.) Let OPT' be an optimal solution to travel from s to Seattle.Suppose on the contrary that the lemma is incorrect. Then, OPT' must use fewer than k − 1 gas stations, since OP T − {s} is a feasible solution to travel from s to Seattle. Consequently, OPT'∪ {s} has at most k−1 gas stations, which implies a solution to travel from SF to Seattle with fewer gas stations than OPT, leading to a contradiction.
```
1. Choose s1 = rightmost gas station from SF within first n km ;
2. k = 1 ;
3. while ( distance(sk, Seattle) > n ) {
4.        Choose sk+1 = rightmost gas station from sk within first n km ;
5.        k = k + 1 ;
6. }
```

## 4. A min-heap with n elements supports Insert and Extract-Min in O(log n) worstcase time. 
* Give a potential function Φ such that the amortized cost of Insert is O(log n)and the amortized cost of Extract-Min is O(1). Show that your Φ works.
### Answer
* Two solution
#### 1 
* For each node u in the heap, Φ(u) = size of the subtree rooted at u. Then, for a heap H, $Φ(H) = \sum_{u∈H} Φ(u) = sum$ of potentials of all the nodes. It is easy to check that at any time, Φ(H) ≥ 0.
* When Insert is performed, at most log n nodes will increase each of their potential by 1, so that the potential of H will be increased by at most log n. Since the actual cost of insertion is also log n, the amortized cost of Insert is O(log n).
* When Extract-Min is performed, each ancestor of the last node of the heap will decrease their potential by 1, which is the same as the actual cost of Extract-Min. Thus, its amortized cost is O(1).

#### 2
* For each node u in the heap, Φ(u) = node-depth of u. Then, for a heap H, $Φ(H) = \sum_{u∈H} Φ(u) = sum$ of potentials of all the nodes. It is easy to check that at any time, Φ(H) ≥ 0. 
* When Insert is performed, a new node is created with node-depth at most log n. Consequently, the potential of H will be increased by at most log n. Since the actual cost ofinsertion is also log n, the amortized cost of Insert is O(log n).
* When Extract-Min is performed, the last node of the heap is removed. This causes a drop in the potential by its node-depth, which is the same as the actual cost of Extract-Min. Thus, the amortized cost of Extract-Min is O(1).
## 5. A sorted array allows efficient searching in logarithmic time. 
* However, if we want to insert a new element, it requires linear time in the worst case to keep the array sorted. In fact, we can improve the insertion time (in the amortized sense) by making the searching time a bit slower. Let n be the number of elements in the current array. Let $k = \lceil log(n+1)\rceil$, so that the binary representation of n has k bits. Our scheme is to partition the n elements into k arrays $A_0, A_1, . . . , A_{k−1}$ based on n’s binary representation. Precisely, let ($b_{k−1}, b_{k−2}, . . . , b_0$) be the binary representation, with $b_{j−1}$ being the jth least-significant bit. The array $A_i$ will hold $2^i$ elements in sorted order if $b_i = 1$; otherwise, it will be empty.
* Based on this scheme, searching for an element will need to search all k arrays in the worstcase, and the total time will be $O(k log n) = O(log^2 n)$. To insert a new element, the number of elements, n, will be increased. Then, its binary representation will change, so we need to partition the elements in a different way.¶
* Describe how to insert a new element into this data structure so that the partitioning can be maintained correctly. Show that the amortized insertion time is O(log n).
* ¶For example, when there are 5 elements, we will have 3 sorted arrays, such that one is holding 4 elements, one is holding 1 element, and one is empty. When we insert a new element, the number of elements becomes 6, and we want to have one sorted array with 4 elements, one with 2 elements, and one empty.
### Answer
* Let $b$ be the binary representation of the number of elements before an insertion, and let $r$ be the number of consecutive 1’s at the rightmost of $b$. Here, r ranges from 0 to $\lfloor logn \rfloor$.
* After an insertion, the binary representation is changed such that the (r + 1)th rightmost bit changes from 0 to 1, while the last r bits all become 0. Consequently, we need update the set of sorted arrays. One way to do so is to merge the r arrays corresponding to the r 1’s, and merge them together with the newly inserted element. We can do so by merging the newly inserted element with the 1-element array, forming a 2-element array; then, merge this with the original 2-element array to form a 4-element array; and so on. This process can be done in $O(2^r)$ time.
* When m insertions (with m ≤ n) are performed, the number of times that a binaryrepresentation has exactly r rightmost consecutive 1’s is $O(m/2^r)$. Thus, the total timefor m insertions is at most:
	* $\sum_{r=0}^{\lfloor logn \rfloor}O(m/2^r) \times O(2^r) = O(mlogn)$
* Thus, the amortized cost of insertion is O(log n).
## 6.  This question is an extension of Question 2. 
* Our target is to show that we can determine if (x, y) is a losing combination in O(n) time. You may devise your own proof, or you may follow the steps suggested below.
### Questions
#### (a)
##### Q
* Show that for each k, there is at most one x such that (x, x+k) is a losing combination.
##### A
* Suppose on the contrary that there exist distinct (x, x + k) and (y, y + k) which are both losing. WLOG, let y > x. Now, by removing y − x coins from both piles in (y, y + k), we obtain a losing combination (x, x + k). Thus, contradiction occurs
#### (b)
##### Q
* Show that for each x, there is at most one r such that (x, r) is a losing combination.
##### A
* Suppose on the contrary that there exist distinct $(x, r)$ and $(x, r')$ which are both losing. WLOG, let $r' > r$. Now, by removing $r' − r$ coins from the second pile in$(x, r')$, we obtain a losing combination (x, r). Thus, contradiction occurs.
#### (c)
##### Q
* (c) We are going to describe a procedure to find losing combinations $L_0$, $L_1$, . . .:
	* Set L0 = (0, 0);
    for k = 1, 2, . . . , {
Set v = smallest positive integer not in $L_0, L_1, L_2, L_{k−1}$;
        Set $L_k$ = (v, v + k);
        }
* E.g., the above procedure sets $L_1$ = (1, 2),  $L_2$ = (3, 5),$L_3$ = (4, 7), and $L_4$ = (6, 10). Show that each $L_k$ from the above procedure is a losing combination. (Hint: Use induction and the results of (a) and (b).)
##### A
* We shall prove the statement “$L_k$ is a losing combination” by induction.
	* Base case: Since $L_0$ is losing, the statement is correct for k = 0.
	* Inductive case: Suppose the statement is true for k = 0, 1, . . . , t−1. Then, consider $L_t$ = (v, v + t). We shall prove $L_t$ is losing by showing each move of $L_t$ leads to a winning combination. There are three cases for a move:
1.  Take from 1st pile: We obtain a combination (v', v + t) with v' < v. By the choice of v, v' appears in $L_k$ for some k ≤ t − 1. This implies there is a losing combination (v', x) or (x, v')with |x − v'| at most t − 1. By part (b), we see that (v', v + t) cannot be losing.
2.  Take from both piles: We obtain a combination (v', v' + t) with v' < v. Similarly, by part (b), we see that (v', v' + t) cannot be losing.
3.  Taking from 2nd pile:If taking at least t coins, we get a combination (v, v') with v' < v. By our choice of v, there is some losing combination (v', x) or (x, v') with x < v. Then, by part(b), we see that (v, v') cannot be losing.
	If taking less than t coins, we get a combination (v, v + t') with t' < t. By our choice of v, there is some losing combination (v', v' + t') with v' < v. Then, by part (a), we see that (v, v + t') cannot be losing.
* In conclusion, every move of (v, v +t) leads to a winning combination. Thus, $L_t$ must be losing, and this completes the proof of the inductive case.
#### (d)
##### Q
* Show that after x iterations, there must be some Li containing x.
##### A
* The v-value of $L_k$ is strictly increasing. Thus, the v-value of $L_x$, $v_x$, is at least x. This implies that $L_0$, $L_1$, . . . , $L_x$ must contain all values at most $v_x$, and thus containing x.
#### (e)
##### Q
* Show how to implement the procedure in (c) so that the total running time for x iterations is O(n).
##### A
* The most time-consuming step is to find the smallest unseen number. We can make this efficient by using an auxiliary array A to record whether a number is seen or not. At any time, we maintain a pointer P pointing at the smallest unseen number, so that each time v can be found in O(1) time. Once $L_k$ is computed, we update A accordingly, and move the pointer P rightwards, one entry after another, until it locates the next unseen number. Since x ≤ n, it is easy to check that A is updated at most O(n) times, and the pointer P is moved at most O(n) times. The total time spent is O(n).
#### (f)
##### Q
* Conclude that we can determine if (x, y) is a losing combination in O(n) time.
##### A
* We compute $L_0$, $L_1$, . . . , $L_x$ in O(n) time and find the losing combination that contains x. If that combination is (x, y) or (y, x), we conclude immediately that (x, y) is losing. Otherwise, by part (b), we can also conclude immediately that (x, y) is winning.

###### tags: `Algorithm` `CSnote`