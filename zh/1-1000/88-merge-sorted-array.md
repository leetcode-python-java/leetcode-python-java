# 88. 合并两个有序数组 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

访问原文链接：[88. 合并两个有序数组 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/88-merge-sorted-array)，体验更佳！

力扣链接：[88. 合并两个有序数组](https://leetcode.cn/problems/merge-sorted-array), 难度等级：**简单**。

## LeetCode “88. 合并两个有序数组”问题描述

给你两个按 **非递减顺序** 排列的整数数组 `nums1` 和 `nums2`，另有两个整数 `m` 和 `n` ，分别表示 `nums1` 和 `nums2` 中的元素数目。

请你 **合并** `nums2` 到 `nums1` 中，使合并后的数组同样按 **非递减顺序** 排列。

注意：最终，合并后数组不应由函数返回，而是存储在数组 `nums1` 中。为了应对这种情况，`nums1` 的初始长度为 `m + n`，其中前 `m` 个元素表示应合并的元素，后 `n` 个元素为 `0` ，应忽略。`nums2` 的长度为 `n` 。

### [示例 1]

**输入**: `nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3`

**输出**: `[1,2,2,3,5,6]`

**解释**: 

<p>需要合并 [1,2,3] 和 [2,5,6] 。<br>
合并结果是 [1,2,2,3,5,6] ，其中斜体加粗标注的为 nums1 中的元素。</p>


### [示例 2]

**输入**: `nums1 = [1], m = 1, nums2 = [], n = 0`

**输出**: `[1]`

**解释**: `需要合并 [1] 和 [] 。
合并结果是 [1] 。`

### [示例 3]

**输入**: `nums1 = [0], m = 0, nums2 = [1], n = 1`

**输出**: `[1]`

**解释**: 

<p>需要合并的数组是 [] 和 [1] 。<br>
合并结果是 [1] 。<br>
注意，因为 m = 0 ，所以 nums1 中没有元素。nums1 中仅存的 0 仅仅是为了确保合并结果可以顺利存放到 nums1 中。</p>


### [约束]

- `nums1.length == m + n`
- `nums2.length == n`
- `0 <= m, n <= 200`
- `1 <= m + n <= 200`
- `-10^9 <= nums1[i], nums2[j] <= 10^9`

进阶：你可以设计实现一个时间复杂度为 O(m + n) 的算法解决此问题吗？

## 思路

- 这道题目可以用编程语言自带的 `sort()` 方法对数组进行排序，实现起来很简单。但这样的方式，时间复杂度是 `O(n log n)`。
- 所以本题一般会限制时间复杂度为 `O(n)` 。 如何做到 `O(n)` ? 
- 我们要看拥有的条件了。这两个数组都是已经排好序的，这个条件肯定要利用起来。
- 在重新组织数组的过程中，可以考虑从左向右把数按顺序安置好，也可以考虑从右向左把数安置好。该选哪个方向？
- 如果不问自己这个问题，一般就直接从左向右了。这时，会出现一个不好的情况：`nums1` 中的当前值数如果不是最小的，不能被直接替换掉，需要把它存起来。解决这个问题的简单办法是把引入一个新的空的数组保存最终结果，最后把新的空的数组的值重新赋值给 `nums1`。最终实现的代码量会加大。
- 所以最好是从右向左把数按顺序安置好。

## 复杂度

- 时间复杂度: `m + n`.
- 空间复杂度: `m + n`.

## Python

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        # Make a good example first.
        # nums1: [1, 5, 7, 0, 0, 0, 0]
        # nums2: [2, 3, 4, 8]
        # result:[1, 2, 3, 4, 5, 7, 8]
        i = m - 1
        j = n - 1

        for k in range(len(nums1) - 1, -1, -1):
            if i < 0 or (j >= 0 and nums2[j] > nums1[i]):
                nums1[k] = nums2[j]
                j -= 1
            else:
                nums1[k] = nums1[i]
                i -= 1
```

## Ruby

```ruby
# @param {Integer[]} nums1
# @param {Integer} m
# @param {Integer[]} nums2
# @param {Integer} n
# @return {Void} Do not return anything, modify nums1 in-place instead.
def merge(nums1, m, nums2, n)
  # Make a good example first.
  # nums1: [1, 5, 7, 0, 0, 0, 0]
  # nums2: [2, 3, 4, 8]
  # result:[1, 2, 3, 4, 5, 7, 8]
  i = m - 1
  j = n - 1

  (nums1.size - 1).downto(0) do |k|
    if i < 0 || (j >= 0 and nums2[j] > nums1[i])
      nums1[k] = nums2[j]
      j -= 1
    else
      nums1[k] = nums1[i]
      i -= 1
    end
  end
end

```

## Java

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        // Make a good example first.
        // nums1: [1, 5, 7, 0, 0, 0, 0]
        // nums2: [2, 3, 4, 8]
        // result:[1, 2, 3, 4, 5, 7, 8]

        var i = m - 1;
        var j = n - 1;

        for (var k = nums1.length - 1; k >= 0; k--) {
            if (i < 0 || (j >= 0 && nums2[j] > nums1[i])) {
                nums1[k] = nums2[j];
                j--;
            } else {
                nums1[k] = nums1[i];
                i--;
            }
        }
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.blog](https://leetcode.blog/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[88. 合并两个有序数组 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/88-merge-sorted-array).

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

