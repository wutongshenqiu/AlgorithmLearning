1. 用普通队列怎么做
2. 将队列中冗余的元素删掉 -> 具有了单调性
3. 可以用 O(1) 的时间从队头/尾取出最值

## 单调队列

- 在解决滑动窗口极值的问题中，单调队列维护的是**原数组的索引**，因为需要判断队列中的元素是否在一个窗口之内
- 将一个新的元素(索引)加入到队尾时，我们需要**先删除队尾冗余的元素**
- 如何思考[^1]
  - 用普通队列怎么做
  - 将队列中冗余的元素删除，使队列具有单调性
  - 用 $O(1)$ 的时间从队头、队尾取出最值

### 代码

```cpp
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    vector<int> ans;
    deque<int> dq;

    for (int i = 0; i < nums.size(); i++) {
        // 队头元素是否在窗口之内
        if (!dq.empty() && dq.back() - dq.front() >= k - 1) dq.pop_front();
        // 删除队尾冗余元素
        while (!dq.empty() && nums[dq.back()] <= nums[i]) dq.pop_back();
        dq.push_back(i);

        if (i >= k - 1) {
            ans.push_back(nums[dq.front()]);
        }
    }

    return ans;
}
```

## ref

[^1]: [acwing滑动窗口](https://www.acwing.com/problem/content/156/)