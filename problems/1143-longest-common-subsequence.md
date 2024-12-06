# 1143. Longest Common Subsequence
LeetCode problem: [1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)

## LeetCode problem description
Given two strings `text1` and `text2`, return the length of their longest **common subsequence**. If there is no common subsequence, return `0`.

A `subsequence` of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

* For example, `"ace"` is a subsequence of `"abcde"`.

A **common subsequence** of two strings is a subsequence that is common to both strings.

```
----------------------------------------------------------------------------
[Example 1]

Input: text1 = "abcde", text2 = "ace" 
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.
----------------------------------------------------------------------------
[Example 2]

Input: text1 = "abc", text2 = "abc"
Output: 3
Explanation: The longest common subsequence is "abc" and its length is 3.
----------------------------------------------------------------------------
[Example 3]

Input: text1 = "abc", text2 = "def"
Output: 0
Explanation: There is no such common subsequence, so the result is 0.
----------------------------------------------------------------------------
[Constraints]

1 <= text1.length, text2.length <= 1000
text1 and text2 consist of only lowercase English characters.
----------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Dynamic programming**.

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Complexity
* Time: `O(n * m)`.
* Space: `O(n * m)`.

## Java
```java
// Example of a 2D 'dp' array:
//     a c e
//   0 0 0 0
// a 0 1 1 1 
// b 0 1 1 1
// c 0 1 2 2
// d 0 1 2 2
// e 0 1 2 3
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        var dp = new int[text1.length() + 1][text2.length() + 1];

        for (var i = 1; i < dp.length; i++) {
            for (var j = 1; j < dp[0].length; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
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
public class Solution {
    public int LongestCommonSubsequence(string text1, string text2) {
        var dp = new int[text1.Length + 1, text2.Length + 1];

        for (var i = 1; i < dp.GetLength(0); i++) {
            for (var j = 1; j < dp.GetLength(1); j++) {
                if (text1[i - 1] == text2[j - 1]) {
                    dp[i, j] = dp[i - 1, j - 1] + 1;
                } else {
                    dp[i, j] = Math.Max(dp[i - 1, j], dp[i, j - 1]);
                }
            }
        }

        return dp[dp.GetUpperBound(0), dp.GetUpperBound(1)];
    }
}
```

## Python
```python
# Example of a 2D 'dp' array:
#     a b f k m a j b 
#   0 0 0 0 0 0 0 0 0
# a 0 1 1 1 1 1 1 1 1 
# j 0 1 1 1 1 1 1 2 2
# f 0 1 1 2 2 2 2 2 2  
# b 0 1 2 2 2 2 2 2 2 
# m 0 1 2 2 2 3 3 3 3 
# k 0 1 2 2 2 3 3 3 3 
# j 0 1 2 2 2 3 3 4 4
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        dp = [[0] * (len(text2) + 1) for _ in range(len(text1) + 1)]

        for i in range(1, len(dp)):
            for j in range(1, len(dp[0])):
                if text1[i - 1] == text2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1] + 1
                else:
                    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
        
        return dp[-1][-1]
```

## C++
```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        vector<vector<int>> dp(text1.size() + 1, vector<int>(text2.size() + 1));

        for (auto i = 1; i < dp.size(); i++) {
            for (auto j = 1; j < dp[0].size(); j++) {
                if (text1[i - 1] == text2[j - 1]) {
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
var longestCommonSubsequence = function (text1, text2) {
  const dp = Array(text1.length + 1).fill().map(
    () => Array(text2.length + 1).fill(0)
  )

  for (let i = 1; i < dp.length; i++) {
    for (let j = 1; j < dp[0].length; j++) {
      if (text1[i - 1] === text2[j - 1]) {
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
func longestCommonSubsequence(text1 string, text2 string) int {
    dp := make([][]int, len(text1) + 1)
    for i := range dp {
        dp[i] = make([]int, len(text2) + 1)
    }

    for i := 1; i < len(dp); i++ {
        for j := 1; j < len(dp[0]); j++ {
            if text1[i - 1] == text2[j - 1] {
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
def longest_common_subsequence(text1, text2)
  dp = Array.new(text1.size + 1) do
    Array.new(text2.size + 1, 0)
  end

  (1...dp.size).each do |i|
    (1...dp[0].size).each do |j|
      dp[i][j] =
        if text1[i - 1] == text2[j - 1]
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
