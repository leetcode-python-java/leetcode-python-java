# 377. Combination Sum IV
LeetCode problem link: [377. Combination Sum IV](https://leetcode.com/problems/combination-sum-iv/)

## LeetCode problem description
> Given an array of **distinct** integers `nums` and a target integer `target`, return the number of possible combinations that add up to `target`.

The test cases are generated so that the answer can fit in a 32-bit integer.

```
Example 1:

Input: nums = [1,2,3], target = 4
Output: 7

Explanation:
The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)
Note that different sequences are counted as different combinations.
------------------------------------------------------------------------

Example 2:

Input: nums = [9], target = 3
Output: 0

------------------------------------------------------------------------

Constraints:

1 <= nums.length <= 200
1 <= nums[i] <= 1000
All the elements of 'nums' are 'unique'.
1 <= target <= 1000
```

## Thoughts
This is `Unbounded Knapsack Problem` A, and it also requires us to consider the sequences.

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Complexity
* Time: `O(n * m)`.
* Space: `O(n)`.

## C#
```c#
public class Solution
{
    public int CombinationSum4(int[] nums, int target)
    {
        var dp = new int[target + 1];
        dp[0] = 1;

        for (var i = 1; i < dp.Length; i++)
        {
            foreach (var num in nums)
            {
                if (i >= num)
                {
                    dp[i] += dp[i - num];
                }
            }
        }

        return dp.Last();
    }
}
```

## Python
```python
class Solution:
    def combinationSum4(self, nums: List[int], target: int) -> int:
        dp = [0] * (target + 1)
        dp[0] = 1

        for i in range(1, len(dp)):
            for num in nums:
                if i >= num:
                    dp[i] += dp[i - num]

        return dp[-1]
```

## C++
```cpp
class Solution {
public:
    int combinationSum4(vector<int>& nums, int target) {
        vector<unsigned int> dp(target + 1, 0);
        dp[0] = 1;

        for (auto i = 1; i < dp.size(); i++) {
            for (auto num : nums) {
                if (i >= num) {
                    dp[i] += dp[i - num];
                }
            }
        }

        return dp.back();
    }
};
```

## Java
```java
class Solution {
    public int combinationSum4(int[] nums, int target) {
        var dp = new int[target + 1];
        dp[0] = 1;
        
        for (var i = 1; i < dp.length; i++) {
            for (var num : nums) {
                if (i >= num) {
                    dp[i] += dp[i - num];
                }
            }
        }

        return dp[target];
    }
}
```

## JavaScript
```javascript
var combinationSum4 = function (nums, target) {
    const dp = Array(target + 1).fill(0)
    dp[0] = 1

    for (let i = 1; i < dp.length; i++) {
        for (const num of nums) {
            if (i >= num) {
                dp[i] += dp[i - num]
            }
        }
    }

    return dp.at(-1)
};
```

## Go
```go
func combinationSum4(nums []int, target int) int {
    dp := make([]int, target + 1)
    dp[0] = 1
    
    for i := 1; i < len(dp); i++ {
        for _, num := range nums {
            if i >= num {
                dp[i] += dp[i - num]
            }
        }
    }

    return dp[target]
}
```

## Ruby
```ruby
def combination_sum4(nums, target)
  dp = Array.new(target + 1, 0)
  dp[0] = 1

  (1...dp.size).each do |i|
    nums.each do |num|
      dp[i] += dp[i - num] if i >= num
    end
  end

  return dp[-1]
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
