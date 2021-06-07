## 归并排序

- [原理可以参考这篇文章](https://oi-wiki.org/basic/merge-sort/)

- 其核心思路代码如下

  ```c++
  for (int len = 2; len <= l.size(); len *= 2) {
      for (int i = 0; i < l.size() / len; i++) {
          sort(l.begin() + i * len, l.begin() + (i + 1) * len);
      }
      // 值得注意的是这一行
      sort(l.begin() + (l.size() / len) * len, l.end());
  ```

- 在不考虑时间复杂度的情况下可以用 `sort` 函数来代替归并排序实际的替换过程



## 求解逆序对

- 满足 $a_i > a_j \; \text{&&} \; i < j$ 的 $(a_i, a_j)$ 称之为逆序对

- 常见的求解方法有

  - [归并排序](https://oi-wiki.org/basic/merge-sort/)
  - ==树状数组==

  