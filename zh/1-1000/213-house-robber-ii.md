# 213. House Robber II
LeetCode problem link: [213. House Robber II](https://leetcode.com/problems/house-robber-ii/)

## LeetCode problem description
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle**. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return the maximum amount of money you can rob tonight **without alerting the police**.

```
----------------------------------------------------------------------------------------------------------------------
[Example 1]

Input: nums = [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.
----------------------------------------------------------------------------------------------------------------------
[Example 2]

Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
----------------------------------------------------------------------------------------------------------------------
[Example 3]

Input: nums = [1,2,3]
Output: 3
----------------------------------------------------------------------------------------------------------------------
[Constraints]

1 <= nums.length <= 100
0 <= nums[i] <= 1000
----------------------------------------------------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Dynamic programming**.

Detailed solutions will be given later, and now only the best practices in 3 to 7 languages are given.

### Complexity
* Time: `O(n)`.
* Space: `O(n)`.

## Python
### Solution 1
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) <= 2:
            return max(nums)

        return max(
            max_money_robbed(nums[1:]),
            max_money_robbed(nums[:len(nums) - 1])
        )

def max_money_robbed(nums):
    dp = [0] * len(nums)
    dp[0] = nums[0]
    dp[1] = max(nums[0], nums[1])

    for i in range(2, len(dp)):
        dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])

    return dp[-1]
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## Java
```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## C#
```c#
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
var rob = function (nums) {
  if (nums.length <= 2) {
    return Math.max(...nums)
  }

  return Math.max(
      maxMoneyRobbed(nums.slice(1,)),
      maxMoneyRobbed(nums.slice(0, nums.length - 1))
  )
};

var maxMoneyRobbed = function (nums) {
  const dp = Array(nums.length).fill(0)
  dp[0] = nums[0]
  dp[1] = Math.max(nums[0], nums[1])

  for (let i = 2; i < dp.length; i++) {
    dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i])
  }

  return dp.at(-1)
};
```

## Go
```go
func rob(nums []int) int {
    if len(nums) <= 2 {
        return slices.Max(nums)
    }

    return max(
        maxMoneyRobbed(nums[1:]),
        maxMoneyRobbed(nums[:len(nums) - 1]),
    )
}

func maxMoneyRobbed(nums []int) int {
    dp := make([]int, len(nums))
    dp[0] = nums[0]
    dp[1] = max(nums[0], nums[1])

    for i := 2; i < len(dp); i++ {
        dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])
    }

    return dp[len(dp) - 1]
}
```

## Ruby
```ruby
# Welcome to create a PR to complete the code of this language, thanks!
```

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
