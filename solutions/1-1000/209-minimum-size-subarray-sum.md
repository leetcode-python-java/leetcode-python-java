# 209. Minimum Size Subarray Sum - LeetCode Solution
LeetCode problem link: [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum)

## LeetCode problem description
Given an array of positive integers `nums` and a positive integer `target`, return _the **minimal length** of a **subarray** whose sum is greater than or equal to `target`_. If there is no such subarray, return `0` instead.

* A **subarray** is a contiguous non-empty sequence of elements within an array.

### Example 1
```ruby
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
```

### Example 2
```ruby
Input: target = 4, nums = [1,4,4]
Output: 1
```

### Example 3
```ruby
Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0
```

### Constraints
- `1 <= target <= 10 ** 9`
- `1 <= nums.length <= 100000`
- `1 <= nums[i] <= 10000`

## Intuition behind the Solution
For **subarray** problems, you can consider using **Sliding Window Technique**, which belongs to the **Fast and Slow Pointers Technique**.

## Steps to the Solution
* Traverse the `nums` array, the `index` of the element is named `fast_index`. This is a common method of the _Fast and Slow Pointers Technique_.
* `sum += nums[fast_index]`.
* If `sum >= target`, `sum -= nums[slow_index]; slow_index += 1`:
```python
while sum >= target:
    min_length = min(min_length, fast_index - slow_index + 1)
    sum -= nums[slow_index]
    slow_index += 1
```

## Complexity
* Time: `O(n)`.
* Space: `O(1)`.

## Java
```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        var minLength = Integer.MAX_VALUE;
        var sum = 0;
        var slowIndex = 0;

        for (var fastIndex = 0; fastIndex < nums.length; fastIndex++) {
            sum += nums[fastIndex];

            while (sum >= target) {
                minLength = Math.min(minLength, fastIndex - slowIndex + 1);
                sum -= nums[slowIndex];
                slowIndex++;
            }
        }

        if (minLength == Integer.MAX_VALUE) {
            return 0;
        }

        return minLength;
    }
}
```

## Python
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        min_length = float('inf')
        sum_ = 0
        slow_index = 0

        for fast_index, num in enumerate(nums):
            sum_ += num

            while sum_ >= target:
                min_length = min(min_length, fast_index - slow_index + 1)
                sum_ -= nums[slow_index]
                slow_index += 1

        if min_length == float('inf'):
            return 0

        return min_length
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
var minSubArrayLen = function(target, nums) {
  let minLength = Number.MAX_SAFE_INTEGER
  let sum = 0
  let slowIndex = 0

  nums.forEach((num, fastIndex) => {
    sum += num

    while (sum >= target) {
      minLength = Math.min(minLength, fastIndex - slowIndex + 1)
      sum -= nums[slowIndex]
      slowIndex++
    }
  })

  if (minLength == Number.MAX_SAFE_INTEGER) {
    return 0
  }

  return minLength
};
```

## C#
```c#
public class Solution
{
    public int MinSubArrayLen(int target, int[] nums)
    {
        int minLength = Int32.MaxValue;
        int sum = 0;
        int slowIndex = 0;

        for (int fastIndex = 0; fastIndex < nums.Length; fastIndex++)
        {
            sum += nums[fastIndex];

            while (sum >= target)
            {
                minLength = Math.Min(minLength, fastIndex - slowIndex + 1);
                sum -= nums[slowIndex];
                slowIndex++;
            }
        }

        if (minLength == Int32.MaxValue)
            return 0;

        return minLength;
    }
}
```

## Go
```go
// Welcome to create a PR to complete the code of this language, thanks!
```

## Ruby
```ruby
# Welcome to create a PR to complete the code of this language, thanks!
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
