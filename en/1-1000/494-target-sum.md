# 494. Target Sum - LeetCode Python/Java/C++/JS code

Visit original link: [494. Target Sum - LeetCode Python/Java/C++/JS code](https://leetcodepython.com/en/leetcode/494-target-sum) for a better experience!

LeetCode link: [494. Target Sum](https://leetcode.com/problems/target-sum), difficulty: **Medium**.

## LeetCode description of "494. Target Sum"

You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `+` and `-` before each integer in nums and then concatenate all the integers.

- For example, if `nums = [2, 1]`, you can add a `+` before 2 and a `-` before `1` and concatenate them to build the expression `+2-1`.

Return the number of different **expressions** that you can build, which evaluates to `target`.

### [Example 1]

**Input**: `nums = [1,1,1,1,1], target = 3`

**Output**: `5`

**Explanation**: 

<p>-1 + 1 + 1 + 1 + 1 = 3<br>
+1 - 1 + 1 + 1 + 1 = 3<br>
+1 + 1 - 1 + 1 + 1 = 3<br>
+1 + 1 + 1 - 1 + 1 = 3<br>
+1 + 1 + 1 + 1 - 1 = 3</p>


### [Example 2]

**Input**: `nums = [1], target = 1`

**Output**: `1`

### [Constraints]

- `1 <= nums.length <= 20`
- `0 <= nums[i] <= 1000`
- `0 <= sum(nums[i]) <= 1000`
- `-1000 <= target <= 1000`

## Intuition

This problem is quite difficult if you have not solved similar problems before. So before you start working on this question, it is recommended that you first work on another relatively simple question [416. Partition Equal Subset Sum](416-partition-equal-subset-sum.md) that is similar to this one.

## Pattern of "Dynamic Programming"

"Dynamic Programming" requires the use of the `dp` array to store the results. The value of `dp[i][j]` can be converted from its previous (or multiple) values ​​through a formula. Therefore, the value of `dp[i][j]` is derived step by step, and it is related to the previous `dp` record value.

#### "Dynamic programming" is divided into five steps

1. Determine the meaning of each value of the array `dp`.
2. Initialize the value of the array `dp`.
3. Fill in the `dp` grid data "in order" according to an example.
4. Based on the `dp` grid data, derive the "recursive formula".
5. Write a program and print the `dp` array. If it is not as expected, adjust it.

#### Detailed description of these five steps

1. Determine the meaning of each value of the array `dp`.
    - First determine whether `dp` is a one-dimensional array or a two-dimensional array. A `one-dimensional rolling array` means that the values ​​of the array are overwritten at each iteration. Most of the time, using `one-dimensional rolling array` instead of `two-dimensional array` can simplify the code; but for some problems, such as operating "two swappable arrays", for the sake of ease of understanding, it is better to use `two-dimensional array`.
    - Try to use the meaning of the `return value` required by the problem as the meaning of `dp[i]` (one-dimensional) or `dp[i][j]` (two-dimensional). It works about 60% of the time. If it doesn't work, try other meanings.
    - Try to save more information in the design. Repeated information only needs to be saved once in a `dp[i]`.
    - Use simplified meanings. If the problem can be solved with `boolean value`, don't use `numeric value`.
2. Initialize the value of the array `dp`. The value of `dp` involves two levels:
    1. The length of `dp`. Usually: `condition array length plus 1` or `condition array length`.
    2. The value of `dp[i]` or `dp[i][j]`. `dp[0]` or `dp[0][0]` sometimes requires special treatment.
3. Fill in the `dp` grid data "in order" according to an example.
    - The "recursive formula" is the core of the "dynamic programming" algorithm. But the "recursive formula" is obscure. If you want to get it, you need to make a table and use data to inspire yourself.
    - If the original example is not good enough, you need to redesign one yourself.
    - According to the example, fill in the `dp` grid data "in order", which is very important because it determines the traversal order of the code.
    - Most of the time, from left to right, from top to bottom. But sometimes it is necessary to traverse from right to left, from bottom to top, from the middle to the right (or left), such as the "palindrome" problems. Sometimes, it is necessary to traverse a line twice, first forward and then backward.
    - When the order is determined correctly, the starting point is determined. Starting from the starting point, fill in the `dp` grid data "in order". This order is also the order in which the program processes.
    - In this process, you will get inspiration to write a "recursive formula". If you can already derive the formula, you do not need to complete the grid.
4. Based on the `dp` grid data, derive the "recursive formula".
    - There are three special positions to pay attention to: `dp[i - 1][j - 1]`, `dp[i - 1][j]` and `dp[i][j - 1]`, the current `dp[i][j]` often depends on them.
    - When operating "two swappable arrays", due to symmetry, we may need to use `dp[i - 1][j]` and `dp[i][j - 1]` at the same time.
5. Write a program and print the `dp` array. If it is not as expected, adjust it.
    - Focus on analyzing those values that are not as expected.

After reading the above, do you feel that "dynamic programming" is not that difficult? Try to solve this problem. 🤗

## Step by Step Solutions

1. Determine the **meaning** of the `dp[j]`
    - `dp[j]` represents that by using the **first** `i` nums, the **number** of different **expressions** that you can build, which evaluates to `j`.
    - `dp[j]` is an **integer**.
2. Determine the `dp` array's initial value
    - Use an example. We didn't use the `Example 1: Input: nums = [1,1,1,1,1], target = 3` because it is too special and is not a good example for deriving a formula.
    - I made up an example: `nums = [1,2,1,2], target = 4`.
    - First, determine the `size` of the knapsack.
        - The `target` value may be very small, such as `0`, so it alone cannot determine the `size` of the knapsack.
        - The sum of `nums` should also be taken into account to fully cover all knapsack sizes.
        - `target` may be negative, but considering that `+` and `-` are added to `num` arbitrarily, the `dp[j]` should be symmetrical around `0`. So the result of negative `target` `dp[target]` is equal to `dp[abs(target)]`.
        - So the `size` of the knapsack can be `max(sum(nums), target) + 1`.
    - Second, determine what are the `items`. The `items` are the `nums` in this problem.

        ```
        So after initialization, the 'dp' array would be:
        #   0 1 2 3 4 5 6
        #   1 0 0 0 0 0 0 # dp
        # 1
        # 2 
        # 1
        # 2
        ```
    - `dp[0]` is set to `1`, indicating that an empty knapsack can be achieved by not using any `nums`. In addition, it is used as the starting value, and the subsequent `dp[j]` will depend on it. If it is `0`, all values of `dp[j]` will be `0`.
    - `dp[j] = 0 (j != 0)`, indicating that it is impossible to get `j` with no `nums`.
3. According to an example, fill in the `dp` grid data "in order".

    ```
    1. Use the first num '1'.
    #   0 1 2 3 4 5 6
    #   1 0 0 0 0 0 0
    # 1 0 1 0 0 0 0 0 # dp
    # 2
    # 1
    # 2
    ```
    ```
    2. Use the second num '2'.
    #   0 1 2 3 4 5 6
    #   1 0 0 0 0 0 0
    # 1 0 1 0 0 0 0 0
    # 2 0 1 0 1 0 0 0
    # 1
    # 2
    ```
    ```
    3. Use the third num '1'.
    #   0 1 2 3 4 5 6
    #   1 0 0 0 0 0 0
    # 1 0 1 0 0 0 0 0
    # 2 0 1 0 1 0 0 0
    # 1 2 0 2 0 1 0 0
    # 2
    ```
    ```
    4. Use the fourth num '2'.
    #   0 1 2 3 4 5 6
    #   1 0 0 0 0 0 0
    # 1 0 1 0 0 0 0 0
    # 2 0 1 0 1 0 0 0
    # 1 2 0 2 0 1 0 0
    # 2 4 0 3 0 2 0 1 # dp
    ```
4. According to the `dp` grid data, derive the "recursive formula".

    ```java
    dp[j] = dp[abs(j - nums[i])] + dp[j + nums[i]]
    ```
    - If `j < nums[i]`, `dp[j - nums[i]]` will raise `array index out of range` exception. So we use the `dp[abs(j - num)]` which is equal to it, because the `dp[j]` are symmetrical around `0`, such as `dp[-j]` equals to `dp[j]` (`-j` is an imaginary index).
    - When `j + nums[i] >= dp.length`, `dp[j + nums[i]]` must be `0` to prevent interference.
5. Write a program and print the `dp` array. If it is not as expected, adjust it.

## Complexity

- Time complexity: `O(n * sum)`.
- Space complexity: `O(n * sum)`.

## C#

```csharp
public class Solution
{
    public int FindTargetSumWays(int[] nums, int target)
    {
        target = Math.Abs(target);

        var dp = new int[Math.Max(nums.Sum(), target) + 1];
        dp[0] = 1;

        foreach (var num in nums)
        {
            var dc = (int[])dp.Clone();

            for (var j = 0; j < dp.Length; j++)
            {
                dp[j] = dc[Math.Abs(j - num)] + (j + num < dp.Length ? dc[j + num] : 0);
            }
        }

        return dp[target];
    }
}
```

## Python

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        target = abs(target)

        dp = [0] * (max(sum(nums), target) + 1)
        dp[0] = 1

        for num in nums:
            dc = dp.copy()

            for j in range(len(dp)):
                dp[j] = dc[abs(j - num)] + (dc[j + num] if j + num < len(dp) else 0)

        return dp[target]
```

## C++

```cpp
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int target) {
        auto sum = reduce(nums.begin(), nums.end());
        target = abs(target);

        auto dp = vector<int>(max(sum, target) + 1);
        dp[0] = 1;

        for (auto num : nums) {
            auto dc = dp;

            for (auto j = 0; j < dp.size(); j++) {
                dp[j] = dc[abs(j - num)] + (j + num < dp.size() ? dc[j + num] : 0);
            }
        }

        return dp[target];
    }
};
```

## Java

```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        var sum = IntStream.of(nums).sum();
        target = Math.abs(target);

        var dp = new int[Math.max(sum, target) + 1];
        dp[0] = 1;

        for (var num : nums) {
            var dc = dp.clone();

            for (var j = 0; j < dp.length; j++) {
                dp[j] = dc[Math.abs(j - num)] + (j + num < dp.length ? dc[j + num] : 0);
            }
        }

        return dp[target];
    }
}
```

## JavaScript

```javascript
var findTargetSumWays = function (nums, target) {
   target = Math.abs(target)

   const dp = Array(Math.max(_.sum(nums), target) + 1).fill(0)
   dp[0] = 1

   for (const num of nums) {
      const dc = [...dp]

      for (let j = 0; j < dp.length; j++) {
         dp[j] = dc[Math.abs(j - num)] + (j + num < dp.length ? dc[j + num] : 0)
      }
   }

   return dp[target]
};
```

## Go

```go
func findTargetSumWays(nums []int, target int) int {
    sum := 0
    for _, num := range nums {
        sum += num
    }
    target = int(math.Abs(float64(target)))

    dp := make([]int, max(sum, target) + 1)
    dp[0] = 1

    for _, num := range nums {
        dc := slices.Clone(dp)

        for j := 0; j < len(dp); j++ {
            addition := 0
            if j + num < len(dp) {
                addition = dc[j + num]
            }
            dp[j] = dc[int(math.Abs(float64((j - num))))] + addition
        }
    }

    return dp[target]
}
```

## Ruby

```ruby
def find_target_sum_ways(nums, target)
  target = target.abs

  dp = Array.new([ nums.sum, target ].max + 1, 0)
  dp[0] = 1

  nums.each do |num|
    dc = dp.clone

    dp.each_with_index do |_, j|
      dp[j] = dc[(j - num).abs] + (j + num < dp.size ? dc[j + num] : 0)
    end
  end

  dp[target]
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCodePython.com](https://leetcodepython.com): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [494. Target Sum - LeetCode Python/Java/C++/JS code](https://leetcodepython.com/en/leetcode/494-target-sum).

GitHub repository: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

