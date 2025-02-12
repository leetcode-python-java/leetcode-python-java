# 1514. Path with Maximum Probability - Best Practices of LeetCode Solutions
LeetCode link: [1514. Path with Maximum Probability](https://leetcode.com/problems/path-with-maximum-probability), difficulty: **Medium**.

## LeetCode description of "1514. Path with Maximum Probability"
You are given an undirected weighted graph of `n` nodes (0-indexed), represented by an edge list where `edges[i] = [a, b]` is an undirected edge connecting the nodes `a` and `b` with a probability of success of traversing that edge `succProb[i]`.

Given two nodes `start` and `end`, find the path with the maximum probability of success to go from `start` to `end` and return its success probability.

If there is no path from `start` to `end`, return 0. Your answer will be accepted if it differs from the correct answer by at most **1e-5**.

### [Example 1]
![](../../images/examples/1514_1.png)

**Input**: `n = 3, edges = [[0,1],[1,2],[0,2]], succProb = [0.5,0.5,0.2], start = 0, end = 2`

**Output**: `0.25000`

**Explanation**: `There are two paths from start to end, one having a probability of success = 0.2 and the other has 0.5 * 0.5 = 0.25.`

### [Example 2]
![](../../images/examples/1514_2.png)
**Input**: `n = 3, edges = [[0,1],[1,2],[0,2]], succProb = [0.5,0.5,0.3], start = 0, end = 2`

**Output**: `0.30000`

### [Example 3]
![](../../images/examples/1514_3.png)
**Input**: `n = 3, edges = [[0,1]], succProb = [0.5], start = 0, end = 2`

**Output**: `0.00000`

**Explanation**: `There is no path between 0 and 2.`

### [Constraints]
- `2 <= n <= 10^4`
- `0 <= start, end < n`
- `start != end`
- `0 <= a, b < n`
- `a != b`
- `0 <= succProb.length == edges.length <= 2*10^4`
- `0 <= succProb[i] <= 1`
- There is at most one edge between every two nodes.

### [Hints]
<details>
  <summary>Hint 1</summary>
  Multiplying probabilities will result in precision errors.
</details>

<details>
  <summary>Hint 2</summary>
  Take log probabilities to sum up numbers instead of multiplying them.
</details>

<details>
  <summary>Hint 3</summary>
  Use Dijkstra's algorithm to find the minimum path between the two nodes after negating all costs.
</details>

## Intuition
We can use **Dijkstra's algorithm**.

![](../../images/graph_Dijkstra_algorithm_animation.gif)

This animation is about **Dijkstra's algorithm** to find the shortest path between `a` and `b`.
It picks the unvisited vertex with the lowest distance, calculates the distance through it to each unvisited neighbor, and updates the neighbor's distance if smaller. Mark **visited** (set to red) when done with neighbors.

In short, **Dijkstra's algorithm** means **to find the nearest point and walk through it, and never go back. Repeatedly**. 

## Complexity
**V**: vertex count, **E**: Edge count.

### Dijkstra's algorithm without using `heap sort`
* Time: `O(V * V)`.
* Space: `O(V + E)`.

### Dijkstra's algorithm using `heap sort`
* Time: `O(E * log(E))`.
* Space: `O(V + E)`.

## Python
### Dijkstra's algorithm without using `heap sort`
The code will time out when executed on LeetCode, but this is not a problem with the code itself. The `heap sort` implementation below will not time out.
```python
class Solution:
    def maxProbability(self, n: int, edges: List[List[int]], succ_prob: List[float], start_node: int, end_node: int) -> float:
        node_to_pairs = defaultdict(set)

        for i, (source_node, target_node) in enumerate(edges):
            node_to_pairs[source_node].add((target_node, succ_prob[i]))
            node_to_pairs[target_node].add((source_node, succ_prob[i]))

        max_probabilities = [0] * n
        max_probabilities[start_node] = 1
        visited = [False] * n

        for _ in range(n - 1):
            current_node = None
            maximum_probability = 0

            for node, probability in enumerate(max_probabilities):
                if not visited[node] and probability > maximum_probability:
                    maximum_probability = probability
                    current_node = node

            if current_node is None:
                break

            visited[current_node] = True

            for target_node, probability in node_to_pairs[current_node]:
                probability_ = probability * max_probabilities[current_node]

                if probability_ > max_probabilities[target_node]:
                    max_probabilities[target_node] = probability_

        return max_probabilities[end_node]
```

### Dijkstra's algorithm using `heap sort`
#### `heap sort` without using `visited`
```python
import heapq

class Solution:
    def maxProbability(self, n: int, edges: List[List[int]], succ_prob: List[float], start_node: int, end_node: int) -> float:
        node_to_pairs = defaultdict(set)

        for i, (source_node, target_node) in enumerate(edges):
            node_to_pairs[source_node].add((target_node, succ_prob[i]))
            node_to_pairs[target_node].add((source_node, succ_prob[i]))

        max_probabilities = [0 for node in range(n)]
        max_probabilities[start_node] = 1
        items = [(-1, start_node)]

        while items:
            current_probability, current_node = heapq.heappop(items)

            if current_node == end_node:
                return -current_probability

            for target_node, probability in node_to_pairs[current_node]:
                probability_ = abs(current_probability) * probability

                if probability_ > max_probabilities[target_node]:
                    max_probabilities[target_node] = probability_
                    # It may cause the same `target_node` added into `items` more than once, but it doesn't matter. Because only the one `heappush`ed first may change the `max_probabilities` data.
                    heapq.heappush(items, (-probability_, target_node))

        return 0
```

#### `heap sort` using `visited`
```python
import heapq

class Solution:
    def maxProbability(self, n: int, edges: List[List[int]], succ_prob: List[float], start_node: int, end_node: int) -> float:
        node_to_pairs = defaultdict(set)

        for i, (source_node, target_node) in enumerate(edges):
            node_to_pairs[source_node].add((target_node, succ_prob[i]))
            node_to_pairs[target_node].add((source_node, succ_prob[i]))

        max_probabilities = [0 for node in range(n)]
        max_probabilities[start_node] = 1
        items = [(-1, start_node)]
        visited = [False] * n # added 1

        while items:
            current_probability, current_node = heapq.heappop(items)

            if current_node == end_node:
                return -current_probability

            if visited[current_node]: # added 3
                continue

            visited[current_node] = True # added 2

            for target_node, probability in node_to_pairs[current_node]:
                if visited[target_node]: # added 4
                    continue

                probability_ = abs(current_probability) * probability

                if probability_ > max_probabilities[target_node]:
                    max_probabilities[target_node] = probability_
                    # It may cause the same `target_node` added into `items` more than once, but it doesn't matter. Because only the one `heappush`ed first may change the `max_probabilities` data.
                    heapq.heappush(items, (-probability_, target_node))

        return 0
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
