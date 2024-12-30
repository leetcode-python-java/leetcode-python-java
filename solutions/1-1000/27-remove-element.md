# 27. Remove Element - LeetCode Solution
LeetCode problem link: [27. Remove Element](https://leetcode.com/problems/remove-element)

## LeetCode problem description
Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` [in-place](https://en.wikipedia.org/wiki/In-place_algorithm). The order of the elements may be changed. Then return _the number of elements in `nums` which are not equal to `val`_.

Consider the number of elements in `nums` which are not equal to `val` be `k`, to get accepted, you need to do the following things:

* Change the array `nums` such that the first `k` elements of `nums` contain the elements which are not equal to `val`. The remaining elements of `nums` are not important as well as the size of `nums`.
* Return `k`.

### Example 1
```ruby
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

### Example 2
```ruby
Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
Note that the five elements can be returned in any order.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

### Constraints
- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`

<details>
  <summary>Hint 1</summary>
  The problem statement clearly asks us to modify the array in-place and it also says that the element beyond the new length of the array can be anything. Given an element, we need to remove all the occurrences of it from the array. We don't technically need to remove that element per-say, right?
</details>

<details>
  <summary>Hint 2</summary>
  We can move all the occurrences of this element to the end of the array. Use two pointers!
</details>

<details>
  <summary>Hint 3</summary>
  Yet another direction of thought is to consider the elements to be removed as non-existent. In a single pass, if we keep copying the visible elements in-place, that should also solve this problem for us.
</details>

## Intuition behind the Solution
The goal is to remove the elements in the array that are equal to `val`, and the order of the remaining elements is not important.

### Solution 1 (easier to think of)
Then we only need to use the following elements that are not equal to `val` to occupy the elements that are equal to `val`.

![](../../images/examples/27_hint_2.png)

### Solution 2 (more concise and easier to code)
You only need to traverse the array once and keep all numbers that are not equal to `val` at the front of the array.

`slowIndex` is used to save the current front position.

## Complexity
* Time: `O(n)`.
* Space: `O(1)`.

## Java
### Solution 1: Two pointers (easier to think of)
```java
class Solution {
    public int removeElement(int[] nums, int val) {
        var left = 0;
        var right = nums.length - 1;

        while (left <= right) {
            if (nums[left] != val) {
                left += 1;
                continue;
            }

            if (nums[right] == val) {
                right -= 1;
                continue;
            }

            nums[left] = nums[right];
            left += 1;
            right -= 1;
        }

        return left;
    }
}
```

### Solution 2: Fast and Slow Pointers (more concise and easier to code)
```java
class Solution {
    public int removeElement(int[] nums, int val) {
        var slowIndex = 0;

        for (var num : nums) {
            if (num != val) {
                nums[slowIndex] = num;
                slowIndex += 1;
            }
        }

        return slowIndex;
    }
}
```

## Python
### Solution 1: Two pointers (easier to think of)
```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        left = 0
        right = len(nums) - 1

        while left <= right:
            if nums[left] != val:
                left += 1
                continue

            if nums[right] == val:
                right -= 1
                continue

            nums[left] = nums[right]
            left += 1
            right -= 1

        return left
```

### Solution 2: Fast and Slow Pointers (more concise and easier to code)
```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        slow_index = 0

        for num in nums:
            if num != val:
                nums[slow_index] = num
                slow_index += 1

        return slow_index
```

## C++
### Solution 1: Two pointers (easier to think of)
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int left = 0;
        int right = nums.size() - 1;

        while (left <= right) {
            if (nums[left] != val) {
                left += 1;
                continue;
            }

            if (nums[right] == val) {
                right -= 1;
                continue;
            }

            nums[left] = nums[right];
            left += 1;
            right -= 1;
        }

        return left;
    }
};
```

### Solution 2: Fast and Slow Pointers (more concise and easier to code)
```c++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        auto slow_index = 0;

        for (auto num : nums) {
            if (num != val) {
                nums[slow_index] = num;
                slow_index += 1;
            }
        }

        return slow_index;
    }
};
```

## JavaScript
### Solution 1: Two pointers (easier to think of)
```javascript
var removeElement = function (nums, val) {
  let left = 0
  let right = nums.length - 1

  while (left <= right) {
    if (nums[left] != val) {
      left += 1
      continue
    }

    if (nums[right] == val) {
      right -= 1
      continue
    }

    nums[left] = nums[right]
    left += 1
    right -= 1
  }

  return left
};
```

### Solution 2: Fast and Slow Pointers (more concise and easier to code)
```javascript
var removeElement = function (nums, val) {
  let slowIndex = 0

  nums.forEach((num) => {
    if (num != val) {
      nums[slowIndex] = num
      slowIndex += 1
    }
  })

  return slowIndex
};
```

## C#
### Solution 1: Two pointers (easier to think of)
```c#
public class Solution
{
    public int RemoveElement(int[] nums, int val)
    {
        int left = 0;
        int right = nums.Length - 1;

        while (left <= right)
        {
            if (nums[left] != val)
            {
                left += 1;
                continue;
            }

            if (nums[right] == val)
            {
                right -= 1;
                continue;
            }

            nums[left] = nums[right];
            left += 1;
            right -= 1;
        }

        return left;
    }
}
```

### Solution 2: Fast and Slow Pointers (more concise and easier to code)
```c#
public class Solution
{
    public int RemoveElement(int[] nums, int val)
    {
        int slowIndex = 0;

        foreach (int num in nums)
        {
            if (num != val)
            {
                nums[slowIndex] = num;
                slowIndex += 1;
            }
        }

        return slowIndex;
    }
}
```

## Go
### Solution 1: Two pointers (easier to think of)
```go
func removeElement(nums []int, val int) int {
    left := 0
    right := len(nums) - 1

    for left <= right {
        if nums[left] != val {
            left += 1
            continue
        }

        if nums[right] == val {
            right -= 1
            continue
        }

        nums[left] = nums[right]
        left++
        right--
    }

    return left
}
```

### Solution 2: Fast and Slow Pointers (more concise and easier to code)
```go
func removeElement(nums []int, val int) int {
    slowIndex := 0

    for _, num := range nums {
        if num != val {
            nums[slowIndex] = num
            slowIndex += 1
        }
    }

    return slowIndex
}
```

## Ruby
### Solution 1: Two pointers (easier to think of)
```ruby
def remove_element(nums, val)
  left = 0
  right = nums.size - 1

  while left <= right
    if nums[left] != val
      left += 1
      next
    end

    if (nums[right] == val)
      right -= 1
      next
    end

    nums[left] = nums[right]
    left += 1
    right -= 1
  end

  left
end
```

### Solution 2: Fast and Slow Pointers (more concise and easier to code)
```ruby
def remove_element(nums, val)
  slow_index = 0

  nums.each do |num|
    if num != val
      nums[slow_index] = num
      slow_index += 1
    end
  end

  slow_index
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
