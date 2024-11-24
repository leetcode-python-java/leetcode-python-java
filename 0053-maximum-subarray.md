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
* Imagine the size of nums is `i`, let us consider if the same question is applied to the `subarray` of `nums` from index `0` to `i - 1`.
* The answer is `yes`. Then let us think if the `i - 1`'s answer could impact the answer of `i`.
* The answer is still `yes`. What would be the impact?
* For index `i`,
if the `previous sum` is negative, we can discard it;
if the `previous sum` is positive, we can add it to the `current sum`.
* So we can use dynamic programming to solve the problem, but we should use the `current sum` instead of the `largest sum` in the `dp` array because `largest sum` is recorded in the `dp` array. 

### Steps of dynamic programming
These five steps are a pattern for solving dynamic programming problems.

1. Define the `dp` array
    * `dp[i]` represents the `current sum` at index `i`.
2. Determine the `dp` array's recurrence formula
    * `dp[i] = max(nums[i], dp[i - 1] + nums[i])`.
3. Determine the `dp` array's initial value
    * `dp[i] = nums[i]` would be good.
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
