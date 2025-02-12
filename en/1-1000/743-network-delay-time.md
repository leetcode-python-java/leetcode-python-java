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

## Complexity
* Time: `O()`.
* Space: `O()`.

## Python
```python
class Solution:
    def networkDelayTime(self, items: List[List[int]], n: int, start: int) -> int:
        min_distances = [float('inf')] * (n + 1)
        min_distances[start] = 0

        node_to_pairs = defaultdict(set)

        for source, target, distance in items:
            node_to_pairs[source].add((target, distance))

        for _ in range(n - 1):
            for node, min_distance in enumerate(min_distances):
                if min_distance == float('inf'):
                    continue

                for target_node, distance in node_to_pairs[node]:
                    distance_ = distance + min_distance

                    if distance_ < min_distances[target_node]:
                        min_distances[target_node] = distance_

        result = max(min_distances[1:])

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
