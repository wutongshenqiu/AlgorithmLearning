### 贡献法

#### 子序列宽度之和

> 一个序列的 **宽度** 定义为该序列中最大元素和最小元素的差值
> 
> 给定一个整数数组 `nums`，返回 `nums` 的所有非空 **子序列** 的宽度之和

- 排序后不影响子序列的宽度之和

- 考虑排序后的第 $i$ 个元素(下标从 $0$ 开始) $x$，则
  
  - $x$ 对最大值的贡献为 $2^i - 1$
  
  - $x$ 对最小值的贡献为 $2^{len(nums) - i - 1} - 1$

- 因此宽度之和为
  
  $$
  \sum_{i = 0}^{n - 1} (2^i - 2^{len(nums) - i - 1}) \cdot nums[i]
  $$

#### 子数组宽度之和

> 一个子数组的 **宽度** 定义为该序列中最大元素和最小元素的差值
> 
> 给定一个子数组 `nums`，返回 `nums` 的所有非空 **子数组** 的宽度之和

- 定义
  
  - `leftNearestGreater[i]`：第 $i$ 个元素(下标从 $0$ 开始) $x$ 的左边第一个比 $x$ 大的元素的下标
  
  - `leftNearestLess[i]`：第 $i$ 个元素(下标从 $0$ 开始) $x$ 的左边第一个比 $x$ 小的元素的下标
  
  - `rightNearestGreater[i]`：第 $i$ 个元素(下标从 $0$ 开始) $x$ 的右边第一个比 $x$ **大于等于**的元素的下标
  
  - `rightNearestLess[i]`：第 $i$ 个元素(下标从 $0$ 开始) $x$ 的右边第一个比 $x$ **小于等于**的元素的下标

- 考虑第 $i$ 个元素(下标从 $0$ 开始) $x$，则
  
  - $x$ 对最大值的贡献($\text{maxContribution}$)为
    
    $$
    (\text{rightNearestGreater[i]} - i) \times (i - \text{leftNearestGreater[i]}) - 1
    $$
  
  - $x$ 对最小值的贡献($\text{minContribution}$)为
    
    $$
    (\text{rightNearestLess[i]} - i) \times (i - \text{leftNearestLess[i]}) - 1
    $$

- 因此宽度之和为
  
  $$
  \sum_{i = 0}^{n - 1} (\text{maxContribution} - \text{minContribution}) \cdot nums[i]
  $$
  
  
