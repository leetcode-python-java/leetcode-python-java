# 53. 最大子数组和 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

访问原文链接：[53. 最大子数组和 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.to/zh/leetcode/53-maximum-subarray)，体验更佳！

力扣链接：[53. 最大子数组和](https://leetcode.cn/problems/maximum-subarray), 难度等级：**中等**。

## LeetCode “53. 最大子数组和”问题描述

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
- 对于`nums[i]`：
    1. 如果`上一次的和`为负数，我们可以丢弃`上一次的和`；
    2. 如果`上一次的和`为正数，我们可以将`上一次的和`加到`当前和`中。
- 因此，它符合`动态规划`问题的特点。

## “动态规划”的模式

“动态规划”，需要用`dp`数组来保存结果。`dp[i][j]`的值可以由它的前一个（或多个）值通过公式转化出来。因此，`dp[i][j]`值是一步一步推导出来的，它和先前的`dp`记录值都有联系。

#### “动态规划”分为五步

1. 确定数组`dp`的每个值代表的**含义**。
2. 初始化数组`dp`的值。
3. 根据一个示例，**按顺序**填入`dp`网格数据。
4. 根据`dp`网格数据，推导出**递推公式**。
5. 写出程序，并打印`dp`数组，不合预期就调整。

#### 细说这五步

1. 确定数组`dp`的每个值代表的**含义**。
    - 先确定`dp`是一维数组还是二维数组。“一维滚动数组”意味着每次迭代时都会覆盖数组的值。大多时候，用“一维滚动数组”代替“二维数组”可以简化代码；但有些题目，比如要操作“两个位置可互换的数组”，为了理解方便，还是使用“二维数组”。
    - 尝试使用问题所求的`返回值`的含义作为 `dp[i]`（一维）或`dp[i][j]`（二维）的含义，约60%的概率能行。如果不行，再尝试其他含义。
    - 设计上尽量考虑保存更丰富的信息，重复信息只在某个`dp[i]`中保存一次就够了。
    - 使用简化的含义。如果用`布尔值`可以解决问题，就不要用`数值`。
2. 初始化数组`dp`的值。`dp`的值涉及两个层面：
    1. `dp`的长度。通常是：`条件数组长度加1`或`条件数组长度`。
    2. `dp[i]`或`dp[i][j]`的值。`dp[0]`或`dp[0][0]`有时需要特殊处理。
3. 根据一个示例，**按顺序**填入`dp`网格数据。
    - “递推公式”是“动态规划”算法的核心。但“递推公式”是隐晦的，想得到它，就需要制表，用数据启发自己。
    - 如果原示例不够好，需要自己重新设计一个。
    - 根据示例，填入`dp`网格数据，需要“按顺序”填，这是很重要的，因为它决定了代码的遍历顺序。
    - 大多时候，从左到右，从上到下。但有时需要从右向左、由下而上、从中间向右（或左），如“回文串”问题。有时，还需要一行遍历两次，先正向，再反向。
    - 当顺序决定对了，起点就决定好了，从起点出发，“按顺序”填写`dp`网格数据，这也是在模拟程序处理的过程。
    - 在此过程中，您将获得写出“递推公式”的灵感。如果您已经能推导出公式，不需要填完网格。
4. 根据`dp`网格数据，推导出**递推公式**。
    - 有三个特别的位置需要注意： `dp[i - 1][j - 1]`、`dp[i - 1][j]`和`dp[i][j - 1]`，当前的 `dp[i][j]`往往取决于它们。
    - 操作“两个位置可互换的数组”时，因为对称性，我们可能需要同时使用`dp[i - 1][j]`和`dp[i][j - 1]`。
5. 写出程序，并打印`dp`数组，不合预期就调整。
    - 重点分析那些不合预期的数值。

读完了上面的内容，是不是感觉“动态规划”也没有那么难了？试着解出这道题吧。🤗

## 步骤

### 动态规划的常用步骤

这五个步骤是解决`动态规划`问题的模式。

1. 确定`dp[i]`的**含义**。
    - 假设`dp[i]`表示索引`i`处的`最大和`。这样做行吗？
        mark-detail `dp[i + 1]`无法通过`dp[i]`计算。所以我们必须改变这个含义。mark-detail
    - 该如何设计呢？
        mark-detail 如果`dp[i]`表示索引`i`处的`当前和`，`dp[i + 1]`就可以通过`dp[i]`计算。最后，我们就可以看到`最大和`记录在`当前和`数组中。mark-detail
2. 确定 `dp` 数组的初值。

    ```ruby
    nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
    dp = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
    ```
3. 根据一个示例，“按顺序”填入`dp`网格数据。


    ```ruby
    nums = [-2,  1, -3,  4, -1,  2,  1, -5,  4]
    dp   = [-2,  1,  N,  N,  N,  N,  N,  N,  N] # N 表示现在不关注
    dp   = [-2,  1, -2,  N,  N,  N,  N,  N,  N]
    dp   = [-2,  1, -2,  4,  N,  N,  N,  N,  N]
    dp   = [-2,  1, -2,  4,  3,  N,  N,  N,  N]
    dp   = [-2,  1, -2,  4,  3,  5,  N,  N,  N]
    dp   = [-2,  1, -2,  4,  3,  5,  6,  N,  N]
    dp   = [-2,  1, -2,  4,  3,  5,  6,  1,  N]
    dp   = [-2,  1, -2,  4,  3,  5,  6,  1,  5]
    ```
4. 根据`dp`网格数据，推导出“递推公式”。

    ```python
    dp[i] = max(nums[i], dp[i - 1] + nums[i])
    ```
5. 写出程序，并打印`dp`数组，不合预期就调整。

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

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.to](https://leetcode.to/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[53. 最大子数组和 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.to/zh/leetcode/53-maximum-subarray).

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

