---
layout: post
title: 离散数学知识点总结
mathjax: true
tags: 应考归纳
key: 20180118
modify_date: 2018-01-18
---

**仅供个人期末回顾使用，如有错漏请谅解**

<!--more-->

老师提供的复习重点

> 1.关系：性质、等价关系、偏序关系的属性及拓扑排序。
> 2.群论：同态、同构、半群和群的特性及证明、群编码。
> 3.概率：条件概率、Bayes Theorem。
> 4.递推关系：找出递推关系、方程求解、生成函数求解。
> 5.图：哈密顿回路、欧拉回路、最短路径、平面性判定、最小着色数（含着色多项式）、传输网最大流量。
> 6.树：树的特性、最小生成树及算法。



# Chapter 9. Relations

### 9.1 Relations and Their Properties

- relation代表了一个集合R，包含所有的$$A \times B$$结果中的**order pairs**，特别的**a relation on set A**就是A=B的时。

- reflexive, symmetric, transitive

- irreflexive, asymmetric, antisymmetric（只能在主对角线）

- 对于**R-relative set of x**，即$$R(x)=\{y\in B|xRy\},x\in A,R=A\times B$$，集合的二元操作可以直接提取出括号(proof)：
$$
A_1 \subseteq A_2 \rightarrow R(A_1)\subseteq R(A_2) \\ 
R(A_1\cup A_2) = R(A_1)\cup R(A_2)\\
R(A_1\cap A_2) \subseteq R(A_1)\cap R(A_2)
$$
- how many **reflexive/symmetric** relations are there **on a set with n element**
- combing relations: relation之间进行集合的二元运算
- $$coposition\  of\  R\  and\ S: a\ S\circ R\ c$$， 先进行后面的R，再到S，即$$(S\circ R)(A)=S(R(A))$$(proof)
- 定义$$R^n=R^{n-1}\circ R$$ ，**$$R\ is\ transitive\ \leftrightarrow R^n \subseteq R$$** (proof)
-[ ] (R◦S)◦T = R◦(S ◦T)，所以 R◦Rn+1 = R◦(Rn ◦R) = (R◦Rn)◦R = Rn+1 ◦R，也就是虽然矩阵乘法不满足交换律，但是在relation中求高阶coposition的时候是可以使用交换律的


### 9.2 n-ray Relations

- primary key 都不一样
- composite key，两个或者key组合以后的pair可以distinguish

### 9-3 Representing Relations

- directed graph or zero-one matrix
- $$S\circ R$$的矩阵由矩阵乘法（**$$+,\cdot$$代表与、或**）$$M_R\odot M_S$$得到的结果，注意前后顺序
- ***restricition of R to B*** is $$R\cap (B\times B)$$
-[ ] $$if\ R_1\ is\ [property1],R_2\ is\ [property2], then\ R_1*R_2 is [property3]$$

### 9-4 Closures

- **closure of R with respect to property P** 是由R构建的新的一个R，并且添加的pair的**数量要最小**
- 用digraph表示的relation的三种closure的构建方式
- $$connectivity\ relation\ R^*$$或者$$R^\infty$$ 是所有$$R^n$$ 的union，同时也是**R的transitive closure（应该不用证，太复杂）**
- 用来证明connectivity relation is transitive closure 的几个theorem
  - $$A\subseteq B,\ C\subseteq B \rightarrow A\cup C \subseteq B$$
  - $$A\subseteq S,\ B\subseteq T \rightarrow A\circ B \subseteq S\circ T$$
    - 由第二个可以推出 $$R\subseteq S \rightarrow R^n \subseteq S^n$$  
  - $$R\ is\ transitive \rightarrow R^n\ is\ transitive(prooved\ by (R^n)^2=(R^2)^n\subset R^n)$$
- 因为一条path最长不过n-1，所以transitive closure里面求$$R^k$$的时候最多只用求到$$R^n$$,n是顶点数
- 一般的算法，直接用矩阵求$$R^*:M_{r^*}=M_R\vee M_R^{[2]}\vee M_R^{[3]}\vee M_R^{[4]}...\vee M_R^{[n]}$$
- Warshall Algorithm：$$w_{ij}^{[k]}=w_{ij}^{[k-1]}\vee(w_{ix}^{[k-1]}\wedge w_{xj}^{[k-1]})$$w是W矩阵的一个元素，找中间点

### 9-5 Equivalence Relation

- 定义，也是需要证明的三种性质：**reflexive, symmetric, transitive**
- **Equivalence Class**：一个equivalence relation的集合上互相之间有关联的子集
- Partition：对大集合的一种划分的方式，可以利用partition反向得到一种equivalence relation
- $$R\ is \ E.R.,a\ R\ b\leftrightarrow R(a)=R(b)$$ 这里的R（a）是一个集合，然后用三个性质可以证明
- **quotient set A/R**：由equivalence relation R得到的划分
-[ ] 第56题，交集保留ER的三个性质，并集不transitive
- 64题，得到不同closure的顺序会导致R不再是一个ER，也就是要最后再求R*

### 9-6 Partial Ordering

- 定义与证明题：**reflexive, antisymmetric（对角线）, transitive**

- **Poset**：一个带有partial ordering R 的集合

- **total order/linear order**表示所有的元素之间都**comparable**，也就是存在关系

- **well order**：全序的情况下，所有的非空子集都有一个**最小**的值，比如$$(Z,\leq)$$就不是

- 构造**hasse diagram**：去掉自己的loop，所有transitive的第三边去掉，从下到上画有向图

- 在这里提前加了isomorphism：a ≤ b     if and only if      f(a) ≤’ f(b).

- 两个isomorphism的poset拥有相同的hasse diagram，相同的性质，相同的LUB/GLB

- maximal/minimal和greatest/least element的区别：前者是最大/最小的，后者是**最大/最小且唯一的element**，并且后者可能不存在

- LUB和GLB是唯一且不一定存在的，并且是可以属于该集合的

- **Lattice**是在partial ordering的前提下，任意两个元素都由LUB和GLB的一种关系，做题举反例的时候找两个点没有LUB或者GLB就行。另外会用$$\vee,\wedge$$来表示upper bound和lower bound，特指LUB和GLB吗？

- sublattice：同时保留了GLB和LUB的subsetn

  - Let (L, ≤)be a lattice.  A nonempty subset S of L iscalled a sublattice of L

    nif a∨b $$\in$$ S and a∧b $$\in$$ Swhenever a $$\in$$  Sand   b  $$\in$$ S. 

- lattice的isomorphism要包括joint和meet的运算



# Chapter 9 Group Theory

### 9-1 Binary Operations

- 二元操作区分前后，并且必须要满足**closed**， 即f(a,b)=a*b也要在A内
- commutative, associatvie, idempotent 是可以有的性质，但不是必须有的
- inverse和identity element的的性质证明都要满足commutative，并且identity和inverse都是**唯一的**

### 9-2 Semigroups and Group

- 群：一个集合加上一个二元操作，并且根据这个二元操作在集合内满足的各个性质来确定群的种类


- |  类型  | Groupoid | Semigroup     | Monoid   | Group     | Abelian       |
  | :--: | -------- | ------------- | -------- | --------- | ------------- |
  |  性质  | Closure  | Associativity | Identity | Inversity | Communitivity |

- 用binary operation的idempoten, commutative and associative,以及b=a\*b 可以证明LUB(a,b)=a*b 

- **free semigroup**：$$(A^*,\cdot )$$ is a semigroup

- **permutation group**：对n个点进行permutation操作可以有n！种，所以$$|S_n|=n!$$


### 9-3 New Algebra

- 子群需要满足的性质有，集合是原集合的**非空子集**，同时二元操作需要满足相应的性质

- | 原群G    | semigroup | monoid       | group                             |
  | ------ | --------- | ------------ | --------------------------------- |
  | *在T中满足 | closed    | $$e\in T$$   | $$a\in T\rightarrow a^{-1}\in T$$ |
  | T的前提   | 无         | subsemigroup | submonoid                         |

  由于*本来就associative，所以$$T\ subsemigroup\ of\ semigroup\ G \rightarrow T\ is\ also\ semigroup$$,类似对submonoid也成立

- 定义二元操作的幂运算：$$a^n=a^{n-1}*a\ and\ a^0=e$$

- 证明$$\forall a,b\in H\rightarrow a^-1*b\in H$$,H是G的非空子集，则H是subgroup，这个证明必须要按identity，inverse，closed的顺序，identity怎么证= =？

- 规定两个semigroup(monoid,group)的笛卡尔乘积：$$(s1,t1)*''(s2,t2)=(s1*s2,t1*'t2)$$

- $$Z_m \times Z_n \cong Z_{mn},if\ GCD(m,n)=1$$

- **congruence relation**同余关系：有一 equivalence relation R和groupoid (G,*)，并且R满足这个关系
  $$a\ R\ a',b\ R\ b' \rightarrow (a*b)\ R\ (a'*b')$$

- quotient groupoid/semigroup：定义一个groupoid $$(G/R,\circledast)$$，并且**R为congruence**,这个二元操作的含义是$$[a]\circledast [b]=[a*b]$$，该证明可以推广到$$(Z/\equiv,\oplus)$$ ,\oplus 和这个类似，是class之间的二元操作

### 9-4 Homomorphism

- **isomorphism($$\cong$$)**证明的四个步骤

  1. 定义$$f:S\rightarrow T$$，并且这两个集合的二元操作为\*和*‘
  2. 证明 f one-to-one（一个x对应一个y，$$f(x_1)=f(x_2)\rightarrow x_1=x_2$$ ）
  3. 证明f onto （每个y都有对应x）
  4. 证明等式**$$f(a*b)=f(a)*'f(b)$$**

- **homomorphism($$\sim$$)**只需要满足等式**$$f(a*b)=f(a)*'f(b)$$**，*onto homomorphism*则需要证明f是onto

- 对于monoid，如果S to T是isomorphism（**onto homomorphism也成立，而且更强力**），则可以证明以下命题，（逆命题可以用来证明不同构）

  - $$
    f(e)=e'\\
    f(a^{-1})=(f(a))^{-1}\\
    H\ is\ subgroup\ of\ G\rightarrow f(H)\ is\ subgroup\ of\ G'\\
    G是某种群，则G’也是
    $$



### 9-5 Fundamental Homomorphism Theorem and Normal Subgroup

- natural homomorphism：有$$（G，*）\ and\ (G/R,\circledast)$$，则$$f: G\rightarrow G/R$$是**onto homomorphism**
- fundamental homorphism therome：如果$$f:S\rightarrow T$$是onto homomorphism，规定S中的R是 $$a\ R\ b \leftrightarrow f(a)=f(b)$$，则
  - R is congruence
  - $$T\cong S/R$$
- H是G的subgroup，如果a属于H，则aH=H，所以在求H的所有coset的时候，可以跳过aH的运算，转而算别的$$b \in G$$
- normal subgroup：aH=Ha  for all a in G；如果是**Abelian group**，则它的所有subgroup都是normal的
- 如果存在(G,R)，且R是congruence relation，令H=[e]，则这个H是normal group；这里的证明主要运用了aH=[a]=Ha的证明，其中关键是$$[a]=[b]\rightarrow [e]=[a]^{-1}[b]=[a^{-1}b]$$
- 令N作normal subgroup，a R b作 $$a^{-1}b\in N$$，则可以推出
  - R is a congruence relation on G
  - N=[e]
- ker：如果有$$f:S\rightarrow T$$是homomorphism，则$$ker(f)=\{a\in G \| f(a)=e' \}$$就是S的正规子群，

### 9-6 Group Code

- encoding function：$$e:B^m \rightarrow B^n,m<n$$；并且把e(b)=x称作代表b的**code word**
- 在$$x\rightarrow x_t$$的过程中，如果出现了小于等于k个错误，可以立刻发现$$x_t$$不是code word，就说明 方程e可以**detects k or fewer errows**；换言之，大于k个错误的时候有可能发现不了
- Haming Distance：$$\delta(x,y)= |x \oplus y|$$ ，求x和y有几个不同

  - 可以发现$$\delta(x,y) \leq \delta(x,z)+\delta(z,y)$$
- **minimum distance** of an encoding function：$$min\{\delta(e(x),e(y)|x,y\in B^m\}$$，编码后的最小差异
- minimum distance 是k+1时，等价于方程 e 可以检测 k or fewer errors：如果传输出现了k+1个错误，则有可能传输完以后虽然错了，但是发生和别的code word 长得一样的情况，无法被检测出来
- **group code**：令编码后的$$(B^n,\oplus)$$作为一个群，则有

  - **code word 的集合N是它的subgroup**，于是满足 identity，inverse，**closure**
  - 并且由于$$\oplus$$是community的，所以$$B^n$$是一个Abelian group，它的所有子群都是**normal subgroup**
  - 于是根据群的性质，$$\delta(x,y)=\eta,\eta$$指N中**minimum weight of nonzero code word **,注意只有在group code中才满足这个性质
- 定义 mod-2 boolean product D * E，就是矩阵乘法，同时将展开式中的加法换成**异或运算**，乘法换成**与预算**；同时矩阵间还有 mod-2 sum $$D\oplus E$$，结果是同一位置上的元素进行疑惑运算；两种矩阵运算满足乘法分配律
- 由上述定义的二元操作可以定义函数$$f_H:B^n \rightarrow B^r,\ f_H(x)=x*H_{n \times r}$$，并且可以证明这是一个homomorphism；于是，对于这个函数的$$kernel(f_H)={x\in B^n|x*H=\overline 0\}=N$$,是 Bn的正规子群；特别的，令r=n-m的时候，H就成为 parity check matrix，可以利用它进行编码，校验位长度为r
- H 的两部分在不同的过程中组合方式不同：在**编码**的时候$$e_H=b_{1\times m}*H_{m\times n},\ H_{m\times n}=E_{m\times m}\&H_{m\times r}$$；在**校验**的时候，如果满足$$x_{1\times n}*H_{n\times r}=\overline 0\ H_{n\times r}={H_{m\times r}\over E_{r\times r}}$$说明传输过来的x属于noraml subgroup的一员，也就是code word的一员，没有传输错误
- 对于同一个H得到的编码和译码组合(e,d)，在k个或以下传输错误出现的时候，他们可以**correct k or fewer errors**
- **maximum likelihood technique**：选择和传输过来的码串 最相似的code word，再选对应的b

  - (e,d) 可以correct k or fewer errors 的条件是 **minimum distance of e is at least 2k+1**；就是出现了k个错误的时候，如果码字之间的差异大于这个的话，才能判断传输过来的串和哪个码字更加接近；奇数个是可以为了防止偶数个刚好跟两个的hamming distance都相等
- 对于每个$$x_t$$，都存在用它和N得到的coset，$$x_t \oplus N=\{\epsilon_1,\epsilon_2...,\epsilon_{2^m}\}$$，这些元素的weight代表接收码串和code word的距离，其中weight最小的元素称为**coset leader**；在这个过程中假设coset leader 就是$$\epsilon_j$$，那么接收码纠错后的结果就是码字$$x^{(j)}$$,同时我们有对应的计算关系$$x^{(j)}=x_t \oplus \epsilon_j$$；容易证明对于finite subgroup K，所有coset aK的大小相等
- 综上，用极大似然的decoding过程应如下
  1. 求出N的所有left coset
  2. 确定所有的left coset的leader
  3. 在 2^r个coset中找到$$x_t$$所属的行
  4. 用leader计算codeword  $$x=x_t \oplus \epsilon$$
- 构建decoding table的时候，如果中间计算出现了相同的，就肯定错了；选用的coset leader不同，会导致那一行的次序不同，解码的结果也不同，但是coset的元素是不变的
- 由fundamental 得到 $$B^r \cong B^n/N$$，规定$$f_H=x*H$$得到的长度为r的串是**syndrome**，由于这个isomorphism，可以知道所有同一个N的left coset中的元素有相同的syndrome（类似共有一个coset leader）
- 于是利用syndrome，再次简化解码的过程：
  1. 求出所有N的left coset
  2. 求出所有的coset leader，然后用它或者coset中的随便一个元素作$$f_H=x*H$$，求出syndrome
  3. 当接收到$$x_t$$的时候，通过计算syndrome找到归属的行（原来的话要全图找），同时确定了leader
  4. 利用$$x=x_t \oplus \epsilon$$和$$e_H$$的对应关系，找到b




# Chapter 10 Graph

### 10-1 graph and models

- simple graph : 没有loop 和multiple edge，两个都有的叫pseudo graph
- directed graph：可以有loop，不能有multiple edge（因为是function）

### 10-2 terminology

- adjacent：存在一条边(u,v)则他们adjacent
- N(v)=neighborhood of v：所有和顶点v相邻的点的集合
- deg(v)
  - undirected graph：与该点所有的相关边，**loop计算两次**；另外deg(v)=1时，称为**pendant**
  - directed graph：分为 in-degree=$$deg^-(v)$$ 和out-degree=$$deg^+(v)$$
  - 对于一个顶点来说，有向和无向的时候的度数是相同的
- Handshaking Theorem：
  - 无向图中，$$2|E|=\Sigma_{v\in V}deg(v)$$；同时可以推出deg为奇数的顶点的个数一定是偶数
  - 有向图中，$$|E|={1\over 2 }\Sigma_{v\in V}deg(v)=\Sigma_{v\in V}deg^-(v)=\Sigma_{v\in V}deg^+(v)$$
- 应用：判断一个度序列 degree sequence 是否**graphic**，可以数是不是有偶数个奇数度
- special graph structures
  - complete graphs $$K_n$$
  - cycles $$C_n$$
  - wheels $$W_n$$，n-环中间加一点
  - n-cubes $$Q_n$$，Q3是立方体，构造方法是上一层的点一一对应，得到两倍的顶点
  - **complete bipartite graph** $$K_{m,n}$$：有m+n个点，m*n条边，所有的点都能到另一个集合的任意点
- bipartite：用（V1,V2）标记，将simple graph 分为两个集合，集合内的点互不相邻，所有的边的两端都分别属于V1和V2；可以用着色来理解，一共涂两种颜色，所有相邻的点的颜色都不同
- matching：bipartite中的一个边的集合M，其中这些边的顶点都不相同；没有在matching中的点称作unmatched；**maximum matching**指该集合包含了能包含的最多的边；**complete matching from V1 to V2**指的是|M|=|V1|
- hall's marriage theorem: $$(V1,V2)$$has complete matching from V1 to V2 $$\leftrightarrow |N(A)|\geq |A|$$，for all subsets A of V1，其实蛮好理解，就是要把V1的点分配完，那么它的相邻的点或者说它引出去的边的数量肯定要多于它本身的顶点数
- **subgraph**：如果H=(W,F)是G=(V,E)的subgraph，那么它的点集和边集都是它的子集，两者不等时称作proper；通过某个点集 induce 出来的subgraph 保留这个点集里面的点以及可以形成的边
- edge contraction ：通过合并点来构造新的图；谜一样的东西，应该没有考点

### 10-3 Representing Graphs

- ​

# Chapter 8 Advanced Counting Techniques 

### 8-1

### 8-2

### 8-3 Divide and Conquer

- 由recurrence$$f(n)=af(n/b)+c$$ ，可以推出$$f(n)=a^kf(1)+\sum_{j=0}^{j=k-1} a^jg(n/{b^j})$$，这个要记
- 当g(n)=c为常数的时候，我们可以得到 f(n)的时间复杂度
  - $$a>1 \rightarrow O(n^{log_ba})$$
  - $$a=1 \rightarrow O(logn)$$
  - 代入记忆的式子里面的时候，可以得到f(n)关于n的表达式
- **Master Theorem**，上一个式子的推广，此时$$g(n)=cn^d$$，则有 f(n)的时间复杂度
  - $$ a<b^d \rightarrow O(n^d)$$
  - $$ a=b^d \rightarrow O(n^dlogn)$$
  - $$a>b^d \rightarrow O(n^{log_ba})$$


