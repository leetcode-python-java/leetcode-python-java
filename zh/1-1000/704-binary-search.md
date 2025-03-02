# 704. Binary Search - Best Practices of LeetCode Solutions
LeetCode link: [704. Binary Search](https://leetcode.com/problems/binary-search)

## LeetCode problem description
给定一个 `n` 个元素有序的（升序）整型数组 `nums` 和一个目标值 `target`  ，写一个函数搜索 `nums` 中的 `target`，如果目标值存在返回下标，否则返回 `-1`。

### Example 1
```ruby
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

### Example 2
```ruby
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

### Constraints
- 你可以假设 `nums` 中的所有元素是不重复的。
- `n` 将在 `[1, 10000]` 之间。
- `nums` 的每个元素都将在 `[-9999, 9999]` 之间。

## Intuition
Because it is an already sorted array, by using the middle value for comparison, half of the numbers can be eliminated each time.

## Approach
The fastest and easiest way is to use the three indices `left`, `right`, and `middle`. If `nums[middle] > target`, then `right = middle - 1`, otherwise, `left = middle + 1`.

## Complexity
* Time: `O(log n)`.
* Space: `O(1)`.

## Java
```java
class Solution {
    public int search(int[] nums, int target) {
        var left = 0;
        var right = nums.length - 1;

        while (left <= right) {
            var middle = (left + right) / 2;
            
            if (nums[middle] == target) {
                return middle;
            }
            
            if (nums[middle] > target) {
                right = middle - 1;
            } else {
                left = middle + 1;
            }
        }

        return -1;
    }
}
```

## Python
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1

        while left <= right:
            middle = (left + right) // 2

            if nums[middle] == target:
                return middle

            if nums[middle] > target:
                right = middle - 1
            else:
                left = middle + 1

        return -1
```

## C++
```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        auto left = 0;
        int right = nums.size() - 1; // Should not use 'auto' here because 'auto' will make this variable become `unsigned long` which has no `-1`.

        while (left <= right) {
            auto middle = (left + right) / 2;
            
            if (nums[middle] == target) {
                return middle;
            }
            
            if (nums[middle] > target) {
                right = middle - 1;
            } else {
                left = middle + 1;
            }
        }

        return -1;
    }
};
```

## JavaScript
```javascript
var search = function (nums, target) {
  let left = 0
  let right = nums.length - 1

  while (left <= right) {
    const middle = Math.floor((left + right) / 2)

    if (nums[middle] == target) {
      return middle
    }

    if (nums[middle] > target) {
      right = middle - 1
    } else {
      left = middle + 1
    }
  }

  return -1
};
```

## C#
```c#
public class Solution
{
    public int Search(int[] nums, int target)
    {
        int left = 0;
        int right = nums.Length - 1;

        while (left <= right)
        {
            int middle = (left + right) / 2;
            
            if (nums[middle] == target)
            {
                return middle;
            }
            
            if (nums[middle] > target)
            {
                right = middle - 1;
            } 
            else
            {
                left = middle + 1;
            }
        }

        return -1;
    }
}
```

## Go
```go
func search(nums []int, target int) int {
    left := 0
    right := len(nums) - 1

    for left <= right {
        middle := (left + right) / 2

        if nums[middle] == target {
            return middle
        }

        if nums[middle] > target {
            right = middle - 1
        } else {
            left = middle + 1
        }
    }

    return -1
}
```

## Ruby
```ruby
def search(nums, target)
  left = 0
  right = nums.size - 1

  while left <= right
    middle = (left + right) / 2

    return middle if nums[middle] == target

    if nums[middle] > target
      right = middle - 1
    else
      left = middle + 1
    end
  end

  -1
end
```

## C
```c
// Welcome to create a PR to complete the code of this language, thanks!
```

## Kotlin
```kotlin
// Welcome to create a PR to complete the code of this language, thanks!
```

## Swift
```swift
// Welcome to create a PR to complete the code of this language, thanks!
```

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
