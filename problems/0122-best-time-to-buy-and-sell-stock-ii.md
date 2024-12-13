# 122. Best Time to Buy and Sell Stock II
LeetCode problem link: [122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

## LeetCode problem description
You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `i-th` day.

On each day, you may decide to buy and/or sell the stock. You can only hold **at most one** share of the stock at any time. However, you can buy it then immediately sell it **on the same day**.

Find and return the **maximum** profit you can achieve.

```
-----------------------------------------------------------------------------------------------------------------------
[Example 1]

Input: prices = [7,1,5,3,6,4]
Output: 7

Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Total profit is 4 + 3 = 7.
-----------------------------------------------------------------------------------------------------------------------
[Example 2]

Input: prices = [1,2,3,4,5]
Output: 4

Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Total profit is 4.
-----------------------------------------------------------------------------------------------------------------------
[Example 3]

Input: prices = [7,6,4,3,1]
Output: 0

Explanation: There is no way to make a positive profit, so we never buy the stock to achieve the maximum profit of 0.
-----------------------------------------------------------------------------------------------------------------------
[Constraints]

1 <= prices.length <= 3 * 10000
0 <= prices[i] <= 10000
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
            dp[1] = max(dc[1], dc[0] + price)

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
var maxProfit = function (prices) {
  const dp = [-prices[0], 0]

  for (let i = 1; i < prices.length; i++) {
    const dc = [...dp]

    dp[0] = Math.max(dc[0], dc[1] - prices[i])
    dp[1] = Math.max(dc[1], dc[0] + prices[i])
  }

  return dp[1]
};
```

## Go
```go
func maxProfit(prices []int) int {
    dp := []int{-prices[0], 0}

    for i := 1; i < len(prices); i++ {
        dc := slices.Clone(dp)

        dp[0] = max(dc[0], dc[1] - prices[i])
        dp[1] = max(dc[1], dc[0] + prices[i])
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
