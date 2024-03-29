### 到达首都的最小油耗

> 一颗有 $n$ 个节点的树，每个节点表示一个城市，编号从 $0 \sim n - 1$，且恰好有 $n - 1$ 条路。$0$ 代表首都
> 
> 每个城市里有一个代表，他们都要去首都参加一个会议
> 
> 每个城市里有一辆车，车的座位数为 `seat`
> 
> 城市里的代表可以选择乘坐所在城市的车，或者乘坐其他城市的车，相邻城市之间一辆车的油耗是一升
> 
> 所有代表返回首都至少需要多少升汽油

- 本题有一个关键点在于，**若 $u$ 处的一辆车需要往更深的地方 $v$ 去接人，则不如 $v$ 开一辆车到 $u$ 汇合**

- 因此到某一点 $u$ 所需要的车辆即
  
  $$
  \sum \frac{v_i \rightarrow u}{\text{seat}}
  $$
  
  - 其中 $v_i \rightarrow u$ 表示从 $v$ 到 $u$ 这条边上的流量(即 $u$ 的以 $v$ 为子树根节点的大小)
