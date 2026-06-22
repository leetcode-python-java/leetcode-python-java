# 1833. Maximum Ice Cream Bars - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

Visit original link: [1833. Maximum Ice Cream Bars - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/1833-maximum-ice-cream-bars) for a better experience!

LeetCode link: [1833. Maximum Ice Cream Bars](https://leetcode.com/problems/maximum-ice-cream-bars), difficulty: **Medium**.

## LeetCode description of "1833. Maximum Ice Cream Bars"

It is a sweltering summer day, and a boy wants to buy some ice cream bars.

At the store, there are `n` ice cream bars. You are given an array `costs` of length `n`, where `costs[i]` is the price of the `i^{th}` ice cream bar in coins. The boy initially has `coins` coins to spend, and he wants to buy as many ice cream bars as possible. 

**Note:** The boy can buy the ice cream bars in any order.

Return *the **maximum** number of ice cream bars the boy can buy with* `coins` *coins.*

You must solve the problem by counting sort.

### [Example 1]

**Input**: `costs = [1,3,2,4,1], coins = 7`

**Output**: `4`

**Explanation**: 

<p>The boy can buy ice cream bars at indices 0,1,2,4 for a total price of 1 + 3 + 2 + 1 = 7.</p>


### [Example 2]

**Input**: `costs = [10,6,8,7,7,8], coins = 5`

**Output**: `0`

**Explanation**: 

<p>The boy cannot afford any of the ice cream bars.</p>


### [Example 3]

**Input**: `costs = [1,6,3,1,2,5], coins = 20`

**Output**: `6`

**Explanation**: 

<p>The boy can buy all the ice cream bars for a total price of 1 + 6 + 3 + 1 + 2 + 5 = 18.</p>


### [Constraints]

- `costs.length == n`
- `1 <= n <= 10^5`
- `1 <= costs[i] <= 10^5`
- `1 <= coins <= 10^8`

### [Hints]

<details>
  <summary>Hint 1</summary>
  It is always optimal to buy the least expensive ice cream bar first.

  
</details>

<details>
  <summary>Hint 2</summary>
  Sort the prices so that the cheapest ice cream bar comes first.

  
</details>

## Intuition

The problem explicitly requires solving it using Counting Sort. To maximize the number of ice cream bars we can buy, we should always buy the cheapest ones first (Greedy Approach).

Since the maximum possible cost is bounded (up to 10^5), Counting Sort is extremely efficient here. Instead of sorting the array in O(N log N) time, we can tally the frequencies of each cost in an array. Then, we iterate through the possible costs from 1 to the maximum cost found. 

For each cost, we calculate how many ice creams of that cost we can buy with our remaining coins and subtract the total cost accordingly. This avoids the overhead of a full sort and provides an O(N + M) time complexity solution.

## Step-by-Step Solution

1. Find the maximum cost `m` in the `costs` array.
2. Initialize a `freq` array of size `m + 1` with zeros to store the count of each cost.
3. Iterate through `costs` and populate the `freq` array.
4. Initialize a counter `ans = 0` for the number of ice creams bought.
5. Loop through possible costs from `1` to `m`:
   - If the current `cost` is strictly greater than our remaining `coins`, break early because we can't afford this or any more expensive ice creams.
   - If there are ice creams available at this `cost` (`freq[cost] > 0`), calculate the maximum number we can buy: `count = min(freq[cost], coins / cost)`.
   - Add `count` to `ans`.
   - Deduct `count * cost` from `coins`.
6. Return the total `ans`.

## Complexity

> - **Time Complexity**: `O(N + M)`, where `N` is the number of elements in `costs` and `M` is the maximum value in `costs`. Finding the max value takes `O(N)`, populating frequencies takes `O(N)`, and iterating through the frequency array takes `O(M)`.
- **Space Complexity**: `O(M)`. We require a frequency array of size `M + 1` to tally the counts of each possible cost.

- Time complexity: `O(N + M)`.
- Space complexity: `O(M)`.

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

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.leader.me`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [1833. Maximum Ice Cream Bars - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/1833-maximum-ice-cream-bars) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

