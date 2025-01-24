# 1. Two Sum - Best Practices of LeetCode Solutions
LeetCode link: [1. Two Sum](https://leetcode.com/problems/two-sum), difficulty: **Easy**

## Description of "1. Two Sum"
Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.

You may assume that each input would have **_exactly_ one solution**, and you may not use the same element twice.

You can return the answer in any order.

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

### [Hints]
<details>
  <summary>Hint 1</summary>
A really brute force way would be to search for all possible pairs of numbers but that would be too slow. Again, it's best to try out brute force solutions for just for completeness. It is from these brute force solutions that you can come up with optimizations.
</details>

<details>
  <summary>Hint 2</summary>
So, if we fix one of the numbers, say `x`, we have to scan the entire array to find the next number `y` which is `value - x` where value is the input parameter. Can we change our array somehow so that this search becomes faster?
</details>

<details>
  <summary>Hint 3</summary>
The second train of thought is, without changing the array, can we use additional space somehow? Like maybe a hash map to speed up the search?
</details>

## Intuition
1. The time complexity of the brute force solution is `O(n**2)`. To improve efficiency, you can sort the array, and then use **two pointers**, one pointing to the head of the array and the other pointing to the tail of the array, and decide `left += 1` or `right -= 1` according to the comparison of `sum` and `target`.
2. After finding the two values which `sum` is `target`, you can use the `index()` method to find the `index` corresponding to the value.

### Complexity
* Time: `O(N * log N)`.
* Space: `O(N)`.

## Solution 2: Use Map (also should master)
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
### Solution 1: Two pointers
```java
// Welcome to create a PR to complete the code, thanks!
```

### Solution 2: Using Map
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

## C++
### Solution 1: Two pointers
```cpp
// Welcome to create a PR to complete the code, thanks!
```

### Solution 2: Using Map
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
### Solution 1: Two pointers
```javascript
// Welcome to create a PR to complete the code, thanks!
```

### Solution 2: Using Map
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
### Solution 1: Two pointers
```c#
// Welcome to create a PR to complete the code, thanks!
```

### Solution 2: Using Map
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
### Solution 1: Two pointers
```go
// Welcome to create a PR to complete the code, thanks!
```

### Solution 2: Using Map
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
### Solution 1: Two pointers
```ruby
# Welcome to create a PR to complete the code, thanks!
```

### Solution 2: Using Map
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

## C, Kotlin, Swift, Rust or other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
