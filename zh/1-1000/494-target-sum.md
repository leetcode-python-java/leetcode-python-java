# 494. Target Sum
LeetCode link: [494. Target Sum](https://leetcode.com/problems/target-sum/)

## LeetCode problem description
You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `+` and `-` before each integer in nums and then concatenate all the integers.

* For example, if `nums = [2, 1]`, you can add a `+` before 2 and a `-` before `1` and concatenate them to build the expression `+2-1`.

Return the number of different **expressions** that you can build, which evaluates to `target`.
```
Example 1:

Input: nums = [1,1,1,1,1], target = 3
Output: 5

Explanation: There are 5 ways to assign symbols to make the sum of nums be target 3.
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3
--------------------------------------------------------------------------------------------------

Example 2:

Input: nums = [1], target = 1
Output: 1
--------------------------------------------------------------------------------------------------

Constraints:

1 <= nums.length <= 20
0 <= nums[i] <= 1000
0 <= sum(nums[i]) <= 1000
-1000 <= target <= 1000
```

* This problem is quite difficult if you have not solved similar problems before. So before you start working on this question,
it is recommended that you first work on another relatively simple question [416. Partition Equal Subset Sum](416-partition-equal-subset-sum.md) that is similar to this one.

## Thoughts
* When we see a set of numbers being used once to obtain another number through some calculation (just like this question), we can consider this to be a `0/1 Knapsack Problem`.
* `0/1 Knapsack Problem` belongs to `Dynamic Programming`. `Dynamic programming` means that the answer to the current problem can be derived from the previous similar problem. Therefore, the `dp` array is used to record all the answers.
* The core logic of the `0/1 Knapsack Problem` uses a two-dimensional `dp` array or a one-dimensional `dp` **rolling array**, first **traverses the items**, then **traverses the knapsack size** (`in reverse order` or use `dp.clone`), then **reference the previous value corresponding to the size of current 'item'**.
* There are many things to remember when using a two-dimensional `dp` array, and it is difficult to write it right at once during an interview, so I won't describe it here.

### Common steps in '0/1 Knapsack Problem'
These five steps are a pattern for solving `Dynamic Programming` problems.

1. Determine the **meaning** of the `dp[j]`
    * We can use a one-dimensional `dp` **rolling array**. Rolling an array means that the values of the array are overwritten each time through the iteration. 
    * At first, try to use the problem's `return` value as the value of `dp[j]` to determine the meaning of `dp[j]`. If it doesn't work, try another way.
    * So, `dp[j]` represents that by using the **first** `i` nums, the **number** of different **expressions** that you can build, which evaluates to `j`.
    * `dp[j]` is an **integer**.
2. Determine the `dp` array's initial value
    * Use an example. We didn't use the `Example 1: Input: nums = [1,1,1,1,1], target = 3` because it is too special and is not a good example for deriving a formula.
    * I made up an example: `nums = [1,2,1,2], target = 4`. The example must be simple, otherwise it would take too long to complete the grid.
    * First, determine the `size` of the knapsack.
    * The `target` value may be very small, such as `0`, so it alone cannot determine the `size` of the knapsack.
    * The sum of `nums` should also be taken into account to fully cover all knapsack sizes.
    * `target` may be negative, but considering that `+` and `-` are added to `num` arbitrarily, the `dp[j]` should be symmetrical around `0`. So the result of negative `target` `dp[target]` is equal to `dp[abs(target)]`.
    * So the `size` of the knapsack can be `max(sum(nums), target) + 1`.
    * The `items` are the `nums`.
    ```
    So after initialization, the 'dp' array would be:
    #    0  1  2  3  4  5  6
    #    1  0  0  0  0  0  0 # dp
    # 1  
    # 2  
    # 1  
    # 2  
    ```
    * You can see the `dp` array size is **one** greater than the knapsack size. In this way, the knapsack size and index value are equal, which helps to understand.
    * `dp[0]` is set to `1`, indicating that an empty knapsack can be achieved by not using any `nums`. In addition, it is used as the starting value, and the subsequent `dp[j]` will depend on it. If it is `0`, all values of `dp[j]` will be `0`.
    * `dp[j] = 0 (j != 0)`, indicating that it is impossible to get `j` with no `nums`.
3. Determine the `dp` array's recurrence formula
    * Try to complete the grid. In the process, you will get inspiration to derive the formula.
   ```
   1. Use the first num '1'.
   #    0  1  2  3  4  5  6
   #    1  0  0  0  0  0  0
   # 1  0  1  0  0  0  0  0 # dp
   # 2
   # 1
   # 2
   ```
   ```
   2. Use the second num '2'.
   #    0  1  2  3  4  5  6
   #    1  0  0  0  0  0  0
   # 1  0  1  0  0  0  0  0
   # 2  0  1  0  1  0  0  0
   # 1  
   # 2  
   ```
   ```
   3. Use the third num '1'.
   #    0  1  2  3  4  5  6
   #    1  0  0  0  0  0  0
   # 1  0  1  0  0  0  0  0
   # 2  0  1  0  1  0  0  0
   # 1  2  0  2  0  1  0  0
   # 2  
   ```
   ```
   4. Use the fourth num '2'.
   #    0  1  2  3  4  5  6
   #    1  0  0  0  0  0  0
   # 1  0  1  0  0  0  0  0
   # 2  0  1  0  1  0  0  0
   # 1  2  0  2  0  1  0  0
   # 2  4  0  3  0  2  0  1 # dp
   ```
    * After analyzing the sample `dp` grid, we can derive the `Recurrence Formula`:
   ```java
   dp[j] = dp[abs(j - nums[i])] + dp[j + nums[i]]
   ```
    * If `j < nums[i]`, `dp[j - nums[i]]` will raise `array index out of range` exception. So we use the `dp[abs(j - num)]` which is equal to it, because the `dp[j]` are symmetrical around `0`, such as `dp[-j]` equals to `dp[j]` (`-j` is an imaginary index).
4. Determine the `dp` array's traversal order
    * `dp[j]` depends on `dp[abs(j - nums[i])]` and `dp[j + nums[i]]`, so we can traverse the `dp` array in any order, but must reference the clone of `dp` to prevent the referenced value from being modified during the iteration.
    * For `j + nums[i] >= dp.length`, `dp[j + nums[i]]` must be `0` because their values are too large and exceed the maximum sum of `nums`.
5. Check the `dp` array's value
    * Print the `dp` to see if it is as expected.

### Complexity
* Time: `O(n * sum)`.
* Space: `O(n * sum)`.

## C#
```c#
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

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
