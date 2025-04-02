# 49. 字母异位词分组 - 力扣题解最佳实践

访问原文链接：[49. 字母异位词分组 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/49-group-anagrams)，体验更佳！

力扣链接：[49. 字母异位词分组](https://leetcode.cn/problems/group-anagrams), 难度：**中等**。

## 力扣“49. 字母异位词分组”问题描述

给你一个字符串数组，请你将 **字母异位词** 组合在一起。可以按任意顺序返回结果列表。

> **字母异位词** 是由重新排列源单词的所有字母得到的一个新单词。

### [示例 1]

**输入**: `strs = ["eat", "tea", "tan", "ate", "nat", "bat"]`

**输出**: `[["bat"],["nat","tan"],["ate","eat","tea"]]`

### [示例 2]

**输入**: `strs = [""]`

**输出**: `[[""]]`

### [示例 3]

**输入**: `strs = ["a"]`

**输出**: `[["a"]]`

### [约束]

- `1 <= strs.length <= 10^4`
- `0 <= strs[i].length <= 100`
- `strs[i]` 仅包含小写字母

## 思路

- 两个字符串，`bat`和`atb`，用什么方法能最快地知道他们是字母异位词呢？

    <details><summary>点击查看答案</summary><p>将每个字符串都按字母表顺序排序，然后比较排过序的两个字符串。相等，就是。</p></details>

- 但是排序后，原字符串没有被考虑进来，而结果求的是原字符串的分组。如何解决？

    <details><summary>点击查看答案</summary><p>用元组，即把按字母表顺序排序后的字符串和原字符串放在一个元组里，像这样：`("abt", "bat")`。</p></details>

- 剩下要做的，就是对这个元组数组进行分组了。如何分组最简单？

    <details><summary>点击查看答案</summary><p>用`Map`，`key`是按字母表顺序排过序的字符串，`value`是原字符串的数组。</p></details>

## 复杂度

> M = string.length

- 时间复杂度: `O(N * M * logM)`.
- 空间复杂度: `O(N)`.

## Python

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        pairs = [(''.join(sorted(string)), string) for string in strs]

        ordered_to_original = defaultdict(list)

        for ordered, original in pairs:
            ordered_to_original[ordered].append(original)

        return list(ordered_to_original.values())
```

## Ruby

```ruby
# @param {String[]} strs
# @return {String[][]}
def group_anagrams(strs)
  pairs = strs.map { |string| [ string.chars.sort.join, string ] }

  ordered_to_original = Hash.new([])

  pairs.each do |ordered, original|
    ordered_to_original[ordered] += [original]
  end

  ordered_to_original.values
end

# Or solution 2: More concise way

# @param {String[]} strs
# @return {String[][]}
def group_anagrams(strs)
  strs.group_by { |string| string.chars.sort }.values
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [leetcoder.net](https://leetcoder.net/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[49. 字母异位词分组 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/49-group-anagrams).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

