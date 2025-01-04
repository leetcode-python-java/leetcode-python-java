# 1. Two Sum - LeetCode Solution
LeetCode problem link: [1. Two Sum](https://leetcode.com/problems/two-sum),
[1. 两数之和](https://leetcode.cn/problems/two-sum)

[中文题解](#中文题解)

## LeetCode problem description
Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.

You may assume that each input would have **_exactly_ one solution**, and you may not use the same element twice.

You can return the answer in any order.

Difficulty: **Easy**

### [Example 1]
**Input**: `nums = [2,7,11,15], target = 9`

**Output**: `[0,1]`

**Explanation**： `Because nums[0] + nums[1] == 9, we return [0, 1].`

### [Example 2]
**Input**: `nums = [3,2,4], target = 6`

**Output**: `[1,2]`

### [Constraints]
- `2 <= nums.length <= 10**4`
- `-10**9 <= nums[i] <= 10**9`
- `-10**9 <= target <= 10**9`
- **Only one valid answer exists.**

## Solution 1
[中文题解](#中文题解)

1. The time complexity of the brute force solution is `O(n**2)`. To improve efficiency, you can sort the array, and then use **two pointers**, one pointing to the head of the array and the other pointing to the tail of the array, and decide `left += 1` or `right -= 1` according to the comparison of `sum` and `target`.
2. After finding the two values which `sum` is `target`, you can use the `index()` method to find the `index` corresponding to the value.

### Complexity
* Time: `O(N * log N)`.
* Space: `O(N)`.

## Solution 2
1. In `Map`, `key` is `num`, and `value` is array `index`.
2. Traverse the array, if `target - num` is in `Map`, return it. Otherwise, add `num` to `Map`.

### Steps
1. In `Map`, `key` is `num`, and `value` is array `index`.
```javascript
let numToIndex = new Map()

for (let i = 0; i < nums.length; i++) {
  numToIndex.set(nums[i], i)
}
```

2. Traverse the array, if `target - num` is in `Map`, return it. Otherwise, add `num` to `Map`.
```javascript
let numToIndex = new Map()

for (let i = 0; i < nums.length; i++) {
  if (numToIndex.has(target - nums[i])) { // 1
    return [numToIndex.get(target - nums[i]), i] // 2
  }

  numToIndex.set(nums[i], i)
}
```

### Complexity
* Time: `O(n)`.
* Space: `O(n)`.

## Java
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        var numToIndex = new HashMap<Integer, Integer>();
  
        for (var i = 0; i < nums.length; i++) {
            if (numToIndex.containsKey(target - nums[i])) {
                return new int[]{numToIndex.get(target - nums[i]), i};
            }

            numToIndex.put(nums[i], i);
        }

        return null;
    }
}
```

## Python
### Solution 2: Using Map
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_to_index = {}
        
        for i, num in enumerate(nums):
            if target - num in num_to_index:
                return [num_to_index[target - num], i]

            num_to_index[num] = i
```

### Solution 1: Two pointers
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        original_nums = nums.copy()
        nums.sort()

        left = 0
        right = len(nums) - 1

        while left < right:
            sum_ = nums[left] + nums[right]

            if sum_ == target:
                break

            if sum_ < target:
                left += 1
                continue

            right -= 1

        return [original_nums.index(nums[left]), len(nums) - 1 - original_nums[::-1].index(nums[right])]
```

## C++
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> num_to_index;
  
        for (auto i = 0; i < nums.size(); i++) {
            if (num_to_index.contains(target - nums[i])) {
                return {num_to_index[target - nums[i]], i};
            }

            num_to_index[nums[i]] = i;
        }

        return {};
    }
};
```

## JavaScript
```javascript
var twoSum = function (nums, target) {
  let numToIndex = new Map()
  
  for (let i = 0; i < nums.length; i++) {
    if (numToIndex.has(target - nums[i])) {
      return [numToIndex.get(target - nums[i]), i]
    }

    numToIndex.set(nums[i], i)
  }
};
```

## C#
```c#
public class Solution {
    public int[] TwoSum(int[] nums, int target) {
        var numToIndex = new Dictionary<int, int>();
  
        for (int i = 0; i < nums.Length; i++) {
            if (numToIndex.ContainsKey(target - nums[i])) {
                return [numToIndex[target - nums[i]], i];
            }

            numToIndex[nums[i]] = i;
        }

        return null;
    }
}
```

## Go
```go
func twoSum(nums []int, target int) []int {
    numToIndex := map[int]int{}

    for i, num := range nums {
        if index, ok := numToIndex[target - num]; ok {
            return []int{index, i}
        }

        numToIndex[num] = i
    }

    return nil
}
```

## Ruby
```ruby
def two_sum(nums, target)
  num_to_index = {}

  nums.each_with_index do |num, i|
    if num_to_index.key?(target - num)
      return [num_to_index[target - num], i]
    end

    num_to_index[num] = i
  end
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

## 问题描述
给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** `target`  的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案，并且你不能使用两次相同的元素。

你可以按任意顺序返回答案。

难度: **容易**

### [示例 1]
**输入**: `nums = [2,7,11,15], target = 9`

**输出**: `[0,1]`

**解释**: `Because nums[0] + nums[1] == 9, we return [0, 1].`

# 中文题解
## 思路1：双指针
1. 暴力解法的时间复杂度为`O(n**2)`，想提升效率，可以对数组进行排序，然后用双指针，一个指向数组头，一个指向数组尾，根据**和**情况决定`left += 1`还是`right -= 1`。
2. 找出了两个值后，需要用`index()`方法去找值对应的`index`。

## 思路2：使用Map提升查找一个值的效率
1. `Map`中，`key`是`num`，`value`是数组`index`。
2. 遍历数组，如果`target - num`在`Map`中，返回。反之，将`num`加入`Map`中。

### 步骤
1. `Map`中，`key`是`num`，`value`是数组`index`。
```javascript
let numToIndex = new Map()

for (let i = 0; i < nums.length; i++) {
  numToIndex.set(nums[i], i)
}
```

2. 遍历数组，如果`target - num`在`Map`中，返回。反之，将`num`加入`Map`中。
```javascript
let numToIndex = new Map()

for (let i = 0; i < nums.length; i++) {
  if (numToIndex.has(target - nums[i])) { // 1
    return [numToIndex.get(target - nums[i]), i] // 2
  }

  numToIndex.set(nums[i], i)
}
```
