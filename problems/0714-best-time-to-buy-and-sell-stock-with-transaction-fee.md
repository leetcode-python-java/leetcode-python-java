# 714. Best Time to Buy and Sell Stock with Transaction Fee
LeetCode problem: [714. Best Time to Buy and Sell Stock with Transaction Fee](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

## LeetCode problem description
You are given an array `prices` where `prices[i]` is the price of a given stock on the `i-th` day, and an integer `fee` representing a transaction fee.

Find the **maximum profit** you can achieve. You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction.

**Note:**

* You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).
* The transaction fee is only charged once for each stock purchase and sale.

```
------------------------------------------------------------------
[Example 1]

Input: prices = [1,3,2,8,4,9], fee = 2
Output: 8

Explanation: The maximum profit can be achieved by:
- Buying at prices[0] = 1
- Selling at prices[3] = 8
- Buying at prices[4] = 4
- Selling at prices[5] = 9
The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
------------------------------------------------------------------
[Example 2]

Input: prices = [1,3,7,5,10,3], fee = 3
Output: 6
------------------------------------------------------------------
[Constraints]

1 <= prices.length <= 5 * 10000
1 <= prices[i] < 5 * 10000
0 <= fee < 5 * 10000
------------------------------------------------------------------
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
    def maxProfit(self, prices: List[int], fee: int) -> int:
        # states:
        #   0: hold stock
        #     1) keep holding
        #     2) today just bought
        #   1: no stock
        #     1) keep no stock
        #     2) today just sold
        dp = [-prices[0], 0]

        for price in prices[1:]:
            dc = dp.copy()

            dp[0] = max(dc[0], dc[1] - price)
            dp[1] = max(dc[1], dc[0] + price - fee)

        return dp[1]
```

## C++
```cpp

```

## Java
```java

```

## C#
```c#

```

## JavaScript
```javascript
var maxProfit = function (prices, fee) {
  const dp = [-prices[0], 0]

  for (let i = 1; i < prices.length; i++) {
    const dc = [...dp]

    dp[0] = Math.max(dc[0], dc[1] - prices[i])
    dp[1] = Math.max(dc[1], dc[0] + prices[i] - fee)
  }

  return dp[1]
};
```

## Go
```go
func maxProfit(prices []int, fee int) int {
    dp := []int{-prices[0], 0}

    for i := 1; i < len(prices); i++ {
        dc := slices.Clone(dp)

        dp[0] = max(dc[0], dc[1] - prices[i])
        dp[1] = max(dc[1], dc[0] + prices[i] - fee)
    }

    return dp[1]
}
```

## Ruby
```ruby
```

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
