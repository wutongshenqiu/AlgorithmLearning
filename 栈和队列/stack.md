## Leetcode

### 括号的分数

> 给定一个平衡括号字符串(只包含括号且括号平衡的字符串) `S`，按下述规则计算字符串的分数
> 
> - `()` 得 1 分
> 
> - `AB` 得 `A + B` 分，其中 `A` 和 `B` 是平衡括号字符串
> 
> - `(A)` 得 `2A` 分，其中 `A` 是平衡括号字符串

- 在遍历字符串 `S` 的过程中
  
  - 遇见左括号
    
    - 需要计算该左括号对应的平衡字符串的分数，首先将 0 入栈中
  
  - 遇见右括号
    
    - 说明右括号对应的平衡字符串分数已经算完(即栈顶的分数)
    
    - 若栈顶分数为 0，说明是 `()`，将栈顶分数 + 1，否则将栈顶分数 x 2
    
    - pop 栈顶分数，加到下一个栈顶分数上

### 使用机器人打印字典序最小的字符串

> 给定一个字符串 `s` 和空字符串 `t`，每次可以执行以下两种操作之一
> 
> - 删除字符串 `s` 的**第一个**字符，并将该字符串添加到 `t` 的尾部
> - 删除字符串 `t` 的**最后一个**字符，并将该字符写到纸上
> 
> 请找出纸上能够写出的字段序最小的字符串

- 容易发现两个操作相当于 入栈+出栈

- 我们容易想到的贪心解法是将栈顶的元素和剩余字符串中最小的元素进行对比
  
  - 如果小于等于，则应该 pop 出
  
  - 如果大于，则不应该 pop 出

- 为什么栈顶元素小于等于剩余字符串中最小的元素时应该 pop 出，可以分为以下两种情况
  
  1. 如果栈顶元素严格小于剩余字符串中最小的元素，则显然应该 pop 出
  
  2. 如果栈顶元素等于剩余字符串中最小的元素，那么 pop 出该元素后剩余的字符串构成的字典序显然不会变得更大
