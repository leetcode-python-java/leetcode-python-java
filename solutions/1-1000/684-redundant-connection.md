# LeetCode 684. Redundant Connection's Solution
LeetCode problem link: [684. Redundant Connection](https://leetcode.com/problems/redundant-connection)

## LeetCode problem description
In this problem, a tree is an **undirected graph** that is connected and has no cycles.

You are given a graph that started as a tree with `n` nodes labeled from `1` to `n`, with one additional edge added. The added edge has two **different** vertices chosen from `1` to `n`, and was not an edge that already existed. The graph is represented as an array `edges` of length `n` where `edges[i] = [ai, bi]` indicates that there is an edge between nodes `ai` and `bi` in the graph.

Return an edge that can be removed so that the resulting graph is a tree of `n` nodes. If there are multiple answers, return the answer that occurs last in the input.

### Example 1
![](../../images/examples/684_1.jpg)
```
Input: edges = [[1,2],[1,3],[2,3]]
Output: [2,3]
```

### Example 2
![](../../images/examples/684_2.jpg)
```
Input: edges = [[1,2],[2,3],[3,4],[1,4],[1,5]]
Output: [1,4]
```

### Constraints
- `n == edges.length`
- `3 <= n <= 1000`
- `edges[i].length == 2`
- `1 <= ai < bi <= edges.length`
- `ai != bi`
- There are no repeated edges.
- The given graph is connected.

## Intuition
- In graph theory, a tree is an _undirected graph_ in which any two vertices are connected by exactly one path, or equivalently a **connected acyclic undirected graph**. Like this:
![A labeled tree with six vertices and five edges.](../../images/graph_tree_1.png)

- When an edge is added to the graph, its two nodes are also added to the graph.
- If the two nodes are already in the graph, then they must be on the same tree. At this time, a cycle is bound to be formed.

![](../../images/684.png)

- We are given `edges` data and need to divide them into multiple groups, each group can be abstracted into a **tree**.
- Finally, those trees will be merged into one tree.
- `UnionFind` algorithm is designed for grouping and searching data.

### 'UnionFind' algorithm
- `UnionFind` algorithm typically has three methods:
    - The `unite(node1, node2)` operation is used to merge two trees.
    - The `find_root(node)` method is used to return the root of a node.
    - The `same_root(node1, node2) == true` method is used to determine whether two nodes are in the same tree.

## Approach (UnionFind algorithm)
1. Initially, each node is in its own group.
1. Iterate `edges` data and `unite(node1, node2)`.
1. As soon as `same_root(node1, node2) == true` (a cycle will be formed), return `[node1, node2]`.

## Complexity
* Time: `O(n)`.
* Space: `O(n)`.

## Python
```python
class Solution:
    def __init__(self):
        self.parent = None

    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:
        self.parent = list(range(len(edges) + 1))

        for x, y in edges:
            if self.same_root(x, y):
                return [x, y]
        
            self.unite(x, y)

    def unite(self, x, y):
        root_x = self.find_root(x)
        root_y = self.find_root(y)
        
        self.parent[root_y] = root_x # Error-prone point

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
class Solution {
    private int[] parent;

    public int[] findRedundantConnection(int[][] edges) {
        parent = new int[edges.length + 1];

        for (var i = 0; i < parent.length; i++) {
            parent[i] = i;
        }

        for (var edge : edges) {
            if (sameRoot(edge[0], edge[1])) {
                return edge;
            }

            unite(edge[0], edge[1]);
        }

        return null;
    }

    private void unite(int x, int y) {
        int rootX = findRoot(x);
        int rootY = findRoot(y);

        parent[rootY] = rootX; // Error-prone point 1
    }

    private int findRoot(int x) {
        if (x == parent[x]) {
            return x;
        }

        parent[x] = findRoot(parent[x]); // Error-prone point 2

        return parent[x];
    }

    private boolean sameRoot(int x, int y) {
        return findRoot(x) == findRoot(y);
    }
}
```

## C++
```cpp
class Solution {
public:
    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        for (auto i = 0; i <= edges.size(); i++) {
            parent.push_back(i);
        }

        for (auto& edge : edges) {
            if (sameRoot(edge[0], edge[1])) {
                return edge;
            }

            unite(edge[0], edge[1]);
        }

        return {};
    }

private:
    vector<int> parent;

    void unite(int x, int y) {
        int root_x = findRoot(x);
        int root_y = findRoot(y);

        parent[root_y] = root_x; // Error-prone point 1
    }

    int findRoot(int x) {
        if (x == parent[x]) {
            return x;
        }

        parent[x] = findRoot(parent[x]); // Error-prone point 2

        return parent[x];
    }

    bool sameRoot(int x, int y) {
        return findRoot(x) == findRoot(y);
    }
};
```

## JavaScript
```javascript
let parent

var findRedundantConnection = function(edges) {
  parent = []
  for (let i = 0; i <= edges.length; i++) {
    parent.push(i)
  }

  for (let [x, y] of edges) {
    if (sameRoot(x, y)) {
      return [x, y]
    }

    unite(x, y)
  }

  return sameRoot(source, destination)
};

function unite(x, y) {
  rootX = findRoot(x)
  rootY = findRoot(y)

  parent[rootY] = rootX // Error-prone point 1
}

function findRoot(x) {
  if (x == parent[x]) {
    return x
  }

  parent[x] = findRoot(parent[x]) // Error-prone point 2

  return parent[x]
}

function sameRoot(x, y) {
  return findRoot(x) == findRoot(y)
}
```

## C#
```c#
public class Solution
{
    int[] parent;

    public int[] FindRedundantConnection(int[][] edges)
    {
        parent = new int[edges.Length + 1];
        
        for (int i = 0; i < parent.Length; i++)
            parent[i] = i;

        foreach (int[] edge in edges)
        {
            if (sameRoot(edge[0], edge[1]))
            {
                return edge;
            }

            unite(edge[0], edge[1]);
        }

        return null;
    }

    void unite(int x, int y)
    {
        int rootX = findRoot(x);
        int rootY = findRoot(y);

        parent[rootY] = rootX; // Error-prone point 1
    }

    int findRoot(int x)
    {
        if (x == parent[x])
            return x;

        parent[x] = findRoot(parent[x]); // Error-prone point 2

        return parent[x];
    }

    bool sameRoot(int x, int y)
    {
        return findRoot(x) == findRoot(y);
    }
}
```

## Go
```go
var parent []int

func findRedundantConnection(edges [][]int) []int {
    parent = make([]int, len(edges) + 1)
    for i := 0; i < len(parent); i++ {
        parent[i] = i
    }

    for _, edge := range edges {
        if sameRoot(edge[0], edge[1]) {
            return edge
        }

        unite(edge[0], edge[1])
    }

    return nil
}

func unite(x, y int) {
    rootX := findRoot(x)
    rootY := findRoot(y)

    parent[rootY] = rootX // Error-prone point 1
}

func findRoot(x int) int {
    if x == parent[x] {
        return x
    }

    parent[x] = findRoot(parent[x]) // Error-prone point 2

    return parent[x]
}

func sameRoot(x, y int) bool {
    return findRoot(x) == findRoot(y)
}
```

## Ruby
```ruby
def find_redundant_connection(edges)
  @parent = []
  (0..edges.size).each { |i| @parent << i }

  edges.each do |edge|
    if same_root(edge[0], edge[1])
      return edge
    end

    unite(edge[0], edge[1])
  end
end

def unite(x, y)
  root_x = find_root(x)
  root_y = find_root(y)

  @parent[root_y] = root_x # Error-prone point 1
end

def find_root(x)
  if x == @parent[x]
    return x
  end

  @parent[x] = find_root(@parent[x]) # Error-prone point 2

  @parent[x]
end

def same_root(x, y)
  find_root(x) == find_root(y)
end
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
