# 977. Squares of a Sorted Array - LeetCode solutions in Python/Java/C++ and more

Visit original link: [977. Squares of a Sorted Array - LeetCode solutions in Python/Java/C++ and more](https://leetcodepython.com/en/leetcode/977-squares-of-a-sorted-array) for a better experience!

LeetCode link: [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array), difficulty: **Easy**.

## LeetCode description of "977. Squares of a Sorted Array"

Given an integer array `nums` sorted in **non-decreasing** order, return *an array of* ***the squares of each number*** *sorted in non-decreasing order.*

**Follow up**: Squaring each element and sorting the new array is very trivial, could you find an `O(n)` solution using a different approach?

### [Example 1]

**Input**: `nums = [-4,-1,0,3,10]`

**Output**: `[0,1,9,16,100]`

**Explanation**: 

<p>After squaring, the array becomes [16,1,0,9,100].<br>
After sorting, it becomes [0,1,9,16,100].</p>


### [Example 2]

**Input**: `nums = [-7,-3,2,3,11]`

**Output**: `[4,9,9,49,121]`

### [Constraints]

- `1 <= nums.length <= 10000`
- `10000 <= nums[i] <= 10000`
- `nums` is sorted in **non-decreasing** order.

## Intuition 1

- The smallest number in the array is inside the array, and it needs to be traversed to find it, which is not very convenient.
- But if we think in reverse, can we prioritize other numbers more conveniently? So which numbers should be prioritized?

    <details><summary>Click to view the answer</summary><p>The answer is to prioritize the numbers at **both ends** of the array because they are the largest. </p></details>

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(N)`.

## Java

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

```csharp
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

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## Intuition 2



## Complexity

- Time complexity: `O(N * log N)`.
- Space complexity: `O(N)`.

## Java

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

## Python

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        results = [num ** 2 for num in nums]

        results.sort()

        return results
```

## C++

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

## JavaScript

```javascript
var sortedSquares = function (nums) {
  return _.sortBy(
    nums.map((num) => num * num)
  )
};
```

## C#

```csharp
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

## Go

```go
func sortedSquares(nums []int) []int {
    for i, _ := range nums {
        nums[i] *= nums[i]
    }

    sort.Sort(sort.IntSlice(nums))

    return nums
}
```

## Ruby

```ruby
def sorted_squares(nums)
  nums.map { |num| num ** 2 }.sort
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCodePython.com](https://leetcodepython.com): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [977. Squares of a Sorted Array - LeetCode solutions in Python/Java/C++ and more](https://leetcodepython.com/en/leetcode/977-squares-of-a-sorted-array).

GitHub repository: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

