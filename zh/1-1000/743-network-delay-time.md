# 743. 网络延迟时间 - 力扣题解最佳实践
力扣链接：[743. 网络延迟时间](https://leetcode.cn/problems/network-delay-time) ，难度：**中等**。

## 力扣“743. 网络延迟时间”问题描述
有 `n` 个网络节点，标记为 `1` 到 `n`。

给你一个列表 `times`，表示信号经过 **有向** 边的传递时间。 `times[i] = (ui, vi, wi)`，其中 `ui` 是源节点，`vi` 是目标节点， `wi` 是一个信号从源节点传递到目标节点的时间。

现在，从某个节点 K 发出一个信号。需要多久才能使所有节点都收到信号？如果不能使所有节点收到信号，返回 `-1` 。

### [示例 1]
![](../../images/examples/743_1.png)

**输入**: `times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2`

**输出**: `2`

### [示例 2]
**输入**: `times = [[1,2,1]], n = 2, k = 1`

**输出**: `1`

### [示例 3]
**输入**: `times = [[1,2,1]], n = 2, k = 2`

**输出**: `-1`

### [约束]
- `1 <= k <= n <= 100`
- `1 <= times.length <= 6000`
- `times[i].length == 3`
- `1 <= ui, vi <= n`
- `ui != vi`
- `0 <= wi <= 100`
- 所有 `(ui, vi)` 对都 **互不相同**（即，不含重复边）

### [提示]
<details>
  <summary>提示 1</summary>
  We visit each node at some time, and if that time is better than the fastest time we've reached this node, we travel along outgoing edges in sorted order. Alternatively, we could use Dijkstra's algorithm.
</details>

## 思路
本题可用 **Bellman-Ford算法** 或 **Dijkstra算法** 解决。

### Bellman-Ford算法
*Bellman-Ford算法*的动画演示：

![](../../images/graph_Bellman-Ford_algorithm_animation.gif)

* `Bellman-Ford`算法代码量少，还能处理`边`权值为**负数**的情况，但如果没有被优化过，运行得比较慢。下文代码会介绍如何优化。

* `Dijkstra算法`因为始终走最短路径，所以执行**效率高**！但代码量大，无法处理`边`权值为**负数**的情况。

**Dijkstra算法**的详细说明，请参考 [1514. 概率最大的路径](../1001-2000/1514-path-with-maximum-probability.md)。

### 常见图论算法对照表

|算法名称|主要的适用场景|优化方式|重要度|难度|min_<br>distances|负边权值|额外的适用场景|
|-------|-----------|-------|-------|---|-------------|--------|------------|
|[深度优先搜索](./797-all-paths-from-source-to-target.md)                                                            |遍历图     |无需优化  |很重要 |简单|不用|能处理||
|[广度优先搜索](../1001-2000/1971-find-if-path-exists-in-graph.md)                                                   |遍历图     |无需优化  |很重要 |简单|不用|能处理|不考虑权时，可用于求单源最短路径|
|[并查集](./684-redundant-connection.md)                                                                            |检测图的连通性|路径压缩|很重要 |中等|不用|能处理|[有向图环检测](./685-redundant-connection-ii.md)|
|[Prim 算法](../1001-2000/1584-min-cost-to-connect-all-points.md)                                                   |最小生成树 |堆排序简化|重要   |中等|用到|能处理||
|[Kruskal 算法](../1001-2000/1584-min-cost-to-connect-all-points-2.md)                                              |最小生成树 |无需优化  |重要   |较难|不用|能处理||
|[Dijkstra 算法](../1001-2000/1514-path-with-maximum-probability.md)                                                |单源最短路径|堆排序优化|很重要 |较难|用到|无能力||
|[A* 算法](./752-open-the-lock.md)                                                                                  |单源最短路径|固有堆排序|很重要 |中等|不用|看情况||
|[Bellman-Ford](./743-network-delay-time.md)                                                                       |单源最短路径|集合优化  |很重要 |简单|用到|能处理|[负环检测](https://www.geeksforgeeks.org/detect-negative-cycle-graph-bellman-ford/), [限定步数最短路径](./787-cheapest-flights-within-k-stops.md)|
|[Floyd–Warshall](../1001-2000/1334-find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance.md)|多源最短路径|无需优化  |较不重要|较难|用到|能处理||

## 复杂度
**V**: 顶点数量，**E**: 边的数量。

### Bellman-Ford 算法
* 时间: `O(V * E)`.
* 空间: `O(V)`.

### 列队（或集合）优化的 Bellman-Ford 算法 (又称 `最短路径快速算法`，缩写为 `SPFA`)
* Time: `O(V * X)` (`X` < `E`).
* Space: `O(V + E)`.

### Dijkstra 算法（采用`堆排序`）
* 时间: `O(E * log(E))`.
* 空间: `O(V + E)`.

## Python
### Bellman-Ford 算法（较慢，后文介绍如何性能提升）
一个与本题非常类似的题目: [787. K 站中转内最便宜的航班](./787-cheapest-flights-within-k-stops.md), 然而，如果你用上面同样的代码，会无法通过力扣测试。

你可以先尝试解决`787. K 站中转内最便宜的航班`，然后再继续阅读下文。

```python
class Solution:
    def networkDelayTime(self, edges: List[List[int]], n: int, start_node: int) -> int:
        min_times = [float('inf')] * (n + 1)
        min_times[start_node] = 0

        for _ in range(n - 1):
            # 删除这一行，始终用`min_times`，也能通过，但`787. K 站中转内最便宜的航班` https://leetcode.cn/problems/cheapest-flights-within-k-stops/ 就通过不了了。
            # 如果你打印`min_times`，很可能会发现结果不一样。请尝试下。
            # 原因就是本轮循环中修改了的`min_times`的值，有可能在本轮循环中被使用到，对本轮后续的`min_times`产生影响。
            # 为更好地理解本行代码，请做 `787. K 站中转内最便宜的航班`。  
            min_times_clone = min_times.copy() # addition 1

            for source_node, target_node, time in edges: # process edges directly
                if min_times_clone[source_node] == float('inf'): # change 1
                    continue

                target_time = time + min_times_clone[source_node] # change 2

                if target_time < min_times[target_node]:
                    min_times[target_node] = target_time

        result = max(min_times[1:])

        if result == float('inf'):
            return -1

        return result
```

### Bellman-Ford 算法的变体，可用于后文的性能提升
```python
class Solution:
    def networkDelayTime(self, edges: List[List[int]], n: int, start_node: int) -> int:
        min_times = [float('inf')] * (n + 1)
        min_times[start_node] = 0
        node_to_pairs = defaultdict(set)

        for source, target, time in edges: # process nodes first, then their edges
            node_to_pairs[source].add((target, time))

        for _ in range(n - 1):
            for node, min_time in enumerate(min_times): # process nodes first
                if min_time == float('inf'):
                    continue

                for target_node, time in node_to_pairs[node]: # process edges of the node
                    target_time = time + min_time

                    if target_time < min_times[target_node]:
                        min_times[target_node] = target_time

        result = max(min_times[1:])

        if result == float('inf'):
            return -1

        return result
```

### 列队（或集合）优化的 Bellman-Ford 算法 (Queue-improved Bellman-Ford)
又称 `最短路径快速算法` (`Shortest Path Faster Algorithm` 缩写为 `SPFA`)。
```python
class Solution:
    def networkDelayTime(self, edges: List[List[int]], n: int, start_node: int) -> int:
        min_times = [float('inf')] * (n + 1)
        min_times[start_node] = 0
        node_to_pairs = defaultdict(set)

        for source, target, time in edges: # process nodes first, then their edges
            node_to_pairs[source].add((target, time))

        updated_nodes = set([start_node]) # added 1

        for _ in range(n - 1):
            nodes = updated_nodes.copy() # added 3
            updated_nodes.clear() # added 4

            for node in nodes: # changed 1
                for target_node, time in node_to_pairs[node]: # process edges of the node
                    target_time = time + min_times[node]

                    if target_time < min_times[target_node]:
                        min_times[target_node] = target_time
                        updated_nodes.add(target_node) # added 2

        result = max(min_times[1:])

        if result == float('inf'):
            return -1

        return result
```

### Dijkstra's algorithm using `heap sort` (without `visited`)
```python
import heapq

class Solution:
    def networkDelayTime(self, edges: List[List[int]], n: int, start_node: int) -> int:
        min_times = [float('inf')] * (n + 1)
        min_times[start_node] = 0
        node_to_pairs = defaultdict(set)

        for source, target, time in edges:
            node_to_pairs[source].add((target, time))

        priority_queue = [(0, start_node)]

        while priority_queue:
            current_time, current_node = heapq.heappop(priority_queue)

            for target_node, time in node_to_pairs[current_node]:
                target_time = time + current_time

                if target_time < min_times[target_node]:
                    min_times[target_node] = target_time
                    heapq.heappush(priority_queue, (target_time, target_node))

        result = max(min_times[1:])

        if result == float('inf'):
            return -1

        return result
```

### Dijkstra's algorithm using `heap sort` (with `visited`)
```python
import heapq

class Solution:
    def networkDelayTime(self, edges: List[List[int]], n: int, start_node: int) -> int:
        min_times = [float('inf')] * (n + 1)
        min_times[start_node] = 0
        node_to_pairs = defaultdict(set)
        visited = [False] * (n + 1) # added 1

        for source, target, time in edges:
            node_to_pairs[source].add((target, time))

        priority_queue = [(0, start_node)]

        while priority_queue:
            current_time, current_node = heapq.heappop(priority_queue)

            if visited[current_node]: # added 3
                continue

            visited[current_node] = True # added 2            

            for target_node, time in node_to_pairs[current_node]:
                if visited[target_node]: # added 4
                    continue

                target_time = time + current_time

                if target_time < min_times[target_node]:
                    min_times[target_node] = target_time
                    heapq.heappush(priority_queue, (target_time, target_node))

        result = max(min_times[1:])

        if result == float('inf'):
            return -1

        return result
```

## JavaScript
```javascript
// Welcome to create a PR to complete the code of this language, thanks!
```

## Java
```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## C#
```c#
// Welcome to create a PR to complete the code of this language, thanks!
```

## Go
```go
// Welcome to create a PR to complete the code of this language, thanks!
```

## Ruby
```ruby
# Welcome to create a PR to complete the code of this language, thanks!
```

## C, Kotlin, Swift, Rust or other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
