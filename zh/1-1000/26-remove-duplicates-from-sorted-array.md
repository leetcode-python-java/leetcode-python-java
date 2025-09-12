# 26. 删除有序数组中的重复项 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

访问原文链接：[26. 删除有序数组中的重复项 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.to/zh/leetcode/26-remove-duplicates-from-sorted-array)，体验更佳！

力扣链接：[26. 删除有序数组中的重复项](https://leetcode.cn/problems/remove-duplicates-from-sorted-array), 难度等级：**简单**。

## LeetCode “26. 删除有序数组中的重复项”问题描述

给你一个 **非严格递增排列** 的数组 `nums` ，请你 [原地](https://en.wikipedia.org/wiki/In-place_algorithm) 删除重复出现的元素，使每个元素 **只出现一次** ，返回删除后数组的新长度。元素的 **相对顺序** 应该保持 **一致** 。然后返回 `nums` 中唯一元素的个数。

考虑 `nums` 的唯一元素的数量为 `k` ，你需要做以下事情确保你的题解可以被通过：

- 更改数组 `nums` ，使 `nums` 的前 `k` 个元素包含唯一元素，并按照它们最初在 `nums` 中出现的顺序排列。`nums` 的其余元素与 `nums` 的大小不重要。
- 返回 `k` 。

### [示例 1]

**输入**: `nums = [1,1,2]`

**输出**: `2, nums = [1,2,_]`

**解释**: 

<p>函数应该返回新的长度 <code>2</code> ，并且原数组 <code>nums</code> 的前两个元素被修改为 <code>1, 2</code> 。不需要考虑数组中超出新长度后面的元素。</p>


### [示例 2]

**输入**: `nums = [0,0,1,1,1,2,2,3,3,4]`

**输出**: `5, nums = [0,1,2,3,4,_,_,_,_,_]`

**解释**: 

<p>函数应该返回新的长度 <code>5</code> ， 并且原数组 <code>nums</code> 的前五个元素被修改为 <code>0</code>, <code>1</code>, <code>2</code>, <code>3</code>, <code>4</code> 。不需要考虑数组中超出新长度后面的元素。</p>


### [约束]

- `1 <= nums.length <= 3 * 10^4`
- `-10^4 <= nums[i] <= 10^4`
- `nums` 已按 **非严格递增** 排列

### [Hints]

<details>
  <summary>提示 1</summary>
  In this problem, the key point to focus on is the input array being sorted. As far as duplicate elements are concerned, what is their positioning in the array when the given array is sorted? Look at the image below for the answer. If we know the position of one of the elements, do we also know the positioning of all the duplicate elements?

  
</details>

<details>
  <summary>提示 2</summary>
  We need to modify the array in-place and the size of the final array would potentially be smaller than the size of the input array. So, we ought to use a two-pointer approach here. One, that would keep track of the current element in the original array and another one for just the unique elements.

  
</details>

<details>
  <summary>提示 3</summary>
  Essentially, once an element is encountered, you simply need to **bypass** its duplicates and move on to the next unique element.


  
</details>

## 思路

本题数组中的数值是排好序的，所以重复的数值一定是连续出现的。
要去掉其中的重复的数值，那么每一个不同于前一个数值的数都需要保留，否则就不保留。
因为要原地修改数据，所以需要涉及两个指针，一个指针走得快，一个指针走得慢。
快指针每次位置自动加1，慢指针指向当前需要修改位置。

## “快慢指针技术”的模式

```java
int slow = 0; // slow pointer
// ...

for (int fast = 1; fast < array_length; fast++) { // 本行是关键!
    if (condition_1) {
        // ...
        continue; // 'continue' 比 'else' 好，因为 'else' 会引入更多的缩进空格！
    }

    if (condition_2) {
        // ...
        continue; // 'continue' 比 'else' 好
    }

    // condition_3
    // ...
    slow++;
    // ...
}

return something;
```

## 复杂度

- 时间复杂度: `N`.
- 空间复杂度: `1`.

## Python

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        slow = 1

        # nums = [0,0,1,1,1,2,2,3,3,4]
        for fast in range(1, len(nums)):
            if nums[fast] == nums[slow - 1]:
                continue

            nums[slow] = nums[fast]
            slow += 1

        return slow

```

## Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer}
def remove_duplicates(nums)
  slow = 1

  # nums = [0,0,1,1,1,2,2,3,3,4]
  (1...nums.size).each do |fast|
    if nums[fast] == nums[slow - 1]
      next
    end

    nums[slow] = nums[fast]
    slow += 1
  end

  slow
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.to](https://leetcode.to/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[26. 删除有序数组中的重复项 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.to/zh/leetcode/26-remove-duplicates-from-sorted-array).

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

