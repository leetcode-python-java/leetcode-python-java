# 1584. Min Cost to Connect All Points - Best Practices of LeetCode Solutions (Kruskal's Algorithm)
LeetCode link: [1584. Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points)

## LeetCode problem description
You are given an array `points` representing integer coordinates of some points on a 2D-plane, where `points[i] = [xi, yi]`.

The cost of connecting two points `[xi, yi]` and `[xj, yj]` is the manhattan distance between them: `|xi - xj| + |yi - yj|`, where `|val|` denotes the absolute value of `val`.

Return _the minimum cost to make all points connected_. All points are connected if there is **exactly one** simple path between any two points.

### Example 1
![](../../images/examples/1584_1_1.png)
```java
Input: points = [[0,0],[2,2],[3,10],[5,2],[7,0]]
Output: 20
Explanation: 
```
![](../../images/examples/1584_1_2.png)
```
We can connect the points as shown above to get the minimum cost of 20.
Notice that there is a unique path between every pair of points.
```

### Example 2
```java
Input: points = [[3,12],[-2,5],[-4,1]]
Output: 18
```

### Constraints
- `1 <= points.length <= 1000`
- `-1000000 <= xi, yi <= 1000000`
- All pairs `(xi, yi)` are distinct.

<details>
  <summary>Hint 1</summary>
  Connect each pair of points with a weighted edge, the weight being the manhattan distance between those points.
</details>

<details>
  <summary>Hint 2</summary>
  The problem is now the cost of minimum spanning tree in graph with above edges.
</details>

## Intuition
* Connect each pair of points with a **weighted** edge, the weight being the manhattan distance between those points.
* Cycles will increase the `cost`, so there is no cycle.
* A connected graph without cycles is called a tree.
* The problem is now the cost of **minimum spanning tree** in graph with above edges.
* A minimum spanning tree (MST) or minimum weight spanning tree is a subset of the edges of a connected, edge-weighted undirected graph that connects all the vertices together, without any cycles and with the minimum possible total edge weight.

### Another solution: Prim's Algorithm
Please see [1584. Min Cost to Connect All Points (Prim's Algorithm)](1584-min-cost-to-connect-all-points.md).

This page, I will only talk about the solution of **Kruskal's Algorithm**.

### Approach: Kruskal's Algorithm
- _Prim's Algorithm_ adds the closest point to the tree each time, while _Kruskal's Algorithm_ adds the shortest edge to the tree each time.
- If both vertices of an edge are already in the tree, this edge can be skipped. Because once this edge is added, a cycle will be formed, which will increase the cost and destroy the structure of the tree.
- To determine whether a cycle will be formed, the **Union-Find** algorithm can be used.
- Traverse all edges once, add up the lengths of the edges and return the sum as the result.
- If you are familiar with the **Union-Find** algorithm, it is easy to solve the problem with _Kruskal's algorithm_. However, this problem does not directly give the `edges` information, and we need to calculate it through the vertex information, which is not difficult, but this causes the algorithm to run slower than _Prim's Algorithm_ because there are too many edges. The more edges, the slower _Kruskal's Algorithm_.

## Complexity
`E` is the `edges.length`.

`N` is the `points.length`.

* Time: `O(E * logE)`.
* Space: `O(N * N)`.

## Python
```python
class Solution:
    def __init__(self):
        self.parent = []

    def minCostConnectPoints(self, points: List[List[int]]) -> int:
        self.parent = list(range(len(points)))
        result = 0
        edged_points = []

        for i, point in enumerate(points):
            for j in range(i + 1, len(points)):
                distance = abs(point[0] - points[j][0]) + \
                           abs(point[1] - points[j][1])
                heapq.heappush(edged_points, (distance, i, j))
        
        while edged_points:
            distance, i, j = heapq.heappop(edged_points)
            
            if self.same_root(i, j):
                continue
            
            self.unite(i, j)
            
            result += distance
            
        return result
    
    def unite(self, x, y):
        root_x = self.find_root(x)
        root_y = self.find_root(y)
        self.parent[root_y] = root_x

    def find_root(self, x):
        if x == self.parent[x]:
            return x
        
        self.parent[x] = self.find_root(self.parent[x])

        return self.parent[x]

    def same_root(self, x, y):
        return self.find_root(x) == self.find_root(y)
```

## Java
```java
```

## Python
```python
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
