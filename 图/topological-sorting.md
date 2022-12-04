## 拓扑排序

- [简介](http://songlee24.github.io/2015/05/07/topological-sorting/)
- 如何判断是否为拓扑排序
  - 判断依次选取的顶点入度是否为零
    - [PAT 1146](https://pintia.cn/problem-sets/994805342720868352/problems/994805343043829760)
- [如何构造拓扑序列](http://jingsam.github.io/2020/08/11/topological-sort.html#DFS%E7%AE%97%E6%B3%95)
  - Kahn
    - 选择入度为0的顶点
    - 删除该节点以及该节点的边(即将其所有指向顶点的入度-1)
    - 重复上两步操作
  - DFS
    - 对有向图进行深度优先搜索
    - 如果某个顶点不能前进(出度为0)，将该顶点入栈
    - 堆栈中的序列进行逆排序，即得到一个拓扑排序