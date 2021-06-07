## refs

- [oi-wiki](https://oi-wiki.org/graph/tree-diameter/)
- [acwing](https://www.acwing.com/blog/content/1632/)



## 注意的点

- 对于一个顶点数为 $n$ ，边数为 $n-1$ 的无向连通图，并且从某个顶点到其他所有顶点的路径(不经过重复顶点)是唯一的，那么该图退化为一棵树
- 我们再求上述树的顶点时，dfs不需要回溯