# 1833. 雪糕的最大数量 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[1833. 雪糕的最大数量 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/1833-maximum-ice-cream-bars)，体验更佳！

力扣链接：[1833. 雪糕的最大数量](https://leetcode.cn/problems/maximum-ice-cream-bars), 难度等级：**中等**。

## LeetCode “1833. 雪糕的最大数量”问题描述

夏日炎炎，小男孩 Tony 想买一些雪糕消消暑。

商店中新到 `n` 支雪糕，用长度为 `n` 的数组 `costs` 表示雪糕的定价，其中 `costs[i]` 表示第 `i` 支雪糕的现金价格。Tony 一共有 `coins` 现金可以用于消费，他想要买尽可能多的雪糕。

**注意：** Tony 可以按任意顺序购买雪糕。

给你价格数组 `costs` 和现金量 `coins` ，请你计算并返回 Tony 用 `coins` 现金能够买到的雪糕的 **最大数量** 。

你必须使用计数排序解决此问题。

### [示例 1]

**输入**: `costs = [1,3,2,4,1], coins = 7`

**输出**: `4`

**解释**: 

<p>Tony 可以买下标为 0、1、2、4 的雪糕，总价为 1 + 3 + 2 + 1 = 7。</p>


### [示例 2]

**输入**: `costs = [10,6,8,7,7,8], coins = 5`

**输出**: `0`

**解释**: `Tony 没有足够的钱买任何一支雪糕。`

### [示例 3]

**输入**: `costs = [1,6,3,1,2,5], coins = 20`

**输出**: `6`

**解释**: 

<p>Tony 可以买下所有的雪糕，总价为 1 + 6 + 3 + 1 + 2 + 5 = 18 。</p>


### [约束]

- `costs.length == n`
- `1 <= n <= 10^5`
- `1 <= costs[i] <= 10^5`
- `1 <= coins <= 10^8`

### [Hints]

<details>
  <summary>提示 1</summary>
  It is always optimal to buy the least expensive ice cream bar first.

  
</details>

<details>
  <summary>提示 2</summary>
  Sort the prices so that the cheapest ice cream bar comes first.

  
</details>

## 思路

题目明确要求使用计数排序（Counting Sort）来解决。为了最大化能购买的雪糕数量，我们应该始终优先购买最便宜的雪糕（贪心策略）。
由于成本的最大值是有界的（最高为 10^5），因此在这里使用计数排序非常高效。我们不需要以 O(N log N) 的时间复杂度对数组进行全量排序，而是可以在一个数组中统计每种成本出现的频率。然后，我们从 1 到找到的最大成本依次遍历。对于每种成本，我们计算用剩余的硬币最多能买多少根该价格的雪糕，并相应地减去总成本。这避免了常规排序的开销，并提供了一个时间复杂度为 O(N + M) 的解决方案。

## 步骤

1. 找出 `costs` 数组中的最大成本 `m`。
2. 初始化一个大小为 `m + 1` 的 `freq` 数组，全置为 0，用于存储每种成本出现的次数。
3. 遍历 `costs` 数组，填充 `freq` 数组进行计数。
4. 初始化一个计数器 `ans = 0`，用于记录已购买的雪糕数量。
5. 遍历从 `1` 到 `m` 的所有可能成本：
   - 如果当前 `cost` 严格大于我们剩余的 `coins`，则提前跳出循环，因为我们买不起这个价格以及更贵价格的雪糕了。
   - 如果当前 `cost` 的雪糕有存货（`freq[cost] > 0`），计算我们最多能买的数量：`count = min(freq[cost], coins / cost)`。
   - 将 `count` 累加到 `ans` 中。
   - 从 `coins` 中扣除花费的总额 `count * cost`。
6. 返回总数量 `ans`。

## 复杂度

> - **时间复杂度**: `O(N + M)`，其中 `N` 是 `costs` 中的元素个数，`M` 是 `costs` 中的最大值。寻找最大值需要 `O(N)`，填充频率数组需要 `O(N)`，遍历频率数组需要 `O(M)`。
- **空间复杂度**: `O(M)`。我们需要一个大小为 `M + 1` 的频率数组来统计每种可能成本的出现次数。

- 时间复杂度: `O(N + M)`.
- 空间复杂度: `O(M)`.

## Python

```python
class Solution:
    def maxIceCream(self, costs: List[int], coins: int) -> int:
        # Step 1: Find the maximum cost to size the frequency array
        max_cost = max(costs)
        
        # Step 2: Create a frequency array and count occurrences
        freq = [0] * (max_cost + 1)
        for cost in costs:
            freq[cost] += 1
            
        ans = 0
        
        # Step 3: Iterate through costs from 1 to max_cost
        for cost in range(1, max_cost + 1):
            # If we don't have enough coins for the current cost, stop
            if coins < cost:
                break
            
            # If there are ice creams of this cost available
            if freq[cost] > 0:
                # Calculate how many we can buy
                count = min(freq[cost], coins // cost)
                ans += count
                coins -= count * cost
                
        return ans
```

## Java

```java
class Solution {
    public int maxIceCream(int[] costs, int coins) {
        // Step 1: Find the maximum cost to define bucket size
        int max = 0;
        for (int cost : costs) {
            if (cost > max) {
                max = cost;
            }
        }
        
        // Step 2: Initialize frequency array and count
        int[] freq = new int[max + 1];
        for (int cost : costs) {
            freq[cost]++;
        }
        
        int ans = 0;
        
        // Step 3: Greedily pick the cheapest ice creams
        for (int cost = 1; cost <= max; cost++) {
            // Stop if remaining coins cannot buy the current cheapest available ice cream
            if (coins < cost) {
                break;
            }
            
            if (freq[cost] > 0) {
                // Determine how many we can buy: bounded by availability and coins
                int count = Math.min(freq[cost], coins / cost);
                ans += count;
                coins -= count * cost;
            }
        }
        
        return ans;
    }
}
```

## JavaScript

```javascript
/**
 * @param {number[]} costs
 * @param {number} coins
 * @return {number}
 */
var maxIceCream = function(costs, coins) {
    // Step 1: Find the maximum cost
    let maxCost = 0;
    for (let cost of costs) {
        if (cost > maxCost) {
            maxCost = cost;
        }
    }
    
    // Step 2: Frequency array for counting sort
    const freq = new Int32Array(maxCost + 1);
    for (let cost of costs) {
        freq[cost]++;
    }
    
    let ans = 0;
    
    // Step 3: Iterate from cheapest to most expensive
    for (let cost = 1; cost <= maxCost; cost++) {
        if (coins < cost) break;
        
        if (freq[cost] > 0) {
            // We buy as many as we can afford up to what's available
            let count = Math.min(freq[cost], Math.floor(coins / cost));
            ans += count;
            coins -= count * cost;
        }
    }
    
    return ans;
};
```

## Cpp

```cpp
class Solution {
public:
    int maxIceCream(vector<int>& costs, int coins) {
        // Step 1: Find max cost
        int maxCost = 0;
        for (int cost : costs) {
            if (cost > maxCost) maxCost = cost;
        }
        
        // Step 2: Create a frequency array
        vector<int> freq(maxCost + 1, 0);
        for (int cost : costs) {
            freq[cost]++;
        }
        
        int ans = 0;
        
        // Step 3: Greedy selection based on counting sort
        for (int cost = 1; cost <= maxCost; cost++) {
            if (coins < cost) break;
            
            if (freq[cost] > 0) {
                int count = min(freq[cost], coins / cost);
                ans += count;
                coins -= count * cost;
            }
        }
        
        return ans;
    }
};
```

## Csharp

```csharp
public class Solution {
    public int MaxIceCream(int[] costs, int coins) {
        int maxCost = 0;
        foreach (int cost in costs) {
            if (cost > maxCost) {
                maxCost = cost;
            }
        }
        
        int[] freq = new int[maxCost + 1];
        foreach (int cost in costs) {
            freq[cost]++;
        }
        
        int ans = 0;
        
        for (int cost = 1; cost <= maxCost; cost++) {
            if (coins < cost) break;
            
            if (freq[cost] > 0) {
                int count = Math.Min(freq[cost], coins / cost);
                ans += count;
                coins -= count * cost;
            }
        }
        
        return ans;
    }
}
```

## Go

```go
func maxIceCream(costs []int, coins int) int {
    // Find the maximum cost for our counting sort buckets
    maxCost := 0
    for _, cost := range costs {
        if cost > maxCost {
            maxCost = cost
        }
    }
    
    // Create frequency array
    freq := make([]int, maxCost + 1)
    for _, cost := range costs {
        freq[cost]++
    }
    
    ans := 0
    
    // Greedily pick the cheapest options
    for cost := 1; cost <= maxCost; cost++ {
        if coins < cost {
            break
        }
        
        if freq[cost] > 0 {
            count := freq[cost]
            maxCanBuy := coins / cost
            if maxCanBuy < count {
                count = maxCanBuy
            }
            
            ans += count
            coins -= count * cost
        }
    }
    
    return ans
}
```

## Ruby

```ruby
# @param {Integer[]} costs
# @param {Integer} coins
# @return {Integer}
def max_ice_cream(costs, coins)
    max_cost = costs.max
    
    # Initialize frequency array
    freq = Array.new(max_cost + 1, 0)
    costs.each do |cost|
        freq[cost] += 1
    end
    
    ans = 0
    
    # Process from the lowest price upwards
    (1..max_cost).each do |cost|
        break if coins < cost
        
        if freq[cost] > 0
            count = [freq[cost], coins / cost].min
            ans += count
            coins -= count * cost
        end
    end
    
    ans
end
```

## Rust

```rust
impl Solution {
    pub fn max_ice_cream(costs: Vec<i32>, mut coins: i32) -> i32 {
        let max_cost = *costs.iter().max().unwrap_or(&0) as usize;
        
        // Initialize frequency array
        let mut freq = vec![0; max_cost + 1];
        for &cost in costs.iter() {
            freq[cost as usize] += 1;
        }
        
        let mut ans = 0;
        
        for cost in 1..=max_cost {
            let cost_i32 = cost as i32;
            if coins < cost_i32 {
                break;
            }
            
            if freq[cost] > 0 {
                let count = freq[cost].min(coins / cost_i32);
                ans += count;
                coins -= count * cost_i32;
            }
        }
        
        ans
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun maxIceCream(costs: IntArray, coins: Int): Int {
        var maxCost = 0
        for (cost in costs) {
            if (cost > maxCost) {
                maxCost = cost
            }
        }
        
        val freq = IntArray(maxCost + 1)
        for (cost in costs) {
            freq[cost]++
        }
        
        var remainingCoins = coins
        var ans = 0
        
        for (cost in 1..maxCost) {
            if (remainingCoins < cost) break
            
            if (freq[cost] > 0) {
                val count = Math.min(freq[cost], remainingCoins / cost)
                ans += count
                remainingCoins -= count * cost
            }
        }
        
        return ans
    }
}
```

## Swift

```swift
class Solution {
    func maxIceCream(_ costs: [Int], _ coins: Int) -> Int {
        guard let maxCost = costs.max() else { return 0 }
        
        var freq = Array(repeating: 0, count: maxCost + 1)
        for cost in costs {
            freq[cost] += 1
        }
        
        var currentCoins = coins
        var ans = 0
        
        for cost in 1...maxCost {
            if currentCoins < cost {
                break
            }
            
            if freq[cost] > 0 {
                let count = min(freq[cost], currentCoins / cost)
                ans += count
                currentCoins -= count * cost
            }
        }
        
        return ans
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**leader.me**](https://www.leader.me) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.leader.me`，极具职业含金量的专属域名。

>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[1833. 雪糕的最大数量 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/1833-maximum-ice-cream-bars)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

