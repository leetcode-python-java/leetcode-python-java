Original link: [leetcoder.net - LeetCoder: Fucking Good LeetCode Solutions](https://leetcoder.net/en/leetcode/303-range-sum-query-immutable)

# 303. Range Sum Query - Immutable - LeetCoder: Fucking Good LeetCode Solutions

LeetCode link: [303. Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable), difficulty: **Easy**.

## LeetCode description of "303. Range Sum Query - Immutable"

Given an integer array `nums`, handle multiple queries of the following type:

1. Calculate the sum of the elements of `nums` between indices `left` and `right` inclusive where `left <= right`.

Implement the `NumArray` class:

- `NumArray(int[] nums)` Initializes the object with the integer array `nums`.
- `int sumRange(int left, int right)` Returns the **sum** of the elements of `nums` between indices `left` and `right` **inclusive** (i.e. `nums[left] + nums[left + 1] + ... + nums[right]`).

### [Example 1]

**Input**: `["NumArray", "sumRange", "sumRange", "sumRange"] [[[-2, 0, 3, -5, 2, -1]], [0, 2], [2, 5], [0, 5]]`

**Output**: `[null, 1, -1, -3]`

**Explanation**: 

NumArray numArray = new NumArray([-2, 0, 3, -5, 2, -1]);
numArray.sumRange(0, 2); // return (-2) + 0 + 3 = 1
numArray.sumRange(2, 5); // return 3 + (-5) + 2 + (-1) = -1
numArray.sumRange(0, 5); // return (-2) + 0 + 3 + (-5) + 2 + (-1) = -3

### [Constraints]

- `1 <= nums.length <= 10^4`
- `-10^5 <= nums[i] <= 10^5`
- `0 <= left <= right < nums.length`
- At most `10^4` calls will be made to `sumRange`.

## Intuition 1

- Use a new array `prefix_sums` to save the sum of the previous elements.
- The first element of `prefix_sums` is `0` because the prefix sum **does not include the current element**.
- To find the `sum` of the elements from index `left` to `right` (inclusive), just use `prefix_sums[right + 1] - prefix_sums[left]`.

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(N)`.

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

## Intuition 2

Directly returning the sum of the values ​​in the array range can pass the test, but it will fail if the test case is stricter.
So we still need to learn a more efficient solution: `Prefix Sum` solution.

## Complexity

- Time complexity: `O(M * N)`.
- Space complexity: `O(M * N)`.

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

