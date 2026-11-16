# 77. 组合 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 coder.id 打造你的开发者个人IP →**](https://www.coder.id)

访问原文链接：[77. 组合 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/77-combinations)，体验更佳！

力扣链接：[77. 组合](https://leetcode.cn/problems/combinations), 难度等级：**中等**。

## LeetCode “77. 组合”问题描述

给定两个整数 `n` 和 `k`，返回范围 `[1, n]` 中所有可能的 `k` 个数的组合。

你可以按 **任何顺序** 返回答案。

### [示例 1]

**输入**: `n = 4, k = 2`

**输出**: `[[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]`

**解释**: 

<div class="highlight"><pre class="highlight plaintext"><code>There are 4 choose 2 = 6 total combinations.
Note that combinations are unordered, i.e., [1,2] and [2,1] are considered to be the same combination.
</code></pre></div>

### [示例 2]

**输入**: `n = 1, k = 1`

**输出**: `[[1]]`

**解释**: `There is 1 choose 1 = 1 total combination.`

### [约束]

- `1 <= n <= 20`
- `1 <= k <= n`

## 思路

要枚举从范围 `[1, n]` 中选出 `k` 个数字的所有组合，我们可以使用经典的 **回溯法**（也叫 **深度优先搜索**）。

核心思想很简单：我们**逐个数字**地构建一个组合，每一步都选择一个数字追加到当前路径中。

让这道题变得干净的**关键观察**是**顺序**：这正是递归需要携带一个 `start_index` 参数的原因。

在当前路径的这个位置上，所有小于 `start_index` 的数字都已经被使用过（或被有意跳过）了，因此它们**绝不允许**再次被使用。

所以，在每一次递归调用中，我们只尝试从 `start_index` 到 `n` 的候选数字。

当当前路径已经恰好包含 `k` 个数字时，它就是一个**完整且有效**的组合，于是我们把它的一个**副本**存入结果列表。

接着，借助回溯，我们**撤销**最后选择的那个数字，然后继续尝试下一个候选数字。

这个“选择、探索、撤销”的循环就是算法的核心。

## 步骤

1. **定义递归辅助函数。** 创建一个函数 `backtracking(start_index)`，它在任意时刻都作用于存储在 `self.result` 中的当前部分组合。
2. **定义基准情形（base case）。** 在辅助函数的最开头，检查当前路径是否已经完整：
   - 如果 `len(self.result) == self.k`，说明路径中正好有 `k` 个数字。
   - 把 `self.result` 的一个**副本**追加到 `self.results`（必须是副本，因为 `self.result` 之后还会不断变化）。
   - 然后 `return`，停止继续扩展这条分支。
3. **遍历候选数字。** 让 `i` 从 `start_index` 循环到 `self.n`（含端点）。每个 `i` 都是组合下一个位置的候选数字。
4. **选择。** 把 `i` 追加到 `self.result`。
5. **探索。** 递归调用 `backtracking(i + 1)`。传入 `i + 1` 保证下一个被选择的数字**大于** `i`，从而强制严格递增顺序并消除重复。
6. **撤销（回溯）。** 把最后一个元素从 `self.result` 中弹出，使路径恢复到第 4 步之前的状态，以便循环尝试下一个候选数字。
7. **启动搜索。** 在主函数 `combine` 中初始化实例变量，并调用 `backtracking(1)`，从最小的数字 `1` 开始。
8. **返回答案。** 最后返回 `self.results`。

```
combine(n, k):
    result = []
    results = []
    backtracking(start_index = 1)

backtracking(start_index):
    if len(result) == k:
        results.append(copy of result)
        return
    for i in range(start_index, n + 1):
        result.append(i)          # 选择
        backtracking(i + 1)       # 探索
        result.pop()              # 撤销
```

## 复杂度

- 时间复杂度: `O(k * C(n, k))`.
- 空间复杂度: `O(k)`.

## Python

```python
class Solution:
    def combine(self, n: int, k: int) -> list[list[int]]:
        # Store n and k as instance variables so the nested helper can read them.
        self.results = []   # Final list holding every valid combination.
        self.result = []    # Current path: one partial combination being built.
        self.k = k
        self.n = n

        # Start the search from the smallest candidate number 1.
        self.backtracking(1)

        return self.results

    def backtracking(self, start_index):
        # Base case: the path already has exactly k numbers, so it is complete.
        if len(self.result) == self.k:
            # Append a COPY of the path, because self.result keeps changing.
            self.results.append(self.result.copy())
            return

        # Try every candidate number from start_index up to n (inclusive).
        for i in range(start_index, self.n + 1):
            self.result.append(i)        # Choose i.
            self.backtracking(i + 1)     # Explore: next number must be larger.
            self.result.pop()            # Un-choose: undo the choice (backtrack).
```

## Java

```java
class Solution {
    // Final list holding every valid combination.
    private List<List<Integer>> results = new ArrayList<>();
    // Current path: one partial combination being built.
    private List<Integer> result = new ArrayList<>();
    private int n;
    private int k;

    public List<List<Integer>> combine(int n, int k) {
        this.n = n;
        this.k = k;
        // Reset the state so this method is safe to call again on the same instance.
        results = new ArrayList<>();
        result = new ArrayList<>();
        // Start the search from the smallest candidate number 1.
        backtracking(1);
        return results;
    }

    private void backtracking(int startIndex) {
        // Base case: the path already has exactly k numbers, so it is complete.
        if (result.size() == k) {
            // Store a COPY, because result is mutated afterwards.
            results.add(new ArrayList<>(result));
            return;
        }

        // Try every candidate number from startIndex up to n (inclusive).
        for (int i = startIndex; i <= n; i++) {
            result.add(i);                      // Choose i.
            backtracking(i + 1);                // Explore: next number must be larger.
            result.remove(result.size() - 1);   // Un-choose: undo the choice (backtrack).
        }
    }
}
```

## JavaScript

```javascript
/**
 * @param {number} n
 * @param {number} k
 * @return {number[][]}
 */
var combine = function(n, k) {
    // Final list holding every valid combination.
    const results = [];
    // Current path: one partial combination being built.
    const result = [];

    const backtracking = (startIndex) => {
        // Base case: the path already has exactly k numbers, so it is complete.
        if (result.length === k) {
            // Store a shallow COPY of the path, because result is mutated afterwards.
            results.push([...result]);
            return;
        }

        // Try every candidate number from startIndex up to n (inclusive).
        for (let i = startIndex; i <= n; i++) {
            result.push(i);        // Choose i.
            backtracking(i + 1);   // Explore: next number must be larger.
            result.pop();          // Un-choose: undo the choice (backtrack).
        }
    };

    // Start the search from the smallest candidate number 1.
    backtracking(1);
    return results;
};
```

## C++

```cpp
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        this->n = n;
        this->k = k;
        // Reset the state so this method is safe to call again on the same instance.
        results.clear();
        result.clear();
        // Start the search from the smallest candidate number 1.
        backtracking(1);
        return results;
    }

private:
    // Final list holding every valid combination.
    vector<vector<int>> results;
    // Current path: one partial combination being built.
    vector<int> result;
    int n;
    int k;

    void backtracking(int startIndex) {
        // Base case: the path already has exactly k numbers, so it is complete.
        if ((int)result.size() == k) {
            results.push_back(result);   // push_back copies the vector.
            return;
        }

        // Try every candidate number from startIndex up to n (inclusive).
        for (int i = startIndex; i <= n; i++) {
            result.push_back(i);   // Choose i.
            backtracking(i + 1);   // Explore: next number must be larger.
            result.pop_back();     // Un-choose: undo the choice (backtrack).
        }
    }
};
```

## C#

```csharp
public class Solution {
    // Final list holding every valid combination.
    private IList<IList<int>> results = new List<IList<int>>();
    // Current path: one partial combination being built.
    private List<int> result = new List<int>();
    private int n;
    private int k;

    public IList<IList<int>> Combine(int n, int k) {
        this.n = n;
        this.k = k;
        // Reset the state so this method is safe to call again on the same instance.
        results = new List<IList<int>>();
        result = new List<int>();
        // Start the search from the smallest candidate number 1.
        Backtracking(1);
        return results;
    }

    private void Backtracking(int startIndex) {
        // Base case: the path already has exactly k numbers, so it is complete.
        if (result.Count == k) {
            // Store a COPY, because result is mutated afterwards.
            results.Add(new List<int>(result));
            return;
        }

        // Try every candidate number from startIndex up to n (inclusive).
        for (int i = startIndex; i <= n; i++) {
            result.Add(i);                       // Choose i.
            Backtracking(i + 1);                 // Explore: next number must be larger.
            result.RemoveAt(result.Count - 1);   // Un-choose: undo the choice (backtrack).
        }
    }
}
```

## Go

```go
func combine(n int, k int) [][]int {
    // Final list holding every valid combination.
    results := [][]int{}
    // Current path: one partial combination being built.
    result := []int{}

    // Recursive helper defined as a closure so it can capture result and results.
    var backtracking func(startIndex int)
    backtracking = func(startIndex int) {
        // Base case: the path already has exactly k numbers, so it is complete.
        if len(result) == k {
            // Copy the current path, because the slice is reused afterwards.
            snapshot := make([]int, len(result))
            copy(snapshot, result)
            results = append(results, snapshot)
            return
        }

        // Try every candidate number from startIndex up to n (inclusive).
        for i := startIndex; i <= n; i++ {
            result = append(result, i)        // Choose i.
            backtracking(i + 1)               // Explore: next number must be larger.
            result = result[:len(result)-1]   // Un-choose: undo the choice (backtrack).
        }
    }

    // Start the search from the smallest candidate number 1.
    backtracking(1)
    return results
}
```

## Ruby

```ruby
# @param {Integer} n
# @param {Integer} k
# @return {Integer[][]}
def combine(n, k)
  # Instance variables so the helper method can read and mutate them.
  @results = []   # Final list holding every valid combination.
  @result = []    # Current path: one partial combination being built.
  @k = k
  @n = n

  # Start the search from the smallest candidate number 1.
  backtracking(1)

  @results
end

def backtracking(start_index)
  # Base case: the path already has exactly k numbers, so it is complete.
  if @result.length == @k
    # Store a COPY (dup), because @result is mutated afterwards.
    @results << @result.dup
    return
  end

  # Try every candidate number from start_index up to n (inclusive).
  (start_index..@n).each do |i|
    @result << i          # Choose i.
    backtracking(i + 1)   # Explore: next number must be larger.
    @result.pop           # Un-choose: undo the choice (backtrack).
  end
end
```

## Rust

```rust
impl Solution {
    pub fn combine(n: i32, k: i32) -> Vec<Vec<i32>> {
        // Final list holding every valid combination.
        let mut results: Vec<Vec<i32>> = Vec::new();
        // Current path: one partial combination being built.
        let mut result: Vec<i32> = Vec::new();

        // Recursive helper that builds combinations in strictly increasing order.
        fn backtracking(
            start_index: i32,
            n: i32,
            k: i32,
            result: &mut Vec<i32>,
            results: &mut Vec<Vec<i32>>,
        ) {
            // Base case: the path already has exactly k numbers, so it is complete.
            if result.len() == k as usize {
                // Clone the path to store a snapshot.
                results.push(result.clone());
                return;
            }

            // Try every candidate number from start_index up to n (inclusive).
            for i in start_index..=n {
                result.push(i);                                  // Choose i.
                backtracking(i + 1, n, k, result, results);      // Explore.
                result.pop();                                    // Un-choose (backtrack).
            }
        }

        // Start the search from the smallest candidate number 1.
        backtracking(1, n, k, &mut result, &mut results);
        results
    }
}
```

## Kotlin

```kotlin
class Solution {
    // Final list holding every valid combination.
    private val results = mutableListOf<List<Int>>()
    // Current path: one partial combination being built.
    private val result = mutableListOf<Int>()

    fun combine(n: Int, k: Int): List<List<Int>> {
        // Reset the state so this method is safe to call again on the same instance.
        results.clear()
        result.clear()
        // Start the search from the smallest candidate number 1.
        backtracking(1, n, k)
        return results
    }

    private fun backtracking(startIndex: Int, n: Int, k: Int) {
        // Base case: the path already has exactly k numbers, so it is complete.
        if (result.size == k) {
            // Store a COPY (toList), because result is mutated afterwards.
            results.add(result.toList())
            return
        }

        // Try every candidate number from startIndex up to n (inclusive).
        for (i in startIndex..n) {
            result.add(i)                     // Choose i.
            backtracking(i + 1, n, k)         // Explore: next number must be larger.
            result.removeAt(result.size - 1)  // Un-choose: undo the choice (backtrack).
        }
    }
}
```

## Swift

```swift
class Solution {
    func combine(_ n: Int, _ k: Int) -> [[Int]] {
        // Final list holding every valid combination.
        var results = [[Int]]()
        // Current path: one partial combination being built.
        var result = [Int]()

        // Recursive helper defined as a nested function so it can capture state.
        func backtracking(_ startIndex: Int) {
            // Base case: the path already has exactly k numbers, so it is complete.
            if result.count == k {
                // Arrays are value types, so appending copies the current path.
                results.append(result)
                return
            }

            // Guard: if there are no candidate numbers left, stop.
            // This also prevents building an invalid range such as 5...4, which
            // would crash Swift at runtime.
            if startIndex > n {
                return
            }

            // Try every candidate number from startIndex up to n (inclusive).
            for i in startIndex...n {
                result.append(i)     // Choose i.
                backtracking(i + 1)  // Explore: next number must be larger.
                result.removeLast()  // Un-choose: undo the choice (backtrack).
            }
        }

        // Start the search from the smallest candidate number 1.
        backtracking(1)
        return results
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

访问原文链接：[77. 组合 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/77-combinations)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

