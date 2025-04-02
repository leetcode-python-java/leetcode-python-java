# 53. 最大子数组和 - 力扣题解最佳实践

访问原文链接：[53. 最大子数组和 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/53-maximum-subarray)，体验更佳！

力扣链接：[53. 最大子数组和](https://leetcode.cn/problems/maximum-subarray), 难度：**中等**。

## 力扣“53. 最大子数组和”问题描述

给你一个整数数组 `nums` ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

**子数组**是数组中的一个连续部分。

### [示例 1]

**输入**: `nums = [-2,1,-3,4,-1,2,1,-5,4]`

**输出**: `6`

**解释**: `连续子数组 [4,-1,2,1] 的和最大，为 6 。`

### [示例 2]

**输入**: `nums = [1]`

**输出**: `1`

**解释**: `The subarray [1] has the largest sum 1.`

### [示例 3]

**输入**: `nums = [5,4,-1,7,8]`

**输出**: `23`

**解释**: 

<p>The subarray [5,4,-1,7,8] has the largest sum 23.</p>


### [约束]

- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`

## 思路 1

- 本题可以用贪心算法解决（请看`方案2`），不过这里我们使用另一种方法。
- 假设`nums`的大小为`i`，我们考虑将同样的问题应用到`nums`的子数组中，从索引`0`到`i - 1`。
- 答案是肯定的。那么我们再想想`i - 1`的答案是否会影响`i`的答案。
- 答案仍然是肯定的。那会有什么影响呢？对于nums[i]，
    1. 如果`上一次的和`为负数，我们可以丢弃`上一次的和`；
    2. 如果`上一次的和`为正数，我们可以将`上一次的和`加到`当前和`中。
- 所以我们可以使用`动态规划`来解决这个问题。 “动态规划”算法的特点是，`dp[i]` 的值由 `dp[i - 1]` 转化而来。

## 步骤

### 动态规划的常用步骤

这五个步骤是解决`动态规划`问题的模式。

1. 确定`dp[i]`的**含义**
    - 首先，尝试使用问题的`return`值作为`dp[i]`的值来确定`dp[i]`的含义。如果不行，请尝试另一种方法。
    - 假设`dp[i]`表示索引`i`处的`最大和`。这样做行吗？
        mark-detail `dp[i + 1]`无法通过`dp[i]`计算。所以我们必须改变这个含义。mark-detail
    - 该如何设计呢？
        mark-detail 如果`dp[i]`表示索引`i`处的`当前和`，`dp[i + 1]`就可以通过`dp[i]`计算。最后，我们就可以看到`最大和`记录在`当前和`数组中。mark-detail
2. 确定 `dp` 数组的初值
    - 使用示例：

        ```ruby
        nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
        dp = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
        ```
    - `dp[i] = nums[i]` 就好。
3. 确定 `dp` 数组的递归公式
    - 尝试完成 `dp` 数组。在此过程中，您将获得推导公式的灵感。

        ```ruby
        nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
        dp = [-2, 1, N, N, N, N, N, N, N] # N 表示现在不关注
        dp = [-2, 1, -2, N, N, N, N, N, N]
        dp = [-2, 1, -2, 4, N, N, N, N, N]
        dp = [-2, 1, -2, 4, 3, N, N, N, N]
        dp = [-2, 1, -2, 4, 3, 5, N, N, N]
        dp = [-2, 1, -2, 4, 3, 5, 6, N, N]
        dp = [-2, 1, -2, 4, 3, 5, 6, 1, N]
        dp = [-2, 1, -2, 4, 3, 5, 6, 1, 5]
        ```
    - 分析完示例 `dp` 数组，我们可以得出 `递归公式`:

        ```python
        dp[i] = max(nums[i], dp[i - 1] + nums[i])
        ```
4. 确定 `dp` 数组的遍历顺序
    - `dp[i]` 依赖于 `dp[i - 1]`，所以我们应该从左到右遍历 `dp` 数组。
5. 检查 `dp` 数组的值
    - 打印 `dp` 看看是否符合预期。

## 复杂度

- 时间复杂度: `O(n)`.
- 空间复杂度: `O(n)`.

## Python

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        dp = nums.copy()

        for i in range(1, len(dp)):
            dp[i] = max(nums[i], dp[i - 1] + nums[i])

        return max(dp)
```

## Java

```java
class Solution {
    public int maxSubArray(int[] nums) {
        var dp = nums.clone();
        
        for (var i = 1; i < dp.length; i++) {
            dp[i] = Math.max(nums[i], dp[i - 1] + nums[i]);
        }

        return IntStream.of(dp).max().getAsInt(); // if you want to beat 99%, refer to C# soluiton's comment 
    }
}
```

## JavaScript

```javascript
var maxSubArray = function (nums) {
  const dp = [...nums]

  for (let i = 1; i < dp.length; i++) {
    dp[i] = Math.max(nums[i], dp[i - 1] + nums[i])
  }

  return Math.max(...dp)
};
```

## Go

```go
func maxSubArray(nums []int) int {
    dp := slices.Clone(nums)

    for i := 1; i < len(nums); i++ {
        dp[i] = max(nums[i], dp[i - 1] + nums[i])
    }

    return slices.Max(dp)
}
```

## Ruby

```ruby
def max_sub_array(nums)
  dp = nums.clone

  (1...dp.size).each do |i|
    dp[i] = [ nums[i], dp[i - 1] + nums[i] ].max
  end

  dp.max
end
```

## C#

```csharp
public class Solution
{
    public int MaxSubArray(int[] nums)
    {
        var dp = (int[])nums.Clone();

        for (var i = 1; i < dp.Length; i++)
        {
            dp[i] = Math.Max(nums[i], dp[i - 1] + nums[i]);
        }

        return dp.Max(); // if you want to beat 99%, you can use a variable to collect the maximum value: `if (dp[i] > result) result = dp[i];`
    }
}
```

## C++

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        auto dp = nums;

        for (auto i = 1; i < dp.size(); i++) {
            dp[i] = max(nums[i], dp[i - 1] + nums[i]);
        }

        return *max_element(dp.begin(), dp.end());
    }
};
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## 思路 2

- 本题的“贪心”算法解法和“动态规划”算法解法在本质上是一样的，都是“动态规划”，只不过此处的“贪心”算法把从使用`dp`一维数组，再降一个维度，变成了只使用两个变量。
- 此处的“贪心”算法可以被称为“滚动变量”。就像“滚动数组（一维）”对应的是二维数组一样，一滚动就能降一个维度。

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Python

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        result = -float('inf')
        pre_sum = 0

        for num in nums:
            pre_sum = max(pre_sum + num, num)
            result = max(result, pre_sum)
        
        return result
```

## C++

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int result = INT_MIN;
        int pre_sum = 0;

        for (int num : nums) {
            pre_sum = max(pre_sum + num, num);
            result = max(result, pre_sum);
        }

        return result;
    }
};
```

## Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer}
def max_sub_array(nums)
  result = -Float::INFINITY
  pre_sum = 0

  nums.each do |num|
    pre_sum = [pre_sum + num, num].max
    result = [result, pre_sum].max
  end

  result
end
```

## Go

```go
func maxSubArray(nums []int) int {
    result := math.MinInt
    preSum := 0

    for _, num := range nums {
        preSum = max(preSum + num, num)
        if preSum > result {
            result = preSum
        }
    }

    return result
}
```

## JavaScript

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    let result = -Infinity;
    let preSum = 0;

    for (const num of nums) {
        preSum = Math.max(preSum + num, num);
        result = Math.max(result, preSum);
    }

    return result;
};
```

## C#

```csharp
public class Solution
{
    public int MaxSubArray(int[] nums)
    {
        int result = int.MinValue;
        int preSum = 0;

        foreach (int num in nums)
        {
            preSum = Math.Max(preSum + num, num);
            result = Math.Max(result, preSum);
        }

        return result;
    }
}
```

## Java

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int result = Integer.MIN_VALUE;
        int preSum = 0;

        for (int num : nums) {
            preSum = Math.max(preSum + num, num);
            result = Math.max(result, preSum);
        }

        return result;
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [leetcoder.net](https://leetcoder.net/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[53. 最大子数组和 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/53-maximum-subarray).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

