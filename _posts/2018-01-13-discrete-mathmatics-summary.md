---
layout: post
title: 离散数学知识点总结
mathjax: true
published: false
tags: summary
---

**仅供个人期末回顾使用，如有错漏请谅解**

# Chapter 9. Relations

### 9.1 Relations and Their Properties

- relation代表了一个集合R，包含所有的$A \times B$结果中的**order pairs**，特别的**a relation on set A**就是A=B的时。

- reflexive, symmetric, transitive

- irreflexive, asymmetric, antisymmetric（只能在主对角线）

- 对于**R-relative set of x**，即$R(x)=\{y\in B|xRy\},x\in A,R=A\times B$，集合的二元操作可以直接提取出括号(proof)：
$$
A_1 \subseteq A_2 \rightarrow R(A_1)\subseteq R(A_2) \\ 
R(A_1\cup A_2) = R(A_1)\cup R(A_2)\\
R(A_1\cap A_2) \subseteq R(A_1)\cap R(A_2)
$$
- how many **reflexive/symmetric** relations are there **on a set with n element**
- combing relations: relation之间进行集合的二元运算
- $coposition\  of\  R\  and\ S: a\ S\circ R\ c$， 先进行后面的R，再到S，即$(S\circ R)(A)=S(R(A))$(proof)
- 定义$R^n=R^{n-1}\circ R$ ，**$R\ is\ transitive\ \leftrightarrow R^n \subseteq R$** (proof)
-[ ] (R◦S)◦T = R◦(S ◦T)，所以 R◦Rn+1 = R◦(Rn ◦R) = (R◦Rn)◦R = Rn+1 ◦R，也就是虽然矩阵乘法不满足交换律，但是在relation中求高阶coposition的时候是可以使用交换律的


### 9.2 n-ray Relations

- primary key 都不一样
- composite key，两个或者key组合以后的pair可以distinguish

### 9-3 Representing Relations

- directed graph or zero-one matrix
- $S\circ R$的矩阵由矩阵乘法（**$+,\cdot$代表与、或**）$M_R\odot M_S$得到的结果，注意前后顺序
- ***restricition of R to B*** is $R\cap (B\times B)$
-[ ] $if\ R_1\ is\ [property1],R_2\ is\ [property2], then\ R_1*R_2 is [property3]$

### 9-4 Closures

- **closure of R with respect to property P** 是由R构建的新的一个R，并且添加的pair的**数量要最小**
- 用digraph表示的relation的三种closure的构建方式
- $connectivity\ relation\ R^*$或者$R^\infty$ 是所有$R^n$ 的union，同时也是**R的transitive closure（应该不用证，太复杂）**
- 用来证明connectivity relation is transitive closure 的几个theorem
  - $A\subseteq B,\ C\subseteq B \rightarrow A\cup C \subseteq B$
  - $A\subseteq S,\ B\subseteq T \rightarrow A\circ B \subseteq S\circ T$
    - 由第二个可以推出 $R\subseteq S \rightarrow R^n \subseteq S^n$  
  - $R\ is\ transitive \rightarrow R^n\ is\ transitive(prooved\ by (R^n)^2=(R^2)^n\subset R^n)$
- 因为一条path最长不过n-1，所以transitive closure里面求$R^k$的时候最多只用求到$R^n$,n是顶点数
- 一般的算法，直接用矩阵求$R^*:M_{r^*}=M_R\vee M_R^{[2]}\vee M_R^{[3]}\vee M_R^{[4]}...\vee M_R^{[n]}$
- Warshall Algorithm：$w_{ij}^{[k]}=w_{ij}^{[k-1]}\vee(w_{ix}^{[k-1]}\wedge w_{xj}^{[k-1]})$w是W矩阵的一个元素，找中间点

### 9-5 Equivalence Relation

- 定义，也是需要证明的三种性质：**reflexive, symmetric, transitive**
- **Equivalence Class**：一个equivalence relation的集合上互相之间有关联的子集
- Partition：对大集合的一种划分的方式，可以利用partition反向得到一种equivalence relation
- $R\ is \ E.R.,a\ R\ b\leftrightarrow R(a)=R(b)$ 这里的R（a）是一个集合，然后用三个性质可以证明
- **quotient set A/R**：由equivalence relation R得到的划分
-[ ] 第56题，交集保留ER的三个性质，并集不transitive
- 64题，得到不同closure的顺序会导致R不再是一个ER，也就是要最后再求R*

### 9-6 Partial Ordering

- 定义与证明题：**reflexive, antisymmetric（对角线）, transitive**

- **Poset**：一个带有partial ordering R 的集合

- **total order/linear order**表示所有的元素之间都**comparable**，也就是存在关系

- **well order**：全序的情况下，所有的非空子集都有一个**最小**的值，比如$(Z,\leq)$就不是

- 构造**hasse diagram**：去掉自己的loop，所有transitive的第三边去掉，从下到上画有向图

- 在这里提前加了isomorphism：a ≤ b     if and only if      f(a) ≤’ f(b).

- 两个isomorphism的poset拥有相同的hasse diagram，相同的性质，相同的LUB/GLB

- maximal/minimal和greatest/least element的区别：前者是最大/最小的，后者是**最大/最小且唯一的element**，并且后者可能不存在

- LUB和GLB是唯一且不一定存在的，并且是可以属于该集合的

- **Lattice**是在partial ordering的前提下，任意两个元素都由LUB和GLB的一种关系，做题举反例的时候找两个点没有LUB或者GLB就行。另外会用$\vee,\wedge$来表示upper bound和lower bound，特指LUB和GLB吗？

- sublattice：同时保留了GLB和LUB的subsetn

  - Let (L, ≤)be a lattice.  A nonempty subset S of L iscalled a sublattice of L

    nif a∨b $\in$ S and a∧b $\in$ Swhenever a $\in$  Sand   b  $\in$ S. 

- lattice的isomorphism要包括joint和meet的运算

# Chapter 9 Group Theory

### 9-1 Binary Operations

- 二元操作区分前后，并且必须要满足**closed**， 即f(a,b)=a*b也要在A内
- commutative, associatvie, idempotent 是可以有的性质，但不是必须有的
- inverse和identity element的的性质证明都要满足commutative，并且identity和inverse都是**唯一的**

### 9-2 Semigroups and Group

- |  类型  | Groupoid | Semigroup     | Monoid   | Group     | Abelian       |
  | :--: | -------- | ------------- | -------- | --------- | ------------- |
  |  性质  | Closure  | Associativity | Identity | Inversity | Communitivity |

- **free semigroup**：$(A^*,\cdot )$ is a semigroup

- **permutation group**：对n个点进行permutation操作可以有n！种，所以$|S_n|=n!$

- ​

# Chapter 8 Advanced Counting Techniques 

### 8-1

### 8-2

### 8-3 Divide and Conquer

- 由recurrence$f(n)=af(n/b)+c$ ，可以推出$f(n)=a^kf(1)+\sum_{j=0}^{j=k-1} a^jg(n/{b^j})$，这个要记
- 当g(n)=c为常数的时候，我们可以得到 f(n)的时间复杂度
  - $a>1 \rightarrow O(n^{log_ba})$
  - $a=1 \rightarrow O(logn)$
  - 代入记忆的式子里面的时候，可以得到f(n)关于n的表达式
- **Master Theorem**，上一个式子的推广，此时$g(n)=cn^d$，则有 f(n)的时间复杂度
  - $ a<b^d \rightarrow O(n^d)$
  - $ a=b^d \rightarrow O(n^dlogn)$
  - $ a>b^d \rightarrow O(n^{log_ba})$

