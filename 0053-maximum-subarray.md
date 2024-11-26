# 53. Maximum Subarray
LeetCode problem: [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

## Problem
> Given an integer array nums, find the subarray with the largest sum, and return its sum.

```
Example 1:
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The subarray [4,-1,2,1] has the largest sum 6.
```

## Thoughts
* This problem can be solved by using `greedy algorithm`, but here we will use another way.
* Imagine the size of nums is `i`, let us consider if the same question is applied to the `subarray` of `nums` from index `0` to `i - 1`.
* The answer is `yes`. Then let us think if the `i - 1`'s answer could impact the answer of `i`.
* The answer is still `yes`. What would be the impact?
* For `nums[i]`,
if the `previous sum` is negative, we can discard it;
if the `previous sum` is positive, we can add it to the `current sum`.
* So we can use dynamic programming to solve the problem.

### Common steps in dynamic programming
These five steps are a pattern for solving dynamic programming problems.

1. Determine the **meaning** of the `dp[i]`
    * At first, try to use the problem's `return` value as the value of `dp[i]` to determine the meaning of `dp[i]`. If it doesn't work, try another way.
    * Imagine that `dp[i]` represents the `largest sum` at index `i`. The `dp[i + 1]` cannot be calculated by `dp[i]`. So we have to change this meaning.
    * Then consider that `dp[i]` represents the `current sum` at index `i`. We can see the `largest sum` is recorded in the `current sum` array. It may work.
2. Determine the `dp` array's initial value
    * `dp[i] = nums[i]` would be good.
3. Determine the `dp` array's recurrence formula
    * Use an example:
```
nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
dp   = [-2, 1, -2, 4,  3, 5, 6,  1, 5]
```
   * After analyzing the sample `dp` data, we can derive the `recurrence formula`:
    * `dp[i] = max(nums[i], dp[i - 1] + nums[i])`.
4. Determine the `dp` array's traversal order
    * `dp[i]` depends on `dp[i - 1]`, so we should traverse the `dp` array from left to right.
5. Check the `dp` array's value
    * Print the `dp` to see if it is as expected.

### Complexity
* Time: `O(n)`.
* Space: `O(n)`.

## Python
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        dp = nums.copy()
        
        for i in range(1, len(dp)):
            dp[i] = max(nums[i], dp[i - 1] + nums[i])
        
        return max(dp)
```

## C++
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        vector<int> dp = nums;

        for (int i = 1; i < dp.size(); i++) {
            dp[i] = max(nums[i], dp[i - 1] + nums[i]);
        }

        return *max_element(dp.begin(), dp.end());
    }
};
```

## Java
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int[] dp = nums.clone();
        int result = dp[0];
        
        for (int i = 1; i < dp.length; i++) {
            dp[i] = Math.max(nums[i], dp[i - 1] + nums[i]);
            if (dp[i] > result) result = dp[i];
        }

        return result; // or 'return Arrays.stream(dp).max().getAsInt();'
    }
}
```

## C#
```c#
public class Solution {
    public int MaxSubArray(int[] nums) {
        int[] dp = (int[]) nums.Clone();
        int result = dp[0];

        for (int i = 1; i < dp.Length; i++) {
            dp[i] = Math.Max(nums[i], dp[i - 1] + nums[i]);
            if (dp[i] > result) result = dp[i];
        }
        
        return result; // or 'return dp.Max();'
    }
}
```

## JavaScript
```javascript
var maxSubArray = function(nums) {
    let dp = [...nums]

    for (let i = 1; i < dp.length; i++) {
        dp[i] = Math.max(nums[i], dp[i - 1] + nums[i])
    }

    return Math.max(...dp)
};
```

## Go
```go
func maxSubArray(nums []int) int {
    dp := slices.Clone(nums)

    for i := 1; i < len(nums); i++ {
        dp[i] = max(nums[i], dp[i - 1] + nums[i])
    }

    return slices.Max(dp)
}
```

## Ruby
```ruby
def max_sub_array(nums)
    dp = nums.clone

    for i in 1..dp.size - 1
      dp[i] = [nums[i], dp[i - 1] + nums[i]].max
    end
    
    dp.max
end
```
