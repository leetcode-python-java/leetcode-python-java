# 704. 二分查找 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

访问原文链接：[704. 二分查找 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/704-binary-search)，体验更佳！

力扣链接：[704. 二分查找](https://leetcode.cn/problems/binary-search), 难度等级：**简单**。

## LeetCode “704. 二分查找”问题描述

给定一个 `n` 个元素有序的（升序）整型数组 `nums` 和一个目标值 `target`  ，写一个函数搜索 `nums` 中的 `target`，如果目标值存在返回下标，否则返回 `-1`。

### [示例 1]

**输入**: `nums = [-1,0,3,5,9,12], target = 9`

**输出**: `4`

**解释**: `9 出现在 `nums` 中并且下标为 4`

### [示例 2]

**输入**: `nums = [-1,0,3,5,9,12], target = 2`

**输出**: `-1`

**解释**: `2 不存在 `nums` 中因此返回 -1`

### [约束]

- 你可以假设 `nums` 中的所有元素是不重复的。
- `n` 将在 `[1, 10000]` 之间。
- `nums` 的每个元素都将在 `[-9999, 9999]` 之间。

## 思路

因为是已经排好序的数组，所以用中间的值进行比较，每次都可以排除掉一半的数字。

## 步骤

最快、最简单的方法是使用三个索引：`left`、`right` 和 `middle`。
如果 `nums[middle] > target`，则 `right = middle - 1`，否则 `left = middle + 1`。

## 复杂度

- 时间复杂度: `O(log N)`.
- 空间复杂度: `O(1)`.

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

```csharp
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

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.blog](https://leetcode.blog/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[704. 二分查找 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/704-binary-search).

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

