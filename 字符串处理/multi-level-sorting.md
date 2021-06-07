## 二级排序

在字符串处理的问题中，我们有时候需要按照多个标准对结果进行排序。

例如 [PAT 1153](https://pintia.cn/problem-sets/994805342720868352/problems/1071785190929788928) 中，我们需要首先按照成绩降序排列，当成绩相同时，我们需要按照字符串的字典序进行升序排列。

一开始做这道题的想法是先对字符串按照字典序进行升序排列，再对用**stable_sort**对分数进行降序排列。后来在[柳神的题解](https://www.liuchuo.net/archives/8023)中发现其实只需要进行一次排序就足够了。想法是我们**首先比较重要的那一项是否相等，如果不相等，则根据该项进行排序；如果相等，则根据次要项进行排序**

更高级别的排序可以类推



### 例子

```c++
//
// Created by qiufeng on 2021/1/28.
//

#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;


// TODO
// 如何限定泛型具有特定的性质？类似于 rust 中的 trait bound
template<typename T, typename V>
inline bool cmp(const pair<T, V> &a, const pair<T, V> &b) {
    return a.second != b.second ? a.second > b.second : a.first < b.first;
}


int main() {
    typedef pair<string, int> psi;

    psi test_data[]{make_pair("a", 10), make_pair("b", 10),
                                  make_pair("c", 20), make_pair("d", 20)};
    vector<psi> test_original_sort(test_data, test_data + sizeof(test_data) / sizeof(psi));
    auto test_cmp_sort(test_original_sort);

    auto str_cmp = [](const psi& a, const psi& b) -> bool { return a.first < b.first; };
    auto int_cmp = [](const psi& a, const psi& b) -> bool { return a.second > b.second; };
    sort(test_original_sort.begin(), test_original_sort.end(), str_cmp);
    stable_sort(test_original_sort.begin(), test_original_sort.end(), int_cmp);
    cout << "original sort: ";
    for (const auto& it : test_original_sort) cout << it.first << " " << it.second << "; ";

    sort(test_cmp_sort.begin(), test_cmp_sort.end(), cmp<string, int>);
    cout << "\ncmp sort: ";
    for (const auto& it : test_cmp_sort) cout << it.first << " " << it.second << "; ";

    return 0;
}
```

