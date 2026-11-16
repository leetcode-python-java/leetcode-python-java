# 3689. 最大子数组总和 I - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 coder.id 打造你的开发者个人IP →**](https://www.coder.id)

访问原文链接：[3689. 最大子数组总和 I - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/3689-maximum-total-subarray-value-i)，体验更佳！

力扣链接：[3689. 最大子数组总和 I](https://leetcode.cn/problems/maximum-total-subarray-value-i), 难度等级：**中等**。

## LeetCode “3689. 最大子数组总和 I”问题描述

给你一个长度为 `n` 的整数数组 `nums` 和一个整数 `k`。

你需要恰好选择 `k` 个 `nums` 的非空子数组 `nums[l..r]`。子数组可以重叠，并且完全相同的子数组（相同的 `l` 和 `r`）**可以**被多次选择。

子数组 `nums[l..r]` 的 **值** 定义为：`max(nums[l..r]) - min(nums[l..r])`。

**总和** 是所有被选中的子数组的 **值** 之和。

返回你能达到的 **最大** 可能总和。

**子数组** 是数组中连续的 **非空** 元素序列。


### [示例 1]

**输入**: `nums = [1,3,2], k = 2`

**输出**: `4`

**解释**: 

<p>一种最优方案是：<br>
- 选择 <code>nums[0..1] = [1, 3]</code>。最大值是 3，最小值是 1，产生的值为 <code>3 - 1 = 2</code>。<br>
- 选择 <code>nums[0..2] = [1, 3, 2]</code>。最大值仍然是 3，最小值仍然是 1，因此值也为 <code>3 - 1 = 2</code>。<br>
将这些值相加得到 <code>2 + 2 = 4</code>。</p>


### [示例 2]

**输入**: `nums = [4,2,5,1], k = 3`

**输出**: `12`

**解释**: 

<p>一种最优方案是：<br>
- 选择 <code>nums[0..3] = [4, 2, 5, 1]</code>。最大值是 5，最小值是 1，产生的值为 <code>5 - 1 = 4</code>。<br>
- 选择 <code>nums[0..3] = [4, 2, 5, 1]</code>。最大值是 5，最小值是 1，所以值也为 <code>4</code>。<br>
- 选择 <code>nums[2..3] = [5, 1]</code>。最大值是 5，最小值是 1，所以值再次为 <code>4</code>。<br>
将这些值相加得到 <code>4 + 4 + 4 = 12</code>。</p>


### [约束]

- `1 <= n == nums.length <= 5 * 10^4`
- `0 <= nums[i] <= 10^9`
- `1 <= k <= 10^5`

### [Hints]

<details>
  <summary>提示 1</summary>
  Choose the whole subarray `k` times.

  
</details>

## 思路

问题要求我们准确选择 `k` 个子数组，使得所有选定子数组的 `max(subarray) - min(subarray)` 之和最大化。我们可以选择重叠的子数组，甚至可以多次选择完全相同的子数组。

这里的一个关键观察是，对于任何子数组 `nums[l..r]`，其最大值永远不会超过整个数组的全局最大值，其最小值也永远不会小于整个数组的全局最小值。在数学上，`max(nums[l..r]) <= max(nums)` 且 `min(nums[l..r]) >= min(nums)`。

因此，*任何*子数组的值的上限都是 `max(nums) - min(nums)`。因为我们想要最大化恰好 `k` 个子数组的总和，而且题目允许我们多次选择完全相同的子数组，所以最优策略就是直接把整个数组 `nums` 选择 `k` 次。

这个问题就简化成了：找到数组的全局最大值和全局最小值，计算它们的差值，然后将该差值乘以 `k`。

## 步骤

1. **寻找全局极值：** 遍历数组 `nums` 一次，找到最大值（`maxVal`）和最小值（`minVal`）。
2. **计算差值：** 从全局最大值中减去全局最小值，得到单个子数组可能产生的最大值（`maxVal - minVal`）。
3. **乘以 `k`：** 因为我们可以把整个数组选择 `k` 次，所以将差值乘以 `k` 即可得到最大总和。
4. **处理大数：** 结果可能高达 `10^5 * 10^9 = 10^{14}`，这超出了 32 位有符号整数的限制。确保在计算时使用 64 位整数（例如 Java/C# 中的 `long`，C++ 中的 `long long`）以防止溢出。

## 复杂度

> - **时间复杂度：** `O(N)`，其中 `N` 是数组的长度。我们只需要遍历数组一次即可找到最大值和最小值。
- **空间复杂度：** `O(1)`。我们只使用了几个额外的变量来跟踪最大值和最小值，这需要常数级别的额外空间。

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Python

```python
class Solution:
    def maxTotalValue(self, nums: List[int], k: int) -> int:
        # We can find the global maximum and minimum of the entire array using built-in functions.
        # The time complexity of max() and min() is O(N) each, making the total O(N).
        max_val = max(nums)
        min_val = min(nums)
        
        # The optimal approach is to pick the entire array exactly k times.
        # This gives us the absolute maximum difference possible.
        # Python automatically handles arbitrarily large integers, so no overflow concerns.
        return k * (max_val - min_val)
```

## Java

```java
class Solution {
    public long maxTotalValue(int[] nums, int k) {
        // Initialize max and min values with the first element of the array
        int maxVal = nums[0];
        int minVal = nums[0];
        
        // Iterate through the array to find the global maximum and minimum
        for (int num : nums) {
            if (num > maxVal) {
                maxVal = num;
            }
            if (num < minVal) {
                minVal = num;
            }
        }
        
        // The maximum value for a single subarray is maxVal - minVal.
        // We multiply this by k to get the maximum total value.
        // Cast k to a long before multiplication to prevent 32-bit integer overflow.
        return (long) k * (maxVal - minVal);
    }
}
```

## JavaScript

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var maxTotalValue = function(nums, k) {
    // Initialize the global extreme values
    let maxVal = nums[0];
    let minVal = nums[0];
    
    // Iterate through the array once to find the global max and min.
    // We do not use Math.max(...nums) because it can throw a Maximum Call Stack Size 
    // Exceeded error if the array is very large (e.g. 50,000 elements).
    for (let i = 1; i < nums.length; i++) {
        if (nums[i] > maxVal) maxVal = nums[i];
        if (nums[i] < minVal) minVal = nums[i];
    }
    
    // Return the difference multiplied by k.
    // JS numbers are double-precision floats, which safely represent integers up to 2^53 - 1.
    // Our max possible answer is 10^14, which fits comfortably without needing BigInt.
    return k * (maxVal - minVal);
};
```

## C++

```cpp
class Solution {
public:
    long long maxTotalValue(vector<int>& nums, int k) {
        // Initialize max and min with the first element
        int maxVal = nums[0];
        int minVal = nums[0];
        
        // Find the global maximum and minimum in the array
        for (int num : nums) {
            if (num > maxVal) maxVal = num;
            if (num < minVal) minVal = num;
        }
        
        // We choose the entire array k times.
        // The maximum possible value is 10^14, which exceeds the 32-bit int limit.
        // So we cast k to long long to perform 64-bit arithmetic.
        return (long long) k * (maxVal - minVal);
    }
};
```

## C#

```csharp
public class Solution {
    public long MaxTotalValue(int[] nums, int k) {
        // Initialize the extreme values using the first element
        int maxVal = nums[0];
        int minVal = nums[0];
        
        // Iterate over all elements to find the global maximum and minimum
        foreach (int num in nums) {
            if (num > maxVal) maxVal = num;
            if (num < minVal) minVal = num;
        }
        
        // Since max difference is 10^9 and k is 10^5, the product can be 10^14.
        // We explicitly cast to long to avoid 32-bit integer overflow.
        return (long) k * (maxVal - minVal);
    }
}
```

## Go

```go
func maxTotalValue(nums []int, k int) int64 {
    // Start by assuming the first element is both the max and the min
    maxVal := nums[0]
    minVal := nums[0]
    
    // Make a single pass through the array to update max and min
    for _, num := range nums {
        if num > maxVal {
            maxVal = num
        }
        if num < minVal {
            minVal = num
        }
    }
    
    // Calculate the difference and multiply by k.
    // Cast everything to int64 to avoid overflow since the answer can be up to 10^14.
    return int64(k) * int64(maxVal - minVal)
}
```

## Ruby

```ruby
# @param {Integer[]} nums
# @param {Integer} k
# @return {Integer}
def max_total_value(nums, k)
    # Ruby arrays have highly optimized built-in methods for max and min.
    # We find the global maximum and minimum.
    max_val = nums.max
    min_val = nums.min
    
    # We can pick the entire array exactly k times to get the maximum sum.
    # Ruby automatically handles large integers seamlessly, so no overflow occurs.
    k * (max_val - min_val)
end
```

## Rust

```rust
impl Solution {
    pub fn max_total_value(nums: Vec<i32>, k: i32) -> i64 {
        // Initialize max and min with the first element of the array
        let mut max_val = nums[0];
        let mut min_val = nums[0];
        
        // Iterate through the array to find the global extreme values
        for &num in nums.iter() {
            if num > max_val { max_val = num; }
            if num < min_val { min_val = num; }
        }
        
        // Calculate the maximum difference
        let diff = (max_val - min_val) as i64;
        
        // Multiply by k using 64-bit integer arithmetic to prevent overflow
        (k as i64) * diff
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun maxTotalValue(nums: IntArray, k: Int): Long {
        // Assume the first element is both the minimum and maximum
        var maxVal = nums[0]
        var minVal = nums[0]
        
        // Iterate through all elements to find the global max and min
        for (num in nums) {
            if (num > maxVal) maxVal = num
            if (num < minVal) minVal = num
        }
        
        // Cast k and the difference to Long to prevent 32-bit integer overflow.
        // The max possible value is 10^14.
        return k.toLong() * (maxVal - minVal).toLong()
    }
}
```

## Swift

```swift
class Solution {
    func maxTotalValue(_ nums: [Int], _ k: Int) -> Int {
        // Initialize extremes using the first element
        var maxVal = nums[0]
        var minVal = nums[0]
        
        // Single pass to find the global maximum and minimum
        for num in nums {
            if num > maxVal { maxVal = num }
            if num < minVal { minVal = num }
        }
        
        // Swift's Int is 64-bit on 64-bit platforms, which safely holds 10^14.
        // Simply return the difference multiplied by k.
        return k * (maxVal - minVal)
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

访问原文链接：[3689. 最大子数组总和 I - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/3689-maximum-total-subarray-value-i)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

