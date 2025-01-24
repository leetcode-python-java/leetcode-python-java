# 674. Longest Continuous Increasing Subsequence
LeetCode link: [674. Longest Continuous Increasing Subsequence](https://leetcode.com/problems/longest-continuous-increasing-subsequence/)

## LeetCode problem description
Given an integer array `nums`, return the length of the **longest strictly increasing subsequence**.

```
----------------------------------------------------------------------------------------------
[Example 1]

Input: nums = [10,9,2,5,3,7,101,18]
Output: 4

Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
----------------------------------------------------------------------------------------------
[Example 2]

Input: nums = [0,1,0,3,2,3]
Output: 4
----------------------------------------------------------------------------------------------
[Example 3]

Input: nums = [7,7,7,7,7,7,7]
Output: 1
----------------------------------------------------------------------------------------------
[Constraints]

1 <= nums.length <= 2500
-10000 <= nums[i] <= 10000
----------------------------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Dynamic programming**.

Detailed solutions will be given later, and now only the best practices in 4 to 7 languages are given.

### Complexity
* Time: `O(n)`.
* Space: `O(n)`.

## C#
```c#
// [1, 3, 5, 4, 3, 6, 2, 4, 5, 7, 4] # nums
// [1, 2, 3, 1, 1, 2, 1, 2, 3, 4, 1] # dp
public class Solution
{
    public int FindLengthOfLCIS(int[] nums)
    {
        var dp = new int[nums.Length];
        Array.Fill(dp, 1);

        for (var i = 1; i < nums.Length; i++)
        {
            if (nums[i] > nums[i - 1])
            {
                dp[i] = dp[i - 1] + 1;
            }
        }

        return dp.Max(); // If you want to beat 90%, refer to Java code.
    }
}
```

## Java
```java
class Solution {
    public int findLengthOfLCIS(int[] nums) {
        var result = 1;
        var dp = new int[nums.length];
        Arrays.fill(dp, 1);

        for (var i = 1; i < nums.length; i++) {
            if (nums[i] > nums[i - 1]) {
                dp[i] = dp[i - 1] + 1;
                result = Math.max(result, dp[i]);
            }
        }

        return result;
    }
}
```

## Python
```python
class Solution:
    def findLengthOfLCIS(self, nums: List[int]) -> int:
        dp = [1] * len(nums)

        for i, num in enumerate(nums):
            if i == 0:
                continue
            
            if num > nums[i - 1]:
                dp[i] = dp[i - 1] + 1

        return max(dp)
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
var findLengthOfLCIS = function (nums) {
  const dp = Array(nums.length).fill(1)

  nums.forEach((num, i) => {
    for (let j = i - 1; j >= 0; j--) {
      if (num > nums[i - 1]) {
        dp[i] = dp[i - 1] + 1
      }
    }
  })

  return Math.max(...dp) // If you want to beat 90%, refer to Java code.
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
