Visit 原文链接：[leetcoder.net - 力扣题解最佳实践 - 力扣人](https://leetcoder.net/zh/leetcode/303-range-sum-query-immutable) for a better experience!

GitHub repo: [fuck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

# 303. 区域和检索 - 数组不可变 - 力扣题解最佳实践 - 力扣人

力扣链接：[303. 区域和检索 - 数组不可变](https://leetcode.cn/problems/range-sum-query-immutable), 难度：**简单**。

## 力扣“303. 区域和检索 - 数组不可变”问题描述

给定一个整数数组  `nums`，处理以下类型的多个查询:

计算索引 `left` 和 `right` （包含 `left` 和 `right`）之间的 `nums` 元素的 **和** ，其中 `left <= right`
实现 `NumArray` 类：

- `NumArray(int[] nums)` 使用数组 `nums` 初始化对象
- `int sumRange(int i, int j)` 返回数组 `nums` 中索引 `left` 和 `right` 之间的元素的 **总和** ，包含 `left` 和 `right` 两点（也就是 `nums[left] + nums[left + 1] + ... + nums[right]` )

### [示例 1]

**输入**: `["NumArray", "sumRange", "sumRange", "sumRange"] [[[-2, 0, 3, -5, 2, -1]], [0, 2], [2, 5], [0, 5]]`

**输出**: `[null, 1, -1, -3]`

**解释**: 

<p>NumArray numArray = new NumArray([-2, 0, 3, -5, 2, -1]);<br>
numArray.sumRange(0, 2); // return (-2) + 0 + 3 = 1<br>
numArray.sumRange(2, 5); // return 3 + (-5) + 2 + (-1) = -1<br>
numArray.sumRange(0, 5); // return (-2) + 0 + 3 + (-5) + 2 + (-1) = -3</p>


### [约束]

- `1 <= nums.length <= 10^4`
- `-10^5 <= nums[i] <= 10^5`
- `0 <= left <= right < nums.length`
- 最多调用 `10^4` 次 `sumRange` 方法

## 思路 1

- 使用新数组 `prefix_sums` 保存前面元素的总和。
- `prefix_sums` 的第一个元素为 `0`，因为前缀和 **不包含当前元素**。
- 要查找从索引 `left` 到 `right`（含）元素的总和，只需使用 `prefix_sums[right + 1] - prefix_sums[left]`。

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(N)`.

## Java

```java
class NumArray {
    private int[] prefixSums;

    public NumArray(int[] nums) {
        prefixSums = new int[nums.length + 1];
        var sum = 0;

        for (var i = 0; i < nums.length; i++) {
            sum += nums[i];
            prefixSums[i + 1] = sum;
        }
    }

    public int sumRange(int left, int right) {
        return prefixSums[right + 1] - prefixSums[left];
    }
}
```

## Python

```python
class NumArray:
    def __init__(self, nums: List[int]):
        self.prefix_sums = [0]
        sum_ = 0

        for num in nums:
            sum_ += num
            self.prefix_sums.append(sum_)

    def sumRange(self, left: int, right: int) -> int:
        return self.prefix_sums[right + 1] - self.prefix_sums[left]
```

## C++

```cpp
class NumArray {
private:
    vector<int> prefixSums;

public:
    NumArray(vector<int>& nums) {
        prefixSums.push_back(0);
        auto sum = 0;

        for (auto num : nums) {
            sum += num;
            prefixSums.push_back(sum);
        }
    }
    
    int sumRange(int left, int right) {
        return prefixSums[right + 1] - prefixSums[left];
    }
};
```

## JavaScript

```javascript
let prefixSums

var NumArray = function (nums) {
  prefixSums = [0]
  let sum = 0

  nums.forEach((num) => {
    sum += num
    prefixSums.push(sum)
  })
};

NumArray.prototype.sumRange = function (left, right) {
  return prefixSums[right + 1] - prefixSums[left]
};
```

## C#

```csharp
public class NumArray
{
    int[] prefixSums;

    public NumArray(int[] nums)
    {
        prefixSums = new int[nums.Length + 1];
        int sum = 0;

        for (int i = 0; i < nums.Length; i++)
        {
            sum += nums[i];
            prefixSums[i + 1] = sum;
        }
    }
    
    public int SumRange(int left, int right)
    {
        return prefixSums[right + 1] - prefixSums[left];
    }
}
```

## Go

```go
type NumArray struct {
    prefixSums []int
}

func Constructor(nums []int) NumArray {
    prefixSums := make([]int, len(nums) + 1)
    sum := 0

    for i, num := range nums {
        sum += num
        prefixSums[i + 1] = sum
    }

    return NumArray{prefixSums}
}

func (this *NumArray) SumRange(left int, right int) int {
    return this.prefixSums[right + 1] - this.prefixSums[left]
}
```

## Ruby

```ruby
class NumArray
  def initialize(nums)
    @prefix_sums = [0]
    sum = 0

    nums.each do |num|
      sum += num
      @prefix_sums << sum
    end
  end

  def sum_range(left, right)
    @prefix_sums[right + 1] - @prefix_sums[left]
  end
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## 思路 2

直接返回数组区域内值之和，虽然可以通过测试，但是如果测试用例更严格的话就会失败。
所以我们还需要学习一种更有效的解决方案：`前缀和`方案。

## 复杂度

- 时间复杂度: `O(M * N)`.
- 空间复杂度: `O(M * N)`.

## Python

```python
class NumArray:
    def __init__(self, nums: List[int]):
        self.nums = nums

    def sumRange(self, left: int, right: int) -> int:
        return sum(self.nums[left:right + 1])
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [leetcoder.net](https://leetcoder.net): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

原文链接：[leetcoder.net - 力扣题解最佳实践 - 力扣人](https://leetcoder.net/zh/leetcode/303-range-sum-query-immutable).

GitHub repo: [fuck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).
