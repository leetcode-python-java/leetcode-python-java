# 53. Maximum Subarray - LeetCode Best Practices

Visit original link: [53. Maximum Subarray - LeetCode Best Practices](https://leetcoder.net/en/leetcode/53-maximum-subarray) for a better experience!

LeetCode link: [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray), difficulty: **Medium**.

## LeetCode description of "53. Maximum Subarray"

Given an integer array `nums`, find the `subarray` with the largest sum, and return its sum.

### [Example 1]

**Input**: `nums = [-2,1,-3,4,-1,2,1,-5,4]`

**Output**: `6`

**Explanation**: 

<p>The subarray [4,-1,2,1] has the largest sum 6.</p>


### [Example 2]

**Input**: `nums = [1]`

**Output**: `1`

**Explanation**: `The subarray [1] has the largest sum 1.`

### [Example 3]

**Input**: `nums = [5,4,-1,7,8]`

**Output**: `23`

**Explanation**: 

<p>The subarray [5,4,-1,7,8] has the largest sum 23.</p>


### [Constraints]

- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`

## Intuition 1

- This problem can be solved by using `Greedy Algorithm` (please see `solution 2`), but here we will use another way.
- Imagine the size of nums is `i`, let us consider if the same question is applied to the `subarray` of `nums` from index `0` to `i - 1`.
- The answer is `yes`. Then let us think if the `i - 1`'s answer could impact the answer of `i`.
- The answer is still `yes`. What would be the impact?
- For `nums[i]`,
    1. If the `previous sum` is negative, we can discard `previous sum`;
    2. If the `previous sum` is positive, we can add `previous sum` to the `current sum`.
- So we can use `Dynamic Programming` to solve the problem. The characteristic of the "Dynamic Programming" algorithm is that the value of `dp[i]` is converted from `dp[i - 1]`.

## Steps

### Common steps in dynamic programming

These five steps are a pattern for solving `dynamic programming` problems.

1. Determine the **meaning** of the `dp[i]`
    - At first, try to use the problem's `return` value as the value of `dp[i]` to determine the meaning of `dp[i]`. If it doesn't work, try another way.
    - Imagine that `dp[i]` represents the `largest sum` at index `i`. Is this okay?
        mark-detail `dp[i + 1]` cannot be calculated by `dp[i]`. So we have to change the meaning. mark-detail
- How to design it?
        mark-detail If `dp[i]` represents the `current sum` at index `i`, `dp[i + 1]` can be calculated by `dp[i]`. Finally, we can see that the `maximum sum` is recorded in the `current sum` array. mark-detail
2. Determine the `dp` array's initial value
    - Use an example:

        ```ruby
        nums = [-2,  1, -3,  4, -1,  2,  1, -5,  4]
        dp   = [-2,  1, -3,  4, -1,  2,  1, -5,  4]
        ```
    - `dp[i] = nums[i]` would be good.
3. Determine the `dp` array's recurrence formula
    - Try to complete the `dp` array. In the process, you will get inspiration to derive the formula.

        ```ruby
        nums = [-2,  1, -3,  4, -1,  2,  1, -5,  4]
        dp   = [-2,  1,  N,  N,  N,  N,  N,  N,  N] # N means don't pay attention to it now
        dp   = [-2,  1, -2,  N,  N,  N,  N,  N,  N]
        dp   = [-2,  1, -2,  4,  N,  N,  N,  N,  N]
        dp   = [-2,  1, -2,  4,  3,  N,  N,  N,  N]
        dp   = [-2,  1, -2,  4,  3,  5,  N,  N,  N]
        dp   = [-2,  1, -2,  4,  3,  5,  6,  N,  N]
        dp   = [-2,  1, -2,  4,  3,  5,  6,  1,  N]
        dp   = [-2,  1, -2,  4,  3,  5,  6,  1,  5]
        ```
    - After analyzing the sample `dp` array, we can derive the `Recurrence Formula`:

        ```python
        dp[i] = max(nums[i], dp[i - 1] + nums[i])
        ```
4. Determine the `dp` array's traversal order
    - `dp[i]` depends on `dp[i - 1]`, so we should traverse the `dp` array from left to right.
5. Check the `dp` array's value
    - Print the `dp` to see if it is as expected.

## Complexity

- Time complexity: `O(n)`.
- Space complexity: `O(n)`.

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

## Intuition 2

- The "greedy" algorithm solution and the "dynamic programming" algorithm solution for this problem are essentially the same, both are "dynamic programming", but the "greedy" algorithm here changes from using the dp one-dimensional array and then reducing one dimension to using only two variables.
- The "greedy" algorithm here can be called "rolling variables". Just like "rolling array (one-dimensional)" corresponds to a two-dimensional array, one dimension can be reduced by rolling.

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

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

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [leetcoder.net](https://leetcoder.net): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [53. Maximum Subarray - LeetCode Best Practices](https://leetcoder.net/en/leetcode/53-maximum-subarray).

GitHub repository: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

