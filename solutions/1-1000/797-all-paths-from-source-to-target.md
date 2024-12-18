# 797. All Paths From Source to Target
LeetCode problem link: [797. All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/)

## LeetCode problem description
Given a directed acyclic graph (**DAG**) of `n` nodes labeled from `0` to `n - 1`, find all possible paths from node `0` to node `n - 1` and return them in **any order**.

The graph is given as follows: `graph[i]` is a list of all nodes you can visit from node `i` (i.e., there is a directed edge from node `i` to node `graph[i][j]`).

### Example 1
![](../../images/examples/797_1.jpg)
```
Input: graph = [[1,2],[3],[3],[]]
Output: [[0,1,3],[0,2,3]]
Explanation: There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
```

### Example 2
![](../../images/examples/797_2.jpg)
```
Input: graph = [[4,3,1],[3,2,4],[3],[4],[]]
Output: [[0,4],[0,3,4],[0,1,3,4],[0,1,2,3,4],[0,1,4]]
```

### Constraints
- `n == graph.length`
- `2 <= n <= 15`
- `0 <= graph[i][j] < n`
- `graph[i][j] != i` (i.e., there will be no self-loops).
- All the elements of `graph[i]` are **unique**.
- The input graph is **guaranteed** to be a **DAG**.

# Intuition
This problem can be solved using **Depth-First Search of a Graph**.

# Approach
1. From node `0`, visit all of its neighbors `graph[node]` in an iteration.
2. In the iteration, recursively call the `dfs` function to visit all the paths.
3. Use an array `path` to save the path (node itself inclusive).
4. Around the `dfs()` call code are the `path.push(node)` (use `node`) and `path.pop()` (undo use `node`).
5. Use an array `paths` to save the results.

## Complexity
* Time: `O(2**n)`.
* Space: `O(n)`.

## Python
### Solution 1: New array as 'path' parameter
```python
class Solution:
    def __init__(self):
        self.paths = []
        self.graph = None

    def allPathsSourceTarget(self, graph: List[List[int]]) -> List[List[int]]:
        self.graph = graph

        self.dfs(0, [0])

        return self.paths
    
    def dfs(self, node, path):
        if node == len(self.graph) - 1:
            self.paths.append(path.copy())
            return

        for target_node in self.graph[node]:
            self.dfs(target_node, path + [target_node])
```

### Solution 2: More efficient by reusing one array (recommended)
```python
class Solution:
    def __init__(self):
        self.paths = []
        self.path = [0]
        self.graph = None

    def allPathsSourceTarget(self, graph: List[List[int]]) -> List[List[int]]:
        self.graph = graph

        self.dfs(0)

        return self.paths

    def dfs(self, node):
        if node == len(self.graph) - 1:
            self.paths.append(self.path.copy())
            return

        for target_node in self.graph[node]:
            self.path.append(target_node)

            self.dfs(target_node)

            self.path.pop()
```

## Java
```java
class Solution {
    List<List<Integer>> paths = new ArrayList<>();
    List<Integer> path = new ArrayList<>();
    int[][] graph;

    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        this.graph = graph;
        path.add(0);

        dfs(0);

        return paths;
    }

    void dfs(int node) {
        if (node == graph.length - 1) {
            paths.add(new ArrayList<>(path));
            return;
        }

        for (int targetNode : graph[node]) {
            path.add(targetNode);

            dfs(targetNode);

            path.removeLast();
        }
    }
}
```

## C++
```cpp
class Solution {
private:
    vector<vector<int>> paths_;
    vector<int> path_;
    vector<vector<int>> graph_;

    void dfs(int node) {
        if (node == graph_.size() - 1) {
            paths_.push_back(path_);
            return;
        }

        for (int target_node : graph_[node]) {
            path_.push_back(target_node);

            dfs(target_node);

            path_.pop_back();
        }
    }

public:
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
        graph_ = graph;
        path_.push_back(0);

        dfs(0);

        return paths_;
    }
};
```

## JavaScript
```javascript
let paths
let path
let graph

var allPathsSourceTarget = function (graph_) {
  graph = graph_
  paths = []
  path = [0]

  dfs(0)

  return paths
};

function dfs(node) {
  if (node === graph.length - 1) {
    paths.push([...path])
    return
  }

  for (const targetNode of graph[node]) {
    path.push(targetNode)

    dfs(targetNode)

    path.pop()
  }
}
```

## C#
```c#
public class Solution
{
    IList<IList<int>> paths = new List<IList<int>>();
    IList<int> path = new List<int>();
    int[][] graph;

    public IList<IList<int>> AllPathsSourceTarget(int[][] graph)
    {
        this.graph = graph;
        path.Add(0);

        dfs(0);

        return paths;
    }

    void dfs(int node)
    {
        if (node == graph.Length - 1)
        {
            paths.Add(path.ToList());
            return;
        }

        foreach (int targetNode in graph[node])
        {
            path.Add(targetNode);

            dfs(targetNode);

            path.RemoveAt(path.Count - 1);
        }
    }
}
```

## Go
```go
var (
    paths [][]int
    path []int
    graph [][]int
)

func allPathsSourceTarget(graph_ [][]int) [][]int {
    graph = graph_
    paths = nil
    path = []int{0}

    dfs(0)

    return paths
}

func dfs(node int) {
    if (node == len(graph) - 1) {
        paths = append(paths, slices.Clone(path))
        return
    }

    for _, targetNode := range graph[node] {
        path = append(path, targetNode)

        dfs(targetNode)

        path = path[:len(path) - 1]
    }
}
```

## Ruby
```ruby
def all_paths_source_target(graph)
  @graph = graph
  @paths = []
  @path = [0]

  dfs(0)

  @paths
end

def dfs(node)
  if node == @graph.size - 1
    @paths.append(@path.clone)
    return
  end

  @graph[node].each do |target_node|
    @path << target_node

    dfs(target_node)

    @path.pop
  end
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
