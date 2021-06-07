```mermaid
graph LR
	style F fill: #F0F8FF, stroke-width:2px, color:red;
	style G fill: #F0F8FF, stroke-width:2px, color:red;
	style H fill: #F0F8FF, stroke-width:2px, color:red;

	A((动态规划)) --> B(状态表示): 12
	A --> C(状态计算)
	B --> D[集合]
	B --> E[属性]
	E --> F[[max]]
	E --> G[[min]]
	E --> H[[count]]
```

## 如何解决动态规划问题[^1]

### 核心思想

- **==从集合的角度考虑问题==**

### 状态表示

$$
dp[i_1, ... i_k] \triangleq s
$$



- 集合
  - 状态 $s$ 代表什么样的集合
- 属性
  - $s$ 中的数与集合的关系
  - 通常有表示极值或者数量
    - 如果表示极值，则在计算的时候可以重复，但不能遗漏
    - 如果表示数量，则必须不重不漏

### 状态计算

- 将状态 $s$ 代表的集合根据**新增的不同点**进行划分，**每个**被划分的子集为之前的某一个状态 $s'$ 所代表的集合，或者可以根据 $s'$ 计算而来
  - 例如01背包问题中即为第 $i$ 个物品选或者不选



## 常见模型

### 背包问题

#### 01背包问题

> 有 $N$ 件物品和一个容量是 $V$ 的背包。每件物品只能使用一次。第 $i$ 件物品的体积是 $v_i$，价值是 $w_i$。求在不超过背包容量的情况下能够获得的最大价值

- 闫式DP分析法
  $$
  \begin{cases}
  状态表示: f[i, j]
  \begin{cases} 集合: 只考虑前 i 个物品,且背包容量不超过 j 的方案,  \\ 
  			  属性: max 
  \end{cases} \\
  状态计算:
  \begin{cases}
  划分: 第 i 个物品选或者不选 \\
  f[i, j] = max(f[i - 1, j], f[i - 1, j - v_i] + w_i)
  \end{cases}
  \end{cases}
  $$

#### 完全背包问题

> 有 $N$ 件物品和一个容量是 $V$ 的背包。==每件物品都有无限件可用==。求在不超过背包容量的情况下能够获得的最大价值

- 闫式DP分析法
  $$
  \begin{cases}
  状态表示: f[i, j] 
  \begin{cases}
  集合: 只考虑前 i 个物品, 且背包容量不超过 j 的方案 \\
  属性: max 
  \end{cases} \\
  状态计算: 
  \begin{cases}
  划分: 第 i 个物品选 0-k 次 \\
  f[i, j] = max(f[i - 1, j - kv_i] + kw_i) = max(f[i - 1, j], f[i, j - v_i] + w_i)
  \end{cases}
  \end{cases}
  $$

#### 多重背包问题

> 有 $N$ 件物品和一个容量是 $V$ 的背包。==第 $i$ 件物品最多有 $s_i$ 件==。求在不超过背包容量的情况下能够获得的最大价值

- 当数据量较小时可以直接使用完全背包问题的思路
  - 第 $i$ 个物品最多可以选择的次数 $k = min(s_i, floor(j / v_i))$
- 当数据量较大时可以使用**二进制优化**[^2]将其转化为等效的01背包问题

#### 分组背包问题

> 有 $N$ 件物品和一个容量是 $V$ 的背包。==每组物品有若干个，同一组内的物品最多只能选一个==。每件物品的体积是 $v_{ij}$，价值是 $w_{ij}$，其中 $i$ 是组号，$j$ 是组内编号。求在不超过背包容量的情况下能够获得的最大价值

- 闫式DP分析法
  $$
  \begin{cases}
  状态表示: f[i, j] 
  \begin {cases}
  集合: 只考虑前 i 组物品, 且背包容量不超过 j 的方案 \\
  属性: max
  \end{cases} \\
  状态计算: 
  \begin{cases}
  划分: 第 i 组物品不选或者选择第 k 个 \\
  f[i, j] = max(f[i - 1, j], max(f[i - 1, j - v_{ik}] + w_{ik}))
  \end{cases}
  \end{cases}
  $$



### 线性DP

#### 最长上升子序列

> 给定一个长度为 $N$ 的数列，求数值严格单调递增的子序列的长度最长是多少

- 朴素版本闫式DP分析法
  $$
  \begin{cases}
  状态表示: f[i]
  \begin{cases}
  集合: 数组中前 i 个数并且以第 i 个数结尾的子序列 \\
  属性: max
  \end{cases} \\ 
  状态计算: 
  \begin{cases}
  划分: 子序列的倒数第二个数是数组中的第 j 个数(j \in [0, i - 1], j = 0 表示子序列长度为1) \\
  f[i] = max(f[j]) + 1
  \end{cases}
  \end{cases}
  $$

- 优化版本本质上更像贪心[^3]
  - $dp[i]$：所有长度为 $i$ 的上升子序列中**末尾**元素的**最小值**

#### 最长公共子序列

> 给定两个长度分别为 $N$ 和 $M$ 的字符串 $A$ 和 $B$，求既是 $A$ 的子序列又是 $B$ 的子序列的字符串长度最长是多少

- 闫式DP分析法
  $$
  \begin{cases}
  状态表示: f[i, j]
  \begin{cases}
  集合: 字符串 A 的前 i 个字符和字符串 B 的前 j 个字符所有公共子序列的长度 \\
  属性: max
  \end{cases} \\
  状态计算: 
  \begin{cases}
  划分: A[i] 和 B[j] 是否相等 \\
  \begin{cases}
  f[i, j] = f[i - 1][j - 1] + 1, & if (A[i] = B[j]) \\
  f[i, j] = max(f[i - 1][j], f[i][j - 1]) & if(A[i] \ne B[j]) 
  \end{cases}
  \end{cases}
  \end{cases}
  $$

#### 最短编辑距离

> 给定两个字符串 $A$ 和 $B$，现在要将 $A$ 经过若干操作变为 $B$，可进行的操作有
>
> 1. 删除：将字符串 $A$ 中的某个字符删除
> 2. 插入：在字符串 $A$ 的某个位置插入某个字符
> 3. 替换：将字符串 $A$ 中的某个字符替换为另一个字符
>
> 求将 $A$ 变为 $B$ 至少需要进行多少次操作

- 闫式DP分析法
  $$
  \begin{cases}
  状态表示: f[i, j]
  \begin{cases}
  集合: 将 A 的前 i 个字符变为 B 的前 j 个字符需要操作的次数 \\
  属性: min
  \end{cases} \\
  状态计算: 
  \begin{cases}
  划分: A[i] 和 B[j] 是否相等, 如果不相等，则执行三种操作 \\
  \begin{cases}
  f[i, j] = f[i - 1, j - 1] & if (A[i] = B[j]) \\
  f[i, j] = min(f[i - 1, j - 1], f[i - 1, j], f[i, j - 1]) + 1 & if (A[i] != B[j])
  \end{cases}
  \end{cases}
  \end{cases}
  $$

### 区间DP

- 区间合并问题循环中通常先**枚举区间长度**，再**枚举左端点起始位置**

#### 石子合并

> 设有 $N$ 堆石子拍成一排，其编号为 $1, 2, \dots, N$。每堆石子有一定的质量，可以用一个整数来描述，现在要将这 $N$ 堆石子合并成为一堆。
>
> 每次只能合并相邻的两堆，合并的代价为这两堆石子的质量之和，合并后与这两堆石子相邻的石子将和新堆相邻，合并时由于选择的顺序不同，合并的总代价也不相同。
>
> 找出一种合理的方法，使总代价最小，输出最小代价

- 闫式DP分析法
  $$
  \begin{cases}
  状态表示: f[i, j] 
  \begin{cases}
  集合: 长度为 i 且左端点 j 的所有合并方法的代价 \\
  属性: min
  \end{cases} \\
  状态计算:
  \begin{cases}
  划分: 由 [l, k] 和 (k, r] 两堆石子合并而来(r = l + i - 1) \\
  f[i, j] = min(f[l][k] + f[k + 1][r]) + \sum_{t = l}^r w_t & (k \in [l, r), w_t 为第 t 堆石子的重量)
  \end{cases}
  \end{cases}
  $$

#### 环形石子合并

> 石子排列的方式不是一排而是环绕摆放

- 将环形展平成一排即可

  > 例如原来一堆石子的质量为 $weights[1 : n + 1]$，则新的石子用 $weights[1 : 2 \times n + 1]$ 来表示，且 $weights[n + 1 : 2 \times n + 1] = weights[1 : n + 1]$

### 计数类DP

#### 整数划分

> 一个正整数可以表示成若干个正整数之和，形如 $n = \sum_{i = 1}^k n_i$，其中$n_1 \ge n_2 \ge \cdots \ge n_k, k \ge 1$。
>
> 我们将这样的一种表示称为正整数 $n$ 的一种划分
>
> 给定一个正整数 $n$，求 $n$ 共有多少种不同的划分方法

- 本题可看作**==完全背包问题==**的变形

  > 将 $1, 2, \cdots, n$ 看作 $n$ 个物品的体积

- 闫式DP分析法
  $$
  \begin{cases}
  状态表示: f[i, j]
  \begin{cases}
  集合: 只考虑 1-i, 且总和不超过 j 的方案树 \\
  属性: count
  \end{cases} \\
  状态计算: 
  \begin{cases}
  划分: 第 i 个数选 0 - k 次 \\ 
  f[i, j] = \sum_{t = 0}^k f[i - 1, j - ti] = f[i - 1, j] + f[i, j - i]
  \end{cases}
  \end{cases}
  $$

### 数位统计DP

- <font color="red">**暂略，有点难**</font>

### 状态压缩DP

- 解决状态压缩DP问题的基本思路
  - 预处理合法的状态
  - 状态转移

#### 蒙德里安的梦想

> 求把 $N \times M$ 的棋盘分割成若干个 $1 \times 2$ 的长方形，有多少种方案

- 只需要考虑所有竖着的 $1 \times 2$ 长方形的摆放方法数

- 闫式DP分析法
  $$
  \begin{cases}
  状态表示: f[i, j]
  \begin{cases}
  集合: 前 i - 1 行已经摆好, 且伸出到第 i 行状态为 j 的方案 \\
  属性: count
  \end{cases} \\
  状态计算: 
  \begin{cases}
  划分: 所有能从 f[i - 1, k] 合法转移到 f[i, j] 的状态 \\
  f[i, j] = \sum\limits_{k} f[i - 1, k], \quad s.t. \; (j \& k = 0 \; and \; is\_valid(j | k) 
  \end{cases}
  \end{cases}
  $$

#### 最短 Hamilton 路径

> 给定一张 $n$ 个点的带权无向图，点从 $0 \backsim n - 1$ 标号，求起点 $0$ 到终点 $n - 1$ 的最短 Hamilton 路径。
>
> Hamilton 路径的定义是从 $0 \backsim n - 1$ 不重不漏的经过每个点恰好一次

- 用二进制数 $i$ 表示已经走过的路径(某个点走过其对应的二进制为 $1$)

- 闫式DP分析法
  $$
  \begin{cases}
  状态表示: f[i, j]
  \begin{cases}
  集合: 从 0 走到 j 且路径为 i 的所有距离 \\
  属性: min
  \end{cases} \\
  状态计算: 
  \begin{cases}
  划分: 所有能从 f[i \texttt{^} (1 \texttt{<<} j), k] 转移到 f[i, j] 的状态 \\
  f[i, j] = \min(f[i \texttt{^} (1 \texttt{<<} j), k] + w[k, j]), \quad s.t. \;(i \texttt{>>} j \texttt{&} 1 \; and \; i \texttt{^} (1 \texttt{<<} j) \texttt{>>} k \texttt{&} 1) 
  \end{cases}
  \end{cases}
  $$

#### 小国王

> 在 $n \times n$ 的棋盘上放 $k$ 个国王，国王可攻击相邻的 $8$ 个格子，求是它们无法互相攻击的方案总数

- 闫式DP分析法
  $$
  \begin{cases}
  状态表示: f[i, j, s]
  \begin{cases}
  集合: 前 i 行已经放置 j 个国王, 且第 i 行的状态为 s 的方案 \\
  属性: count
  \end{cases} \\
  状态计算:
  \begin{cases}
  划分: 所有能从 f[i - 1, j - cnt[s], s'] 转移到 f[i, j, s] 的方案 \\
  f[i, j, s] = \sum\ f[i - 1, j - cnt[s], s'], \; 其中 cnt[s] 表示状态 s 二进制表示中 1 的个数, s' 能合法转移到 s 
  \end{cases}
  \end{cases}
  $$

### 树形DP

#### 没有上司的舞会

> Ural 大学有 $N$ 名职员，编号为 $1 \backsim N$。
>
> 他们的关系就像一棵以校长为根的树，父节点就是子节点的直接上司。
>
> 每个职员有一个快乐指数，用整数 $H_i$ 给出，其中 $1 \le i \le N$。
>
> 现在要召开一场周年庆宴会，不过，没有职员愿意和直接上司一起参会。
>
> 在满足这个条件的前提下，主办方希望邀请一部分职员参会，使得所有参会职员的快乐指数总和最大，求这个最大值 

- 闫式DP分析法
  $$
  \begin{cases}
  状态表示: f[i, j]
  \begin{cases}
  集合: 以节点 i 为根节点的子树在状态 j(0 代表不选 i, 1 代表选 i)下的所有快乐指数 \\
  属性: \max
  \end{cases} \\
  状态计算: 
  \begin{cases}
  划分: j = 0 \; or \; 1 \\
  \begin{cases}
  f[i, 0] = \sum\limits_{c \in i.children} \max(f[c, 0], f[c, 1]) \\
  f[i, 1] = \sum\limits_{c \in i.children} f[c, 0]
  \end{cases}
  \end{cases}
  \end{cases}
  $$

#### 树的最长路径

> 给定一棵树，树中包含 $n$ 个节点，编号 $1 \backsim n$ 和 $n - 1$ 条无向边，每条边都有一个权值。
>
> 请找到一条路径，使得路径两端点的距离最短

- 本体的关键在于
  - **经过某一个点且不经过其父节点的最长距离为以其为根节点的树的最长深度和第二长深度之和**
  - **树的直径即以任一个点为根节点的树最长深度和次长深度之和**
- 在 `dfs(u, fa)` 中用父节点 `fa` 来控制不走回头路

#### 数字转换

> 如果一个数 $x$ 的约数(不包括其本身)之和为 $y$ 比他小，那么 $x$ 可以变成 $y$，$y$ 也可以变成 $x$
>
> 例如 $4$ 可以变成 $3$，$1$ 可以变成 $7$
>
> 限定所有数字变换在不超过 $n$ 的正整数范围内进行，求不断进行数字变换且不出现重复数字的最多变换步数

- 若将变换看成一条无向边，此题即变成求树的直径



## refs

[^1]: [闫式DP分析法](https://www.cnblogs.com/IzayoiMiku/p/13635809.html)
[^2]: [多重背包问题$\rm{II}$](https://www.acwing.com/solution/content/5527/)
[^3]: [最长上升子序列$\rm{II}$](https://www.acwing.com/solution/content/3783/)

