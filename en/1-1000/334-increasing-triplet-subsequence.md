# 334. Increasing Triplet Subsequence - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

Visit original link: [334. Increasing Triplet Subsequence - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.to/en/leetcode/334-increasing-triplet-subsequence) for a better experience!

LeetCode link: [334. Increasing Triplet Subsequence](https://leetcode.com/problems/increasing-triplet-subsequence), difficulty: **Medium**.

## LeetCode description of "334. Increasing Triplet Subsequence"

Given an integer array `nums`, return `true` if there exists a triple of indices `(i, j, k)` such that `i < j < k` and `nums[i] < nums[j] < nums[k]`. If no such indices exists, return `false`.

### [Example 1]

**Input**: `nums = [1,2,3,4,5]`

**Output**: `true`

**Explanation**: `Any triplet where i < j < k is valid.`

### [Example 2]

**Input**: `nums = [5,4,3,2,1]`

**Output**: `false`

**Explanation**: `No triplet exists.`

### [Example 3]

**Input**: `nums = [2,1,5,0,4,6]`

**Output**: `true`

**Explanation**: 

<p>The triplet (3, 4, 5) is valid because nums[3] == 0 &lt; nums[4] == 4 &lt; nums[5] == 6.</p>


### [Constraints]

- `1 <= nums.length <= 5 * 10^5`
- `-2^31 <= nums[i] <= 2^31 - 1`

**Follow up**: Could you implement a solution that runs in `O(n)` time complexity and `O(1)` space complexity?

## Intuition

To find an increasing triplet subsequence, we can track the smallest and second-smallest elements seen so far. If we encounter an element larger than both, we've found our triplet.

## Pattern of "Greedy Algorithm"

The `Greedy Algorithm` is a strategy that makes the locally optimal choice at each step with the hope of leading to a "globally optimal" solution. In other words, "local optima" can result in "global optima."

## Step-by-Step Solution

1. Initialize `first` as the first element and `second` as infinity.
2. Iterate through the array starting from the second element:
    - If current element > `second`, triplet found → return `true`.
    - If current element > `first`, update `second` to current element.
    - Else, update `first` to current element (keeping it the smallest seen so far).
3. If loop completes without finding a triplet, return `false`.

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Python

```python
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        first = nums[0]
        second = float('inf')

        for i in range(1, len(nums)):
            if nums[i] > second:
                return True

            if nums[i] > first:
                second = nums[i]
            else:
                first = nums[i]

        return False
```

## Java

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        int first = nums[0];
        int second = Integer.MAX_VALUE;

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] > second) {
                return true;
            }

            if (nums[i] > first) {
                second = nums[i];
            } else {
                first = nums[i];
            }
        }
        return false;
    }
}
```

## C++

```cpp
class Solution {
public:
    bool increasingTriplet(vector<int>& nums) {
        int first = nums[0];
        int second = INT_MAX;

        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] > second) {
                return true;
            }

            if (nums[i] > first) {
                second = nums[i];
            } else {
                first = nums[i];
            }
        }

        return false;
    }
};
```

## JavaScript

```javascript
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var increasingTriplet = function (nums) {
  let first = nums[0]
  let second = Infinity

  for (let i = 1; i < nums.length; i++) {
    if (nums[i] > second) {
      return true
    }
    
    if (nums[i] > first) {
      second = nums[i]
    } else {
      first = nums[i]
    }
  }

  return false
};
```

## C#

```csharp
public class Solution {
    public bool IncreasingTriplet(int[] nums) {
        int first = nums[0];
        int second = int.MaxValue;
        
        for (int i = 1; i < nums.Length; i++) {
            if (nums[i] > second) {
                return true;
            }

            if (nums[i] > first) {
                second = nums[i];
            } else {
                first = nums[i];
            }
        }

        return false;
    }
}
```

## Go

```go
func increasingTriplet(nums []int) bool {
    first := nums[0]
    second := math.MaxInt32

    for _, num := range nums[1:] {
        if num > second {
            return true
        }

        if num > first {
            second = num
        } else {
            first = num
        }
    }

    return false
}
```

## Ruby

```ruby
# @param {Integer[]} nums
# @return {Boolean}
def increasing_triplet(nums)
  first = nums[0]
  second = Float::INFINITY

  nums[1..].each do |num|
    if num > second
      return true
    end  
    
    if num > first
      second = num
    else
      first = num
    end
  end

  false
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCode.to](https://leetcode.to): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [334. Increasing Triplet Subsequence - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.to/en/leetcode/334-increasing-triplet-subsequence).

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

