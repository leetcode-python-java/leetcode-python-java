# 209. 长度最小的子数组 - 力扣题解最佳实践

访问 原文链接：[209. 长度最小的子数组 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/209-minimum-size-subarray-sum) 体验更佳！

GitHub 仓库: [fuck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

力扣链接：[209. 长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum), 难度：**中等**。

## 力扣“209. 长度最小的子数组”问题描述

给定一个含有 `n` 个正整数的数组和一个正整数 `target` 。

找出该数组中满足其总和大于等于 `target` 的长度**最小的** **子数组** `[numsl, numsl+1, ..., numsr-1, numsr]` ，并返回*其长度*。如果不存在符合条件的子数组，返回 `0` 。

> **子数组** 是数组中连续的 **非空** 元素序列。

### [示例 1]

**输入**: `target = 7, nums = [2,3,1,2,4,3]`

**输出**: `2`

**解释**: `子数组 [4,3] 是该条件下的长度最小的子数组。`

### [示例 2]

**输入**: `target = 4, nums = [1,4,4]`

**输出**: `1`

**解释**: `target = 11, nums = [1,1,1,1,1,1,1,1]`

### [示例 3]

**输入**: `target = 11, nums = [1,1,1,1,1,1,1,1]`

**输出**: `0`

### [约束]

- `1 <= target <= 10^9`
- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^4`

## 思路

1. 对于**子数组**问题，可以考虑使用**滑动窗口技术**，它类似于**快慢双指针方法**。

## 步骤

1. **遍历** `nums` 数组，元素的 `index` 可命名为 `fastIndex`。虽然不起眼，但这是 `快慢指针技术` **最重要**的逻辑。请最好记住它。

2. `sum += nums[fast_index]`.

    ```java
    var minLength = Integer.MAX_VALUE;
    var sum = 0;
    var slowIndex = 0;
	
    for (var fastIndex = 0; fastIndex < nums.length; fastIndex++) { // 本行是`快慢指针技术`最重要的逻辑
        sum += nums[fastIndex]; // 1
    }
	
    return minLength;
    ```

3. 控制`slowIndex`。

	```java
	var minLength = Integer.MAX_VALUE;
	var sum = 0;
	var slowIndex = 0;
	
	for (var fastIndex = 0; fastIndex < nums.length; fastIndex++) {
	    sum += nums[fastIndex];
	
	    while (sum >= target) { // 1
	        minLength = Math.min(minLength, fastIndex - slowIndex + 1); // 2
	        sum -= nums[slowIndex]; // 3
	        slowIndex++; // 4
	    }
	}
	
	if (minLength == Integer.MAX_VALUE) { // 5
	    return 0; // 6
	}
	
	return minLength;
	```

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Java

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        var minLength = Integer.MAX_VALUE;
        var sum = 0;
        var slowIndex = 0;

        for (var fastIndex = 0; fastIndex < nums.length; fastIndex++) { // This line is the most important. You'd better memorize it.
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

        for fast_index, num in enumerate(nums): # This line is the most important. You'd better memorize it.
            sum_ += num

            while sum_ >= target:
                min_length = min(min_length, fast_index - slow_index + 1)
                sum_ -= nums[slow_index]
                slow_index += 1

        if min_length == float('inf'):
            return 0

        return min_length
```

## JavaScript

```javascript
var minSubArrayLen = function (target, nums) {
  let minLength = Number.MAX_SAFE_INTEGER
  let sum = 0
  let slowIndex = 0

  nums.forEach((num, fastIndex) => { // This line is the most important. You'd better memorize it.
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

```csharp
public class Solution
{
    public int MinSubArrayLen(int target, int[] nums)
    {
        int minLength = Int32.MaxValue;
        int sum = 0;
        int slowIndex = 0;

        for (int fastIndex = 0; fastIndex < nums.Length; fastIndex++) // This line is the most important. You'd better memorize it.
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
func minSubArrayLen(target int, nums []int) int {
    minLength := math.MaxInt32
    sum := 0
    slowIndex := 0

    for fastIndex := 0; fastIndex < len(nums); fastIndex++ { // This line is the most important. You'd better memorize it.
        sum += nums[fastIndex]

        for sum >= target {
            minLength = min(minLength, fastIndex - slowIndex + 1)
            sum -= nums[slowIndex]
            slowIndex++
        }
    }

    if minLength == math.MaxInt32 {
        return 0
    }

    return minLength
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
```

## Ruby

```ruby
# @param {Integer} target
# @param {Integer[]} nums
# @return {Integer}
def min_sub_array_len(target, nums)
  min_length = Float::INFINITY
  sum = 0
  slow_index = 0

  nums.each_with_index do |num, fast_index| # This line is the most important. You'd better memorize it.
    sum += num

    while sum >= target
      min_length = [min_length, fast_index - slow_index + 1].min
      sum -= nums[slow_index]
      slow_index += 1
    end
  end

  min_length == Float::INFINITY ? 0 : min_length
end
```

## C++

```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int min_length = INT_MAX;
        int sum = 0;
        int slow_index = 0;
        
        for (int fast_index = 0; fast_index < nums.size(); fast_index++) {
            sum += nums[fast_index];
            
            while (sum >= target) {
                min_length = min(min_length, fast_index - slow_index + 1);
                sum -= nums[slow_index];
                slow_index++;
            }
        }
        
        if (min_length == INT_MAX) {
            return 0;
        }
        
        return min_length;
    }
};
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [leetcoder.net](https://leetcoder.net)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[209. 长度最小的子数组 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/209-minimum-size-subarray-sum).

GitHub 仓库: [fuck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).
