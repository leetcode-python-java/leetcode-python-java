# 1042. 不邻接植花 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[1042. 不邻接植花 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/1042-flower-planting-with-no-adjacent)，体验更佳！

力扣链接：[1042. 不邻接植花](https://leetcode.cn/problems/flower-planting-with-no-adjacent), 难度等级：**中等**。

## LeetCode “1042. 不邻接植花”问题描述

有 `n` 个花园，按从 `1` 到 `n` 标记。另有数组 `paths`，其中 `paths[i] = [x_i, y_i]` 描述了花园 `x_i` 到花园 `y_i` 的双向路径。在每个花园中，你打算种下四种花之一。

另外，所有花园 **最多** 有 3 条路径可以进入或离开。

你需要为每个花园选择一种花，使得通过路径相连的任何两个花园中的花的种类互不相同。

以数组形式返回 **任一** 可行的方案作为答案 `answer`，其中 `answer[i]` 为在第 `(i+1)` 个花园中种植的花的种类。花的种类用  `1`、`2`、`3`、`4` 表示。保证存在答案。

### [示例 1]

**输入**: `n = 3, paths = [[1,2],[2,3],[3,1]]`

**输出**: `[1,2,3]`

**解释**: 

<p>花园 1 和 2 花的种类不同。<br>
花园 2 和 3 花的种类不同。<br>
花园 3 和 1 花的种类不同。<br>
因此，[1,2,3] 是一个满足题意的答案。其他满足题意的答案有 [1,2,4]、[1,4,2] 和 [3,2,1]。</p>


### [示例 2]

**输入**: `n = 4, paths = [[1,2],[3,4]]`

**输出**: `[1,2,1,2]`

### [示例 3]

**输入**: `n = 4, paths = [[1,2],[2,3],[3,4],[4,1],[1,3],[2,4]]`

**输出**: `[1,2,3,4]`

### [约束]

- `1 <= n <= 10^4`
- `0 <= paths.length <= 2 * 10^4`
- `paths[i].length == 2`
- `1 <= x_i, y_i <= n`
- `x_i != y_i`
- 每个花园 **最多** 有 3 条路径可以进入或离开

### [Hints]

<details>
  <summary>提示 1</summary>
  Since each garden has at most 3 paths, we can always find an available color from the 4 colors.

  
</details>

## 思路

题目要求我们为 `n` 个花园分配 4 种花（颜色）中的一种，使得相连的花园种的花种类互不相同。

这是一个经典的图染色问题。

这里的关键约束是：**每个花园最多只有 3 条路径进入或离开**。

这意味着对于任何一个给定的花园，它最多只有 3 个相邻的花园。

因为我们有 4 种不同的花可供选择，所以无论它的邻居种了什么花，当前花园**总是**至少剩下一种花可以种。

因此，我们可以使用一种简单的**贪心算法（Greedy Algorithm）**：

1. 构建一个邻接表来表示花园和路径的图结构。

2. 从 `1` 到 `n` 遍历每一个花园。

3. 对于当前花园，检查其所有邻居已经种植的花的种类。

4. 从 `{1, 2, 3, 4}` 中挑选一种邻居没有使用过的花，分配给当前花园。

这种方法保证了在单次遍历中就能找到一个有效的配置，而不需要进行回溯。

## 步骤

1. **构建图**：创建一个邻接表 `graph`，其中 `graph[i]` 存储花园 `i` 的所有邻居。注意花园的编号是从 1 开始的。
2. **初始化答案数组**：创建一个大小为 `n` 的数组 `answer` 并初始化为 `0`，其中 `0` 表示该花园尚未种花。
3. **遍历所有花园**：循环变量 `i` 从 `1` 到 `n`（或 `0` 到 `n-1`，取决于索引方式）：
   - 创建一个布尔数组或集合 `used`，用来记录当前花园的邻居已经使用的颜色。
   - 遍历花园 `i` 的每一个邻居 `adj`，如果 `answer[adj]` 不为 `0`，则在 `used` 中将该颜色标记为已使用。
   - 遍历颜色 `1` 到 `4`，找到第一个未被 `used` 标记的颜色，并将其赋值给 `answer[i]`。
4. **返回结果**：循环结束后，返回 `answer` 数组。

## 复杂度

> - **时间复杂度：** `O(n + m)`，其中 `n` 是花园的数量，`m` 是路径（边）的数量。构建图需要 `O(m)` 的时间。遍历每个花园及其邻居总共需要 `O(n + m)` 的时间，因为每条边最多被处理两次。检查可用颜色每个花园只需 `O(1)` 的时间，因为总共只有 4 种颜色。
- **空间复杂度：** `O(n + m)`，用于存储表示图的邻接表。`answer` 数组需要 `O(n)` 的空间。

- 时间复杂度: `O(n + m)`.
- 空间复杂度: `O(n + m)`.

## Python

```python
class Solution:
    def gardenNoAdj(self, n: int, paths: List[List[int]]) -> List[int]:
        # Build the adjacency list for the graph
        graph = [[] for _ in range(n)]
        for u, v in paths:
            graph[u - 1].append(v - 1)
            graph[v - 1].append(u - 1)
        
        # answer array to store the flower type for each garden
        answer = [0] * n
        
        # Iterate through each garden
        for i in range(n):
            # Record the colors used by the neighbors
            used = [False] * 5
            for adj in graph[i]:
                if answer[adj] != 0:
                    used[answer[adj]] = True
            
            # Find the first available color from 1 to 4
            for color in range(1, 5):
                if not used[color]:
                    answer[i] = color
                    break
                    
        return answer
```

## Java

```java
class Solution {
    public int[] gardenNoAdj(int n, int[][] paths) {
        // Build the adjacency list for the graph
        List<Integer>[] graph = new ArrayList[n];
        for (int i = 0; i < n; i++) {
            graph[i] = new ArrayList<>();
        }
        for (int[] path : paths) {
            graph[path[0] - 1].add(path[1] - 1);
            graph[path[1] - 1].add(path[0] - 1);
        }
        
        // answer array to store the flower type for each garden
        int[] answer = new int[n];
        
        // Iterate through each garden
        for (int i = 0; i < n; i++) {
            // Record the colors used by the neighbors
            boolean[] used = new boolean[5];
            for (int adj : graph[i]) {
                if (answer[adj] != 0) {
                    used[answer[adj]] = true;
                }
            }
            
            // Find the first available color from 1 to 4
            for (int color = 1; color <= 4; color++) {
                if (!used[color]) {
                    answer[i] = color;
                    break;
                }
            }
        }
        
        return answer;
    }
}
```

## JavaScript

```javascript
/**
 * @param {number} n
 * @param {number[][]} paths
 * @return {number[]}
 */
var gardenNoAdj = function(n, paths) {
    // Build the adjacency list for the graph
    const graph = Array.from({ length: n }, () => []);
    for (const [u, v] of paths) {
        graph[u - 1].push(v - 1);
        graph[v - 1].push(u - 1);
    }
    
    // answer array to store the flower type for each garden
    const answer = new Array(n).fill(0);
    
    // Iterate through each garden
    for (let i = 0; i < n; i++) {
        // Record the colors used by the neighbors
        const used = new Array(5).fill(false);
        for (const adj of graph[i]) {
            if (answer[adj] !== 0) {
                used[answer[adj]] = true;
            }
        }
        
        // Find the first available color from 1 to 4
        for (let color = 1; color <= 4; color++) {
            if (!used[color]) {
                answer[i] = color;
                break;
            }
        }
    }
    
    return answer;
};
```

## C++

```cpp
class Solution {
public:
    vector<int> gardenNoAdj(int n, vector<vector<int>>& paths) {
        // Build the adjacency list for the graph
        vector<vector<int>> graph(n);
        for (const auto& path : paths) {
            graph[path[0] - 1].push_back(path[1] - 1);
            graph[path[1] - 1].push_back(path[0] - 1);
        }
        
        // answer array to store the flower type for each garden
        vector<int> answer(n, 0);
        
        // Iterate through each garden
        for (int i = 0; i < n; ++i) {
            // Record the colors used by the neighbors
            vector<bool> used(5, false);
            for (int adj : graph[i]) {
                if (answer[adj] != 0) {
                    used[answer[adj]] = true;
                }
            }
            
            // Find the first available color from 1 to 4
            for (int color = 1; color <= 4; ++color) {
                if (!used[color]) {
                    answer[i] = color;
                    break;
                }
            }
        }
        
        return answer;
    }
};
```

## C#

```csharp
public class Solution {
    public int[] GardenNoAdj(int n, int[][] paths) {
        // Build the adjacency list for the graph
        List<int>[] graph = new List<int>[n];
        for (int i = 0; i < n; i++) {
            graph[i] = new List<int>();
        }
        foreach (var path in paths) {
            graph[path[0] - 1].Add(path[1] - 1);
            graph[path[1] - 1].Add(path[0] - 1);
        }
        
        // answer array to store the flower type for each garden
        int[] answer = new int[n];
        
        // Iterate through each garden
        for (int i = 0; i < n; i++) {
            // Record the colors used by the neighbors
            bool[] used = new bool[5];
            foreach (int adj in graph[i]) {
                if (answer[adj] != 0) {
                    used[answer[adj]] = true;
                }
            }
            
            // Find the first available color from 1 to 4
            for (int color = 1; color <= 4; color++) {
                if (!used[color]) {
                    answer[i] = color;
                    break;
                }
            }
        }
        
        return answer;
    }
}
```

## Go

```go
func gardenNoAdj(n int, paths [][]int) []int {
    // Build the adjacency list for the graph
    graph := make([][]int, n)
    for _, path := range paths {
        u, v := path[0]-1, path[1]-1
        graph[u] = append(graph[u], v)
        graph[v] = append(graph[v], u)
    }
    
    // answer array to store the flower type for each garden
    answer := make([]int, n)
    
    // Iterate through each garden
    for i := 0; i < n; i++ {
        // Record the colors used by the neighbors
        used := make([]bool, 5)
        for _, adj := range graph[i] {
            if answer[adj] != 0 {
                used[answer[adj]] = true
            }
        }
        
        // Find the first available color from 1 to 4
        for color := 1; color <= 4; color++ {
            if !used[color] {
                answer[i] = color
                break
            }
        }
    }
    
    return answer
}
```

## Ruby

```ruby
# @param {Integer} n
# @param {Integer[][]} paths
# @return {Integer[]}
def garden_no_adj(n, paths)
    # Build the adjacency list for the graph
    graph = Array.new(n) { [] }
    paths.each do |u, v|
        graph[u - 1] << (v - 1)
        graph[v - 1] << (u - 1)
    end
    
    # answer array to store the flower type for each garden
    answer = Array.new(n, 0)
    
    # Iterate through each garden
    (0...n).each do |i|
        # Record the colors used by the neighbors
        used = Array.new(5, false)
        graph[i].each do |adj|
            if answer[adj] != 0
                used[answer[adj]] = true
            end
        end
        
        # Find the first available color from 1 to 4
        (1..4).each do |color|
            if !used[color]
                answer[i] = color
                break
            end
        end
    end
    
    answer
end
```

## Rust

```rust
impl Solution {
    pub fn garden_no_adj(n: i32, paths: Vec<Vec<i32>>) -> Vec<i32> {
        let n = n as usize;
        // Build the adjacency list for the graph
        let mut graph = vec![Vec::new(); n];
        for path in paths {
            let u = (path[0] - 1) as usize;
            let v = (path[1] - 1) as usize;
            graph[u].push(v);
            graph[v].push(u);
        }
        
        // answer array to store the flower type for each garden
        let mut answer = vec![0; n];
        
        // Iterate through each garden
        for i in 0..n {
            // Record the colors used by the neighbors
            let mut used = [false; 5];
            for &adj in &graph[i] {
                if answer[adj] != 0 {
                    used[answer[adj] as usize] = true;
                }
            }
            
            // Find the first available color from 1 to 4
            for color in 1..=4 {
                if !used[color as usize] {
                    answer[i] = color;
                    break;
                }
            }
        }
        
        answer
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun gardenNoAdj(n: Int, paths: Array<IntArray>): IntArray {
        // Build the adjacency list for the graph
        val graph = Array(n) { mutableListOf<Int>() }
        for (path in paths) {
            graph[path[0] - 1].add(path[1] - 1)
            graph[path[1] - 1].add(path[0] - 1)
        }
        
        // answer array to store the flower type for each garden
        val answer = IntArray(n) { 0 }
        
        // Iterate through each garden
        for (i in 0 until n) {
            // Record the colors used by the neighbors
            val used = BooleanArray(5) { false }
            for (adj in graph[i]) {
                if (answer[adj] != 0) {
                    used[answer[adj]] = true
                }
            }
            
            // Find the first available color from 1 to 4
            for (color in 1..4) {
                if (!used[color]) {
                    answer[i] = color
                    break
                }
            }
        }
        
        return answer
    }
}
```

## Swift

```swift
class Solution {
    func gardenNoAdj(_ n: Int, _ paths: [[Int]]) -> [Int] {
        // Build the adjacency list for the graph
        var graph = Array(repeating: [Int](), count: n)
        for path in paths {
            graph[path[0] - 1].append(path[1] - 1)
            graph[path[1] - 1].append(path[0] - 1)
        }
        
        // answer array to store the flower type for each garden
        var answer = Array(repeating: 0, count: n)
        
        // Iterate through each garden
        for i in 0..<n {
            // Record the colors used by the neighbors
            var used = Array(repeating: false, count: 5)
            for adj in graph[i] {
                if answer[adj] != 0 {
                    used[answer[adj]] = true
                }
            }
            
            // Find the first available color from 1 to 4
            for color in 1...4 {
                if !used[color] {
                    answer[i] = color
                    break
                }
            }
        }
        
        return answer
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
> 我的另一个项目 [**leader.me**](https://www.leader.me) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.leader.me`，极具职业含金量的专属域名。

>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[1042. 不邻接植花 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/1042-flower-planting-with-no-adjacent)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

