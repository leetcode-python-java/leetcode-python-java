# 3558. Number of Ways to Assign Edge Weights I - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at coder.id →**](https://www.coder.id)

Visit original link: [3558. Number of Ways to Assign Edge Weights I - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/3558-number-of-ways-to-assign-edge-weights-i) for a better experience!

LeetCode link: [3558. Number of Ways to Assign Edge Weights I](https://leetcode.com/problems/number-of-ways-to-assign-edge-weights-i), difficulty: **Hard**.

## LeetCode description of "3558. Number of Ways to Assign Edge Weights I"

There is an undirected tree with `n` nodes labeled from 1 to `n`, rooted at node 1. The tree is represented by a 2D integer array `edges` of length `n - 1`, where `edges[i] = [u_i, v_i]` indicates that there is an edge between nodes `u_i` and `v_i`.

Initially, all edges have a weight of 0. You must assign each edge a weight of either **1** or **2**.

The **cost** of a path between any two nodes `u` and `v` is the total weight of all edges in the path connecting them.

Select any one node `x` at the **maximum** depth. Return the number of ways to assign edge weights in the path from node 1 to `x` such that its total cost is **odd**.

Since the answer may be large, return it **modulo** `10^9 + 7`.

**Note:** Ignore all edges **not** in the path from node 1 to `x`.

### [Example 1]

**Input**: `edges = [[1,2]]`

**Output**: `1`

**Explanation**: 

<ul>
<li>The path from Node 1 to Node 2 consists of one edge (<code>1 → 2</code>).</li>
<li>Assigning weight 1 makes the cost odd, while 2 makes it even. Thus, the number of valid assignments is 1.</li>
</ul>


### [Example 2]

**Input**: `edges = [[1,2],[1,3],[3,4],[3,5]]`

**Output**: `2`

**Explanation**: 

<ul>
<li>The maximum depth is 2, with nodes 4 and 5 at the same depth. Either node can be selected for processing.</li>
<li>For example, the path from Node 1 to Node 4 consists of two edges (<code>1 → 3</code> and <code>3 → 4</code>).</li>
<li>Assigning weights (1,2) or (2,1) results in an odd cost. Thus, the number of valid assignments is 2.</li>
</ul>


### [Constraints]

- `2 <= n <= 10^5`
- `edges.length == n - 1`
- `edges[i] == [u_i, v_i]`
- `1 <= u_i, v_i <= n`
- `edges` represents a valid tree.

### [Hints]

<details>
  <summary>Hint 1</summary>
  How can we find the maximum depth of the tree rooted at node 1?

  
</details>

<details>
  <summary>Hint 2</summary>
  Use Breadth-First Search (BFS) or Depth-First Search (DFS) to find the node `x` at the maximum depth and determine its distance `d` from the root.

  
</details>

<details>
  <summary>Hint 3</summary>
  Since we only care about the `d` edges in the path from node 1 to `x`, each edge can be assigned a weight of 1 or 2.

  
</details>

<details>
  <summary>Hint 4</summary>
  The total cost is odd if and only if there is an odd number of edges with weight 1. Using combinatorial math, the number of such assignments is `2^(d-1)`.

  
</details>

## Intuition

The problem asks for the number of ways to assign weights (`1` or `2`) to the edges in the path from node 1 to a node `x` at the maximum depth, such that the sum of the weights is odd. 

First, we recognize that the actual structure of the tree beyond this path does not restrict our assignment on this specific path, because the problem explicitly states: "Ignore all edges not in the path from node 1 to x."

If the path from node 1 to `x` has a length of `d` edges, we need to choose weights from `{1, 2}` for these `d` edges so that their sum is odd. The sum is odd if and only if the number of `1`s chosen is odd (since `2` is even and does not change the parity of the sum).

By the properties of binomial coefficients, the number of ways to choose an odd number of items from `d` items is `2^{d-1}` (for `d > 0`). Thus, the problem simplifies to two steps:
1. Find the maximum depth `d` (number of edges from node 1) using BFS or DFS.
2. Calculate `2^{d-1} \pmod{10^9+7}` using modular exponentiation.

## Step-by-Step Solution

1. **Build the Graph:** Convert the `edges` array into an adjacency list to represent the tree.
2. **Find Maximum Depth:** Initialize a queue for BFS starting from node 1. Track visited nodes to avoid cycles. Level by level, traverse the tree to find the maximum depth `d` (number of edges).
3. **Calculate Combinations:** If `d == 0`, return 0. Otherwise, we need to compute `2^{d-1} \pmod{10^9 + 7}`.
4. **Modular Exponentiation:** Use a fast power algorithm (or built-in functions where available) to compute the result efficiently and avoid overflow.

## Complexity

> - **Time Complexity:** `O(n)`. Building the graph takes `O(n)` time. The BFS traversal visits each node and edge exactly once, taking `O(n)` time. The modular exponentiation takes `O(\log d)` time, which is `O(\log n)`. The overall time complexity is linear `O(n)`.
- **Space Complexity:** `O(n)`. The adjacency list requires `O(n)` space to store the graph. The BFS queue and the visited set/array also require up to `O(n)` space. Thus, the overall space complexity is `O(n)`.

- Time complexity: ``.
- Space complexity: ``.

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

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**coder.id**](https://www.coder.id) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.coder.id`.
>
> [**Build Your Programmer Brand at coder.id →**](https://www.coder.id)

---

Visit original link: [3558. Number of Ways to Assign Edge Weights I - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/3558-number-of-ways-to-assign-edge-weights-i) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

