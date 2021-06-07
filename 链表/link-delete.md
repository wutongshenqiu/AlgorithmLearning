## 链表中删除元素

- 注意如下代码(删除链表中绝对值相同的元素)是有问题的，这是因为当删除某个节点时，不应该执行语句 `pre = p`

```c++
    int p = start;
    int pre;
    while (~p) {
        Node node = linked_list[p];
        if (ss.find(abs(node.key)) != ss.end()) {
            linked_list[pre].next = node.next;
            removed_list.push_back(node);
        }
        else {
            ss.insert(abs(node.key));
        }
        pre = p;
        p = node.next;
    }
```

- 正确的代码如下

```c++
    int p = start;
    int pre;
    while (~p) {
        Node node = linked_list[p];
        if (ss.find(abs(node.key)) != ss.end()) {
            linked_list[pre].next = node.next;
            removed_list.push_back(node);
        }
        else {
            ss.insert(abs(node.key));
            pre = p;
        }
        p = node.next;
    }
```

