# 3558. 分配边权重的方案数 I - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 coder.id 打造你的开发者个人IP →**](https://www.coder.id)

访问原文链接：[3558. 分配边权重的方案数 I - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/3558-number-of-ways-to-assign-edge-weights-i)，体验更佳！

力扣链接：[3558. 分配边权重的方案数 I](https://leetcode.cn/problems/number-of-ways-to-assign-edge-weights-i), 难度等级：**困难**。

## LeetCode “3558. 分配边权重的方案数 I”问题描述

有一棵 `n` 个节点的无向树，节点按从 `1` 到 `n` 编号，树的根节点是节点 `1`。这棵树由一个长度为 `n - 1` 的二维整数数组 `edges` 表示，其中 `edges[i] = [u_i, v_i]` 表示节点 `u_i` 和 `v_i` 之间有一条边。

最初，所有边的权重都是 `0`。你必须为每条边分配一个权重，权重可以是 **1** 或 **2**。

任意两个节点 `u` 和 `v` 之间路径的 **成本** 是连接它们的路径上所有边的权重之和。

选择位于 **最大** 深度的任意一个节点 `x`。返回在从节点 `1` 到 `x` 的路径上分配边权重的方案数，使得该路径的总成本为 **奇数**。

由于答案可能很大，请将其对 `10^9 + 7` **取余** 后返回。

**注意：** 忽略所有 **不在** 从节点 `1` 到 `x` 路径上的边。

### [示例 1]

**输入**: `edges = [[1,2]]`

**输出**: `1`

**解释**: 

<ul>
<li>从节点 1 到节点 2 的路径包含一条边（<code>1 → 2</code>）。</li>
<li>分配权重 1 会使成本变为奇数，而分配权重 2 会使成本变为偶数。因此，有效的分配方案数是 1。</li>
</ul>


### [示例 2]

**输入**: `edges = [[1,2],[1,3],[3,4],[3,5]]`

**输出**: `2`

**解释**: 

<ul>
<li>最大深度为 2，节点 4 和 5 位于同一深度。可以选择任一节点进行处理。</li>
<li>例如，从节点 1 到节点 4 的路径包含两条边（<code>1 → 3</code> 和 <code>3 → 4</code>）。</li>
<li>分配权重 (1,2) 或 (2,1) 会导致成本为奇数。因此，有效的分配方案数是 2。</li>
</ul>


### [约束]

- `2 <= n <= 10^5`
- `edges.length == n - 1`
- `edges[i] == [u_i, v_i]`
- `1 <= u_i, v_i <= n`
- `edges` 表示一棵有效的树。

### [Hints]

<details>
  <summary>提示 1</summary>
  How can we find the maximum depth of the tree rooted at node 1?

  
</details>

<details>
  <summary>提示 2</summary>
  Use Breadth-First Search (BFS) or Depth-First Search (DFS) to find the node `x` at the maximum depth and determine its distance `d` from the root.

  
</details>

<details>
  <summary>提示 3</summary>
  Since we only care about the `d` edges in the path from node 1 to `x`, each edge can be assigned a weight of 1 or 2.

  
</details>

<details>
  <summary>提示 4</summary>
  The total cost is odd if and only if there is an odd number of edges with weight 1. Using combinatorial math, the number of such assignments is `2^(d-1)`.

  
</details>

## 思路

问题要求我们为从节点 1 到最大深度的节点 `x` 的路径上的边分配权重（`1` 或 `2`），使得权重之和为奇数，并返回方案数。

首先，我们意识到除了这条路径之外的树结构并不会限制我们在这条路径上的分配，因为题目明确说明：“忽略所有不在从节点 1 到 x 路径上的边”。

如果从节点 1 到 `x` 的路径长度为 `d` 条边，我们需要为这 `d` 条边从 `{1, 2}` 中选择权重，使得它们的和为奇数。当且仅当选择的 `1` 的数量为奇数时，总和才为奇数（因为 `2` 是偶数，不会改变总和的奇偶性）。

根据二项式系数的性质，从 `d` 个元素中选择奇数个元素的方案数为 `2^{d-1}`（对于 `d > 0`）。因此，问题可以简化为两个步骤：
1. 使用 BFS 或 DFS 找到最大深度 `d`（距离节点 1 的边数）。
2. 使用快速幂计算 `2^{d-1} \pmod{10^9+7}`。

## 步骤

1. **构建图：** 将 `edges` 数组转换为邻接表来表示这棵树。
2. **寻找最大深度：** 初始化一个队列，从节点 1 开始进行 BFS（广度优先搜索）。记录已访问的节点以避免循环。逐层遍历树以找到最大深度 `d`（边数）。
3. **计算组合数：** 如果 `d == 0`，返回 0。否则，我们需要计算 `2^{d-1} \pmod{10^9 + 7}`。
4. **快速幂取模：** 使用快速幂算法（或语言内置的幂函数）高效地计算结果并防止整数溢出。

## 复杂度

> - **时间复杂度：** `O(n)`。构建图需要 `O(n)` 的时间。BFS 遍历精确地访问每个节点和每条边一次，需要 `O(n)` 的时间。快速幂取模需要 `O(\log d)` 的时间，即 `O(\log n)`。总体时间复杂度是线性的 `O(n)`。
- **空间复杂度：** `O(n)`。邻接表需要 `O(n)` 的空间来存储图。BFS 的队列和访问记录集合/数组也需要最多 `O(n)` 的空间。因此，整体空间复杂度为 `O(n)`。

- 时间复杂度: ``.
- 空间复杂度: ``.

## Python

```python
class Solution:
    def assignEdgeWeights(self, edges: List[List[int]]) -> int:
        MOD = 1_000_000_007
        
        # Determine the number of nodes
        n = len(edges) + 1
        
        # Build the adjacency list for the tree
        graph = [[] for _ in range(n + 1)]
        for u, v in edges:
            graph[u].append(v)
            graph[v].append(u)
            
        # BFS to find the maximum depth from node 1
        queue = collections.deque([1])
        seen = {1}
        
        step = 0
        while queue:
            # Process all nodes at the current depth
            for _ in range(len(queue)):
                u = queue.popleft()
                for v in graph[u]:
                    if v not in seen:
                        queue.append(v)
                        seen.add(v)
            step += 1
            
        # step tracks the number of nodes in the path (levels)
        # The number of edges d is step - 1
        # If d > 0, the answer is 2^(d-1) % MOD
        # which is 2^(step - 2) % MOD
        if step > 1:
            return pow(2, step - 2, MOD)
        return 0
```

## Java

```java
class Solution {
    public int assignEdgeWeights(int[][] edges) {
        int n = edges.length + 1;
        
        // Build the graph using an array of lists
        List<Integer>[] graph = new ArrayList[n + 1];
        for (int i = 1; i <= n; i++) {
            graph[i] = new ArrayList<>();
        }
        
        for (int[] edge : edges) {
            graph[edge[0]].add(edge[1]);
            graph[edge[1]].add(edge[0]);
        }
        
        // BFS to find the maximum depth (number of edges)
        Queue<Integer> queue = new LinkedList<>();
        boolean[] visited = new boolean[n + 1];
        
        queue.offer(1);
        visited[1] = true;
        
        int maxDepthEdges = -1; // -1 because the root level has 0 edges
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                int u = queue.poll();
                for (int v : graph[u]) {
                    if (!visited[v]) {
                        visited[v] = true;
                        queue.offer(v);
                    }
                }
            }
            maxDepthEdges++;
        }
        
        // If max depth is 0, no edges exist to assign
        if (maxDepthEdges <= 0) {
            return 0;
        }
        
        // Calculate 2^(maxDepthEdges - 1) % MOD
        return modPow(2, maxDepthEdges - 1, 1_000_000_007);
    }
    
    // Helper function for modular exponentiation
    private int modPow(long base, long exp, int mod) {
        long result = 1;
        base %= mod;
        while (exp > 0) {
            if ((exp & 1) == 1) {
                result = (result * base) % mod;
            }
            base = (base * base) % mod;
            exp >>= 1;
        }
        return (int) result;
    }
}
```

## JavaScript

```javascript
/**
 * @param {number[][]} edges
 * @return {number}
 */
var assignEdgeWeights = function(edges) {
    const MOD = 1000000007n;
    const n = edges.length + 1;
    
    // Build adjacency list
    const graph = Array.from({ length: n + 1 }, () => []);
    for (const [u, v] of edges) {
        graph[u].push(v);
        graph[v].push(u);
    }
    
    // BFS to find max depth
    let queue = [1];
    const visited = new Uint8Array(n + 1);
    visited[1] = 1;
    
    let maxDepthEdges = -1;
    
    while (queue.length > 0) {
        const nextQueue = [];
        for (const u of queue) {
            for (const v of graph[u]) {
                if (visited[v] === 0) {
                    visited[v] = 1;
                    nextQueue.push(v);
                }
            }
        }
        queue = nextQueue;
        maxDepthEdges++;
    }
    
    if (maxDepthEdges <= 0) return 0;
    
    // Calculate 2^(maxDepthEdges - 1) % MOD using BigInt
    let base = 2n;
    let exp = BigInt(maxDepthEdges - 1);
    let result = 1n;
    
    while (exp > 0n) {
        if (exp % 2n === 1n) {
            result = (result * base) % MOD;
        }
        base = (base * base) % MOD;
        exp /= 2n;
    }
    
    return Number(result);
};
```

## C++

```cpp
class Solution {
public:
    int assignEdgeWeights(vector<vector<int>>& edges) {
        int n = edges.size() + 1;
        
        // Build the graph
        vector<vector<int>> graph(n + 1);
        for (const auto& edge : edges) {
            graph[edge[0]].push_back(edge[1]);
            graph[edge[1]].push_back(edge[0]);
        }
        
        // BFS to find max depth
        queue<int> q;
        vector<bool> visited(n + 1, false);
        
        q.push(1);
        visited[1] = true;
        
        int maxDepthEdges = -1;
        
        while (!q.empty()) {
            int size = q.size();
            for (int i = 0; i < size; ++i) {
                int u = q.front();
                q.pop();
                
                for (int v : graph[u]) {
                    if (!visited[v]) {
                        visited[v] = true;
                        q.push(v);
                    }
                }
            }
            maxDepthEdges++;
        }
        
        if (maxDepthEdges <= 0) return 0;
        
        // Calculate 2^(maxDepthEdges - 1) % MOD
        long long base = 2;
        long long exp = maxDepthEdges - 1;
        long long mod = 1e9 + 7;
        long long result = 1;
        
        while (exp > 0) {
            if (exp % 2 == 1) {
                result = (result * base) % mod;
            }
            base = (base * base) % mod;
            exp /= 2;
        }
        
        return result;
    }
};
```

## C#

```csharp
public class Solution {
    public int AssignEdgeWeights(int[][] edges) {
        int n = edges.Length + 1;
        
        // Build the adjacency list
        List<int>[] graph = new List<int>[n + 1];
        for (int i = 1; i <= n; i++) {
            graph[i] = new List<int>();
        }
        
        foreach (var edge in edges) {
            graph[edge[0]].Add(edge[1]);
            graph[edge[1]].Add(edge[0]);
        }
        
        // BFS traversal
        Queue<int> queue = new Queue<int>();
        bool[] visited = new bool[n + 1];
        
        queue.Enqueue(1);
        visited[1] = true;
        
        int maxDepthEdges = -1;
        
        while (queue.Count > 0) {
            int size = queue.Count;
            for (int i = 0; i < size; i++) {
                int u = queue.Dequeue();
                foreach (int v in graph[u]) {
                    if (!visited[v]) {
                        visited[v] = true;
                        queue.Enqueue(v);
                    }
                }
            }
            maxDepthEdges++;
        }
        
        if (maxDepthEdges <= 0) return 0;
        
        // Modular exponentiation
        long baseVal = 2;
        long exp = maxDepthEdges - 1;
        long mod = 1000000007;
        long result = 1;
        
        while (exp > 0) {
            if ((exp & 1) == 1) {
                result = (result * baseVal) % mod;
            }
            baseVal = (baseVal * baseVal) % mod;
            exp >>= 1;
        }
        
        return (int)result;
    }
}
```

## Go

```go
func assignEdgeWeights(edges [][]int) int {
    n := len(edges) + 1
    
    // Build adjacency list
    graph := make([][]int, n + 1)
    for _, edge := range edges {
        u, v := edge[0], edge[1]
        graph[u] = append(graph[u], v)
        graph[v] = append(graph[v], u)
    }
    
    // BFS to find max depth
    queue := []int{1}
    visited := make([]bool, n + 1)
    visited[1] = true
    
    maxDepthEdges := -1
    
    for len(queue) > 0 {
        size := len(queue)
        for i := 0; i < size; i++ {
            u := queue[i]
            for _, v := range graph[u] {
                if !visited[v] {
                    visited[v] = true
                    queue = append(queue, v)
                }
            }
        }
        queue = queue[size:]
        maxDepthEdges++
    }
    
    if maxDepthEdges <= 0 {
        return 0
    }
    
    // Modular exponentiation
    base := int64(2)
    exp := int64(maxDepthEdges - 1)
    mod := int64(1000000007)
    result := int64(1)
    
    for exp > 0 {
        if exp % 2 == 1 {
            result = (result * base) % mod
        }
        base = (base * base) % mod
        exp /= 2
    }
    
    return int(result)
}
```

## Ruby

```ruby
# @param {Integer[][]} edges
# @return {Integer}
def assign_edge_weights(edges)
    n = edges.length + 1
    
    # Build graph
    graph = Array.new(n + 1) { [] }
    edges.each do |u, v|
        graph[u] << v
        graph[v] << u
    end
    
    # BFS traversal
    queue = [1]
    visited = Array.new(n + 1, false)
    visited[1] = true
    
    max_depth_edges = -1
    
    while !queue.empty?
        next_queue = []
        queue.each do |u|
            graph[u].each do |v|
                if !visited[v]
                    visited[v] = true
                    next_queue << v
                end
            end
        end
        queue = next_queue
        max_depth_edges += 1
    end
    
    return 0 if max_depth_edges <= 0
    
    # Calculate 2^(max_depth_edges - 1) % (10^9 + 7)
    # Ruby's pow method natively supports modulo arithmetic
    2.pow(max_depth_edges - 1, 1_000_000_007)
end
```

## Rust

```rust
use std::collections::VecDeque;

impl Solution {
    pub fn assign_edge_weights(edges: Vec<Vec<i32>>) -> i32 {
        let n = edges.len() + 1;
        
        // Build adjacency list
        let mut graph = vec![Vec::new(); n + 1];
        for edge in edges.iter() {
            let u = edge[0] as usize;
            let v = edge[1] as usize;
            graph[u].push(v);
            graph[v].push(u);
        }
        
        // BFS to find max depth
        let mut queue = VecDeque::new();
        let mut visited = vec![false; n + 1];
        
        queue.push_back(1);
        visited[1] = true;
        
        let mut max_depth_edges = -1;
        
        while !queue.is_empty() {
            let size = queue.len();
            for _ in 0..size {
                if let Some(u) = queue.pop_front() {
                    for &v in graph[u].iter() {
                        if !visited[v] {
                            visited[v] = true;
                            queue.push_back(v);
                        }
                    }
                }
            }
            max_depth_edges += 1;
        }
        
        if max_depth_edges <= 0 {
            return 0;
        }
        
        // Modular exponentiation
        let mut base: i64 = 2;
        let mut exp = (max_depth_edges - 1) as i64;
        let mod_val: i64 = 1_000_000_007;
        let mut result: i64 = 1;
        
        while exp > 0 {
            if exp % 2 == 1 {
                result = (result * base) % mod_val;
            }
            base = (base * base) % mod_val;
            exp /= 2;
        }
        
        result as i32
    }
}
```

## Kotlin

```kotlin
import java.util.LinkedList
import java.util.Queue

class Solution {
    fun assignEdgeWeights(edges: Array<IntArray>): Int {
        val n = edges.size + 1
        
        // Build graph
        val graph = Array(n + 1) { mutableListOf<Int>() }
        for (edge in edges) {
            graph[edge[0]].add(edge[1])
            graph[edge[1]].add(edge[0])
        }
        
        // BFS to determine max depth
        val queue: Queue<Int> = LinkedList()
        val visited = BooleanArray(n + 1)
        
        queue.offer(1)
        visited[1] = true
        
        var maxDepthEdges = -1
        
        while (queue.isNotEmpty()) {
            val size = queue.size
            for (i in 0 until size) {
                val u = queue.poll()
                for (v in graph[u]) {
                    if (!visited[v]) {
                        visited[v] = true
                        queue.offer(v)
                    }
                }
            }
            maxDepthEdges++
        }
        
        if (maxDepthEdges <= 0) return 0
        
        // Modular exponentiation
        var base = 2L
        var exp = (maxDepthEdges - 1).toLong()
        val mod = 1_000_000_007L
        var result = 1L
        
        while (exp > 0) {
            if (exp % 2L == 1L) {
                result = (result * base) % mod
            }
            base = (base * base) % mod
            exp /= 2L
        }
        
        return result.toInt()
    }
}
```

## Swift

```swift
class Solution {
    func assignEdgeWeights(_ edges: [[Int]]) -> Int {
        let n = edges.count + 1
        
        // Build adjacency list
        var graph = Array(repeating: [Int](), count: n + 1)
        for edge in edges {
            graph[edge[0]].append(edge[1])
            graph[edge[1]].append(edge[0])
        }
        
        // BFS to find max depth
        var queue = [1]
        var visited = Array(repeating: false, count: n + 1)
        visited[1] = true
        
        var maxDepthEdges = -1
        
        while !queue.isEmpty {
            var nextQueue = [Int]()
            for u in queue {
                for v in graph[u] {
                    if !visited[v] {
                        visited[v] = true
                        nextQueue.append(v)
                    }
                }
            }
            queue = nextQueue
            maxDepthEdges += 1
        }
        
        if maxDepthEdges <= 0 { return 0 }
        
        // Calculate 2^(maxDepthEdges - 1) % MOD
        var base = 2
        var exp = maxDepthEdges - 1
        let mod = 1_000_000_007
        var result = 1
        
        while exp > 0 {
            if exp % 2 == 1 {
                result = (result * base) % mod
            }
            base = (base * base) % mod
            exp /= 2
        }
        
        return result
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**coder.id**](https://www.coder.id) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.coder.id`，极具职业含金量的专属域名。

>
> [**立即前往 coder.id 打造你的个人品牌 →**](https://www.coder.id)

---

访问原文链接：[3558. 分配边权重的方案数 I - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/3558-number-of-ways-to-assign-edge-weights-i)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

