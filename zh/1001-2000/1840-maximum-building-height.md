# 1840. 最高建筑高度 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[1840. 最高建筑高度 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/1840-maximum-building-height)，体验更佳！

力扣链接：[1840. 最高建筑高度](https://leetcode.cn/problems/maximum-building-height), 难度等级：**困难**。

## LeetCode “1840. 最高建筑高度”问题描述

在一座城市里，你需要建 `n` 栋新的建筑。这些新的建筑会从 `1` 到 `n` 编号排成一列。

这座城市对这些新建筑有一些规定：

* 每栋建筑的高度必须是一个非负整数。
* 第一栋建筑的高度 **必须** 是 `0` 。
* 任意两栋相邻建筑的高度差 **不能超过** `1` 。

除此以外，某些建筑还有额外的最高高度限制。这些限制会以二维整数数组 `restrictions` 的形式给出，其中 `restrictions[i] = [idi, maxHeighti]` ，表示建筑 `idi` 的高度 **不能超过** `maxHeighti` 。

题目保证每栋建筑在 `restrictions` 中 **至多出现一次** ，同时建筑 `1` **不会** 出现在 `restrictions` 中。

请你返回 **最高** 建筑能达到的 **最高高度** 。

### [示例 1]

![](../../images/examples/1840_1.png)

**输入**: `n = 5, restrictions = [[2,1],[4,1]]`

**输出**: `2`

**解释**: 

<p>上图中的绿色区域为每栋建筑被允许的最高高度。<br>
我们可以使建筑高度分别为 [0,1,2,1,2] ，最高建筑的高度为 2 。</p>


### [示例 2]

![](../../images/examples/1840_2.png)

**输入**: `n = 6, restrictions = []`

**输出**: `5`

**解释**: 

<p>上图中的绿色区域为每栋建筑被允许的最高高度。<br>
我们可以使建筑高度分别为 [0,1,2,3,4,5] ，最高建筑的高度为 5 。</p>


### [示例 3]

![](../../images/examples/1840_3.png)

**输入**: `n = 10, restrictions = [[5,3],[2,5],[7,4],[10,3]]`

**输出**: `5`

**解释**: 

<p>上图中的绿色区域为每栋建筑被允许的最高高度。<br>
我们可以使建筑高度分别为 [0,1,2,3,3,4,4,5,4,3] ，最高建筑的高度为 5 。</p>


### [约束]

* `2 <= n <= 10^9`
* `0 <= restrictions.length <= min(n - 1, 10^5)`
* `2 <= idi <= n`
* `idi` 是 **唯一的** 。
* `0 <= maxHeighti <= 10^9`

## 思路

题目要求我们找到在满足特定建筑高度限制的条件下，相邻建筑高度差不超过 1 的最大建筑高度。
这意味着在建筑 `A` 的高度限制，也会将建筑 `B` 的最大可能高度限制为 `height[A] + |A - B|`。为了找到每个受限建筑处真正的、最严格的最大允许高度，我们必须将这些约束条件在整个限制数组中进行传递。

首先，我们按建筑 ID 对限制条件进行排序。然后执行两次遍历：
1. **从左到右遍历**：将左侧邻居的约束条件传递给右侧。
2. **从右到左遍历**：将右侧邻居的约束条件传递给左侧。

两次遍历后，所有的限制条件彼此之间达到了完全的一致。然后，我们可以通过数学方法计算出任意两个相邻受限建筑 `i` 和 `j` 之间的最大可能高度。它对应于从它们各自高度出发，斜率分别为 +1 和 -1 的两条直线的交点，公式为：`(height[i] + height[j] + id[j] - id[i]) / 2`。

## 步骤

1. **添加隐式限制**：建筑 1 的高度始终为 0，因此我们添加 `[1, 0]`。建筑 `n` 没有显式限制，但它受第一栋建筑限制的最大可能高度是 `n - 1`，因此我们添加 `[n, n - 1]` 以确保最后一个区间被计算。
2. **排序**：按建筑 ID 升序对 `restrictions` 数组进行排序。
3. **从左到右遍历**：从第二个限制条件遍历到最后。将当前建筑的高度限制更新为它自身的限制与前一个建筑对其施加的限制（`height[i-1] + id[i] - id[i-1]`）两者中的较小值。
4. **从右到左遍历**：从倒数第二个限制条件倒序遍历到第一个。将当前建筑的高度限制更新为其当前限制与后一个建筑对其施加的限制（`height[i+1] + id[i+1] - id[i]`）两者中的较小值。
5. **计算峰值高度**：遍历所有相邻的限制条件对。对于每一对 `i-1` 和 `i`，使用公式 `(height[i-1] + height[i] + id[i] - id[i-1]) / 2` 计算它们之间可以达到的局部峰值高度。
6. 记录并在所有区间中找出全局最大高度，将其返回。

## 复杂度

> - **时间复杂度**: `O(M \log M)`，其中 `M` 是限制条件的数量。对限制数组进行排序占据了主要的时间复杂度。两次线性遍历以及最后的峰值计算需要 `O(M)` 的时间。
- **空间复杂度**: `O(M)` 或 `O(\log M)`，取决于排序算法以及语言是否支持原地排序，或者是否为了添加隐式限制条件而创建了新的数组。

- 时间复杂度: `O(M \log M)`.
- 空间复杂度: `O(M)`.

## Python

```python
class Solution:
    def maxBuilding(self, n: int, restrictions: List[List[int]]) -> int:
        # Add implicit restrictions for the first and last buildings
        restrictions.append([1, 0])
        restrictions.append([n, n - 1])
        
        # Sort restrictions by building ID
        restrictions.sort()
        
        m = len(restrictions)
        
        # Left-to-right pass: Propagate height limits from left to right
        for i in range(1, m):
            restrictions[i][1] = min(restrictions[i][1], restrictions[i-1][1] + restrictions[i][0] - restrictions[i-1][0])
            
        # Right-to-left pass: Propagate height limits from right to left
        for i in range(m - 2, -1, -1):
            restrictions[i][1] = min(restrictions[i][1], restrictions[i+1][1] + restrictions[i+1][0] - restrictions[i][0])
            
        ans = 0
        # Find the maximum height between each adjacent pair of restrictions
        for i in range(1, m):
            h1, h2 = restrictions[i-1][1], restrictions[i][1]
            x1, x2 = restrictions[i-1][0], restrictions[i][0]
            
            # The peak height reached between x1 and x2
            # It's derived from solving intersection: h1 + (x - x1) = h2 + (x2 - x)
            ans = max(ans, (h1 + h2 + x2 - x1) // 2)
            
        return ans
```

## Java

```java
class Solution {
    public int maxBuilding(int n, int[][] restrictions) {
        int m = restrictions.length;
        // Create a new array to include the 2 implicit restrictions
        int[][] r = new int[m + 2][2];
        for (int i = 0; i < m; i++) {
            r[i] = restrictions[i];
        }
        r[m] = new int[]{1, 0};
        r[m + 1] = new int[]{n, n - 1};
        
        // Sort the array based on building IDs
        Arrays.sort(r, (a, b) -> Integer.compare(a[0], b[0]));
        
        // Left-to-right pass
        for (int i = 1; i < r.length; i++) {
            r[i][1] = Math.min(r[i][1], r[i-1][1] + r[i][0] - r[i-1][0]);
        }
        
        // Right-to-left pass
        for (int i = r.length - 2; i >= 0; i--) {
            r[i][1] = Math.min(r[i][1], r[i+1][1] + r[i+1][0] - r[i][0]);
        }
        
        int ans = 0;
        // Calculate the maximum peak height between every adjacent restriction
        for (int i = 1; i < r.length; i++) {
            int h1 = r[i-1][1], h2 = r[i][1];
            int x1 = r[i-1][0], x2 = r[i][0];
            ans = Math.max(ans, (h1 + h2 + x2 - x1) / 2);
        }
        
        return ans;
    }
}
```

## JavaScript

```javascript
/**
 * @param {number} n
 * @param {number[][]} restrictions
 * @return {number}
 */
var maxBuilding = function(n, restrictions) {
    // Append the implicit restrictions
    restrictions.push([1, 0]);
    restrictions.push([n, n - 1]);
    
    // Sort restrictions ascending by ID
    restrictions.sort((a, b) => a[0] - b[0]);
    
    const m = restrictions.length;
    
    // Pass 1: Left to right
    for (let i = 1; i < m; i++) {
        restrictions[i][1] = Math.min(restrictions[i][1], restrictions[i-1][1] + restrictions[i][0] - restrictions[i-1][0]);
    }
    
    // Pass 2: Right to left
    for (let i = m - 2; i >= 0; i--) {
        restrictions[i][1] = Math.min(restrictions[i][1], restrictions[i+1][1] + restrictions[i+1][0] - restrictions[i][0]);
    }
    
    let ans = 0;
    // Calculate peaks between restrictions
    for (let i = 1; i < m; i++) {
        const h1 = restrictions[i-1][1];
        const h2 = restrictions[i][1];
        const x1 = restrictions[i-1][0];
        const x2 = restrictions[i][0];
        
        ans = Math.max(ans, Math.floor((h1 + h2 + x2 - x1) / 2));
    }
    
    return ans;
};
```

## Cpp

```cpp
class Solution {
public:
    int maxBuilding(int n, vector<vector<int>>& restrictions) {
        // Push implicit bounds
        restrictions.push_back({1, 0});
        restrictions.push_back({n, n - 1});
        
        // Sort based on building ID
        sort(restrictions.begin(), restrictions.end());
        
        int m = restrictions.size();
        
        // Left to right propagation
        for (int i = 1; i < m; i++) {
            restrictions[i][1] = min(restrictions[i][1], restrictions[i-1][1] + restrictions[i][0] - restrictions[i-1][0]);
        }
        
        // Right to left propagation
        for (int i = m - 2; i >= 0; i--) {
            restrictions[i][1] = min(restrictions[i][1], restrictions[i+1][1] + restrictions[i+1][0] - restrictions[i][0]);
        }
        
        int ans = 0;
        // Compute maximum peak
        for (int i = 1; i < m; i++) {
            int h1 = restrictions[i-1][1], h2 = restrictions[i][1];
            int x1 = restrictions[i-1][0], x2 = restrictions[i][0];
            ans = max(ans, (h1 + h2 + x2 - x1) / 2);
        }
        
        return ans;
    }
};
```

## Csharp

```csharp
public class Solution {
    public int MaxBuilding(int n, int[][] restrictions) {
        int m = restrictions.Length;
        int[][] r = new int[m + 2][];
        
        // Copy restrictions and add the implicit bounds
        for (int i = 0; i < m; i++) {
            r[i] = restrictions[i];
        }
        r[m] = new int[] { 1, 0 };
        r[m + 1] = new int[] { n, n - 1 };
        
        // Sort by building ID
        Array.Sort(r, (a, b) => a[0].CompareTo(b[0]));
        
        // Sweep left to right
        for (int i = 1; i < r.Length; i++) {
            r[i][1] = Math.Min(r[i][1], r[i-1][1] + r[i][0] - r[i-1][0]);
        }
        
        // Sweep right to left
        for (int i = r.Length - 2; i >= 0; i--) {
            r[i][1] = Math.Min(r[i][1], r[i+1][1] + r[i+1][0] - r[i][0]);
        }
        
        int ans = 0;
        // Evaluate the peak heights
        for (int i = 1; i < r.Length; i++) {
            int h1 = r[i-1][1], h2 = r[i][1];
            int x1 = r[i-1][0], x2 = r[i][0];
            ans = Math.Max(ans, (h1 + h2 + x2 - x1) / 2);
        }
        
        return ans;
    }
}
```

## Go

```go
import "sort"

func maxBuilding(n int, restrictions [][]int) int {
    // Append constraints for first and last building
    restrictions = append(restrictions, []int{1, 0})
    restrictions = append(restrictions, []int{n, n - 1})
    
    // Sort restrictions ascending by ID
    sort.Slice(restrictions, func(i, j int) bool {
        return restrictions[i][0] < restrictions[j][0]
    })
    
    m := len(restrictions)
    
    // Left-to-right pass
    for i := 1; i < m; i++ {
        limit := restrictions[i-1][1] + restrictions[i][0] - restrictions[i-1][0]
        if limit < restrictions[i][1] {
            restrictions[i][1] = limit
        }
    }
    
    // Right-to-left pass
    for i := m - 2; i >= 0; i-- {
        limit := restrictions[i+1][1] + restrictions[i+1][0] - restrictions[i][0]
        if limit < restrictions[i][1] {
            restrictions[i][1] = limit
        }
    }
    
    ans := 0
    // Find the max height achievable between every adjacent restrictions
    for i := 1; i < m; i++ {
        h1, h2 := restrictions[i-1][1], restrictions[i][1]
        x1, x2 := restrictions[i-1][0], restrictions[i][0]
        peak := (h1 + h2 + x2 - x1) / 2
        if peak > ans {
            ans = peak
        }
    }
    
    return ans
}
```

## Ruby

```ruby
# @param {Integer} n
# @param {Integer[][]} restrictions
# @return {Integer}
def max_building(n, restrictions)
    # Append implicit restrictions
    restrictions << [1, 0]
    restrictions << [n, n - 1]
    
    # Sort by building ID
    restrictions.sort_by! { |r| r[0] }
    
    m = restrictions.length
    
    # Left-to-right pass
    (1...m).each do |i|
        limit = restrictions[i-1][1] + restrictions[i][0] - restrictions[i-1][0]
        restrictions[i][1] = [restrictions[i][1], limit].min
    end
    
    # Right-to-left pass
    (m - 2).downto(0) do |i|
        limit = restrictions[i+1][1] + restrictions[i+1][0] - restrictions[i][0]
        restrictions[i][1] = [restrictions[i][1], limit].min
    end
    
    ans = 0
    # Calculate peaks
    (1...m).each do |i|
        h1, h2 = restrictions[i-1][1], restrictions[i][1]
        x1, x2 = restrictions[i-1][0], restrictions[i][0]
        
        ans = [ans, (h1 + h2 + x2 - x1) / 2].max
    end
    
    ans
end
```

## Rust

```rust
impl Solution {
    pub fn max_building(n: i32, mut restrictions: Vec<Vec<i32>>) -> i32 {
        // Add boundary building constraints
        restrictions.push(vec![1, 0]);
        restrictions.push(vec![n, n - 1]);
        
        // Sort restrictions based on ID
        restrictions.sort_unstable_by_key(|r| r[0]);
        
        let m = restrictions.len();
        
        // Left-to-right propagation
        for i in 1..m {
            let limit = restrictions[i-1][1] + restrictions[i][0] - restrictions[i-1][0];
            restrictions[i][1] = restrictions[i][1].min(limit);
        }
        
        // Right-to-left propagation
        for i in (0..m - 1).rev() {
            let limit = restrictions[i+1][1] + restrictions[i+1][0] - restrictions[i][0];
            restrictions[i][1] = restrictions[i][1].min(limit);
        }
        
        let mut ans = 0;
        // Compute peak height between every adjacent pairs
        for i in 1..m {
            let h1 = restrictions[i-1][1];
            let h2 = restrictions[i][1];
            let x1 = restrictions[i-1][0];
            let x2 = restrictions[i][0];
            
            ans = ans.max((h1 + h2 + x2 - x1) / 2);
        }
        
        ans
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun maxBuilding(n: Int, restrictions: Array<IntArray>): Int {
        val r = Array(restrictions.size + 2) { IntArray(2) }
        
        for (i in restrictions.indices) {
            r[i] = restrictions[i]
        }
        r[restrictions.size] = intArrayOf(1, 0)
        r[restrictions.size + 1] = intArrayOf(n, n - 1)
        
        r.sortBy { it[0] }
        
        for (i in 1 until r.size) {
            r[i][1] = Math.min(r[i][1], r[i-1][1] + r[i][0] - r[i-1][0])
        }
        
        for (i in r.size - 2 downTo 0) {
            r[i][1] = Math.min(r[i][1], r[i+1][1] + r[i+1][0] - r[i][0])
        }
        
        var ans = 0
        for (i in 1 until r.size) {
            val h1 = r[i-1][1]
            val h2 = r[i][1]
            val x1 = r[i-1][0]
            val x2 = r[i][0]
            ans = Math.max(ans, (h1 + h2 + x2 - x1) / 2)
        }
        
        return ans
    }
}
```

## Swift

```swift
class Solution {
    func maxBuilding(_ n: Int, _ restrictions: [[Int]]) -> Int {
        var r = restrictions
        // Add boundary conditions
        r.append([1, 0])
        r.append([n, n - 1])
        
        r.sort { $0[0] < $1[0] }
        
        let m = r.count
        
        // Pass 1: sweep left to right
        for i in 1..<m {
            r[i][1] = min(r[i][1], r[i-1][1] + r[i][0] - r[i-1][0])
        }
        
        // Pass 2: sweep right to left
        for i in stride(from: m - 2, through: 0, by: -1) {
            r[i][1] = min(r[i][1], r[i+1][1] + r[i+1][0] - r[i][0])
        }
        
        var ans = 0
        // Find the global maximum height across all gaps
        for i in 1..<m {
            let h1 = r[i-1][1]
            let h2 = r[i][1]
            let x1 = r[i-1][0]
            let x2 = r[i][0]
            
            ans = max(ans, (h1 + h2 + x2 - x1) / 2)
        }
        
        return ans
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

访问原文链接：[1840. 最高建筑高度 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/1840-maximum-building-height)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

