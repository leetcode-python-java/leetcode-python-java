# 518. Coin Change II
LeetCode problem: [518. Coin Change II](https://leetcode.com/problems/coin-change-ii/)

## LeetCode problem description
> You are given an integer array `coins` representing coins of different denominations and an integer amount representing a total `amount` of money.

Return the number of combinations that make up that amount. If that amount of money cannot be made up by any combination of the coins, return `0`.

You may assume that you have an infinite number of each kind of coin.

The answer is **guaranteed** to fit into a signed 32-bit integer.

```
Example 1:

Input: amount = 5, coins = [1,2,5]
Output: 4

Explanation: there are four ways to make up the amount:
5=5
5=2+2+1
5=2+1+1+1
5=1+1+1+1+1
------------------------------------------------------------------------

Example 2:

Input: amount = 3, coins = [2]
Output: 0

Explanation: the amount of 3 cannot be made up just with coins of 2.
------------------------------------------------------------------------

Example 3:

Input: amount = 10, coins = [10]
Output: 1
------------------------------------------------------------------------

Constraints:

1 <= coins.length <= 300
1 <= coins[i] <= 5000
All the values of 'coins' are unique.
0 <= amount <= 5000
```

## Thoughts
It is a `Unbounded Knapsack Problem`.

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Complexity
* Time: `O(n * m)`.
* Space: `O(n)`.

## C#
```c#
public class Solution {
    public int Change(int amount, int[] coins) {
        var dp = new int[amount + 1];
        dp[0] = 1;

        foreach (var coin in coins) {
            for (var j = coin; j < dp.Length; j++) {
                dp[j] += dp[j - coin];
            }
        }

        return dp.Last();
    }
}
```

## Python
```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = [0] * (amount + 1)
        dp[0] = 1
        
        for coin in coins:
            for j in range(coin, len(dp)):
                dp[j] += dp[j - coin]

        return dp[-1]
```

## C++
```cpp
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        auto dp = vector<unsigned int>(amount + 1, 0);
        dp[0] = 1;

        for (auto coin : coins) {
            for (auto j = coin; j < dp.size(); j++) {
                dp[j] += dp[j - coin];
            }
        }

        return dp.back();
    }
};
```

## Java
```java
class Solution {
    public int change(int amount, int[] coins) {
        var dp = new int[amount + 1];
        dp[0] = 1;

        for (var coin : coins) {
            for (var j = coin; j < dp.length; j++) {
                dp[j] += dp[j - coin];
            }
        }

        return dp[dp.length - 1];
    }
}
```

## JavaScript
```javascript
var change = function (amount, coins) {
   const dp = Array(amount + 1).fill(0)
   dp[0] = 1

   for (const coin of coins) {
      for (let j = coin; j < dp.length; j++) {
         dp[j] += dp[j - coin]
      }
   }

   return dp.at(-1);
};
```

## Go
```go
func change(amount int, coins []int) int {
    dp := make([]int, amount + 1)
    dp[0] = 1

    for _, coin := range coins {
        for j := coin; j < len(dp); j++ {
            dp[j] += dp[j - coin]
        }
    }

    return dp[len(dp) - 1]
}
```

## Ruby
```ruby
def change(amount, coins)
  dp = Array.new(amount + 1, 0)
  dp[0] = 1

  coins.each do |coin|
    (coin...dp.size).each do |j|
      dp[j] += dp[j - coin]
    end
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
