## 简介[^1]

- 树状数组要解决的问题
  
  > 前缀和$O(\log n)$ + 单点更新$O (\log n)$
  >
  > 利用差分数组，则可以解决区间更新和单点查询[^2]
  
- <details><summary>符号说明</summary>

  > **规定数组索引从 1 开始**
  >
  > $A$：原始数组
  >
  > $C$：处理后的数组
  >
  > $i$：$C$ 的索引
  >
  > $j$：$A$ 的索引
  >
  > $k$：$i$ 的二进制表示下从右向左第一个 $1$ 之前 $0$ 的个数
  >
  > - $C[i] = \sum \limits_{t = 0}^{2^k - 1} A[i - t]$ 
  > - $2^k = i \text{&} (-i) \triangleq \text{lowbit}(i)$</details>

- 关键性质
  
  - $\text{parent}(i) = i + \text{lowbit}(i)$



## 模板

### python

```python
class FrenwickTree:
    
    def __init__(self, n):
        self._size = n
        self._tr = [0 for _ in range(n + 1)]
        
    @staticmethod 
    def _lowbit(i):
        return i & -i
        
    def update(self, x, idx):
        while idx <= self._size:
            self._tr[idx] += x
            idx += self._lowbit(idx)
            
    def query(self, idx):
        ans = 0
        while idx > 0:
            ans += self._tr[idx]
            idx -= self._lowbit(idx)
            
        return ans
```



## PAT 1057

- 思路

  - 用一个树状数组来记录各个元素出现的个数
    - `Push x` $\implies$ `update(x, 1)`
    - `Pop x` $\implies$ `update(x, -1)`

  - 如何找到中间的元素
    - 使用二分查找法，找到恰好满足前缀和为 `k` 的数组索引


## 计算右侧小于当前元素的个数[^3]

- 离散化 + 树状数组
- 用该方法可以求解逆序对的数量[^4]



## refs

[^1]: [树状数组学习笔记](https://www.acwing.com/blog/content/80/)
[^2]: [一个简单的整数问题](https://www.acwing.com/problem/content/248/)
[^3]: [计算右侧小于当前元素的个数](https://leetcode-cn.com/problems/count-of-smaller-numbers-after-self/)
[^4]: [数组中的逆序对](https://www.acwing.com/problem/content/61/)

