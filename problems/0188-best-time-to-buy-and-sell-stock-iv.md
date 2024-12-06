# 188. Best Time to Buy and Sell Stock IV
LeetCode problem: [188. Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)

## LeetCode problem description
You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `i-th` day, and an integer `k`.

Find the maximum profit you can achieve. You may complete at most `k` transactions: i.e. you may buy at most `k` times and sell at most `k` times.

**Note**: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).
```
-------------------------------------------------------------------------------------------------------
[Example 1]

Input: k = 2, prices = [2,4,1]
Output: 2

Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.
-------------------------------------------------------------------------------------------------------
[Example 2]

Input: k = 2, prices = [3,2,6,5,0,3]
Output: 7

Explanation: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4.
             Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
-------------------------------------------------------------------------------------------------------
[Constraints]

1 <= k <= 100
1 <= prices.length <= 1000
0 <= prices[i] <= 1000
-------------------------------------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Dynamic programming**.

Detailed solutions will be given later, and now only the best practices in 3 to 7 languages are given.

### Complexity
* Time: `O(n * k)`.
* Space: `O(n * k)`.

## Python
```python
class Solution:
    def maxProfit(self, k: int, prices: List[int]) -> int:
        dp = []
        for _ in range(k):
            dp.extend([-prices[0], 0])

        for price in prices[1:]:
            dc = dp.copy()

            dp[0] = max(dc[0], -price)

            for i in range(1, k * 2):
                addition = price if i % 2 == 1 else -price
                dp[i] = max(dc[i], dc[i - 1] + addition)

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
var maxProfit = function (k, prices) {
  const dp = Array(k).fill([-prices[0], 0]).flat()

  for (const price of prices.slice(1,)) {
    const dc = [...dp]

    dp[0] = Math.max(dc[0], -price)

    for (let i = 1; i < k * 2; i++) {
      dp[i] = Math.max(dc[i], dc[i - 1] + (i % 2 === 1 ? price : -price))
    }
  }

  return dp.at(-1)
};
```

## Go
```go
func maxProfit(k int, prices []int) int {
    dp := slices.Repeat([]int{-prices[0], 0}, k)

    for _, price := range prices[1:] {
        dc := slices.Clone(dp)

        dp[0] = max(dc[0], -price)

        for i := 1; i < k * 2; i++ {
            addition := price
            if i % 2 == 0 {
                addition *= -1
            }
            dp[i] = max(dc[i], dc[i - 1] + addition)
        }
    }

    return dp[2 * k - 1]
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
