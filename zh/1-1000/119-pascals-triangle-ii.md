# 119. 杨辉三角 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[119. 杨辉三角 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/119-pascals-triangle-ii)，体验更佳！

力扣链接：[119. 杨辉三角 II](https://leetcode.cn/problems/pascals-triangle-ii), 难度等级：**简单**。

## LeetCode “119. 杨辉三角 II”问题描述

给定一个非负索引 `rowIndex`，返回「杨辉三角」的第 `rowIndex`行。

在「杨辉三角」中，每个数是它左上方和右上方的数的和。

![](https://raw.githubusercontent.com/leetcode-python-java/leetcode-python-java/main/images/problems/119_1.gif)

### [示例 1]

**输入**: `rowIndex = 3`

**输出**: `[1,3,3,1]`

### [示例 2]

**输入**: `rowIndex = 0`

**输出**: `[1]`

### [示例 3]

**输入**: `rowIndex = 1`

**输出**: `[1,1]`

### [约束]

* `0 <= rowIndex <= 33`

## 思路

杨辉三角中每一行的元素都可以利用组合数学通过前一个元素直接计算得出。

第 n 行的第 k 个元素由组合数公式 C(n, k) 给出。我们可以根据 C(n, k-1) 来计算 C(n, k)，方法是将其乘以 `(n - k + 1)` 然后除以 `k`。

这样我们就可以在一次遍历中生成整行，而不需要计算之前的任何行。

## 步骤

1. 初始化一个大小为 `rowIndex + 1` 且全部填充为 1 的数组 `res`。每一行的第一个和最后一个元素总是 1。
2. 初始化一个变量 `prev` 为 1，代表前一个元素 C(n, 0)。
3. 使用变量 `k` 从 1 循环到 `rowIndex - 1`。
4. 在每次迭代中，计算当前元素：`curr = prev * (rowIndex - k + 1) / k`。关键是要先乘后除以避免分数丢失，并且在计算过程中使用 64 位整数类型以防止溢出。
5. 将 `curr` 存入 `res[k]`，并更新 `prev = curr` 供下一次迭代使用。
6. 返回 `res` 数组。

## 复杂度

> - **时间复杂度**: `O(rowIndex)`。我们只迭代了 `rowIndex` 次来计算所需行的每个元素。
- **空间复杂度**: 额外空间为 `O(1)`。题目要求返回一个大小为 `rowIndex + 1` 的数组，这在输出中占据 `O(rowIndex)` 的空间。但除了结果数组，我们只使用了少数几个额外变量（`prev`, `curr`），所以额外空间复杂度为 `O(1)`。

- 时间复杂度: `O(rowIndex)`.
- 空间复杂度: `O(1)`.

## Python

```python
class Solution:
    def getRow(self, rowIndex: int) -> List[int]:
        # Initialize the result array with 1s.
        # This handles the boundary 1s automatically.
        res = [1] * (rowIndex + 1)
        
        # Calculate intermediate values using the combination formula
        for k in range(1, rowIndex):
            # res[k] = res[k-1] * (rowIndex - k + 1) / k
            # Use integer division // to ensure we keep integers
            res[k] = res[k - 1] * (rowIndex - k + 1) // k
            
        return res
```

## Java

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> res = new ArrayList<>();
        // The first element is always 1
        res.add(1);
        
        // Use long to prevent integer overflow during multiplication
        long prev = 1;
        for (int k = 1; k <= rowIndex; k++) {
            // Calculate next combination value: C(n, k) = C(n, k-1) * (n - k + 1) / k
            long curr = prev * (rowIndex - k + 1) / k;
            res.add((int) curr);
            prev = curr;
        }
        
        return res;
    }
}
```

## JavaScript

```javascript
/**
 * @param {number} rowIndex
 * @return {number[]}
 */
var getRow = function(rowIndex) {
    // Initialize array of size rowIndex + 1 with 1s
    const res = new Array(rowIndex + 1).fill(1);
    let prev = 1;
    
    // Calculate the values between the boundary 1s
    for (let k = 1; k < rowIndex; k++) {
        // Numbers in JS are double precision floats, safe up to 2^53 - 1
        // The max value in Pascal's triangle for rowIndex 33 is ~1.16 * 10^9, so it's perfectly safe
        let curr = (prev * (rowIndex - k + 1)) / k;
        res[k] = curr;
        prev = curr;
    }
    
    return res;
};
```

## Cpp

```cpp
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        // Initialize vector with size rowIndex + 1 and default value 1
        vector<int> res(rowIndex + 1, 1);
        long long prev = 1;
        
        // Iterate through the inner elements
        for (int k = 1; k < rowIndex; ++k) {
            // Use long long to avoid overflow when multiplying large numbers
            long long curr = prev * (rowIndex - k + 1) / k;
            res[k] = curr;
            prev = curr;
        }
        
        return res;
    }
};
```

## Csharp

```csharp
public class Solution {
    public IList<int> GetRow(int rowIndex) {
        int[] res = new int[rowIndex + 1];
        // Set the first element
        res[0] = 1;
        
        long prev = 1;
        for (int k = 1; k <= rowIndex; k++) {
            // Compute the next element using the combination formula
            // We use 'long' to prevent multiplication overflow
            long curr = prev * (rowIndex - k + 1) / k;
            res[k] = (int)curr;
            prev = curr;
        }
        
        return res;
    }
}
```

## Go

```go
func getRow(rowIndex int) []int {
    // Initialize the slice with the required size
    res := make([]int, rowIndex + 1)
    res[0] = 1
    
    prev := int64(1)
    for k := 1; k <= rowIndex; k++ {
        // Calculate current element using int64 to prevent overflow
        curr := prev * int64(rowIndex - k + 1) / int64(k)
        res[k] = int(curr)
        prev = curr
    }
    
    return res
}
```

## Ruby

```ruby
# @param {Integer} row_index
# @return {Integer[]}
def get_row(row_index)
    # Create array initialized with 1s
    res = Array.new(row_index + 1, 1)
    prev = 1
    
    # Calculate the inner values
    (1...row_index).each do |k|
        # Ruby automatically handles arbitrarily large integers, so no overflow concerns
        curr = prev * (row_index - k + 1) / k
        res[k] = curr
        prev = curr
    end
    
    res
end
```

## Rust

```rust
impl Solution {
    pub fn get_row(row_index: i32) -> Vec<i32> {
        // Initialize vector with 1s
        let mut res = vec![1; (row_index + 1) as usize];
        let mut prev: i64 = 1;
        
        for k in 1..row_index {
            // Use i64 for calculation to avoid integer overflow
            let curr = prev * (row_index as i64 - k as i64 + 1) / k as i64;
            res[k as usize] = curr as i32;
            prev = curr;
        }
        
        res
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun getRow(rowIndex: Int): List<Int> {
        // Initialize array with 1s
        val res = IntArray(rowIndex + 1) { 1 }
        var prev: Long = 1L
        
        for (k in 1 until rowIndex) {
            // Use Long to prevent overflow during intermediate multiplication
            val curr = prev * (rowIndex - k + 1) / k
            res[k] = curr.toInt()
            prev = curr
        }
        
        return res.toList()
    }
}
```

## Swift

```swift
class Solution {
    func getRow(_ rowIndex: Int) -> [Int] {
        // Initialize array of given size with 1s
        var res = Array(repeating: 1, count: rowIndex + 1)
        var prev = 1
        
        if rowIndex > 1 {
            for k in 1..<rowIndex {
                // Compute using combination formula
                // Standard Int in Swift is 64-bit on modern Apple platforms, avoiding overflow for rowIndex <= 33
                let curr = prev * (rowIndex - k + 1) / k
                res[k] = curr
                prev = curr
            }
        }
        
        return res
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

访问原文链接：[119. 杨辉三角 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/119-pascals-triangle-ii)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

