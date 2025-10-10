# 27. Remove Element - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

Visit original link: [27. Remove Element - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/27-remove-element) for a better experience!

LeetCode link: [27. Remove Element](https://leetcode.com/problems/remove-element), difficulty: **Easy**.

## LeetCode description of "27. Remove Element"

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` [in-place](https://en.wikipedia.org/wiki/In-place_algorithm). The order of the elements may be changed. Then return *the number of elements in `nums` which are not equal to `val`*.

Consider the number of elements in `nums` which are not equal to `val` be `k`, to get accepted, you need to do the following things:

- Change the array `nums` such that the first `k` elements of `nums` contain the elements which are not equal to `val`. The remaining elements of `nums` are not important as well as the size of `nums`.
- Return `k`.

### [Example 1]

**Input**: `nums = [3,2,2,3], val = 3`

**Output**: `2, nums = [2,2,_,_]`

**Explanation**: 

<p>Your function should return k = 2, with the first two elements of nums being 2.<br>
It does not matter what you leave beyond the returned k (hence they are underscores).</p>


### [Example 2]

**Input**: `nums = [0,1,2,2,3,0,4,2], val = 2`

**Output**: `5, nums = [0,1,4,0,3,_,_,_]`

**Explanation**: 

<p>Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.<br>
Note that the five elements can be returned in any order.<br>
It does not matter what you leave beyond the returned k (hence they are underscores).</p>


### [Constraints]

- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`

### [Hints]

<details>
  <summary>Hint 1</summary>
  The problem statement clearly asks us to modify the array in-place and it also says that the element beyond the new length of the array can be anything. Given an element, we need to remove all the occurrences of it from the array. We don't technically need to **remove** that element per-say, right?

  
</details>

<details>
  <summary>Hint 2</summary>
  We can move all the occurrences of this element to the end of the array. Use two pointers!

  ![](../../images/hints/27_2.png)
</details>

<details>
  <summary>Hint 3</summary>
  Yet another direction of thought is to consider the elements to be removed as non-existent. In a single pass, if we keep copying the visible elements in-place, that should also solve this problem for us.

  
</details>

## Intuition 1

- `Two pointers`, one on the left and one on the right. The left one points to the head of the array, and the right one points to the tail of the array.
- If the value pointed by the left pointer is found to be equal to **val**, and the value pointed by the right pointer is not equal to *val*, then swap the two the values.
- This method is easy to think of, but the amount of code is more than the `fast and slow pointers`.

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Java

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

## Python

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

## C++

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

## JavaScript

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

## C#

```csharp
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

## Go

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

## Ruby

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

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## Intuition 2

- The `fast and slow pointer approach` means that both pointers initially point to the head of the array, and then one pointer moves faster.
- For this question, under what circumstances should the fast pointer move faster? When the value corresponding to the fast pointer is equal to *val*. The slow pointer must ensure that each value it passes through is not equal to *val*.
- The swap of values ​​occurs when the value pointed by the fast pointer is not equal to *val*, and the value pointed by the slow pointer is equal to *val*.
- This method is not easy to think of, but it is more concise than `two pointers of left and right`.

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Java

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        var slowIndex = 0;

        for (var num : nums) { // This line is the most important. You'd better memorize it.
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

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        slow_index = 0

        for num in nums: # This line is the most important. You'd better memorize it.
            if num != val:
                nums[slow_index] = num
                slow_index += 1

        return slow_index
```

## C++

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        auto slow_index = 0;

        for (auto num : nums) { // This line is the most important. You'd better memorize it.
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

```javascript
var removeElement = function (nums, val) {
  let slowIndex = 0

  nums.forEach((num) => { // This line is the most important. You'd better memorize it.
    if (num != val) {
      nums[slowIndex] = num
      slowIndex += 1
    }
  })

  return slowIndex
};
```

## C#

```csharp
public class Solution
{
    public int RemoveElement(int[] nums, int val)
    {
        int slowIndex = 0;

        foreach (int num in nums) // This line is the most important. You'd better memorize it.
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

```go
func removeElement(nums []int, val int) int {
    slowIndex := 0

    for _, num := range nums { // This line is the most important. You'd better memorize it.
        if num != val {
            nums[slowIndex] = num
            slowIndex += 1
        }
    }

    return slowIndex
}
```

## Ruby

```ruby
def remove_element(nums, val)
  slow_index = 0

  nums.each do |num| # This line is the most important. You'd better memorize it.
    if num != val
      nums[slow_index] = num
      slow_index += 1
    end
  end

  slow_index
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCode.blog](https://leetcode.blog): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [27. Remove Element - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/27-remove-element).

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).
