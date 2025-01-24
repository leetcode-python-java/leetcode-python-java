# 718. Maximum Length of Repeated Subarray
LeetCode link: [718. Maximum Length of Repeated Subarray](https://leetcode.com/problems/maximum-length-of-repeated-subarray/)

## LeetCode problem description
Given two integer arrays `nums1` and `nums2`, return the **maximum length of a subarray** that appears in **both** arrays.

```
------------------------------------------------------------------------
[Example 1]

Input: nums1 = [1,2,3,2,1], nums2 = [3,2,1,4,7]
Output: 3

Explanation: The repeated subarray with maximum length is [3,2,1].
------------------------------------------------------------------------
[Example 2]

Input: nums1 = [0,0,0,0,0], nums2 = [0,0,0,0,0]
Output: 5

Explanation: The repeated subarray with maximum length is [0,0,0,0,0].
------------------------------------------------------------------------
[Constraints]

1 <= nums1.length, nums2.length <= 1000
0 <= nums1[i], nums2[i] <= 100
------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Dynamic programming**.

Detailed solutions will be given later, and now only the best practices in 4 to 7 languages are given.

**Do not use a rolling array** as `dp` because that is more difficult to write and understand.

### Complexity
* Time: `O(n * m)`.
* Space: `O(n * m)`.

## Java
```java
class Solution {
    public int findLength(int[] nums1, int[] nums2) {
        var maxLength = 0;
        var dp = new int[nums1.length + 1][nums2.length + 1];

        for (var i = 1; i < dp.length; i++) {
            for (var j = 1; j < dp[0].length; j++) {
                if (nums1[i - 1] == nums2[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                    maxLength = Math.max(dp[i][j], maxLength);
                }
            }
        }

        return maxLength;
    }
}
```

## C#
```c#
public class Solution
{
    public int FindLength(int[] nums1, int[] nums2)
    {
        int maxLength = 0;
        var dp = new int[nums1.Length + 1, nums2.Length + 1];

        for (var i = 1; i < dp.GetLength(0); i++)
        {
            for (var j = 1; j < dp.GetLength(1); j++)
            {
                if (nums1[i - 1] == nums2[j - 1])
                {
                    dp[i, j] = dp[i - 1, j - 1] + 1;
                    maxLength = Math.Max(dp[i, j], maxLength);
                }
            }
        }

        return maxLength;
    }
}
```

## Python
```python
class Solution:
    def findLength(self, nums1: List[int], nums2: List[int]) -> int:
        max_length = 0
        dp = [[0] * (len(nums2) + 1) for _ in range(len(nums1) + 1)]

        for i in range(1, len(dp)):
            for j in range(1, len(dp[0])):
                if nums1[i - 1] == nums2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1] + 1
                    max_length = max(dp[i][j], max_length)

        return max_length
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
var findLength = function (nums1, nums2) {
  let maxLength = 0
  const dp = Array(nums1.length + 1).fill().map(
    () => Array(nums2.length + 1).fill(0)
  )

  for (let i = 1; i < dp.length; i++) {
    for (let j = 1; j < dp[0].length; j++) {
      if (nums1[i - 1] == nums2[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1] + 1
        maxLength = Math.max(dp[i][j], maxLength)
      }
    }
  }

  return maxLength
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
