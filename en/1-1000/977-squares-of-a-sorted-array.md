# 977. Squares of a Sorted Array - Best Practices of LeetCode Solutions
LeetCode link: [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array)

## LeetCode problem description
Given an integer array `nums` sorted in **non-decreasing** order, return *an array of* ***the squares of each number*** *sorted in non-decreasing order.*

### Example 1
```ruby
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
```

### Example 2
```ruby
Input: nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]
```

### Constraints
- `1 <= nums.length <= 10000`
- `10000 <= nums[i] <= 10000`
- `nums` is sorted in **non-decreasing** order.

**Follow up**: Squaring each element and sorting the new array is very trivial, could you find an `O(n)` solution using a different approach?

## Intuition
### Solution 1: using `sort()`
* Square each number in the array.
* Sort the new array.

### Solution 2: not using `sort()` (important)
* The smallest number in the array is located inside the array, and you need to traverse to find it.
* But if you think in reverse and give priority to the certain ones, the program will become simple.
* The largest number in the array is located at the two ends. So, deal with the largest number first.

## Complexity
### Solution 1: using `sort()`
* Time: `O(n * log n)`.
* Space: `O(n)`.

### Solution 2: not using `sort()`
* Time: `O(n)`.
* Space: `O(n)`.

## Java
### Solution 1: using `sort()`
```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        for (var i = 0; i < nums.length; i++) {
            nums[i] *= nums[i];
        }

        Arrays.sort(nums);

        return nums;
    }
}
```

### Solution 2: not using `sort()`
```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        var results = new int[nums.length];
        var left = 0;
        var right = nums.length - 1;
        var index = right;

        while (left <= right) {
            if (Math.abs(nums[left]) <= nums[right]) {
                results[index] = nums[right] * nums[right];
                right -= 1;
            } else {
                results[index] = nums[left] * nums[left];
                left += 1;
            }

            index -= 1;
        }

        return results;
    }
}
```

## Python
### Solution 1: using `sort()`
```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        results = [num ** 2 for num in nums]

        results.sort()

        return results
```

### Solution 2: not using `sort()`
```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        results = [None] * len(nums)
        left = 0
        right = index = len(nums) - 1

        while left <= right:
            if abs(nums[left]) <= nums[right]:
                results[index] = nums[right] ** 2
                right -= 1
            else:
                results[index] = nums[left] ** 2
                left += 1

            index -= 1

        return results
```

## C++
### Solution 1: using `sort()`
```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        for (auto i = 0; i < nums.size(); i++) {
            nums[i] *= nums[i];
        }

        sort(nums.begin(), nums.end());

        return nums;
    }
};
```

### Solution 2: not using `sort()`
```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        auto results = vector<int>(nums.size());
        auto left = 0;
        int right = nums.size() - 1;  // Should not use 'auto' here because 'auto' will make this variable become `unsigned long` which has no `-1`.
        auto index = right;

        while (left <= right) {
            if (abs(nums[left]) <= nums[right]) {
                results[index] = nums[right] * nums[right];
                right -= 1;
            } else {
                results[index] = nums[left] * nums[left];
                left += 1;
            }

            index -= 1;
        }

        return results;
    }
};
```

## JavaScript
### Solution 1: using `sort()`
```javascript
var sortedSquares = function (nums) {
  return _.sortBy(
    nums.map((num) => num * num)
  )
};
```

### Solution 2: not using `sort()`
```javascript
var sortedSquares = function (nums) {
  const results = Array(nums.length).fill(null)
  let left = 0
  let right = nums.length - 1
  let index = right

  while (left <= right) {
    if (Math.abs(nums[left]) <= nums[right]) {
      results[index] = nums[right] * nums[right]
      right -= 1
    } else {
      results[index] = nums[left] * nums[left]
      left += 1
    }

    index -= 1
  }

  return results
};
```

## C#
### Solution 1: using `sort()`
```c#
public class Solution
{
    public int[] SortedSquares(int[] nums)
    {
        for (int i = 0; i < nums.Length; i++)
            nums[i] *= nums[i];

        Array.Sort(nums);

        return nums;
    }
}
```

### Solution 2: not using `sort()`
```c#
public class Solution
{
    public int[] SortedSquares(int[] nums)
    {
        var results = new int[nums.Length];
        int left = 0;
        int right = nums.Length - 1;
        int index = right;

        while (left <= right)
        {
            if (Math.Abs(nums[left]) <= nums[right])
            {
                results[index] = nums[right] * nums[right];
                right -= 1;
            }
            else
            {
                results[index] = nums[left] * nums[left];
                left += 1;
            }

            index -= 1;
        }

        return results;
    }
}
```

## Go
### Solution 1: using `sort()`
```go
func sortedSquares(nums []int) []int {
    for i, _ := range nums {
        nums[i] *= nums[i]
    }

    sort.Sort(sort.IntSlice(nums))

    return nums
}
```

### Solution 2: not using `sort()`
```go
func sortedSquares(nums []int) []int {
    results := make([]int, len(nums))
    left := 0
    right := len(nums) - 1
    index := right

    for left <= right {
        if math.Abs(float64(nums[left])) <= float64(nums[right]) {
            results[index] = nums[right] * nums[right]
            right -= 1
        } else {
            results[index] = nums[left] * nums[left]
            left += 1
        }

        index -= 1
    }

    return results
}
```

## Ruby
### Solution 1: using `sort()`
```ruby
def sorted_squares(nums)
  nums.map { |num| num ** 2 }.sort
end
```

### Solution 2: not using `sort()`
```ruby
def sorted_squares(nums)
  results = Array.new(nums.length)
  left = 0
  right = nums.size - 1
  index = right

  while left <= right
    if nums[left].abs <= nums[right]
      results[index] = nums[right] * nums[right]
      right -= 1
    else
      results[index] = nums[left] * nums[left]
      left += 1
    end

    index -= 1
  end

  results
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
