## bfs

- [概念](https://zh.wikipedia.org/wiki/%E5%B9%BF%E5%BA%A6%E4%BC%98%E5%85%88%E6%90%9C%E7%B4%A2)
- 在对矩阵进行广度优先搜索的时候可以用**方位数组+for**代替多个if判断
  - [例子](https://www.liuchuo.net/archives/2307)





### [PAT 1091](https://www.liuchuo.net/archives/2307)

- 题目主要难在不太好读懂
  - 有 `l` 个切片，每个切片的大小为 `m * n`，题目要求计算所有联通的 1 的个数
    - 联通的定义：前后左右上下六个方位
    - 联通的个数小于阈值 `t` 时不计入总联通个数



### 多源BFS

#### 矩阵距离[^1]

- 初始时**将所有 $A[i, j] = 1$ 的点放入队列**

- 等价于**新建一个指向所有 $A[i, j] = 1$ 的虚拟源点**，即转化为单源最短路径



### 最小步数模型

#### 魔板[^2]

- 可以用字符串来表示一种状态
- 要注意顺序是逆时针(有点坑)



## 双向 BFS





## refs

[^1]: [矩阵距离](https://www.acwing.com/problem/content/175/)
[^2]: [魔板](https://www.acwing.com/problem/content/1109/)