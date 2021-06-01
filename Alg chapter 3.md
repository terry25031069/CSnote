---
title: Alg chapter 3
---
# Growth of Functions
* Introduce Asymptotic Notation $\theta(),O(),\Omega(),o(),\omega()$
## Big-O notation
* $f(n) = O(g(n))\rightarrow f(n)'s\ order\leq g(n)'s\ order$
* O(g(n))= **{** f(n) : there exist positive constants $c$ and $n_0$ such that $0\leq f(n) \leq cg(n)\ for\ all\ n\geq n_0$**}** 
* g(n) 是 f(n) 的 asymptotic **upper bound**
![](https://i.imgur.com/EhWDMCE.png)
## Big-Omega notation
* $f(n) = \Omega(g(n))\rightarrow f(n)'s\ order\geq g(n)'s\ order$
* O(g(n))= **{** f(n) : there exist positive constants $c$ and $n_0$ such that $0\leq cg(n) \leq f(n)\ for\ all\ n\geq n_0$**}**
* g(n) 是 f(n) 的 asymptotic **lower bound**
![](https://i.imgur.com/H7ESKjN.png)
### Big-O and Big-Omega
$f(n)=\Omega(g(n))\iff g(n)=O(f(n))$
## $\theta$ notation
* $f(n) = \theta(g(n))\rightarrow f(n)'s\ order= g(n)'s\ order$
* O(g(n))= **{** f(n) : there exist positive constants $c_1,c_2$ and $n_0$ such that $0\leq c_1g(n) \leq f(n) \leq c_2g(n) for\ all\ n\geq n_0$**}**
* g(n) 是 f(n) 的 asymptotic **tight bound**
![](https://i.imgur.com/K4zM5WH.png)

### Big-O and Big-Omega and $\theta$
$f(n)=\theta(g(n))\iff g(n)=O(f(n))\ and\ g(n)=\Omega(f(n))$
## Little-o notation
* $f(n) = o(g(n))\rightarrow f(n)'s\ order < g(n)'s\ order$
* O(g(n))= **{** f(n) : for any positive $c$,there exists positive constant $n_0$ such that $0\leq f(n) < cg(n)\ for\ all\ n\geq n_0$**}**
* Given a function g(n), O(g(n)) is the set of functions **{** $f(n):  lim_{n \rightarrow\infty}(f(n)/g(n))=0$ **}**
## little-omega notation
* $f(n) = o(g(n))\rightarrow f(n)'s\ order > g(n)'s\ order$
* O(g(n))= **{** f(n) : for any positive $c$,there exists positive constant $n_0$ such that $0\leq cg(n) < f(n)\ for\ all\ n\geq n_0$**}**
* Given a function g(n), O(g(n)) is the set of functions **{** $f(n):  lim_{n \rightarrow\infty}(g(n)/f(n))=0$ **}**
### Little-o and little-$\omega$
$f(n)=\omega(g(n))\iff  g(n)=o(f(n))$
## Summary
* $O$ is like $\leq$, upper bound
* $\Omega$ is like $\geq$, lower bound
* $\theta$ is like $=$, tight bound
* $o$ is like $<$
* $\omega$ is like $>$

# Exercises 
## Exercise
### 3.1-2
* Question
	* Show that for any real constants a and b, where b>0,$(n+a)^b = \theta(n^b)$
* Answer
	* Expand $(n+a)^b=C{^{b}_0}n^ba^U+C{^{b}_1}n^{b-1}a^{U-1}+...+C{^{b}_b}n^Ua^b$
	* Besides, we know below is true for any polynomial when $x \ge 1$.
	* $a_0x^0+a_1x^1+...+a_nx^n\leq(a_0+a_1+....+a_n)x^n$
	* This,$C{^{b}_0}n^b\leq C{^{b}_0}n^{b}a^{0}+C{^{b}_1}n^{b-1}a^1+...+C{^{b}_b}n^{0}a^b\leq (C{^{b}_0}+C{^{b}_1}+...+C{^{b}_b})n^b = 2^bn^b \rightarrow (n+a)^b = \theta(n^b)$
### 3.1-4
* Question
	* ![](https://i.imgur.com/8MvPHh0.png)
* Answer
	* (a) $2^{n+1} = 2\times 2^n = O(n^2)$ ,Yes
	* (b) $2^{2n} = 4^n = O(4^n)$, No
## problem
### 3.1 (a,b)
* Question
	* ![](https://i.imgur.com/PhABdJg.png)
* Answer
	* (a) There exists a constant $k$ and $n_0 = 0$ ,such that $0\leq f(n) \leq kg(n)$ for all $n \geq n_0$
	* (b)There exists a constant $k$ and $n_0 = 0$ ,such that $0\leq kg(n)\leq f(n)$ for all $n \geq n_0$
### 3.3 (a)
* ![](https://i.imgur.com/2ZlvDkx.png)

### 3.4 (a,e)
* Question: ![](https://i.imgur.com/jQSYYN0.png)
* Answer
	* (a) False. $n = O(n^2)$ but $O(n^2)!= n$
	* (b) False. if f(n) is $1/n$
###### tags: `Algorithm` `CSnote`