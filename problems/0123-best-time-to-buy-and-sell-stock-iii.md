# 123. Best Time to Buy and Sell Stock III
LeetCode problem: [122. Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)

## LeetCode problem description
You are given an array `prices` where `prices[i]` is the price of a given stock on the `i-th` day.

Find the **maximum** profit you can achieve. You may complete **at most two transactions**.

**Note**: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

```
-----------------------------------------------------------------------------------------------------------------------
[Example 1]

Input: prices = [3,3,5,0,0,3,1,4]
Output: 6

Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
-----------------------------------------------------------------------------------------------------------------------
[Example 2]

Input: prices = [1,2,3,4,5]
Output: 4

Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.
-----------------------------------------------------------------------------------------------------------------------
[Example 3]

Input: prices = [7,6,4,3,1]
Output: 0

Explanation: In this case, no transaction is done, i.e. max profit = 0.
-----------------------------------------------------------------------------------------------------------------------
[Constraints]

1 <= prices.length <= 100000
0 <= prices[i] <= 100000
-----------------------------------------------------------------------------------------------------------------------
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
        dp = [-prices[0], 0, -prices[0], 0]

        for price in prices[1:]:
            dc = dp.copy()

            dp[0] = max(dc[0], -price)
            dp[1] = max(dc[1], dc[0] + price)
            dp[2] = max(dc[2], dc[1] - price)
            dp[3] = max(dc[3], dc[2] + price)

        return dp[-1]
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
var maxProfit = function (prices) {
  const dp = [-prices[0], 0, -prices[0], 0]

  for (const price of prices.slice(1,)) {
    const dc = [...dp]

    dp[0] = Math.max(dc[0], -price)
    dp[1] = Math.max(dc[1], dc[0] + price)
    dp[2] = Math.max(dc[2], dc[1] - price)
    dp[3] = Math.max(dc[3], dc[2] + price)
  }

  return dp[3]
};
```

## Go
```go
func maxProfit(prices []int) int {
    dp := []int{-prices[0], 0, -prices[0], 0}

    for _, price := range prices[1:] {
        dc := slices.Clone(dp)

        dp[0] = max(dc[0], -price)
        dp[1] = max(dc[1], dc[0] + price)
        dp[2] = max(dc[2], dc[1] - price)
        dp[3] = max(dc[3], dc[2] + price)
    }

    return dp[3]
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
