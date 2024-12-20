# LeetCode 1971. Find if Path Exists in Graph's Solution: UnionFind
LeetCode problem link: [1971. Find if Path Exists in Graph](https://leetcode.com/problems/find-if-path-exists-in-graph)

## LeetCode problem description
There is a **bi-directional** graph with `n` vertices, where each vertex is labeled from `0` to `n - 1` (**inclusive**). The edges in the graph are represented as a 2D integer array `edges`, where each `edges[i] = [ui, vi]` denotes a bi-directional edge between vertex `ui` and vertex `vi`. Every vertex pair is connected by **at most one** edge, and no vertex has an edge to itself.

You want to determine if there is a **valid path** that exists from vertex `source` to vertex `destination`.

Given `edges` and the integers `n`, `source`, and `destination`, return `true` _if there is a **valid path** from `source` to `destination`, or `false` otherwise_.

### Example 1
![](../../images/examples/1971_1.png)
```
Input: n = 3, edges = [[0,1],[1,2],[2,0]], source = 0, destination = 2
Output: true
Explanation: There are two paths from vertex 0 to vertex 2:
- 0 → 1 → 2
- 0 → 2
```

### Example 2
![](../../images/examples/1971_2.png)
```
Input: n = 6, edges = [[0,1],[0,2],[3,5],[5,4],[4,3]], source = 0, destination = 5
Output: false
Explanation: There is no path from vertex 0 to vertex 5.
```

### Constraints
- `1 <= n <= 2 * 10**5`
- `0 <= edges.length <= 2 * 10**5`
- `edges[i].length == 2`
- `0 <= ui, vi <= n - 1`
- `ui != vi`
- `0 <= source, destination <= n - 1`
- There are no duplicate edges.
- There are no self edges.

## Another solution: Breadth-First Search Algorithm
Please see [1971. Find if Path Exists in Graph ('Breadth-First Search' Solution)](1971-find-if-path-exists-in-graph.md).

## Intuition
The island problem can be abstracted into a **graph theory** problem. This is an **undirected graph**:

![](../../images/graph_undirected_1.svg)

And this graph may have multiple **connected components**. Initially, we start from `source` vertex which belongs to one of the `connected components`. 

![](../../images/graph_undirected_2.png)

- We need to find if there is a path from `source` to `destination`. This question is equivalent to determine if `source` and `destination` vertices belong to the same `connected component`.
- A `tree` is a type of `graph`. If two nodes are in the same tree, then return `true`. So we need a method `in_same_tree(node1, node2)` to return a boolean value.
- We are `edges` data and need to divide them into multiple groups, each group can be abstracted into a **tree**.
- `UnionFind` algorithm is designed for grouping and searching data.

### 'UnionFind' algorithm
- `UnionFind` algorithm typically has three methods:
    - The `unite(node1, node2)` operation can be used to merge two trees.
    - The `find_root(node)` method can be used to return the root of a node.
    - The `same_root(node1, node2)` method can be used to judge if two nodes are in the same tree.

## Approach (UnionFind algorithm)
1. Initially, every node is in the group of itself.
1. Iterate `edges` data and `unite(node1, node2)`.
1. Return `same_root(source, destination)`.

## Complexity
* Time: `O(n)`. 
* Space: `O(n)`.

## Python
### Standard UnionFind algorithm
```python
class Solution:
    def __init__(self):
        self.father = None

    def validPath(self, n: int, edges: List[List[int]], source: int, destination: int) -> bool:
        self.father = list(range(n))

        for x, y in edges:
            self.unite(x, y)

        return self.same_root(source, destination)

    def unite(self, x, y):
        root_x = self.find_root(x)
        root_y = self.find_root(y)

        self.father[root_y] = root_x # Error-prone point 1
    
    def find_root(self, x):
        if x == self.father[x]:
            return x

        self.father[x] = self.find_root(self.father[x]) # Error-prone point 2

        return self.father[x]

    def same_root(self, x, y):
        return self.find_root(x) == self.find_root(y)
```

### Another UnionFind algorithm (using a map and an array of set)
This solution is slower than the `Standard UnionFind algorithm`, but it is straightforward.
```python
class Solution:
    def __init__(self):
        self.disjoint_sets = []
        self.value_to_set_id = {}

    def validPath(self, n: int, edges: List[List[int]], source: int, destination: int) -> bool:
        for i in range(n):
            self.disjoint_sets.append({i})
            self.value_to_set_id[i] = i

        for x, y in edges:
            self.unite(x, y)

        return self.in_same_set(source, destination)

    def unite(self, x, y):
        if self.in_same_set(x, y):
            return
        
        bigger = x
        smaller = y

        if len(self.get_set(x)) < len(self.get_set(y)):
            bigger = y
            smaller = x
            
        for value in self.get_set(smaller):
            self.get_set(bigger).add(value)
            self.value_to_set_id[value] = self.value_to_set_id.get(bigger)

    def get_set(self, value):
        set_id = self.value_to_set_id.get(value)
        return self.disjoint_sets[set_id]

    def in_same_set(self, x, y):
        return self.get_set(x) == self.get_set(y)
```

## Java
```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
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

## C
```c
// Welcome to create a PR to complete the code of this language, thanks!
```

## Kotlin
```kotlin
// Welcome to create a PR to complete the code of this language, thanks!
```

## Swift
```swift
// Welcome to create a PR to complete the code of this language, thanks!
```

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
