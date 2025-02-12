# 743. 网络延迟时间 - 力扣题解最佳实践
力扣链接：[743. 网络延迟时间](https://leetcode.cn/problems/network-delay-time), 难度: **中等**。

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

`Bellman-Ford`算法代码量少，还能处理`边`权值为**负数**的情况，但较慢。

`Dijkstra算法`因为始终走最短路径，所以执行**效率高**！但代码量大，无法处理`边`权值为**负数**的情况。

**Dijkstra算法**的详细说明，请参考 [1514. 概率最大的路径](../1001-2000/1514-path-with-maximum-probability.md)。

## 复杂度
**V**: 顶点数量，**E**: 边的数量。

### Bellman-Ford 算法
* 时间: `O(V * E)`.
* 空间: `O(V)`.

### Dijkstra 算法（采用`堆排序`）
* 时间: `O(E * log(E))`.
* 空间: `O(V + E)`.

## Python
### Standard Bellman-Ford algorithm
```python
class Solution:
    def networkDelayTime(self, edges: List[List[int]], n: int, start: int) -> int:
        min_times = [float('inf')] * (n + 1)
        min_times[start] = 0

        for _ in range(n - 1):
            for source_node, target_node, time in edges: # process edges directly
                if min_times[source_node] == float('inf'):
                    continue

                target_time = time + min_times[source_node]

                if target_time < min_times[target_node]:
                    min_times[target_node] = target_time

        result = max(min_times[1:])

        if result == float('inf'):
            return -1

        return result
```

### Algorithm similar to Bellman-Ford algorithm
```python
class Solution:
    def networkDelayTime(self, edges: List[List[int]], n: int, start: int) -> int:
        min_times = [float('inf')] * (n + 1)
        min_times[start] = 0
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
