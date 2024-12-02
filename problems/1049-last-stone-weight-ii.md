# 494. Target Sum
LeetCode problem: [494. Target Sum](https://leetcode.com/problems/last-stone-weight-ii/)

## LeetCode problem description
You are given an array of integers `stones` where `stones[i]` is the weight of the `i-th` stone.

We are playing a game with the stones. On each turn, we choose any two stones and smash them together.
Suppose the stones have weights `x` and `y` with `x <= y`. The result of this smash is:

* If `x == y`, both stones are destroyed, and
* If `x != y`, the stone of weight `x` is destroyed, and the stone of weight `y` has new weight `y - x`.

At the end of the game, there is **at most one** stone left.

Return the smallest possible weight of the left stone. If there are no stones left, return `0`.

```
Example 1:

Input: stones = [2,7,4,1,8,1]
Output: 1

Explanation:
We can combine 2 and 4 to get 2, so the array converts to [2,7,1,8,1] then,
we can combine 7 and 8 to get 1, so the array converts to [2,1,1,1] then,
we can combine 2 and 1 to get 1, so the array converts to [1,1,1] then,
we can combine 1 and 1 to get 0, so the array converts to [1], then that's the optimal value.
-----------------------------------------------------------------------------------------------------

Example 2:

Input: stones = [31,26,33,21,40]
Output: 5
-----------------------------------------------------------------------------------------------------

Constraints:

1 <= stones.length <= 30
1 <= stones[i] <= 100
```

* Before you start working on this question, it is recommended that you first work on another relatively simple question [416. Partition Equal Subset Sum](./0416-partition-equal-subset-sum.md) that is very similar to this one.
Once you have completed `416`, it will be effortless to complete this question.

## Thoughts
* This problem can be solved by brute force, that is, find all subsets of the array, see if the sum of each subset array is close to half of the sum of the complete array, and find the one that is closest. But when we see `stones.length <= 30`, we know that such a solution will definitely time out.
* So we need to change our thinking. Before you The question is equivalent to finding the minimum difference between the sums of the two arrays after splitting. If we find a subset array whose sum is closest to half of the sum of the complete array, then it is the subset array we want.
* Then this problem will become a `01 Knapsack Problem` which belongs to `Dynamic Programming`. `Dynamic programming` means that the answer to the current problem can be derived from the previous similar problem. Therefore, the `dp` array is used to record all the answers.

* The core logic of the `01 Knapsack Problem` uses a two-dimensional `dp` array or a one-dimensional `dp` **rolling array**, first **traverses the items**, then **traverses the knapsack size** (`in reverse order` or use `dp.clone`), then **reference the previous value corresponding to the size of current 'item'**.
* There are many things to remember when using a two-dimensional `dp` array, and it is difficult to write it right at once during an interview, so I won't describe it here.

### Common steps in '01 Knapsack Problem'
These five steps are a pattern for solving `Dynamic Programming` problems.

1. Determine the **meaning** of the `dp[j]`
    * We can use a one-dimensional `dp` **rolling array**. Rolling an array means that the values of the array are overwritten each time through the iteration. 
    * At first, try to use the problem's `return` value as the value of `dp[j]` to determine the meaning of `dp[j]`. If it doesn't work, try another way.
    * So, `dp[j]` represents whether it is possible to `sum` the first `i` `stones` to get `j`.
    * `dp[j]` is a boolean.
2. Determine the `dp` array's initial value
    * Use an example:
   ```
   stones = [2,7,4,1,8,1], so 'half of the sum' is 11.
   The `size` of the knapsack is `half of the sum`, and the `items` are `stones`.
   So after initialization, the 'dp' array would be:
   #    0 1 2 3 4 5 6 7 8 9 10 11
   #    T F F F F F F F F F F  F  # dp
   # 2  
   # 7  
   # 4 
   # 1  
   # 8  
   # 1  
   ```
    * You can see the `dp` array size is **one** greater than the knapsack size. In this way, the knapsack size and index value are equal, which helps to understand.
    * `dp[0]` is set to `true`, indicating that an empty knapsack can be achieved by not using any `stones`. In addition, it is used as the starting value, and the subsequent `dp[j]` will depend on it. If it is `false`, all values of `dp[j]` will be `false`.
    * `dp[j] = false (j != 0)`, indicating that it is impossible to get `j` with no `stones`.
    
3. Determine the `dp` array's recurrence formula
    * Try to complete the grid. In the process, you will get inspiration to derive the formula.
   ```
   1. Use the first stone '2'.
   #    0 1 2 3 4 5 6 7 8 9 10 11
   #    T F F F F F F F F F F  F
   # 2  T F T F F F F F F F F  F # dp
   ```
   ```
   2. Use the second stone '7'.
   #    0 1 2 3 4 5 6 7 8 9 10 11
   #    T F F F F F F F F F F  F
   # 2  T F T F F F F F F F F  F
   # 7  T F T F F F F T F T F  F
   ```
   ```
   3. Use the third stone '4'.
   #    0 1 2 3 4 5 6 7 8 9 10 11
   #    T F F F F F F F F F F  F
   # 2  T F T F F F F F F F F  F
   # 7  T F T F F F F T F T F  F
   # 4  T F T F T F T T F T F  T # dp
   # ...
   # You don't need to complete the grid since you have enough information to derive the formula.
   ```
    * After analyzing the sample `dp` grid, we can derive the `Recurrence Formula`:
   ```cpp
   dp[j] = dp[j] || dp[j - stones[i]]
   ```
4. Determine the `dp` array's traversal order
    * `dp[j]` depends on `dp[j]` and `dp[j - stones[i]]`, so we should traverse the `dp` array **in reverse order**.
    * Please think if we can traverse the `dp` array **not in reverse order**? In the `Python` solution's code comments, I will answer this question.
5. Check the `dp` array's value
    * Print the `dp` to see if it is as expected.

### Complexity
* Time: `O(n * sum/2)`.
* Space: `O(sum/2)`.

## Python
### Solution 1: Iterate through knapsack size in reverse order
```python
class Solution:
    def lastStoneWeightII(self, stones: List[int]) -> int:
        sum_ = sum(stones)

        dp = [False] * (sum_ // 2 + 1)
        dp[0] = True

        for stone in stones:
            # If not traversing in reverse order, the newly assigned value `dp[j]` will act as `dp[j - stone]` later,
            # then the subsequent `dp[j]` will be affected. But each `stone` can only be used once!
            for j in range(len(dp) - 1, 0, -1):
                if j < stone:
                    break
                dp[j] = dp[j] or dp[j - stone]

        for i in range(len(dp) - 1, -1, -1):
            if dp[i]:
                return sum_ - i * 2
```

As in the comment above, `for j in range(len(dp) - 1, 0, -1):`'s traversal order is **in reverse order** which really matters.

During the interview, you need to remember it. Is there any way to not worry about the traversal order?

Please think about it.

Below, I will give you a solution without worrying about the traversal order problem.

### Solution 2: Iterate through knapsack size in any order (recommended)
```python
class Solution:
    def lastStoneWeightII(self, stones: List[int]) -> int:
        sum_ = sum(stones)

        dp = [False] * (sum_ // 2 + 1)
        dp[0] = True

        for stone in stones:
            dc = dp.copy()

            for j in range(stone, len(dp)):
                dp[j] = dc[j] or dc[j - stone]

        for i in range(len(dp) - 1, -1, -1):
            if dp[i]:
                return sum_ - i * 2
```

* Personally, I like this approach because it makes the code logic clearer, does not need to consider the traversal order,
and is more applicable (you will encounter many situations in the future where backward iteration does not work).

## C++
### Solution 1: Iterate through knapsack size in reverse order
```cpp
class Solution {
public:
    int lastStoneWeightII(vector<int>& stones) {
        auto sum = reduce(stones.begin(), stones.end());

        auto dp = vector<bool>(sum / 2 + 1);
        dp[0] = true;

        for (const auto& stone : stones) {
            for (auto j = dp.size() - 1; j >= stone; j--) {
                dp[j] = dp[j] || dp[j - stone];
            }
        }

        for (auto i = dp.size() - 1; i >= 0; i--) {
            if (dp[i]) {
                return sum - i * 2;
            }
        }

        throw logic_error("lastStoneWeightII() has a logical error!");
    }
};
```

### Solution 2: Iterate through knapsack size in any order (recommended)
```c++
class Solution {
public:
    int lastStoneWeightII(vector<int>& stones) {
        auto sum = reduce(stones.begin(), stones.end());

        auto dp = vector<bool>(sum / 2 + 1);
        dp[0] = true;

        for (const auto& stone : stones) {
            auto dc = dp;

            for (auto j = stone; j < dp.size(); j++) {
                dp[j] = dc[j] || dc[j - stone];
            }
        }

        for (auto i = dp.size() - 1; i >= 0; i--) {
            if (dp[i]) {
                return sum - i * 2;
            }
        }

        throw logic_error("lastStoneWeightII() has a logical error!");
    }
};
```

## Java
### Solution 1: Iterate through knapsack size in reverse order
```java
class Solution {
    public int lastStoneWeightII(int[] stones) {
        var sum = IntStream.of(stones).sum();

        var dp = new boolean[sum / 2 + 1];
        dp[0] = true;

        for (var stone : stones) {
            for (var j = dp.length - 1; j >= stone; j--) {
                dp[j] = dp[j] || dp[j - stone];
            }
        }

        for (var j = dp.length - 1; j >= 0; j--) {
            if (dp[j]) {
                return sum - j * 2;
            }
        }

        throw new ArithmeticException("lastStoneWeightII() has a logical error!");
    }
}
```

### Solution 2: Iterate through knapsack size in any order (recommended)
```java
class Solution {
    public int lastStoneWeightII(int[] stones) {
        var sum = IntStream.of(stones).sum();

        var dp = new boolean[sum / 2 + 1];
        dp[0] = true;

        for (var stone : stones) {
            var dc = dp.clone();

            for (var j = stone; j < dp.length; j++) {
                dp[j] = dc[j] || dc[j - stone];
            }
        }

        for (var j = dp.length - 1; j >= 0; j--) {
            if (dp[j]) {
                return sum - j * 2;
            }
        }

        throw new ArithmeticException("lastStoneWeightII() has a logical error!");
    }
}
```

## C#
### Solution 1: Iterate through knapsack size in reverse order
```c#
public class Solution {
    public int LastStoneWeightII(int[] stones) {
        var sum = stones.Sum();

        var dp = new bool[sum / 2 + 1];
        dp[0] = true;

        foreach (var stone in stones) {
            for (var j = dp.Length - 1; j >= stone; j--) {
                dp[j] = dp[j] || dp[j - stone];
            }
        }

        for (var j = dp.Length - 1; j >= 0; j--) {
            if (dp[j]) {
                return sum - j * 2;
            }
        }

        throw new ArithmeticException("lastStoneWeightII() has a logical error!");
    }
}
```

### Solution 2: Iterate through knapsack size in any order (recommended)
```c#
public class Solution {
    public int LastStoneWeightII(int[] stones) {
        var sum = stones.Sum();

        var dp = new bool[sum / 2 + 1];
        dp[0] = true;

        foreach (var stone in stones) {
            var dc = (bool[]) dp.Clone();

            for (var j = stone; j < dp.Length; j++) {
                dp[j] = dc[j] || dc[j - stone];
            }
        }

        for (var j = dp.Length - 1; j >= 0; j--) {
            if (dp[j]) {
                return sum - j * 2;
            }
        }

        throw new ArithmeticException("lastStoneWeightII() has a logical error!");
    }
}
```

## JavaScript
### Solution 1: Iterate through knapsack size in reverse order
```javascript
var lastStoneWeightII = function(stones) {
  const sum = _.sum(stones)

  const dp = Array(Math.floor(sum / 2) + 1).fill(false)
  dp[0] = true

  for (const stone of stones) {
    for (let j = dp.length - 1; j >= stone; j--) {
      dp[j] = dp[j] || dp[j - stone]
    }
  }

  for (let j = dp.length - 1; j >= 0; j--) {
    if (dp[j]) {
      return sum - j * 2
    }
  }
};
```

### Solution 2: Iterate through knapsack size in any order (recommended)
```javascript
var lastStoneWeightII = function(stones) {
  const sum = _.sum(stones)

  const dp = Array(Math.floor(sum / 2) + 1).fill(false)
  dp[0] = true

  for (const stone of stones) {
    const dc = [...dp]

    for (let j = stone; j < dp.length; j++) {
      dp[j] = dc[j] || dc[j - stone]
    }
  }

  for (let j = dp.length - 1; j >= 0; j--) {
    if (dp[j]) {
      return sum - j * 2
    }
  }
};
```

## Go
### Solution 1: Iterate through knapsack size in reverse order
```go
func lastStoneWeightII(stones []int) int {
    sum := 0
    for _, stone := range stones {
        sum += stone
    }

    dp := make([]bool, sum / 2 + 1)
    dp[0] = true

    for _, stone := range stones {
        for j := len(dp) - 1; j >= stone; j-- {
            dp[j] = dp[j] || dp[j - stone]
        }
    }

    for j := len(dp) - 1; j >= 0; j-- {
        if dp[j] {
            return sum - j * 2
        }
    }

    return -1 // This line should be unreachable. It represents function has a logical error.
}
```

### Solution 2: Iterate through knapsack size in any order (recommended)
```go
func lastStoneWeightII(stones []int) int {
    sum := 0
    for _, stone := range stones {
        sum += stone
    }

    dp := make([]bool, sum / 2 + 1)
    dp[0] = true

    for _, stone := range stones {
        dc := slices.Clone(dp)

        for j := stone; j < len(dp); j++ {
            dp[j] = dc[j] || dc[j - stone]
        }
    }

    for j := len(dp) - 1; j >= 0; j-- {
        if dp[j] {
            return sum - j * 2
        }
    }

    return -1 // This line should be unreachable. It represents function has a logical error.
}
```

## Ruby
### Solution 1: Iterate through knapsack size in reverse order
```ruby
def last_stone_weight_ii(stones)
  sum = stones.sum

  dp = Array.new(sum / 2 + 1, false)
  dp[0] = true

  stones.each do |stone|
    (1..(dp.size - 1)).reverse_each do |j|
      break if j < stone

      dp[j] = dp[j] || dp[j - stone]
    end
  end

  (0..(dp.size - 1)).reverse_each do |j|
    return sum - j * 2 if dp[j]
  end
end
```

### Solution 2: Iterate through knapsack size in any order (recommended)
```ruby
def last_stone_weight_ii(stones)
  sum = stones.sum

  dp = Array.new(sum / 2 + 1, false)
  dp[0] = true

  stones.each do |stone|
    dc = dp.clone

    (stone..(dp.size - 1)).each do |j|
      dp[j] = dc[j] || dc[j - stone]
    end
  end

  (0..(dp.size - 1)).reverse_each do |j|
    return sum - j * 2 if dp[j]
  end
end
```
