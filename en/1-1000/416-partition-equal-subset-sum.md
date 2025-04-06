# 416. Partition Equal Subset Sum - LeetCode Best Practices

Visit original link: [416. Partition Equal Subset Sum - LeetCode Best Practices](https://leetcoder.net/en/leetcode/416-partition-equal-subset-sum) for a better experience!

LeetCode link: [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum), difficulty: **Medium**.

## LeetCode description of "416. Partition Equal Subset Sum"

Given an integer array `nums`, return `true` if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or `false` otherwise.

### [Example 1]

**Input**: `nums = [1,5,11,5]`

**Output**: `true`

**Explanation**: 

<p>The array can be partitioned as [1, 5, 5] and [11].</p>


### [Example 2]

**Input**: `nums = [1,2,3,5]`

**Output**: `false`

**Explanation**: 

<p>The array cannot be partitioned into equal sum subsets.</p>


### [Constraints]

- `1 <= nums.length <= 200`
- `1 <= nums[i] <= 100`

## Intuition 1

- When we first see this problem, we might want to loop through all subsets of the array. If there is a subset whose sum is equal to `half of the sum`, then return `true`. This can be achieved with a `backtracking algorithm`, but after seeing the constraint `nums.length <= 200`, we can estimate that the program will time out.
- This problem can be solved using the `0/1 knapsack problem` algorithm.

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

## Steps

1. Determine the **meaning** of the `dp[j]`
    - `dp[j]` represents whether it is possible to `sum` the first `i` `nums` to get `j`.
    - `dp[j]` is a boolean.

2. Determine the `dp` array's initial value
   - Use an example:

       ```
       nums = [1,5,11,5], so 'half of the sum' is 11.
       The `size` of the knapsack is `11 + 1`, and the `items` are `nums`.
       So after initialization, the 'dp' array would be:
       #    0 1 2 3 4 5 6 7 8 9 10 11
       #    T F F F F F F F F F F  F  # dp
       # 1  
       # 5  
       # 11 
       # 5  
       ```
    - `dp[0]` is set to `true`, indicating that an empty knapsack can be achieved by not putting any items in it. In addition, it is used as the starting value, and the subsequent `dp[j]` will depend on it. If it is `false`, all values of `dp[j]` will be `false`.
    - `dp[j] = false (j != 0)`, indicating that it is impossible to get `j` with no `nums`.
3. Fill in the `dp` grid data "in order" according to an example.

    ```
    1. Use the first num '1'.
    #    0 1 2 3 4 5 6 7 8 9 10 11
    #    T F F F F F F F F F F  F
    # 1  T T F F F F F F F F F  F # dp
    ```

    ```
    2. Use the second num '5'.
    #    0 1 2 3 4 5 6 7 8 9 10 11
    #    T F F F F F F F F F F  F
    # 1  T T F F F F F F F F F  F
    # 5  T T F F F T T F F F F  F
    ```

    ```
    3. Use the third num '11'.
    #    0 1 2 3 4 5 6 7 8 9 10 11
    #    T F F F F F F F F F F  F
    # 1  T T F F F F F F F F F  F
    # 5  T T F F F T T F F F F  F
    # 11 T T F F F T T F F F F  T
    ```

    ```
    3. Use the last num '5'.
    #    0 1 2 3 4 5 6 7 8 9 10 11
    #    T F F F F F F F F F F  F
    # 1  T T F F F F F F F F F  F
    # 5  T T F F F T T F F F F  F
    # 11 T T F F F T T F F F F  T
    # 5  T T F F F T T F F F T  T # dp
    ```
4. Based on the `dp` grid data, derive the "recursive formula".

    ```cpp
    dp[j] = dp[j] || dp[j - nums[i]]
    ```

5. Write a program and print the `dp` array. If it is not as expected, adjust it.

## Complexity

- Time complexity: `O(n * sum/2)`.
- Space complexity: `O(sum/2)`.

## Python

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        sum_ = sum(nums)

        if sum_ % 2 == 1:
            return False

        dp = [False] * ((sum_ // 2) + 1)
        dp[0] = True

        for num in nums:
            # If not traversing in reverse order, the newly assigned value `dp[j]` will act as `dp[j - num]` later,
            # then the subsequent `dp[j]` will be affected. But each `num` can only be used once!
            j = len(dp) - 1
            while j >= num:
                dp[j] = dp[j] or dp[j - num]
                j -= 1

        return dp[-1]
```

## C#

```csharp
public class Solution
{
    public bool CanPartition(int[] nums)
    {
        int sum = nums.Sum();

        if (sum % 2 == 1)
            return false;

        var dp = new bool[sum / 2 + 1];
        dp[0] = true;

        foreach (var num in nums)
        {
            for (var j = dp.GetUpperBound(0); j >= num; j--)
            {
                dp[j] = dp[j] || dp[j - num];
            }
        }

        return dp.Last();
    }
}
```

## C++

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        auto sum = reduce(nums.begin(), nums.end());

        if (sum % 2 == 1) {
            return false;
        }

        auto dp = vector<bool>(sum / 2 + 1);
        dp[0] = true;

        for (auto num : nums) {
            for (auto j = dp.size() - 1; j >= num; j--) {
                dp[j] = dp[j] || dp[j - num];
            }
        }

        return dp.back();
    }
};
```

## Java

```java
class Solution {
    public boolean canPartition(int[] nums) {
        var sum = IntStream.of(nums).sum();
        
        if (sum % 2 == 1) {
            return false;
        }

        var dp = new boolean[sum / 2 + 1];
        dp[0] = true;

        for (var num : nums) {
            for (var j = dp.length - 1; j >= num; j--) {
                dp[j] = dp[j] || dp[j - num];
            }
        }

        return dp[dp.length - 1];
    }
}
```

## JavaScript

```javascript
var canPartition = function (nums) {
  const sum = _.sum(nums)

  if (sum % 2 == 1) {
    return false
  }

  const dp = Array(sum / 2 + 1).fill(false)
  dp[0] = true

  for (const num of nums) {
    for (let j = dp.length - 1; j >= num; j--) {
      dp[j] = dp[j] || dp[j - num]
    }
  }

  return dp.at(-1)
};
```

## Go

```go
func canPartition(nums []int) bool {
    sum := 0
    for _, num := range nums {
        sum += num
    }

    if sum % 2 == 1 {
        return false
    }

    dp := make([]bool, sum / 2 + 1)
    dp[0] = true

    for _, num := range nums {
        for j := len(dp) - 1; j >= num; j-- {
            dp[j] = dp[j] || dp[j - num]
        }
    }

    return dp[len(dp) - 1]
}
```

## Ruby

```ruby
def can_partition(nums)
  sum = nums.sum

  return false if sum % 2 == 1

  dp = Array.new(sum / 2 + 1, false)
  dp[0] = true

  nums.each do |num|
    (num...dp.size).reverse_each do |j|
      dp[j] = dp[j] || dp[j - num]
    end
  end

  dp[-1]
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

## Complexity

- Time complexity: `O(n * sum/2)`.
- Space complexity: `O(n * sum/2)`.

## Python

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        sum_ = sum(nums)

        if sum_ % 2 == 1:
            return False

        dp = [False] * ((sum_ // 2) + 1)
        dp[0] = True

        for num in nums:
            # Make a copy of the 'dp' that has not been modified to eliminate distractions.
            dc = dp.copy()

            for j in range(num, len(dp)): # any order is fine
                dp[j] = dc[j] or dc[j - num] # Use 'dc' instead of 'dp' because 'dp' will be modified.

        return dp[-1]
```

## C#

```csharp
public class Solution
{
    public bool CanPartition(int[] nums)
    {
        int sum = nums.Sum();

        if (sum % 2 == 1)
            return false;

        var dp = new bool[sum / 2 + 1];
        dp[0] = true;

        foreach (var num in nums)
        {
            var dc = (bool[])dp.Clone();

            for (var j = num; j < dp.Length; j++)
            {
                dp[j] = dc[j] || dc[j - num];
            }
        }

        return dp.Last();
    }
}
```

## C++

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        auto sum = reduce(nums.begin(), nums.end());

        if (sum % 2 == 1) {
            return false;
        }

        auto dp = vector<bool>(sum / 2 + 1);
        dp[0] = true;

        for (auto num : nums) {
            auto dc = dp;

            for (auto j = num; j < dp.size(); j++) {
                dp[j] = dc[j] || dc[j - num];
            }
        }

        return dp.back();
    }
};
```

## Java

```java
class Solution {
    public boolean canPartition(int[] nums) {
        var sum = IntStream.of(nums).sum();
        
        if (sum % 2 == 1) {
            return false;
        }

        var dp = new boolean[sum / 2 + 1];
        dp[0] = true;

        for (var num : nums) {
            var dc = dp.clone();

            for (var j = num; j < dp.length; j++) {
                dp[j] = dc[j] || dc[j - num];
            }
        }

        return dp[dp.length - 1];
    }
}
```

## JavaScript

```javascript
var canPartition = function (nums) {
  const sum = _.sum(nums)

  if (sum % 2 == 1) {
    return false
  }

  const dp = Array(sum / 2 + 1).fill(false)
  dp[0] = true

  for (const num of nums) {
    const dc = [...dp]

    for (let j = num; j < dp.length; j++) {
      dp[j] = dc[j] || dc[j - num]
    }
  }

  return dp.at(-1)
};
```

## Go

```go
func canPartition(nums []int) bool {
    sum := 0
    for _, num := range nums {
        sum += num
    }

    if sum % 2 == 1 {
        return false
    }

    dp := make([]bool, sum / 2 + 1)
    dp[0] = true

    for _, num := range nums {
        dc := slices.Clone(dp)

        for j := num; j < len(dp); j++ {
            dp[j] = dc[j] || dc[j - num]
        }
    }

    return dp[len(dp) - 1]
}
```

## Ruby

```ruby
def can_partition(nums)
  sum = nums.sum

  return false if sum % 2 == 1

  dp = Array.new(sum / 2 + 1, false)
  dp[0] = true

  nums.each do |num|
    dc = dp.clone

    (num...dp.size).each do |j|
      dp[j] = dc[j] || dc[j - num]
    end
  end

  dp[-1]
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [leetcoder.net](https://leetcoder.net): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [416. Partition Equal Subset Sum - LeetCode Best Practices](https://leetcoder.net/en/leetcode/416-partition-equal-subset-sum).

GitHub repository: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

