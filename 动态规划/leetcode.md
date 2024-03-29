### 1235. 规划兼职工作

> 有 $n$ 份兼职工作，每份工作预计从 `S[i]` 开始到 `E[i]` 结束，报酬为 `P[i]`，且时间上出现重叠的工作不能同时进行，求可以获得的最大报酬

- 此题与普通的任务安排问题的区别在于对每个工作多了一个权重(报酬)

- 分析
  
  $$
  \begin{cases}
状态表示:  f[i][0..1] 
\begin{cases}
集合: 只考虑前 i 个任务所能获得的利润 \\
属性: max
\end{cases}
\\
状态计算:
\begin{cases}
划分: 第 i 个任务选(f[i][1])或者不选(f[i][0]) \\
\begin{cases}
f[i][0] = max(f[i - 1][1], f[i - 1][0]) \\
f[i][1] = max(f[j + 1][0], f[j][1]) + P[i], \; 其中 E[j] \le S[i] < E[j + 1]
\end{cases}
\end{cases}
\end{cases}
  $$
  
  - 显然可以将二维优化成一维

### 790. 多米诺和托米诺平铺

> 有两张形状的诺瓷砖，一种是 $2 \times 1$ 的多米诺型，另一种是形如 "L" 的托米诺型，两种形状都可以旋转，给定整数 $n$，返回可以平铺 $2 \times n$ 的面板的方法的数量
> 
> <img src="https://assets.leetcode.com/uploads/2021/07/15/lc-domino.jpg" title="" alt="" data-align="center">

- 本题是典型的状态机 DP + 状态压缩 DP 问题

- 分析
  
  $$
  \begin{cases}
状态表示: f[i][0..3] 
\begin{cases}
集合: 前 i - 1 行已经摆好，且从第 i - 1 列伸到第 i 列的状态为 j 的集合 
\begin{cases}
00 \rightarrow 第 i 列均为空 \\
01 \rightarrow 上面为空, 下面铺有瓷砖 \\
10 \rightarrow 上面铺有瓷砖，下面为空 \\
11 \rightarrow 上下均铺有瓷砖
\end{cases}
\\
属性: 数量
\end{cases}
\\
状态计算: 
\begin{cases}
划分: 第 i - 1 列的状态 \\
\begin{cases}
f[i][0] = f[i - 1][3] \\
f[i][1] = f[i - 1][0] + f[i - 1][2] \\
f[i][2] = f[i - 1][0] + f[i - 1][1] \\ 
f[i][3] = \sum
\begin{cases}
f[i - 1][0], \quad 两个横着的 Domino \\
f[i - 1][1] \\
f[i - 1][2] \\
f[i - 1][3]
\end{cases}
\end{cases}
\end{cases}
\end{cases}
  $$

### 分汤

> 有 **A 和 B 两种类型** 的汤，一开始每种类型的汤有 `n` 毫升，有四种分配操作：
> 
> 1. 提供 `100ml` 的 **汤A** 和 `0ml` 的 **汤B**
> 
> 2. 提供 `75ml` 的 **汤A** 和 `25ml` 的 **汤B**
> 
> 3. 提供 `50ml` 的 **汤A** 和 `50ml` 的 **汤B**
> 
> 4. 提供 `25ml` 的 **汤A** 和 `75ml` 的 **汤B**
> 
> 当我们把汤分配给某人之后，汤会减少相应的份额(被某人喝掉)，每个回合，等概率($P = 0.25$) 执行上述分配操作，如果汤的剩余量不足以完成相应的操作，则会尽可能分配(分配不足的份额)，当两种类型的汤都分配完时，停止操作
> 
> 求：**汤A** 先分配完的概率 + **汤A和汤B** 同时分配完的概率 / 2

- 分析
  
  - 记 **汤A** 剩余 $x$，**汤B** 剩余 $y$ 时所求的概率为 $f(x, y)$
  
  - 则 $f(x, y) = \frac{1}{4} (f(x - 100, 0) + f(x - 75, y - 25) + f(x - 50, y - 50) + f(x - 25, y - 75))$
    
    > 过于巧妙了

- 我们需要考虑边界情况如下
  
  $$
  f(x, y) = 
\begin{cases}
1, & \quad x = 0, y > 0 \\
0.5, & \quad x = 0, y = 0 \\
0, & \quad x > 0, y = 0 
\end{cases}
  $$

- 由于上述四种操作提供的汤均为 25 的倍数，因此我们进行可以将四种操作简化为
  
  1. $n = ceil(n / 25)$
  
  2. 上述四种操作均 / 25
