# 279. Perfect Squares
LeetCode problem: [279. Perfect Squares](https://leetcode.com/problems/perfect-squares/)

## LeetCode problem description
> Given an integer `n`, return the **least** number of perfect square numbers that sum to `n`.

A **perfect square** is an integer that is the square of an integer; in other words, it is the product of some integer with itself. For example, `1`, `4`, `9`, and 16 are perfect squares while `3` and `11` are not.
```
-------------------------------------------------------------
Example 1:

Input: n = 12
Output: 3

Explanation: 12 = 4 + 4 + 4.
-------------------------------------------------------------
Example 2:

Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
-------------------------------------------------------------
Constraints:

1 <= n <= 10000
-------------------------------------------------------------
```

## Thoughts
It is a `Unbounded Knapsack Problem`.

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Complexity
* Time: `O(n * Sqrt(n))`.
* Space: `O(n)`.

## Python
```python
class Solution:
    def numSquares(self, n: int) -> int:
        default_value = n + 2 # As long as the value is greater than 'n', it doesn't matter how much it is.
        dp = [default_value] * (n + 1)
        dp[0] = 0

        for i in range(1, len(dp)):
            j = 1
            while i >= j * j:
                dp[i] = min(dp[i], dp[i - j * j] + 1)
                j += 1

        return dp[-1]
```

## C++
```cpp
class Solution {
public:
    int numSquares(int n) {
        auto default_value = n + 2; // As long as the value is greater than 'n', it doesn't matter how much it is.
        auto dp = vector<int>(n + 1, default_value);
        dp[0] = 0;

        for (auto i = 1; i < dp.size(); i++) {
            for (auto j = 1; j * j <= i; j++) {
                dp[i] = min(dp[i], dp[i - j * j] + 1);
            }
        }

        return dp.back();
    }
};
```

## Java
```java
class Solution {
    public int numSquares(int n) {
        var defaultValue = n + 2; // As long as the value is greater than 'n', it doesn't matter how much it is.
        var dp = new int[n + 1];
        Arrays.fill(dp, defaultValue);
        dp[0] = 0;

        for (var i = 1; i < dp.length; i++) {
            for (var j = 1; j * j <= i; j++) {
                dp[i] = Math.min(dp[i], dp[i - j * j] + 1);
            }
        }

        return dp[dp.length - 1];
    }
}
```

## C#
```c#
public class Solution {
    public int NumSquares(int n) {
        var defaultValue = n + 2; // As long as the value is greater than 'n', it doesn't matter how much it is.
        var dp = Enumerable.Repeat(defaultValue, n + 1).ToArray();
        dp[0] = 0;

        for (var i = 1; i < dp.Length; i++) {
            for (var j = 1; j * j <= i; j++) {
                dp[i] = Math.Min(dp[i], dp[i - j * j] + 1);
            }
        }

        return dp.Last();
    }
}
```

## JavaScript
```javascript
var numSquares = function(n) {
  const DEFAULT_VALUE = n + 2 // As long as the value is greater than 'n', it doesn't matter how much it is.
  const dp = Array(n + 1).fill(DEFAULT_VALUE)
  dp[0] = 0

  for (let i = 1; i < dp.length; i++) {
    for (let j = 1; j * j <= i; j++) {
      dp[i] = Math.min(dp[i], dp[i - j * j] + 1)
    }
  }

  return dp.at(-1)
};
```

## Go
```go
func numSquares(n int) int {
    defaultValue := n + 2 // As long as the value is greater than 'n', it doesn't matter how much it is.
    dp := slices.Repeat([]int{defaultValue}, n + 1)
    dp[0] = 0

    for i := 1; i < len(dp); i++ {
        for j := 1; j * j <= i; j++ {
            dp[i] = min(dp[i], dp[i - j * j] + 1)
        }
    }

    return dp[len(dp) - 1]
}
```

## Ruby
```ruby
def num_squares(n)
  default_value = n + 2 # As long as the value is greater than 'n', it doesn't matter how much it is.
  dp = Array.new(n + 1, default_value)
  dp[0] = 0

  (1...dp.size).each do |i|
    j = 1
    while i >= j * j
      dp[i] = [ dp[i], dp[i - j * j] + 1 ].min
      j += 1
    end
  end

  dp[-1]
end
```
