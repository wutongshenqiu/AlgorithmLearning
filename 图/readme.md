- [acwing](acwing.md)

- [基本概念](https://www.cnblogs.com/xiaobingqianrui/p/8902111.html)

- [拓扑排序](topological-sorting.md)
  
- [PAT 1146](https://pintia.cn/problem-sets/994805342720868352/problems/994805343043829760)
  
- [图的覆盖](https://zh.wikipedia.org/wiki/%E8%A6%86%E7%9B%96_(%E5%9B%BE%E8%AE%BA))
  
  - [PAT 1134](https://pintia.cn/problem-sets/994805342720868352/problems/994805346428633088)
  
- [连通图](https://zhuanlan.zhihu.com/p/37792015)

  - [PAT 1126](https://pintia.cn/problem-sets/994805342720868352/problems/994805349851185152)

    - 判断是否为连通图时==不需要遍历所有路径==，即注释处的代码不应该有

      ```c++
      void dfs(int n) {
          visited[n] = true;
          visited_vertices++;
          if (visited_vertices == g.size() - 1) is_connected = true;
          if (is_connected) return;
      
          for (const auto& it : g[n]) {
              if (!visited[it]) {
                  dfs(it);
                  // visited[it] = false;
                  // visited_vertices--;
              }
          }
      }
      ```

- [dijkstra](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm)
  - [PAT 1072](https://pintia.cn/problem-sets/994805342720868352/problems/994805396953219072)