# 503. Next Greater Element II
LeetCode link: [503. Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/)

## LeetCode problem description
Given a circular integer array `nums` (i.e., the next element of `nums[nums.length - 1]` is `nums[0]`), return the **next greater number** for every element in `nums`.

The **next greater number** of a number `x` is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, return `-1` for this number.
```
------------------------------------------------------------------------------------
[Example 1]

Input: nums = [1,2,1]
Output: [2,-1,2]

Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number. 
The second 1's next greater number needs to search circularly, which is also 2.
------------------------------------------------------------------------------------
[Example 2]

Input: nums = [1,2,3,4,3]
Output: [2,3,4,-1,4]
------------------------------------------------------------------------------------
[Constraints]

1 <= nums.length <= 10000
-10**9 <= nums[i] <= 10**9
------------------------------------------------------------------------------------
```

## Solution 1: Brute Force
This problem can be solved using **Brute Force**. But if the `nums.length` is much greater, the solution will time out.
Then We need to use a more efficient algorithm.

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Complexity
* Time: `O(n * n)`.
* Space: `O(n)`.

## Solution 2: Monotonic Stack Algorithm (more efficient)
This solution will reduce the time complexity to **O(n)**.

A similar issue is [Next Greater Element I](496-next-greater-element-i.md), you can read it first.

Checkout the `Python` section bellow to view the code.

## Python
### Solution 2: Monotonic Stack
```python
# This is a better test case:
# [2, 5, 3, 2, 4, 1] for `nums`
# [2, 5, 3, 2, 4, 1, 2, 5, 3, 2, 4] for `extended_nums`

class Solution:
    def nextGreaterElements(self, nums: List[int]) -> List[int]:
        extended_nums = nums + nums[:-1]
        index_stack = []
        result = [-1] * len(extended_nums)

        for i, num in enumerate(extended_nums):
            while index_stack and extended_nums[index_stack[-1]] < num:
                result[index_stack.pop()] = num

            index_stack.append(i)

        return result[:len(nums)]
```

### Solution 1: Brute Force
```python
class Solution:
    def nextGreaterElements(self, nums: List[int]) -> List[int]:
        results = [-1] * len(nums)
        nums2 = nums + nums

        for i, num1 in enumerate(nums):
            for j in range(i + 1, len(nums2)):
                if nums2[j] > num1:
                    results[i] = nums2[j]
                    break

        return results
```


## C#
```c#
public class Solution
{
    public int[] NextGreaterElements(int[] nums)
    {
        int[] nums2 = [..nums, ..nums];
        var results = new int[nums.Length];
        Array.Fill(results, -1);

        for (var i = 0; i < nums.Length; i++)
        {
            for (var j = i + 1; j < nums2.Length; j++)
            {
                if (nums2[j] > nums[i])
                {
                    results[i] = nums2[j];
                    break;
                }
            }
        }

        return results;
    }
}
```

## Java
```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        var results = new int[nums.length];
        Arrays.fill(results, -1);

        var nums2 = Arrays.copyOf(nums, nums.length * 2);
        System.arraycopy(nums, 0, nums2, nums.length, nums.length);

        for (var i = 0; i < nums.length; i++) {
            for (var j = i + 1; j < nums2.length; j++) {
                if (nums2[j] > nums[i]) {
                    results[i] = nums2[j];
                    break;
                }
            }
        }

        return results;
    }
}
```

## C++
```cpp
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        vector<int> results(nums.size(), -1);
        auto nums2 = nums;
        ranges::copy(nums, back_inserter(nums2));

        for (auto i = 0; i < nums.size(); i++) {
            for (auto j = i + 1; j < nums2.size(); j++) {
                if (nums2[j] > nums[i]) {
                    results[i] = nums2[j];
                    break;
                }
            }
        }

        return results;
    }
};
```

## JavaScript
```javascript
var nextGreaterElements = function (nums) {
  const results = Array(nums.length).fill(-1)
  const nums2 = [...nums, ...nums]

  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums2.length; j++) {
      if (nums2[j] > nums[i]) {
        results[i] = nums2[j]
        break
      }
    }
  }

  return results
};
```

## Go
```go
func nextGreaterElements(nums []int) []int {
    results := slices.Repeat([]int{-1}, len(nums))
    nums2 := slices.Repeat(nums, 2)

    for i, num := range nums {
        for j := i + 1; j < len(nums2); j++ {
            if nums2[j] > num {
                results[i] = nums2[j]
                break
            }
        }
    }

  return results
}
```

## Ruby
```ruby
def next_greater_elements(nums)
  results = Array.new(nums.size, -1)
  nums2 = nums + nums

  nums.each_with_index do |num, i|
    ((i + 1)...nums2.size).each do |j|
      if nums2[j] > num
        results[i] = nums2[j]
        break
      end
    end
  end

  results
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
