## 判断堆类型

以下方法参考自[liuchuo](https://www.liuchuo.net/archives/4667)

- 假使堆的下标从1开始

```c++
int max_flag = 1;
int min_flag = 1;
for (int j = 2; j <= n; j++) {
    if (heap[j / 2] > heap[j]) min_flag = 0;
    if (heap[j / 2] < heap[j]) max_flag = 0;
}
if (max_flag) cout << "Max Heap\n";
else if (min_flag) cout << "Min Heap\n";
else cout << "Not Heap\n";
```

