# 198. House Robber
LeetCode problem: [198. House Robber](https://leetcode.com/problems/house-robber/)

## LeetCode problem description
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected, and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return the maximum amount of money you can rob tonight **without alerting the police**.
```
-------------------------------------------------------------------------------------------------
[Example 1]

Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
-------------------------------------------------------------------------------------------------
[Example 2]
Input: nums = [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
-------------------------------------------------------------------------------------------------
[Constraints]

1 <= nums.length <= 100
0 <= nums[i] <= 400
-------------------------------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Dynamic programming**.

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Complexity
* Time: `O(n)`.
* Space: `O(n)`.

## C#
```c#
public class Solution
{
    public int Rob(int[] nums)
    {
        if (nums.Length == 1)
            return nums[0];

        var dp = new int[nums.Length];
        dp[0] = nums[0];
        dp[1] = Math.Max(nums[0], nums[1]);

        for (var i = 2; i < dp.Length; i++) 
        {
            dp[i] = Math.Max(dp[i - 1], dp[i - 2] + nums[i]);
        }

        return dp.Last();
    }
}
```

## Python
### Solution 1
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return nums[0]

        dp = [0] * len(nums)
        dp[0] = nums[0]
        dp[1] = max(nums[0], nums[1])

        for i in range(2, len(dp)):
            dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])

        return dp[-1]
```

## Solution 2: Using 'dp' which size is 2
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return nums[0]

        dp = [nums[0], max(nums[0], nums[1])]

        for num in nums[2:]:
            dc = dp.copy()

            dp[1] = max(dc[1], dc[0] + num)
            dp[0] = dc[1]

        return max(dp)
```

## C++
```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.size() == 1) {
            return nums[0];
        }

        auto dp = vector<int>(nums.size());
        dp[0] = nums[0];
        dp[1] = max(nums[0], nums[1]);

        for (auto i = 2; i < dp.size(); i++) {
            dp[i] = max(dp[i - 1], dp[i - 2] + nums[i]);
        }

        return dp.back();
    }
};
```

## Java
```java
class Solution {
    public int rob(int[] nums) {
        if (nums.length == 1) {
            return nums[0];
        }

        var dp = new int[nums.length];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);

        for (var i = 2; i < dp.length; i++) {
            dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i]);
        }

        return dp[dp.length - 1];
    }
}
```

## JavaScript
```javascript
var rob = function (nums) {
  if (nums.length === 1) {
    return nums[0]
  }

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
    if len(nums) == 1 {
        return nums[0]
    }

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
def rob(nums)
  return nums[0] if nums.size == 1

  dp = Array.new(nums.size, 0)
  dp[0] = nums[0]
  dp[1] = [ nums[0], nums[1] ].max

  (2...dp.size).each do |i|
    dp[i] = [ dp[i - 1], dp[i - 2] + nums[i] ].max
  end

  dp[-1]
end
```

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
