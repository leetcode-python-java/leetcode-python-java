# 309. Best Time to Buy and Sell Stock with Cooldown
LeetCode problem: [309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

## LeetCode problem description
You are given an array `prices` where `prices[i]` is the price of a given stock on the `i-th` day.

Find the **maximum profit** you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times) with the following restrictions:

* After you sell your stock, you cannot buy stock on the next day (i.e., cooldown one day).

**Note**: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

```
-------------------------------------------------------------------------
[Example 1]

Input: prices = [1,2,3,0,2]
Output: 3

Explanation: transactions = [buy, sell, cooldown, buy, sell]
-------------------------------------------------------------------------
[Example 2]

Input: prices = [1]
Output: 0
-------------------------------------------------------------------------
[Constraints]

1 <= prices.length <= 5000
0 <= prices[i] <= 1000
-------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Dynamic programming**.

Detailed solutions will be given later, and now only the best practices in 3 to 7 languages are given.

### Complexity
* Time: `O(n)`.
* Space: `O(n)`.

## Python
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # 2 states:
        #   0: hold stock
        #     1) keep holding (last day is not a cooldown day)
        #     2) today just bought (last day is a cooldown day)
        #   1: no stock
        #     1) keep no stock (today is not a cooldown day)
        #     2) keep no stock (today is a cooldown day)
        #     3) today just sold
        # 
        # To make things clear, we have to go with 3 states.
        # The process from 2 states to 3 states really makes things easier to understand!
        # 3 states:
        #   0: hold stock
        #     1) keep holding (last day is not a cooldown day)
        #     2) today just bought (last day is a cooldown day)
        #   1: no stock (today is not a cooldown day)
        #     1) keep no stock
        #     2) today just sold
        #   2: no stock (today is a cooldown day)
        dp = [-prices[0], 0, 0]

        for price in prices[1:]:
            dc = dp.copy()

            dp[0] = max(dc[0], dc[2] - price)
            dp[1] = max(dc[1], dc[0] + price)
            dp[2] = dc[1]

        return dp[1]
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## Java
```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## C#
```c#
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
var maxProfit = function(prices) {
  const dp = [-prices[0], 0, 0]

  for (const price of prices.slice(1,)) {
    const dc = [...dp]

    dp[0] = Math.max(dc[0], dc[2] - price)
    dp[1] = Math.max(dc[1], dc[0] + price)
    dp[2] = dc[1]
  }

  return dp[1]
};
```

## Go
```go
func maxProfit(prices []int) int {
    dp := []int{-prices[0], 0, 0}

    for i := 1; i < len(prices); i++ {
        dc := slices.Clone(dp)

        dp[0] = max(dc[0], dc[2] - prices[i])
        dp[1] = max(dc[1], dc[0] + prices[i])
        dp[2] = dc[1]
    }

    return dp[1]
}
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
