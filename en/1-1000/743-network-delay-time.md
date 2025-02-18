# 743. Network Delay Time - Best Practices of LeetCode Solutions
LeetCode link: [743. Network Delay Time](https://leetcode.com/problems/network-delay-time), difficulty: **Medium**.

## LeetCode description of "743. Network Delay Time"
You are given a network of `n` nodes, labeled from `1` to `n`. You are also given `times`, a list of travel times as directed edges `times[i] = (ui, vi, wi)`, where `ui` is the source node, `vi` is the target node, and `wi` is the time it takes for a signal to travel from source to target.

We will send a signal from a given node `k`. Return _the **minimum** time it takes for all the n nodes to receive the signal_. If it is impossible for all the `n` nodes to receive the signal, return `-1`.

### [Example 1]
![](../../images/examples/743_1.png)

**Input**: `times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2`

**Output**: `2`

### [Example 2]
**Input**: `times = [[1,2,1]], n = 2, k = 1`

**Output**: `1`

### [Example 3]
**Input**: `times = [[1,2,1]], n = 2, k = 2`

**Output**: `-1`

### [Constraints]
- `1 <= k <= n <= 100`
- `1 <= times.length <= 6000`
- `times[i].length == 3`
- `1 <= ui, vi <= n`
- `ui != vi`
- `0 <= wi <= 100`
- All the pairs `(ui, vi)` are **unique**. (i.e., no multiple edges.)

### [Hints]
<details>
  <summary>Hint 1</summary>
  We visit each node at some time, and if that time is better than the fastest time we've reached this node, we travel along outgoing edges in sorted order. Alternatively, we could use Dijkstra's algorithm.
</details>

## Intuition
We can solve it via both **Bellman-Ford algorithm** and **Dijkstra's algorithm**.

### Bellman-Ford Algorithm
Here is an animation about _Bellman-Ford algorithm_:

![](../../images/graph_Bellman-Ford_algorithm_animation.gif)

* `Bellman-Ford algorithm` has less code and can handle the situation of **negative** edge weights, but it is slower than `Dijkstra's algorithm` if it is not optimized.
The following code will introduce how to optimize.

* `Dijkstra's algorithm` always takes the shortest path, so it is more efficient, but it requires writing more code and it cannot handle the situation of **negative** edge weights.

For a detailed description of **Dijkstra's algorithm**, please refer to [1514. Path with Maximum Probability](../1001-2000/1514-path-with-maximum-probability.md).

### Common graph theory algorithm comparison table
|Algorithm name|Main application scenarios|Optimization methods|Importance|Difficulty|min_<br>distances|Negative weights|Additional application scenarios|
|--------------|--------------------------|--------------------|----------|----------|-------------|----------------|--------------------------------|
|[Depth-first search](./797-all-paths-from-source-to-target.md)                                                    |Traverse a graph           |No need              |Very important|Easy          |No need |Can handle||
|[Breath-first search](../1001-2000/1971-find-if-path-exists-in-graph.md)                                          |Traverse a graph           |No need              |Very important|Easy          |No need |Can handle|Single-Source Shortest Path if No Weight|
|[UnionFind, aka disjoint-set](./684-redundant-connection.md)                                                      |Graph Connectivity         |Path Compression     |Very important|Medium        |No need |Can handle|[Directed Graph Cycle Detection](./685-redundant-connection-ii.md)|
|[Prim's algorithm](../1001-2000/1584-min-cost-to-connect-all-points.md)                                           |Minimum Spanning Tree      |Heap Sort to Simplify|Important     |Medium         |Used   |Can handle||
|[Kruskal's algorithm](../1001-2000/1584-min-cost-to-connect-all-points-2.md)                                      |Minimum Spanning Tree      |No need              |Important     |Relatively hard|No need|Can handle||
|[Dijkstra's algorithm](../1001-2000/1514-path-with-maximum-probability.md)                                        |Single-Source Shortest Path|Heap Sort            |Very important|Relatively hard|Used   |Cannot handle||
|[A* search algorithm](./752-open-the-lock.md)                                                                     |Single-Source Shortest Path|Built-in Heap Sort   |Very important|Medium         |No need|It depends||
|[Bellman-Ford algorithm](./743-network-delay-time.md)                                                             |Single-Source Shortest Path|Queue-Improved       |Very Important|Easy           |Used   |Can handle|[Detect Negative Cycles](https://www.geeksforgeeks.org/detect-negative-cycle-graph-bellman-ford/), <br>[Shortest Hop-Bounded Paths](./787-cheapest-flights-within-k-stops.md)|
|[Floyd–Warshall](../1001-2000/1334-find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance.md)|Multi-Source Shortest Path |No need              |Less important|Relatively hard|Used   |Can handle||

## Complexity
**V**: vertex count, **E**: Edge count.

### Bellman-Ford algorithm
* Time: `O(V * E)`.
* Space: `O(V)`.

### Queue-improved Bellman-Ford algorithm (also known as `Shortest Path Faster Algorithm` abbreviated as `SPFA`)
* Time: `O(V * X)` (`X` < `E`).
* Space: `O(V + E)`.

### Dijkstra's algorithm using `heap sort`
* Time: `O(E * log(E))`.
* Space: `O(V + E)`.

## Python
### Bellman-Ford algorithm (slow, yet below, I will introduce how to improve its efficiency)
```python
class Solution:
    def networkDelayTime(self, edges: List[List[int]], n: int, start_node: int) -> int:
        min_times = [float('inf')] * (n + 1)
        min_times[start_node] = 0

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

A very similar question: [787. Cheapest Flights Within K Stops](./787-cheapest-flights-within-k-stops.md), but if you use the above code, it will not be accepted by LeetCode.

You can try to solve `787. Cheapest Flights Within K Stops` first, then read on.

```python
class Solution:
    def networkDelayTime(self, edges: List[List[int]], n: int, start_node: int) -> int:
        min_times = [float('inf')] * (n + 1)
        min_times[start_node] = 0

        for _ in range(n - 1):
            # If you remove the next line and always use `min_times`, it can also be accepted.
            # But if you print `min_times`, you may see different result. Please try it.
            # The values of `min_times` modified in this loop will affect the subsequent `min_times` items in the same loop.
            # Please work on `problem 787`: https://leetcode.com/problems/cheapest-flights-within-k-stops/ to better understand this. 
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

### A variant of Bellman-Ford algorithm, which can be used to improve the efficiency of Bellman-Ford algorithm below
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

### Queue-improved Bellman-Ford algorithm (also known as `Shortest Path Faster Algorithm` abbreviated as `SPFA`)
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
