# 322. Coin Change
LeetCode link: [322. Coin Change](https://leetcode.com/problems/coin-change/)

## LeetCode problem description
> You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return the **fewest number** of coins that you need to make up that `amount`. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an **infinite** number of each kind of coin.

```
Example 1:

Input: coins = [1,2,5], amount = 11
Output: 3

Explanation: 11 = 5 + 5 + 1
------------------------------------------------------------------------

Example 2:

Input: coins = [2], amount = 3
Output: -1
------------------------------------------------------------------------

Constraints:

1 <= coins.length <= 12
1 <= coins[i] <= 2**31 - 1
0 <= amount <= 10000
```

## Thoughts
It is a `Unbounded Knapsack Problem`.

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Complexity
* Time: `O(n * m)`.
* Space: `O(n)`.

## C#
```c#
public class Solution
{
    public int CoinChange(int[] coins, int amount)
    {
        int defaultValue = amount + 2; // As long as the value is greater than 'amount', it doesn't matter how much it is.
        int[] dp = Enumerable.Repeat(defaultValue, amount + 1).ToArray();
        dp[0] = 0;

        for (var i = 1; i < dp.Length; i++)
        {
            foreach (int coin in coins)
            {
                if (i >= coin)
                {
                    dp[i] = Math.Min(dp[i], dp[i - coin] + 1);
                }
            }
        }

        if (dp.Last() == defaultValue)
            return -1;

        return dp.Last();
    }
}
```

## Python
```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        default_value = amount + 2 # As long as the value is greater than 'amount', it doesn't matter how much it is.
        dp = [default_value] * (amount + 1)
        dp[0] = 0

        for i in range(1, len(dp)):
            for coin in coins:
                if i >= coin:
                    dp[i] = min(dp[i], dp[i - coin] + 1)

        if dp[-1] == default_value:
            return -1

        return dp[-1]
```

## C++
```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        auto default_value = amount + 2; // As long as the value is greater than 'amount', it doesn't matter how much it is.
        auto dp = vector<int>(amount + 1, default_value);
        dp[0] = 0;

        for (auto i = 1; i < dp.size(); i++) {
            for (auto coin : coins) {
                if (i >= coin) {
                    dp[i] = min(dp[i], dp[i - coin] + 1);
                }
            }
        }

        if (dp.back() == default_value) {
            return -1;
        }
        return dp.back();
    }
};
```

## Java
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        var defaultValue = amount + 2; // As long as the value is greater than 'amount', it doesn't matter how much it is.

        var dp = new int[amount + 1];
        Arrays.fill(dp, defaultValue);
        dp[0] = 0;

        for (var i = 1; i < dp.length; i++) {
            for (var coin : coins) {
                if (i >= coin) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }

        var result = dp[dp.length - 1];
        if (result == defaultValue) {
            return -1;
        }
        return result;
    }
}
```

## JavaScript
```javascript
var coinChange = function (coins, amount) {
  const DEFAULT_VALUE = amount + 2 // As long as the value is greater than 'amount', it doesn't matter how much it is.
  const dp = Array(amount + 1).fill(DEFAULT_VALUE)
  dp[0] = 0

  for (let i = 1; i < dp.length; i++) {
    for (const coin of coins) {
      if (i >= coin) {
        dp[i] = Math.min(dp[i], dp[i - coin] + 1)
      }
    }
  }

  if (dp.at(-1) == DEFAULT_VALUE) {
    return -1
  }
  return dp.at(-1)
};
```

## Go
```go
func coinChange(coins []int, amount int) int {
    defaultValue := amount + 2 // As long as the value is greater than 'amount', it doesn't matter how much it is.
    dp := slices.Repeat([]int{defaultValue}, amount + 1)
    dp[0] = 0

    for i := 1; i < len(dp); i++ {
        for _, coin := range coins {
            if i >= coin {
                dp[i] = min(dp[i], dp[i - coin] + 1)
            }
        }
    }

    result := dp[len(dp) - 1]
    if result == defaultValue {
        return -1
    }
    return result
}
```

## Ruby
```ruby
def coin_change(coins, amount)
  default_value = amount + 2 # As long as the value is greater than 'amount', it doesn't matter how much it is.
  dp = Array.new(amount + 1, default_value)
  dp[0] = 0

  (1...dp.size).each do |i|
    coins.each do |coin|
      dp[i] = [ dp[i], dp[i - coin] + 1 ].min if i >= coin
    end
  end

  return -1 if dp[-1] == default_value

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
