# 334. 递增的三元子序列 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

访问原文链接：[334. 递增的三元子序列 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.to/zh/leetcode/334-increasing-triplet-subsequence)，体验更佳！

力扣链接：[334. 递增的三元子序列](https://leetcode.cn/problems/increasing-triplet-subsequence), 难度等级：**中等**。

## LeetCode “334. 递增的三元子序列”问题描述

给你一个整数数组 `nums` ，判断这个数组中是否存在长度为 `3` 的递增子序列。

如果存在这样的三元组下标 `(i, j, k)` 且满足 `i < j < k` ，使得 `nums[i] < nums[j] < nums[k]` ，返回 `true` ；否则，返回 `false` 。

### [示例 1]

**输入**: `nums = [1,2,3,4,5]`

**输出**: `true`

**解释**: `任何 i < j < k 的三元组都满足题意`

### [示例 2]

**输入**: `nums = [5,4,3,2,1]`

**输出**: `false`

**解释**: `不存在满足题意的三元组`

### [示例 3]

**输入**: `nums = [2,1,5,0,4,6]`

**输出**: `true`

**解释**: 

<p>三元组 (3, 4, 5) 满足题意，因为 nums[3] == 0 &lt; nums[4] == 4 &lt; nums[5] == 6</p>


### [约束]

- `1 <= nums.length <= 5 * 10^5`
- `-2^31 <= nums[i] <= 2^31 - 1`

进阶：你能实现时间复杂度为 `O(n)` ，空间复杂度为 `O(1)` 的解决方案吗？

## 思路

要找到一个递增的三元子序列，我们可以追踪当前遇到的最小值和第二小的值。当遇到比这两个值都大的数时，就找到了满足条件的三元组。

## “贪心算法”的模式

“贪心算法”是在每一步中都采取当前状态下最优的决策，从而希望导致“全局最优”的算法策略。即“局部最优”能导致“全局最优”。

## 步骤

1. 初始化：将`first`设为数组第一个元素，`second`设为最大整数值
2. 从第二个元素开始遍历数组：
    - 如果当前数字 > `second`：找到三元组，直接返回`true`
    - 如果当前数字 > `first`：将`second`更新为当前数字
    - 否则：将`first`更新为当前数字（保持记录最小值）
3. 遍历结束后仍未找到则返回`false`

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

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

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.to](https://leetcode.to/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[334. 递增的三元子序列 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.to/zh/leetcode/334-increasing-triplet-subsequence).

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

