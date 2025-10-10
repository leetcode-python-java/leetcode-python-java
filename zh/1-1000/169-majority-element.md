# 169. 多数元素 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

访问原文链接：[169. 多数元素 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/169-majority-element)，体验更佳！

力扣链接：[169. 多数元素](https://leetcode.cn/problems/majority-element), 难度等级：**简单**。

## LeetCode “169. 多数元素”问题描述

给定一个大小为 `n` 的数组 `nums` ，返回其中的多数元素。多数元素是指在数组中出现次数 **大于** `⌊ n/2 ⌋` 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

### [示例 1]

**输入**: `nums = [3,2,3]`

**输出**: `3`

### [示例 2]

**输入**: `nums = [2,2,1,1,1,2,2]`

**输出**: `2`

### [约束]

- `n == nums.length`
- `1 <= n <= 5 * 10^4`
- `-10^9 <= nums[i] <= 10^9`

**进阶**：尝试设计时间复杂度为 O(n)、空间复杂度为 O(1) 的算法解决此问题。

### [Hints]

<details>
  <summary>提示 1</summary>
  How to solve the problem in `O(1)` space?

Please search `Boyer-Moore majority vote algorithm`.

  
</details>

## 思路

解决本题的关键是用一个 Hash Table 来保存 num 对应的出现次数。key 是 num，value 是 出现次数。

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(N)`.

## Python

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        num_to_count = defaultdict(int)

        for num in nums:
            num_to_count[num] += 1
            if num_to_count[num] >= len(nums) / 2:
                return num

```

## Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer}
def majority_element(nums)
  num_to_count = Hash.new(0)

  nums.each do |num|
    num_to_count[num] += 1

    if num_to_count[num] > nums.size / 2
      return num
    end
  end
end
```

## Java

```java
class Solution {
    public int majorityElement(int[] nums) {
        Map<Integer, Integer> numToCount = new HashMap<>();

        for (int num : nums) {
            numToCount.put(num, numToCount.getOrDefault(num, 0) + 1);

            if (numToCount.get(num) > nums.length / 2) {
                return num;
            }
        }

        return -1; // This line won't be reached due to problem constraints
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.blog](https://leetcode.blog/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[169. 多数元素 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/169-majority-element).

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

