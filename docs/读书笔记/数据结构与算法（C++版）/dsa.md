# 原理

**主定理**

$n=b^k$, $k$ and $b$ is integer, $c, k > 0$, $b > 1$, $a \ge 1$, $d \ge 0$.

$$
f(n) = af(n/b)+cn^d
$$

Compare $a$ and $b^d$.

- less: $O(n^d)$.
- equal: $O(n^d \log n)$.
- greater: $O(n^{\log_b a})$


**Akra-Bazzi方法**

$$
T(n) = \sum_{i = 1}^k a_iT(b_i n) + f(n)
$$

$p$满足$\sum_{i=1}^k a_ib_i^p = 1$，则：

$$
T(n) = \Theta\left(n^p\left(1 + \int_1^n \frac{f(u)}{u^{p+1}}\mathrm{d}u\right)\right)
$$

**数学结论**

- $x(g, h)$为$g$和$h$线性组合出的最大自然数，$x(g,h) = (g - 1)(h - 1)$
- $\ln n = \ln 2 \log_2n$，$\phi^{\lg n}=n^{\lg\phi}$
- $\omega(2^n)=n!=o(n^n)$；$\lg n! = \Theta(n\lg n)$
- Fibonacci数：$F_i = \frac{\phi^i - \hat{\phi}^i}{\sqrt{5}}=\left\lfloor\frac{\phi^i}{\sqrt{5}}+\frac{1}{2}\right\rfloor$；$\phi,\hat{\phi}$为$x^2=x+1$​的共轭双根。
- Catalan数：$Catalan_n=\sum\limits_{i=1}^{n-1}Catalan_{i}\cdot Catalan_{n-i}=\frac{1}{n-1}C_{2n}^{n}$​。​
- $\sum\limits_{i = 1}^n \frac{1}{i} = \ln n + \gamma + \Theta\left(\frac{1}{2n}\right)$ 。

## 概念

- 栈
  - 逆序输出
  - 递归嵌套
    - $n$ 个数进行栈混洗，共有 $Catalan_n$ 种可能。
    - 合法嵌套和相应长度的栈混洗一一对应。
  - 延迟缓冲
    - 表达式求值，逆波兰式。
  - 试探回溯法
  
- 树
  - 单节点的树高为 $0$。
  - 高为 $h$​ 的满二叉树节点数量为 $2^{h+1} -1$​ 。
  - 二叉树度为$2$的节点数量比叶节点数量少 $1$ ，完全二叉树叶节点数量比内部节点数量多 $1$ 或相等。
  
- 图
    - 欧拉环路：各顶点一次；哈密顿环路：各边一次。
    - BFS树每条边深度关系
        - 有向图边$(v, u)$：$depth(v) \le depth(u) + 1$，取等时为树边。
        - 无向图差值为$1$。
    - DFS树，后向边，前向边，跨边，$v$为$u$的祖先即`dtime[v] < dtime[u] < ftime[u] < ftime[v]`。
    - 关节点
        - 根节点：有无分支
        - 内部节点：有无高于父节点的后向边
        - 叶节点：无
    
- BST
    - 删除，单分支，无分支直接删；双分支，寻找后继交换后删
    - 高为$h$​的AVL的至少包含$F_{h+3}-1$​​个节点
    
- 伸展树
    - 每个节点 $v$ 使用势能函数 $lg |v|$​，$|v|$为节点后代数目。
    - 每步调整所需时间 $A=T_i + \Delta\phi_i\le 3[\phi'(v)-\phi(v)]$。
    - 总体分摊时间 $A\le 1+3[\phi(r)-\phi(v)]$。
    
- B-树
    - 高为 $h$​ 的 B-树包括外部节点。
    - $m$​​ 阶B-树除根节点对应分支数为 $\left[\lceil m/2\rceil,m\right]$​​ ，外部节点数对应失败查找的数量，比内部关键码数量多 $1$​ 。
    -  $m$ 阶B-树满足 $\log_m(N+1) \le h \le \log_{\lceil m/2\rceil}((N+1)/2)+1$​​。
    
- 红黑树
    -  对应的 $(2,4)$ -树 $T_B$ 高为 $H$。
    -  $\lg (n+1) \le h \le 2H \le 2\lg(n+1)$​​​ 。
    
- 跳转表
    - 表的高度 $Pr(h < k)=1-n/2^k,E(h)=O(\lg n)$​​​ 。
    - 每层横向跳转 $k$​​ 个塔顶，$1$​​ 个非塔顶，跳转次数 $Pr(Y=k)=(1-p)^k p$​​​​ 。
    
- 散列表
    - 长度为 $M$​ ，装填因子为 $\lambda$​ 。
    - 模余法间隔为 $T$ 的 $M$ 个关键码插入到散列表，$g=gcd(M,T)$，每个关键码约与 $g$ 个关键码冲突。
    - $M$​ 为素数且$\lambda \le 50\%$​，平方试探将终止于某个空桶。​
    
- 左式堆
    - $npl(x)=npl(rc(x))+1$​。
    
- KMP

    - $N(P,j)=\left\{ 0\le t<j|P[0,t)=P[j-t,j)\right\}$ 且 $P[t]\neq P[j])$​，$next[j]=max(N(P,j))$​。

    - 令 $t=next[j]$，则
        $$
        next[j+1]=\begin{cases}
        P[j+1]=P[t+1]?next[t+1]:t+1 &,P[j]=P[t]\\
        next[t]+1,next[next[t]]+1,\cdots &,others
        \end{cases}
        $$
    
- BM

    - $m$ 为 $P$ 的长度，$ss[j]=max\left\{ 0\le s<j|P(j-s,j]=P[m-s,m)\right\}$​​​ 。
    
    - 令 $(lo,hi]$ 为极长匹配后缀，则
      $$
      ss[j]=\begin{cases}
      ss[m-1-hi+j]&,j-lo\le ss[m-1-hi+j]\\
      updated(hi)-updated(lo)&, others
      \end{cases}
      $$
      
      $$
      \begin{cases}
      \forall i<m-j-1, gs[i]=m-j-1&,ss[i]=j+1\\
      gs[m-ss[j]-1]=m-j-1 &,others
      \end{cases}
      $$
    
- 排序
    - 向量 $S$ 已经 $(g,h)$ 有序，且 $g,h$ 属于 $O(d)$ 数量级，则使用插入算法进行 $d$-排序的时间复杂的为 $O(dn)$。

**时间复杂度**

- 平均运行时间
    - 基数排序：$O(t(m+n))$​
    - 快速排序： $T(n) = n + 1 + \frac{1}{n}\sum\limits_{i = 1}^{n}T(i - 1) + T(n - i)$
    - k-选取算法：$T(n) = cn + T(n/Q) + T(3n/4)$​

