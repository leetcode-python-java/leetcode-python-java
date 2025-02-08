# 300. Longest Increasing Subsequence
LeetCode link: [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)

## LeetCode problem description
Given an integer array `nums`, return the length of the **longest strictly increasing subsequence**.

```
-------------------------------------------------------------------------------------------
[Example 1]

Input: nums = [10,9,2,5,3,7,101,18]
Output: 4

Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
-------------------------------------------------------------------------------------------
[Example 2]

Input: nums = [0,1,0,3,2,3]
Output: 4
-------------------------------------------------------------------------------------------
[Example 3]

Input: nums = [7,7,7,7,7,7,7]
Output: 1
-------------------------------------------------------------------------------------------
[Constraints]

1 <= nums.length <= 2500
-10000 <= nums[i] <= 10000
-------------------------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Dynamic programming**.

Detailed solutions will be given later, and now only the best practices in 4 to 7 languages are given.

### Complexity
* Time: `O(n * n)`.
* Space: `O(n)`.

## C#
```c#
// 10, 9, 2, 5, 3, 7, 4, 3,101,18 # nums
//  1, 1, 1, 2, 2, 3, 3, 2,  4,4  # dp
public class Solution
{
    public int LengthOfLIS(int[] nums)
    {
        var dp = new int[nums.Length];
        Array.Fill(dp, 1);

        for (var i = 1; i < nums.Length; i++)
        {
            for (var j = i - 1; j >= 0; j--)
            {
                if (nums[i] > nums[j])
                {
                    dp[i] = Math.Max(dp[i], dp[j] + 1);
                }
            }
        }

        return dp.Max();
    }
}
```

## Python
```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        dp = [1] * len(nums)

        for i in range(1, len(dp)):
            for j in range(i - 1, -1, -1):
                if nums[i] > nums[j] and dp[j] + 1 > dp[i]:
                    dp[i] = dp[j] + 1

        return max(dp)
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## Java
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        var dp = new int[nums.length];
        Arrays.fill(dp, 1);

        for (var i = 1; i < nums.length; i++) {
            for (var j = i - 1; j >= 0; j--) {
                if (nums[i] > nums[j]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
        }

        return IntStream.of(dp).max().getAsInt();
    }
}
```

## JavaScript
```javascript
var lengthOfLIS = function (nums) {
  const dp = Array(nums.length).fill(1)

  nums.forEach((num, i) => {
    for (let j = i - 1; j >= 0; j--) {
      if (num > nums[j]) {
        dp[i] = Math.max(dp[i], dp[j] + 1)
      }
    }
  })

  return Math.max(...dp)
};
```

## Go
```go
// Welcome to create a PR to complete the code of this language, thanks!
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
