# 416. Partition Equal Subset Sum
LeetCode problem: [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

## LeetCode problem description
> Given an integer array `nums`, return `true` if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or `false` otherwise.

```
Example 1:

Input: nums = [1,5,11,5]
Output: true
Explanation: The array can be partitioned as [1, 5, 5] and [11].
------------------------------------------------------------------------

Example 2:

Input: nums = [1,2,3,5]
Output: false
Explanation: The array cannot be partitioned into equal sum subsets.

------------------------------------------------------------------------
Constraints:

1 <= nums.length <= 200
1 <= nums[i] <= 100
```

## Thoughts
* When we first see this problem, we might want to loop through all subsets of the array. If there is a subset whose sum is equal to `half of the sum`, then return `true`. This can be achieved with a `backtracking algorithm`, but after seeing the constraint `nums.length <= 200`, we can estimate that the program will time out.
* This is actually a `01 Knapsack Problem` which belongs to `Dynamic Programming`. `Dynamic programming` means that the answer to the current problem can be derived from the previous similar problem. Therefore, the `dp` array is used to record all the answers.

* The core logic of the `01 Knapsack Problem` uses a two-dimensional `dp` array or a one-dimensional `dp` **rolling array**, first **traverses the items**, then **traverses the knapsack in reverse**, then **reference the previous value corresponding to the size of current 'item'**.
* There are many things to remember when using a two-dimensional `dp` array, and it is difficult to write it right at once during an interview, so I won't describe it here.

### Common steps in '01 Knapsack Problem'
These five steps are a pattern for solving `Dynamic Programming` problems.

1. Determine the **meaning** of the `dp[j]`
    * We can use a one-dimensional `dp` **rolling array**. Rolling an array means that the values of the array are overwritten each time through the loop. 
    * At first, try to use the problem's `return` value as the value of `dp[j]` to determine the meaning of `dp[j]`. If it doesn't work, try another way.
    * So, `dp[j]` represents whether it is possible to `sum` the first `i` `nums` to get `j`.
    * The value of `dp[j]` is a boolean.
2. Determine the `dp` array's initial value
    * Use an example:
   ```
   nums = [1,5,11,5], so 'half of the sum' is 11.
   The `size` of the knapsack is `half of the sum`, and the `items` are `nums`.
   So after initialization, the 'dp' array would be:
   #    0 1 2 3 4 5 6 7 8 9 10 11
   #    T F F F F F F F F F F  F  # dp
   # 1  
   # 5  
   # 11 
   # 5  
   ```
    * You can see the `dp` array size is one greater than the knapsack size. In this way, the backpack size and index value are equal, which helps to understand.
    * `dp[0]` is set to `true`, indicating that an empty backpack can be achieved by not putting any items in it. In addition, it is used as the starting value, and the subsequent `dp[j]` will depend on it. If it is `false`, all values of `dp[j]` will be `false`.
    * `dp[j] = false (j != 0)`, indicating that it is impossible to get `j` with no `nums`.
    
3. Determine the `dp` array's recurrence formula
    * Try to complete the grid. In the process, you will get inspiration to derive the formula.
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
    * After analyzing the sample `dp` grid, we can derive the `Recurrence Formula`:
   ```cpp
   dp[j] = dp[j] || dp[j - nums[i]]
   ```
4. Determine the `dp` array's traversal order
    * `dp[j]` depends on `dp[j]` and `dp[j - nums[i]]`, so we should traverse the `dp` array from top to bottom, then **from right to left**.
    * Please think if we can traverse the `dp` array from top to bottom, then `from left to right`? In the `Python` solution's code comments, I will answer this question.
5. Check the `dp` array's value
    * Print the `dp` to see if it is as expected.

### Complexity
* Time: `O(n * sum/2)`.
* Space: `O(sum/2)`.

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
            # If traversing from left to right, the newly assigned value `dp[j]` will act as `dp[j - num]` later,
            # then the subsequent `dp[j]` will be affected. But each `num` can only be used once.
            for j in range(len(dp) - 1, 0, -1):
                if j < num:
                    break
                dp[j] = dp[j] or dp[j - num]

        return dp[-1]
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

        return dp[dp.size() - 1];
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

## C#
```c#
public class Solution {
    public bool CanPartition(int[] nums) {
        var sum = nums.Sum();

        if (sum % 2 == 1) {
            return false;
        }

        var dp = new bool[sum / 2 + 1];
        dp[0] = true;

        foreach (var num in nums) {
            for (var j = dp.Length - 1; j >= num; j--) {
                dp[j] = dp[j] || dp[j - num];
            }
        }

        return dp[dp.Length - 1];
    }
}
```

## JavaScript
```javascript
var canPartition = function(nums) {
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
    (1..(dp.size - 1)).reverse_each do |j|
      break if j < num
      dp[j] = dp[j] || dp[j - num]
    end
  end

  return dp[-1]
end
```
