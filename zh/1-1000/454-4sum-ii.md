原文链接：[leetcoder.net - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/454-4sum-ii)

# 454. 四数相加 II - 力扣题解最佳实践
力扣链接：[454. 四数相加 II](https://leetcode.cn/problems/4sum-ii) ，难度：**中等**。

## 力扣"454. 四数相加 II"问题描述
给你四个整数数组 `nums1`、`nums2`、`nums3` 和 `nums4` ，数组长度都是 `n` ，请你计算有多少个元组 `(i, j, k, l)` 能满足：

- `0 <= i, j, k, l < n`
- `nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0`

### [示例 1]
**输入**: `nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]`

**输出**: `2`

**解释**:
```
两个元组如下：
1. (0, 0, 0, 1) -> nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0
```

### [示例 2]
**输入**: `nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]`

**输出**: `1`

### [约束]
- `n == nums1.length`
- `n == nums2.length`
- `n == nums3.length`
- `n == nums4.length`
- `1 <= n <= 200`
- `-2^28 <= nums1[i], nums2[i], nums3[i], nums4[i] <= 2^28`

## 思路
1. 因为最终要求是每组数中各取一个数，所以可以把四组数拆分成两个两组数。
2. 统计出每个`和`值对应的个数。使用`Map`储存，`key`为`和`，`value`为`count`。
3. 遍历`nums3`和`nums4`，如果`-(num3 + num4)`存在于`Map`的`keys`中，则`count`计入总数。

## 步骤

1. 统计出每个`和`值对应的个数。使用`Map`储存，`key`为`和`，`value`为`count`。

	```python
	num_to_count = defaultdict(int)
	
	for num1 in nums1:
	    for num2 in nums2:
	        num_to_count[num1 + num2] += 1
	```

2. 遍历`nums3`和`nums4`，如果`-(num3 + num4)`存在于`Map`的`keys`中，则`count`计入总数。

	```python
	result = 0
	
	for num3 in nums3:
	    for num4 in nums4:
	        result += num_to_count[-(num3 + num4)]
	
	return result
	```

## 复杂度
* 时间: `O(n * n)`.
* 空间: `O(n)`.

## Java
```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        var numToCount = new HashMap<Integer, Integer>();

        for (var num1 : nums1) {
            for (var num2 : nums2) {
                numToCount.put(
                    num1 + num2,
                    numToCount.getOrDefault(num1 + num2, 0) + 1
                );
            }
        }

        var result = 0;

        for (var num3 : nums3) {
            for (var num4 : nums4) {
                result += numToCount.getOrDefault(-(num3 + num4), 0);
            }
        }

        return result;
    }
}
```

## Python
```python
# from collections import defaultdict

class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        num_to_count = defaultdict(int)

        for num1 in nums1:
            for num2 in nums2:
                num_to_count[num1 + num2] += 1

        result = 0

        for num3 in nums3:
            for num4 in nums4:
                result += num_to_count[-(num3 + num4)]

        return result
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
var fourSumCount = function (nums1, nums2, nums3, nums4) {
  const numToCount = new Map()

  for (const num1 of nums1) {
    for (const num2 of nums2) {
      numToCount.set(num1 + num2, (numToCount.get(num1 + num2) || 0) + 1)
    }
  }

  let result = 0

  for (const num3 of nums3) {
    for (const num4 of nums4) {
      result += numToCount.get(-(num3 + num4)) || 0
    }
  }

  return result
};
```

## C#
```c#
public class Solution
{
    public int FourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4)
    {
        var numToCount = new Dictionary<int, int>();

        foreach (int num1 in nums1)
        {
            foreach (int num2 in nums2)
            {
                numToCount[num1 + num2] = numToCount.GetValueOrDefault(num1 + num2, 0) + 1;
            }
        }

        int result = 0;

        foreach (int num3 in nums3)
        {
            foreach (int num4 in nums4)
            {
                result += numToCount.GetValueOrDefault(-(num3 + num4), 0);
            }
        }

        return result;
    }
}
```

## Go
```go
// Welcome to create a PR to complete the code of this language, thanks!
```

## Ruby
```ruby
def four_sum_count(nums1, nums2, nums3, nums4)
  num_to_count = Hash.new(0)

  nums1.each do |num1|
    nums2.each do |num2|
      num_to_count[num1 + num2] += 1
    end
  end

  result = 0

  nums3.each do |num3|
    nums4.each do |num4|
      result += num_to_count[-(num3 + num4)]
    end
  end

  result
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
