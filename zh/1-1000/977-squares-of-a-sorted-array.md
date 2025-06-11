# 977. 有序数组的平方 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

访问原文链接：[977. 有序数组的平方 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.to/zh/leetcode/977-squares-of-a-sorted-array)，体验更佳！

力扣链接：[977. 有序数组的平方](https://leetcode.cn/problems/squares-of-a-sorted-array), 难度等级：**简单**。

## LeetCode “977. 有序数组的平方”问题描述

给你一个按 **非递减顺序** 排序的整数数组 `nums`，返回 **每个数字的平方** 组成的新数组，要求也按 **非递减顺序** 排序。

**进阶**：请你设计时间复杂度为 O(n) 的算法解决本问题。

### [示例 1]

**输入**: `nums = [-4,-1,0,3,10]`

**输出**: `[0,1,9,16,100]`

**解释**: 

<p>平方后，数组变为 [16,1,0,9,100]<br>
排序后，数组变为 [0,1,9,16,100]</p>


### [示例 2]

**输入**: `nums = [-7,-3,2,3,11]`

**输出**: `[4,9,9,49,121]`

### [约束]

- `1 <= nums.length <= 10^4`
- `-10^4 <= nums[i] <= 10^4`
- `nums` 已按 **非递减顺序** 排序

## 思路 1

- 数组中最小的数位于数组内部，需要遍历才能找到，不太方便。
- 但如果反向思考，能否更加方便地优先处理另外一些数呢？那么优先处理哪些数呢？

    <details><summary>点击查看答案</summary><p>答案是优先处理数组**两端**的数，因为它们最大。</p></details>

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(N)`.

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

## 思路 2



## 复杂度

- 时间复杂度: `O(N * log N)`.
- 空间复杂度: `O(N)`.

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

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.to](https://leetcode.to/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[977. 有序数组的平方 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.to/zh/leetcode/977-squares-of-a-sorted-array).

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

