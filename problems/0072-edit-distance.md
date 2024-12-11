# 72. Edit Distance
LeetCode problem: [72. Edit Distance](https://leetcode.com/problems/edit-distance/)

## LeetCode problem description
> Given two strings `word1` and `word2`, return the **minimum** number of operations required to convert `word1` to `word2`.

You have the following three operations permitted on a word:
- Insert a character
- Delete a character
- Replace a character

```
Example 1:

Input: word1 = "horse", word2 = "ros"
Output: 3

Explanation:
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
-------------------------------------------------------

Example 2:

Input: word1 = "intention", word2 = "execution"
Output: 5

Explanation:
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
-------------------------------------------------------

Constraints:

1. 0 <= word1.length, word2.length <= 500
2. `word1` and `word2` consist of lowercase English letters.
```

## Thoughts
* It is a question of comparing two strings. After doing similar questions many times, we will develop an intuition to use dynamic programming with two-dimensional arrays.

### Common steps in dynamic programming
These five steps are a pattern for solving `dynamic programming` problems.

1. Determine the **meaning** of the `dp[i][j]`
    * Since there are two strings, we can use two-dimensional arrays as the default option.
    * At first, try to use the problem's `return` value as the value of `dp[i][j]` to determine the meaning of `dp[i][j]`. If it doesn't work, try another way.
    * `dp[i][j]` represents the **minimum** number of operations required to convert `word1`'s first `i` letters to `word2`'s first `j` letters.
    * `dp[i][j]` is an integer.
2. Determine the `dp` array's initial value
    * Use an example:
   ```
   After initialization, the 'dp' array would be:  
   #     r o s
   #   0 1 2 3 # dp[0]
   # h 1 0 0 0
   # o 2 0 0 0
   # r 3 0 0 0
   # s 4 0 0 0
   # e 5 0 0 0
   ```
    * `dp[i][0] = i`, because `dp[i][0]` represents the empty string, and the number of operations is just the number of chars to be deleted.
    * `dp[0][j] = j`, the reason is the same as the previous line, just viewed from the opposite angle: convert `word2` to `word1`.
    
3. Determine the `dp` array's recurrence formula
    * Try to complete the `dp` grid. In the process, you will get inspiration to derive the formula.
   ```
   1. Convert `h` to `ros`. 
   #     r o s
   #   0 1 2 3
   # h 1 1 2 3 # dp[1]
   ```
   ```
   2. Convert `ho` to `ros`. 
   #     r o s
   #   0 1 2 3
   # h 1 1 2 3
   # o 2 2 1 2
   ```
   ```
   3. Convert `hor` to `ros`. 
   #     r o s
   #   0 1 2 3
   # h 1 1 2 3
   # o 2 2 1 2
   # r 3 2 2 2
   ```
   ```
   4. Convert `hors` to `ros`. 
   #     r o s
   #   0 1 2 3
   # h 1 1 2 3
   # o 2 2 1 2
   # r 3 2 2 2
   # s 4 3 3 2
   ```
   ```
   5. Convert `horse` to `ros`. 
   #     r o s
   #   0 1 2 3
   # h 1 1 2 3
   # o 2 2 1 2
   # r 3 2 2 2
   # s 4 3 3 2
   # e 5 4 4 3 # dp[5]
   ```
    * When analyzing the sample `dp` grid, remember there are three important points which you should pay special attention to: `dp[i - 1][j - 1]`, `dp[i - 1][j]` and `dp[i][j - 1]`. The current `dp[i][j]` often depends on them.
    * If the question is also true in reverse (swap `word1` and `word2`), and we need to use `dp[i - 1][j]` or `dp[i][j - 1]`, then we probably need to use both of them.
    * We can derive the `Recurrence Formula`:
   ```python
   if word1[i - 1] == word2[j - 1]
       dp[i][j] = dp[i - 1][j - 1]
   else
       dp[i][j] = min(
         dp[i - 1][j - 1],
         dp[i - 1][j],
         dp[i][j - 1],
       ) + 1
   ```
4. Determine the `dp` array's traversal order
    * `dp[i][j]` depends on `dp[i - 1][j - 1]`, `dp[i - 1][j]` and `dp[i][j - 1]`, so we should traverse the `dp` array from top to bottom, then from left to right.
5. Check the `dp` array's value
    * Print the `dp` to see if it is as expected.

### Complexity
* Time: `O(n * m)`.
* Space: `O(n * m)`.

## Java
```java
class Solution {
    public int minDistance(String word1, String word2) {
        var dp = new int[word1.length() + 1][word2.length() + 1];
        for (var i = 0; i < dp.length; i++) {
            dp[i][0] = i;
        }
        for (var j = 0; j < dp[0].length; j++) {
            dp[0][j] = j;
        }

        for (var i = 1; i < dp.length; i++) {
            for (var j = 1; j < dp[0].length; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = Math.min(dp[i - 1][j - 1], Math.min(dp[i - 1][j], dp[i][j - 1])) + 1;
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
    public int MinDistance(string word1, string word2)
    {
        var dp = new int[word1.Length + 1, word2.Length + 1];
        
        for (var i = 0; i < dp.GetLength(0); i++)
            dp[i, 0] = i;
        
        for (var j = 0; j < dp.GetLength(1); j++)
            dp[0, j] = j;

        for (var i = 1; i < dp.GetLength(0); i++)
        {
            for (var j = 1; j < dp.GetLength(1); j++)
            {
                if (word1[i - 1] == word2[j - 1])
                {
                    dp[i, j] = dp[i - 1, j - 1];
                }
                else
                {
                    dp[i, j] = Math.Min(dp[i - 1, j - 1], Math.Min(dp[i - 1, j], dp[i, j - 1])) + 1;
                }
            }
        }

        return dp[dp.GetUpperBound(0), dp.GetUpperBound(1)];
    }
}
```

## Python
```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        dp = [[0] * (len(word2) + 1) for _ in range(len(word1) + 1)]
        for i in range(len(dp)):
            dp[i][0] = i
        for j in range(len(dp[0])):
            dp[0][j] = j
        
        for i in range(1, len(dp)):
            for j in range(1, len(dp[0])):
                if word1[i - 1] == word2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1]
                else:
                    dp[i][j] = min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1
        
        return dp[-1][-1]
```

## C++
```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        vector<vector<int>> dp(word1.size() + 1, vector<int>(word2.size() + 1));
        for (auto i = 0; i < dp.size(); i++) {
            dp[i][0] = i;
        }
        for (auto j = 0; j < dp[0].size(); j++) {
            dp[0][j] = j;
        }

        for (auto i = 1; i < dp.size(); i++) {
            for (auto j = 1; j < dp[0].size(); j++) {
                if (word1[i - 1] == word2[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = min({dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]}) + 1;
                }
            }
        }

        return dp[dp.size() - 1][dp[0].size() - 1];
    }
};
```

## JavaScript
```javascript
var minDistance = function (word1, word2) {
  const dp = Array(word1.length + 1).fill().map(
    () => Array(word2.length + 1).fill(0)
  )
  dp.forEach((_, i) => { dp[i][0] = i })
  dp[0].forEach((_, j) => { dp[0][j] = j })

  for (let i = 1; i < dp.length; i++) {
    for (let j = 1; j < dp[0].length; j++) {
      if (word1[i - 1] == word2[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1]
      } else {
        dp[i][j] = Math.min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1
      }
    }
  }

  return dp.at(-1).at(-1)
};
```

## Go
```go
func minDistance(word1 string, word2 string) int {
    dp := make([][]int, len(word1) + 1)
    for i := range dp {
        dp[i] = make([]int, len(word2) + 1)
        dp[i][0] = i
    }
    for j := range dp[0] {
        dp[0][j] = j
    }

    for i := 1; i < len(dp); i++ {
        for j := 1; j < len(dp[0]); j++ {
            if word1[i - 1] == word2[j - 1] {
                dp[i][j] = dp[i - 1][j - 1]
            } else {
                dp[i][j] = min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1
            }
        }
    }

    return dp[len(dp) - 1][len(dp[0]) - 1]
}
```

## Ruby
```ruby
def min_distance(word1, word2)
  dp = Array.new(word1.size + 1) do
    Array.new(word2.size + 1, 0)
  end
  dp.each_with_index do |_, i|
    dp[i][0] = i
  end
  dp[0].each_with_index do |_, j|
    dp[0][j] = j
  end

  (1...dp.size).each do |i|
    (1...dp[0].size).each do |j|
      dp[i][j] =
        if word1[i - 1] == word2[j - 1]
          dp[i - 1][j - 1]
        else
          [ dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1] ].min + 1
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
