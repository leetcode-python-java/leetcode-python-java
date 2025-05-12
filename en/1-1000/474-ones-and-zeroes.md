# 474. Ones and Zeroes - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

Visit original link: [474. Ones and Zeroes - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/474-ones-and-zeroes) for a better experience!

LeetCode link: [474. Ones and Zeroes](https://leetcode.com/problems/ones-and-zeroes), difficulty: **Medium**.

## LeetCode description of "474. Ones and Zeroes"

You are given an array of binary strings `strs` and two integers `m` and `n`.

Return the size of the largest subset of `strs` such that there are **at most** `m` `0`'s and `n` `1`'s in the subset.

A set `x` is a **subset** of a set `y` if all elements of `x` are also elements of `y`.

### [Example 1]

**Input**: `strs = ["10","0001","111001","1","0"], m = 5, n = 3`

**Output**: `4`

**Explanation**: 

<p>The largest subset with at most 5 0&#39;s and 3 1&#39;s is {&quot;10&quot;, &quot;0001&quot;, &quot;1&quot;, &quot;0&quot;}, so the answer is 4.<br>
Other valid but smaller subsets include {&quot;0001&quot;, &quot;1&quot;} and {&quot;10&quot;, &quot;1&quot;, &quot;0&quot;}.<br>
{&quot;111001&quot;} is an invalid subset because it contains 4 1&#39;s, greater than the maximum of 3.</p>


### [Example 2]

**Input**: `strs = ["10","0","1"], m = 1, n = 1`

**Output**: `2`

**Explanation**: 

<p>The largest subset is {&quot;0&quot;, &quot;1&quot;}, so the answer is 2.</p>


### [Constraints]

- `1 <= strs.length <= 600`
- `1 <= strs[i].length <= 100`
- `'strs[i]' consists only of digits '0' and '1'`
- `1 <= m, n <= 100`

## Intuition

This question is difficult. It is recommended to complete a simple question of the same type first [416. Partition Equal Subset Sum](416-partition-equal-subset-sum.md).

- After completing 416, you will find that this question requires solving the `0/1 Knapsack Problem` in two dimensions.
- The solution is to first solve the problem in one dimension and then expand it to two dimensions.
- It is no need to draw a grid that considers both dimensions together, that's too complicated. Let's first **only** consider the quantity limit of `0`.

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
    - Since we are only considering the zero count constraint for now, we can use a one-dimensional `dp` array.
    - `items` is `strs`, `backpack` is `max_zero_count`.
    - `dp[j]` represents the maximum number of strings that can be selected with at most `j` zeros.
    - `dp[j]` is an integer.

2. Determine the `dp` array's initial value
    - Use an example, example 1: `Input: strs = ["10","0001","111001","1","0"], m = 5, n = 3`.
    - After initialization:
        ```python
        max_zero_count = m
        dp = [0] * (max_zero_count + 1)
        ```
    - `dp[0] = 0`, indicating that with no zeros, we can select 0 strings.
    - `dp[j] = 0` as the initial value because we will use `max` to increase them later.

3. According to an example, fill in the `dp` grid data "in order".
    - Let's analyze the example step by step:

        ```
        # Initial state
        #    0 1 2 3 4 5
        #    0 0 0 0 0 0

        # After processing "10" (1 zero)
        #    0 1 2 3 4 5
        #    0 1 1 1 1 1

        # After processing "0001" (3 zeros)
        #    0 1 2 3 4 5
        #    0 1 1 1 2 2

        # After processing "111001" (2 zeros)
        #    0 1 2 3 4 5
        #    0 1 1 2 2 2

        # After processing "1" (0 zeros)
        #    0 1 2 3 4 5
        #    0 2 2 3 3 3

        # After processing "0" (1 zero)
        #    0 1 2 3 4 5
        #    0 2 3 3 4 4
        ```
4. According to the `dp` grid data, derive the "recursive formula".

    ```cpp
    dp[j] = max(dp[j], dp[j - zero_count] + 1)
    ```
5. Write a program and print the `dp` array. If it is not as expected, adjust it.
    - The code that only considers the quantity limit of `0` is:

    ```python
    class Solution:
        def findMaxForm(self, strs: List[str], max_zero_count: int, n: int) -> int:
            dp = [0] * (max_zero_count + 1)

            for string in strs:
                zero_count = count_zero(string)

                for j in range(len(dp) - 1, zero_count - 1, -1): # must iterate in reverse order!
                    dp[j] = max(dp[j], dp[j - zero_count] + 1)

            return dp[-1]


    def count_zero(string):
        zero_count = 0

        for bit in string:
            if bit == '0':
                zero_count += 1

        return zero_count
    ```

#### Now, you can consider another dimension: the quantity limit of `1`.

It should be handled similarly to `0` but in another dimension. Please see the complete code below.

## Complexity

- Time complexity: `O(N * M * Len)`.
- Space complexity: `O(N * M)`.

## Python

```python
class Solution:
    def findMaxForm(self, strs: List[str], max_zero_count: int, max_one_count: int) -> int:
        dp = [[0] * (max_one_count + 1) for _ in range(max_zero_count + 1)]

        for string in strs:
            zero_count, one_count = count_zero_one(string)

            for i in range(len(dp) - 1, zero_count - 1, -1):
                for j in range(len(dp[0]) - 1, one_count - 1, -1):
                    dp[i][j] = max(dp[i][j], dp[i - zero_count][j - one_count] + 1)
        
        return dp[-1][-1]


def count_zero_one(string):
    zero_count = 0
    one_count = 0

    for bit in string:
        if bit == '0':
            zero_count += 1
        else:
            one_count += 1

    return zero_count, one_count
```

## C++

```cpp
class Solution {
public:
    int findMaxForm(vector<string>& strs, int max_zero_count, int max_one_count) {
        vector<vector<int>> dp(max_zero_count + 1, vector<int>(max_one_count + 1, 0));

        for (auto& str : strs) {
            auto zero_count = 0;
            auto one_count = 0;

            for (auto bit : str) {
                if (bit == '0') {
                    zero_count++;
                } else {
                    one_count++;
                }
            }

            for (auto i = max_zero_count; i >= zero_count; i--) {
                for (auto j = max_one_count; j >= one_count; j--) {
                    dp[i][j] = max(dp[i][j], dp[i - zero_count][j - one_count] + 1);
                }
            }
        }

        return dp[max_zero_count][max_one_count];
    }
};
```

## Java

```java
class Solution {
    public int findMaxForm(String[] strs, int maxZeroCount, int maxOneCount) {
        var dp = new int[maxZeroCount + 1][maxOneCount + 1];

        for (var str : strs) {
            var zeroCount = 0;
            var oneCount = 0;

            for (var bit : str.toCharArray()) {
                if (bit == '0') {
                    zeroCount++;
                } else {
                    oneCount++;
                }
            }

            for (var i = maxZeroCount; i >= zeroCount; i--) {
                for (var j = maxOneCount; j >= oneCount; j--) {
                    dp[i][j] = Math.max(dp[i][j], dp[i - zeroCount][j - oneCount] + 1);
                }
            }
        }

        return dp[maxZeroCount][maxOneCount];
    }
}
```

## C#

```csharp
public class Solution
{
    public int FindMaxForm(string[] strs, int maxZeroCount, int maxOneCount)
    {
        var dp = new int[maxZeroCount + 1, maxOneCount + 1];

        foreach (var str in strs)
        {
            var (zeroCount, oneCount) = CountZeroOne(str);

            for (var i = maxZeroCount; i >= zeroCount; i--)
            {
                for (var j = maxOneCount; j >= oneCount; j--)
                {
                    dp[i, j] = Math.Max(dp[i, j], dp[i - zeroCount, j - oneCount] + 1);
                }
            }
        }

        return dp[maxZeroCount, maxOneCount];
    }

    (int, int) CountZeroOne(string str)
    {
        var zeroCount = 0;
        var oneCount = 0;

        foreach (var bit in str)
        {
            if (bit == '0')
            {
                zeroCount++;
            }
            else
            {
                oneCount++;
            }
        }

        return (zeroCount, oneCount);
    }
}
```

## JavaScript

```javascript
var findMaxForm = function (strs, maxZeroCount, maxOneCount) {
  const dp = Array(maxZeroCount + 1).fill().map(
    () => Array(maxOneCount + 1).fill(0)
  )

  for (const str of strs) {
    const [zeroCount, oneCount] = countZeroOne(str)

    for (let i = dp.length - 1; i >= zeroCount; i--) {
      for (let j = dp[0].length - 1; j >= oneCount; j--) {
        dp[i][j] = Math.max(dp[i][j], dp[i - zeroCount][j - oneCount] + 1)
      }
    }
  }

  return dp.at(-1).at(-1)
};

function countZeroOne(str) {
  let zeroCount = 0
  let oneCount = 0

  for (const bit of str) {
    if (bit === '0') {
      zeroCount++
    } else {
      oneCount++
    }
  }

  return [zeroCount, oneCount]
}
```

## Go

```go
func findMaxForm(strs []string, maxZeroCount int, maxOneCount int) int {
    dp := make([][]int, maxZeroCount + 1)
    for i := range dp {
        dp[i] = make([]int, maxOneCount + 1)
    }

    for _, str := range strs {
        zeroCount, oneCount := countZeroOne(str)

        for i := len(dp) - 1; i >= zeroCount; i-- {
            for j := len(dp[0]) - 1; j >= oneCount; j-- {
                dp[i][j] = max(dp[i][j], dp[i - zeroCount][j - oneCount] + 1)
            }
        }
    }

    return dp[maxZeroCount][maxOneCount]
}

func countZeroOne(str string) (int, int) {
    zeroCount := 0
    oneCount := 0

    for _, bit := range str {
        if bit == '0' {
            zeroCount++
        } else {
            oneCount++
        }
    }

    return zeroCount, oneCount
}
```

## Ruby

```ruby
def find_max_form(strs, max_zero_count, max_one_count)
  dp = Array.new(max_zero_count + 1) do
    Array.new(max_one_count + 1, 0)
  end

  strs.each do |string|
    zero_count, one_count = count_zero_one(string)

    (zero_count...dp.size).reverse_each do |i|
      (one_count...dp[0].size).reverse_each do |j|
        dp[i][j] = [ dp[i][j], dp[i - zero_count][j - one_count] + 1 ].max
      end
    end
  end

  dp[-1][-1]
end

def count_zero_one(string)
  zero_count = 0
  one_count = 0

  string.each_char do |bit|
    if bit == '0'
      zero_count += 1
    else
      one_count += 1
    end
  end

  [ zero_count, one_count ]
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCode.blog](https://leetcode.blog): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [474. Ones and Zeroes - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/474-ones-and-zeroes).

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

