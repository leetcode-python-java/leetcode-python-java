# 1042. Flower Planting With No Adjacent - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

Visit original link: [1042. Flower Planting With No Adjacent - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/1042-flower-planting-with-no-adjacent) for a better experience!

LeetCode link: [1042. Flower Planting With No Adjacent](https://leetcode.com/problems/flower-planting-with-no-adjacent), difficulty: **Medium**.

## LeetCode description of "1042. Flower Planting With No Adjacent"

You have `n` gardens, labeled from `1` to `n`, and an array `paths` where `paths[i] = [x_i, y_i]` describes a bidirectional path between garden `x_i` to garden `y_i`. In each garden, you want to plant one of 4 types of flowers.

All gardens have at most 3 paths coming into or leaving it.

Your task is to choose a flower type for each garden such that, for any two gardens connected by a path, they have different types of flowers.

Return *any such a choice as an array* `answer`*, where* `answer[i]` *is the type of flower planted in the* `(i+1)^{th}` *garden. The flower types are denoted* `1`*,* `2`*,* `3`*, or* `4`*. It is guaranteed an answer exists.*

### [Example 1]

**Input**: `n = 3, paths = [[1,2],[2,3],[3,1]]`

**Output**: `[1,2,3]`

**Explanation**: 

<p>Gardens 1 and 2 have different types.<br>
Gardens 2 and 3 have different types.<br>
Gardens 3 and 1 have different types.<br>
Hence, [1,2,3] is a valid answer. Other valid answers include [1,2,4], [1,4,2], and [3,2,1].</p>


### [Example 2]

**Input**: `n = 4, paths = [[1,2],[3,4]]`

**Output**: `[1,2,1,2]`

### [Example 3]

**Input**: `n = 4, paths = [[1,2],[2,3],[3,4],[4,1],[1,3],[2,4]]`

**Output**: `[1,2,3,4]`

### [Constraints]

- `1 <= n <= 10^4`
- `0 <= paths.length <= 2 * 10^4`
- `paths[i].length == 2`
- `1 <= x_i, y_i <= n`
- `x_i != y_i`
- Every garden has at most 3 paths coming into or leaving it.

### [Hints]

<details>
  <summary>Hint 1</summary>
  Since each garden has at most 3 paths, we can always find an available color from the 4 colors.

  
</details>

## Intuition

The problem asks us to assign one of 4 types of flowers (colors) to `n` gardens such that no two connected gardens have the same flower type.

This is a classic graph coloring problem. 

The key constraint here is that **each garden has at most 3 paths coming into or leaving it**. 

This means that for any given garden, it can have at most 3 neighbors. 

Since we have 4 different types of flowers available, no matter what flowers are planted in its neighbors, there will **always** be at least one flower type left for the current garden.

Therefore, we can use a simple **Greedy Algorithm**:

1. Build an adjacency list to represent the graph of gardens and paths.

2. Iterate through each garden from `1` to `n`.

3. For the current garden, check the flower types already assigned to its neighbors.

4. Pick any flower type from `{1, 2, 3, 4}` that is not used by its neighbors and assign it to the current garden.

This approach guarantees a valid configuration in a single pass without the need for backtracking.

## Step-by-Step Solution

1. **Build the Graph**: Create an adjacency list `graph` where `graph[i]` stores all the neighbors of garden `i`. Note that gardens are 1-indexed.
2. **Initialize the Answer Array**: Create an array `answer` of size `n` initialized to `0`, where `0` means the garden has not been planted yet.
3. **Iterate Through Gardens**: Loop `i` from `1` to `n` (or `0` to `n-1` depending on indexing):
   - Create a boolean array or a set `used` to keep track of the colors used by the neighbors of the current garden.
   - For each neighbor `adj` of garden `i`, if `answer[adj]` is not `0`, mark that color as used in `used`.
   - Iterate through colors `1` to `4`. Find the first color that is not `used` and assign it to `answer[i]`.
4. **Return the Result**: After the loop finishes, return the `answer` array.

## Complexity

> - **Time Complexity:** `O(n + m)`, where `n` is the number of gardens and `m` is the number of paths (edges). Building the graph takes `O(m)` time. Iterating through each garden and its neighbors takes `O(n + m)` time in total because each edge is processed at most twice. Checking available colors takes `O(1)` time per garden since there are only 4 colors.
- **Space Complexity:** `O(n + m)` to store the adjacency list representing the graph. The `answer` array takes `O(n)` space.

- Time complexity: `O(n + m)`.
- Space complexity: `O(n + m)`.

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

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.leader.me`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [1042. Flower Planting With No Adjacent - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/1042-flower-planting-with-no-adjacent) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

