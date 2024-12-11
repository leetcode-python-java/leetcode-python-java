# 797. All Paths From Source to Target
LeetCode problem: [797. All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/)

## LeetCode problem description
Given a directed acyclic graph (**DAG**) of `n` nodes labeled from `0` to `n - 1`, find all possible paths from node `0` to node `n - 1` and return them in **any order**.

The graph is given as follows: `graph[i]` is a list of all nodes you can visit from node `i` (i.e., there is a directed edge from node `i` to node `graph[i][j]`).

### Example 1
![](../images/examples/0797_1.jpg)
```
Input: graph = [[1,2],[3],[3],[]]
Output: [[0,1,3],[0,2,3]]
Explanation: There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
```

### Example 2
![](../images/examples/0797_2.jpg)
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

## Thoughts
This problem can be solved using **Depth-First Search of a Graph**.

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Complexity
* Time: `O(2**n)`.
* Space: `O(n)`.

## Python
### Solution 1: New array as parameter
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

        target_nodes = self.graph[node]

        for target_node in target_nodes:
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

        target_nodes = self.graph[node]

        for target_node in target_nodes:
            self.path.append(target_node)
            self.dfs(target_node)
            self.path.pop()
```

## Java
```java

```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript

```

## C#
```c#
```

## Go
```go
// Original article is at https://github.com/gazeldx/leetcode-best-practice
// Welcome to create a PR to complete the code of this language, thanks!
```

## Ruby
```ruby
# Original article is at https://github.com/gazeldx/leetcode-best-practice
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
