# 1035. Uncrossed Lines
LeetCode problem: [1035. Uncrossed Lines](https://leetcode.com/problems/uncrossed-lines/)

## LeetCode problem description
You are given two integer arrays `nums1` and `nums2`. We write the integers of `nums1` and `nums2` (in the order they are given) on two separate horizontal lines.

We may draw connecting lines: a straight line connecting two numbers `nums1[i]` and `nums2[j]` such that:

* `nums1[i]` == `nums2[j]`, and
* the line we draw does not intersect any other connecting (non-horizontal) line.

Note that a connecting line cannot intersect even at the endpoints (i.e., each number can only belong to one connecting line).

Return the maximum number of connecting lines we can draw in this way.

```
-------------------------------------------------------------------------------------------------------------------------------------------
[Example 1]

Input: nums1 = [1,4,2], nums2 = [1,2,4]
Output: 2
Explanation: We can draw 2 uncrossed lines as in the diagram.
We cannot draw 3 uncrossed lines, because the line from nums1[1] = 4 to nums2[2] = 4 will intersect the line from nums1[2]=2 to nums2[1]=2.
-------------------------------------------------------------------------------------------------------------------------------------------
[Example 2]

Input: nums1 = [2,5,1,2,5], nums2 = [10,5,2,1,5,2]
Output: 3
-------------------------------------------------------------------------------------------------------------------------------------------
[Example 3]

Input: nums1 = [1,3,7,1,7,5], nums2 = [1,9,2,5,1]
Output: 2
-------------------------------------------------------------------------------------------------------------------------------------------
[Constraints]

1 <= nums1.length, nums2.length <= 500
1 <= nums1[i], nums2[j] <= 2000
-------------------------------------------------------------------------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Dynamic programming**.

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Complexity
* Time: `O(n * m)`.
* Space: `O(n * m)`.

## Python
```python
# Example of a 2D 'dp' array:
# nums1 = [ 2, 5, 1, 2, 5]
# nums2 = [10, 5, 2, 1, 5, 2]
#     10 5 2 1 5 2
#   0  0 0 0 0 0 0          
# 2 0  0 0 1 1 1 1            
# 5 0  0 1 1 1 2 2        
# 1 0  ...           
# 2 0  ...           
# 5 0  ...  
class Solution:
    def maxUncrossedLines(self, nums1: List[int], nums2: List[int]) -> int:
        dp = [[0] * (len(nums2) + 1) for _ in range(len(nums1) + 1)]

        for i in range(1, len(dp)):
            for j in range(1, len(dp[0])):
                if nums1[i - 1] == nums2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1] + 1
                else:
                    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
        
        return dp[-1][-1]
```

## Java
```java
class Solution {
    public int maxUncrossedLines(int[] nums1, int[] nums2) {
        var dp = new int[nums1.length + 1][nums2.length + 1];

        for (var i = 1; i < dp.length; i++) {
            for (var j = 1; j < dp[0].length; j++) {
                if (nums1[i - 1] == nums2[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[dp.length - 1][dp[0].length - 1];
    }
}
```

## C#
```c#
public class Solution
{
    public int MaxUncrossedLines(int[] nums1, int[] nums2)
    {
        var dp = new int[nums1.Length + 1, nums2.Length + 1];

        for (var i = 1; i < dp.GetLength(0); i++)
        {
            for (var j = 1; j < dp.GetLength(1); j++)
            {
                if (nums1[i - 1] == nums2[j - 1])
                {
                    dp[i, j] = dp[i - 1, j - 1] + 1;
                }
                else
                {
                    dp[i, j] = Math.Max(dp[i - 1, j], dp[i, j - 1]);
                }
            }
        }

        return dp[dp.GetUpperBound(0), dp.GetUpperBound(1)];
    }
}
```

## C++
```cpp
class Solution {
public:
    int maxUncrossedLines(vector<int>& nums1, vector<int>& nums2) {
        vector<vector<int>> dp(nums1.size() + 1, vector<int>(nums2.size() + 1));

        for (auto i = 1; i < dp.size(); i++) {
            for (auto j = 1; j < dp[0].size(); j++) {
                if (nums1[i - 1] == nums2[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[dp.size() - 1][dp[0].size() - 1];
    }
};
```

## JavaScript
```javascript
var maxUncrossedLines = function(nums1, nums2) {
  const dp = Array(nums1.length + 1).fill().map(
    () => Array(nums2.length + 1).fill(0)
  )

  for (let i = 1; i < dp.length; i++) {
    for (let j = 1; j < dp[0].length; j++) {
      if (nums1[i - 1] === nums2[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1] + 1
      } else {
        dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1])
      }
    }
  }

  return dp.at(-1).at(-1)
};
```

## Go
```go
func maxUncrossedLines(nums1 []int, nums2 []int) int {
    dp := make([][]int, len(nums1) + 1)
    for i := range dp {
        dp[i] = make([]int, len(nums2) + 1)
    }

    for i := 1; i < len(dp); i++ {
        for j := 1; j < len(dp[0]); j++ {
            if nums1[i - 1] == nums2[j - 1] {
                dp[i][j] = dp[i - 1][j - 1] + 1
            } else {
                dp[i][j] = max(dp[i][j - 1], dp[i - 1][j])
            }
        }
    }

    return dp[len(dp) - 1][len(dp[0]) - 1]
}
```

## Ruby
```ruby
def max_uncrossed_lines(nums1, nums2)
  dp = Array.new(nums1.size + 1) do
    Array.new(nums2.size + 1, 0)
  end

  (1...dp.size).each do |i|
    (1...dp[0].size).each do |j|
      dp[i][j] =
        if nums1[i - 1] == nums2[j - 1]
          dp[i - 1][j - 1] + 1
        else
          [ dp[i][j - 1], dp[i - 1][j] ].max
        end
    end
  end

  dp[-1][-1]
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
