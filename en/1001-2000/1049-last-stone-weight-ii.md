# 1049. Last Stone Weight II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

Visit original link: [1049. Last Stone Weight II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.to/en/leetcode/1049-last-stone-weight-ii) for a better experience!

LeetCode link: [1049. Last Stone Weight II](https://leetcode.com/problems/last-stone-weight-ii), difficulty: **Medium**.

## LeetCode description of "1049. Last Stone Weight II"

You are given an array of integers `stones` where `stones[i]` is the weight of the `i-th` stone.

We are playing a game with the stones. On each turn, we choose any two stones and smash them together.
Suppose the stones have weights `x` and `y` with `x <= y`. The result of this smash is:

- If `x == y`, both stones are destroyed, and
- If `x != y`, the stone of weight `x` is destroyed, and the stone of weight `y` has new weight `y - x`.

At the end of the game, there is **at most one** stone left.

Return the smallest possible weight of the left stone. If there are no stones left, return `0`.

### [Example 1]

**Input**: `stones = [2,7,4,1,8,1]`

**Output**: `1`

**Explanation**: 

<p>We can combine 2 and 4 to get 2, so the array converts to [2,7,1,8,1] then,<br>
we can combine 7 and 8 to get 1, so the array converts to [2,1,1,1] then,<br>
we can combine 2 and 1 to get 1, so the array converts to [1,1,1] then,<br>
we can combine 1 and 1 to get 0, so the array converts to [1], then that&#39;s the optimal value.</p>


### [Example 2]

**Input**: `stones = [31,26,33,21,40]`

**Output**: `5`

### [Constraints]

1 <= stones.length <= 30
1 <= stones[i] <= 100

### [Hints]

<details>
  <summary>Hint 1</summary>
  Think of the final answer as a sum of weights with + or - sign symbols in front of each weight. Actually, all sums with 1 of each sign symbol are possible.

  
</details>

<details>
  <summary>Hint 2</summary>
  Use dynamic programming: for every possible sum with N stones, those sums +x or -x is possible with N+1 stones, where x is the value of the newest stone. (This overcounts sums that are all positive or all negative, but those don't matter.)

  
</details>

## Intuition 1

* This problem can be solved by brute force, that is, find all subsets of the array, see if the sum of each subset array is close to half of the sum of the complete array, and find the one that is closest. But when we see `stones.length <= 30`, we know that such a solution will definitely time out.
* So we need to change our thinking. The question is equivalent to finding the minimum difference between the sums of the two arrays after splitting. If we find a subset array whose sum is closest to half of the sum of the complete array, then it is the subset array we want.
* Then this problem will become a `0/1 Knapsack Problem`.

## Pattern of "Dynamic Programming"

"Dynamic Programming" requires the use of the `dp` array to store the results. The value of `dp[i][j]` can be converted from its previous (or multiple) values ​​through a formula. Therefore, the value of `dp[i][j]` is derived step by step, and it is related to the previous `dp` record value.

#### "Dynamic programming" is divided into five steps

1. Determine the **meaning** of each value of the array `dp`.
2. Initialize the value of the array `dp`.
3. Fill in the `dp` grid data **in order** according to an example.
4. Based on the `dp` grid data, derive the **recursive formula**.
5. Write a program and print the `dp` array. If it is not as expected, adjust it.

#### Detailed description of these five steps

1. Determine the **meaning** of each value of the array `dp`.
    - First determine whether `dp` is a one-dimensional array or a two-dimensional array. A `one-dimensional rolling array` means that the values ​​of the array are overwritten at each iteration. Most of the time, using `one-dimensional rolling array` instead of `two-dimensional array` can simplify the code; but for some problems, such as operating "two swappable arrays", for the sake of ease of understanding, it is better to use `two-dimensional array`.
    - Try to use the meaning of the `return value` required by the problem as the meaning of `dp[i]` (one-dimensional) or `dp[i][j]` (two-dimensional). It works about 60% of the time. If it doesn't work, try other meanings.
    - Try to save more information in the design. Repeated information only needs to be saved once in a `dp[i]`.
    - Use simplified meanings. If the problem can be solved with `boolean value`, don't use `numeric value`.
2. Initialize the value of the array `dp`. The value of `dp` involves two levels:
    1. The length of `dp`. Usually: `condition array length plus 1` or `condition array length`.
    2. The value of `dp[i]` or `dp[i][j]`. `dp[0]` or `dp[0][0]` sometimes requires special treatment.
3. Fill in the `dp` grid data **in order** according to an example.
    - The "recursive formula" is the core of the "dynamic programming" algorithm. But the "recursive formula" is obscure. If you want to get it, you need to make a table and use data to inspire yourself.
    - If the original example is not good enough, you need to redesign one yourself.
    - According to the example, fill in the `dp` grid data "in order", which is very important because it determines the traversal order of the code.
    - Most of the time, from left to right, from top to bottom. But sometimes it is necessary to traverse from right to left, from bottom to top, from the middle to the right (or left), such as the "palindrome" problems. Sometimes, it is necessary to traverse a line twice, first forward and then backward.
    - When the order is determined correctly, the starting point is determined. Starting from the starting point, fill in the `dp` grid data "in order". This order is also the order in which the program processes.
    - In this process, you will get inspiration to write a "recursive formula". If you can already derive the formula, you do not need to complete the grid.
4. Based on the `dp` grid data, derive the **recursive formula**.
    - There are three special positions to pay attention to: `dp[i - 1][j - 1]`, `dp[i - 1][j]` and `dp[i][j - 1]`, the current `dp[i][j]` often depends on them.
    - When operating "two swappable arrays", due to symmetry, we may need to use `dp[i - 1][j]` and `dp[i][j - 1]` at the same time.
5. Write a program and print the `dp` array. If it is not as expected, adjust it.
    - Focus on analyzing those values that are not as expected.

After reading the above, do you feel that "dynamic programming" is not that difficult? Try to solve this problem. 🤗

## Pattern of "0/1 Knapsack Problem"

The typical "0/1 knapsack problem" means that each "item" can only be used once to fill the "knapsack". "Items" have "weight" and "value" attributes. Find the maximum value of "items" that can be stored in the "knapsack".

Its characteristics are: there is a **set of numbers**, each number can only be used once, and through some calculation, **another number** is obtained. The question can also be turned into whether it can be obtained? How many variations are there? And so on.

Because "0/1 Knapsack Problem" belongs to "Dynamic Programming", I will explain it in the pattern of "Dynamic Programming".

1. Determine what each value of the array `dp` represents.
    - Prefer **one-dimensional rolling array** because the code is concise.
    - Determine what is "item" and what is "knapsack".
        - If `dp[j]` is a boolean value, then `dp[j]` indicates whether the `sum` of the first `i` items can get `j`.
        - If `dp[j]` is a numerical value, then `dp[j]` indicates the maximum (or minimum) value that `dp[j]` can reach using the first `i` items.

2. Initialize the value of the array `dp`.
    - Determine the size of the "knapsack". It is necessary to add 1 to the size of the knapsack, that is, insert `dp[0]` as the starting point, which is convenient for understanding and reference.
    - `dp[0]` sometimes needs special treatment.
3. According to an example, fill in the `dp` grid data "in order".
    - First in the outer loop, **traverse the items**.
    - Then in the inner loop, **traverse the knapsack size**.
    - When traversing the knapsack size, since `dp[j]` depends on `dp[j]` and `dp[j - weights[i]]`, we should traverse the `dp` array **from right to left**.
    - Please think about whether it is possible to traverse the `dp` array from `left to right`?
4. According to the `dp` grid data, derive the "recursive formula".
    - If `dp[j]` is a boolean value:

        ```cpp
        dp[j] = dp[j] || dp[j - items[i]]
        ```
    - If `dp[j]` is a numeric value:

        ```cpp
        dp[j] = min_or_max(dp[j], dp[j - weights[i]] + values[i])
        ```
5. Write a program and print the `dp` array. If it is not as expected, adjust it.

## Step by Step Solutions

1. Determine the **meaning** of the `dp[j]`
    - `dp[j]` represents whether it is possible to `sum` the first `i` `stones` to get `j`.
    - `dp[j]` is a boolean.
2. Determine the `dp` array's initial value
    - Use an example:

        ```
        stones = [2,7,4,1,8,1], so 'half of the sum' is 11.
        The `size` of the knapsack is `11 + 1`, and the `items` are `stones`.
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
    - `dp[0]` is set to `true`, indicating that an empty knapsack can be achieved by not using any `stones`. In addition, it is used as the starting value, and the subsequent `dp[j]` will depend on it. If it is `false`, all values of `dp[j]` will be `false`.
    - `dp[j] = false (j != 0)`, indicating that it is impossible to get `j` with no `stones`.
3. Fill in the `dp` grid data "in order" according to an example.

    ```
    1. Use the first stone '2'.
    #   0 1 2 3 4 5 6 7 8 9 10 11
    #   T F F F F F F F F F F  F
    # 2 T F T F F F F F F F F  F  # dp
    ```
    ```
    2. Use the second stone '7'.
    #   0 1 2 3 4 5 6 7 8 9 10 11
    #   T F F F F F F F F F F  F
    # 2 T F T F F F F F F F F  F
    # 7 T F T F F F F T F T F  F
    ```
    ```
    3. Use the third stone '4'.
    #   0 1 2 3 4 5 6 7 8 9 10 11
    #   T F F F F F F F F F F  F
    # 2 T F T F F F F F F F F  F
    # 7 T F T F F F F F T F F  F
    # 4 T F T F T F T T F T F  T # dp
    # ...
    ```
4. Based on the `dp` grid data, derive the "recursive formula".

    ```cpp
    dp[j] = dp[j] || dp[j - stones[i]]
    ```
5. Write a program and print the `dp` array. If it is not as expected, adjust it.

## Complexity

- Time complexity: `O(n * sum/2)`.
- Space complexity: `O(sum/2)`.

## Python

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

## C#

```csharp
public class Solution {
    public int LastStoneWeightII(int[] stones) {
        var sum = stones.Sum();

        var dp = new bool[sum / 2 + 1];
        dp[0] = true;

        foreach (int stone in stones) {
            for (var j = dp.GetUpperBound(0); j >= stone; j--) {
                dp[j] = dp[j] || dp[j - stone];
            }
        }

        for (var j = dp.GetUpperBound(0); j >= 0; j--) {
            if (dp[j]) {
                return sum - j * 2;
            }
        }

        throw new ArithmeticException("lastStoneWeightII() has a logical error!");
    }
}
```

## C++

```cpp
class Solution {
public:
    int lastStoneWeightII(vector<int>& stones) {
        auto sum = reduce(stones.begin(), stones.end());

        auto dp = vector<bool>(sum / 2 + 1);
        dp[0] = true;

        for (auto stone : stones) {
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

## Java

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

## JavaScript

```javascript
var lastStoneWeightII = function (stones) {
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

## Go

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

## Ruby

```ruby
def last_stone_weight_ii(stones)
  sum = stones.sum

  dp = Array.new(sum / 2 + 1, false)
  dp[0] = true

  stones.each do |stone|
    (1...dp.size).reverse_each do |j|
      break if j < stone

      dp[j] = dp[j] || dp[j - stone]
    end
  end

  (0...dp.size).reverse_each do |j|
    return sum - j * 2 if dp[j]
  end
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## Intuition 2

In solution 1, the traversal order is **from right to left** which really matters.

During the interview, you need to remember it. Is there any way to not worry about the traversal order?

<details><summary>Click to view the answer</summary><p> As long as you copy the original `dp` and reference the value of the copy, you don't have to worry about the original `dp` value being modified. </p></details>

## Complexity

- Time complexity: `O(n * sum/2)`.
- Space complexity: `O(n * sum/2)`.

## Python

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

## C#

```csharp
public class Solution
{
    public int LastStoneWeightII(int[] stones)
    {
        int sum = stones.Sum();

        var dp = new bool[sum / 2 + 1];
        dp[0] = true;

        foreach (int stone in stones)
        {
            var dc = (bool[]) dp.Clone();

            for (var j = stone; j < dp.Length; j++)
            {
                dp[j] = dc[j] || dc[j - stone];
            }
        }

        for (var j = dp.GetUpperBound(0); j >= 0; j--)
        {
            if (dp[j])
            {
                return sum - j * 2;
            }
        }

        throw new ArithmeticException("lastStoneWeightII() has a logical error!");
    }
}
```

## C++

```cpp
class Solution {
public:
    int lastStoneWeightII(vector<int>& stones) {
        auto sum = reduce(stones.begin(), stones.end());

        auto dp = vector<bool>(sum / 2 + 1);
        dp[0] = true;

        for (auto stone : stones) {
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

## JavaScript

```javascript
var lastStoneWeightII = function (stones) {
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

```ruby
def last_stone_weight_ii(stones)
  sum = stones.sum

  dp = Array.new(sum / 2 + 1, false)
  dp[0] = true

  stones.each do |stone|
    dc = dp.clone

    (stone...dp.size).each do |j|
      dp[j] = dc[j] || dc[j - stone]
    end
  end

  (0...dp.size).reverse_each do |j|
    return sum - j * 2 if dp[j]
  end
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCode.to](https://leetcode.to): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [1049. Last Stone Weight II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.to/en/leetcode/1049-last-stone-weight-ii).

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

