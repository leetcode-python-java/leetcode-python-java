# 58. 最后一个单词的长度 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

访问原文链接：[58. 最后一个单词的长度 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.to/zh/leetcode/58-length-of-last-word)，体验更佳！

力扣链接：[58. 最后一个单词的长度](https://leetcode.cn/problems/length-of-last-word), 难度等级：**简单**。

## LeetCode “58. 最后一个单词的长度”问题描述

给你一个字符串 `s`，由若干单词组成，单词前后用一些空格字符隔开。返回字符串中 **最后一个** 单词的长度。

**单词** 是指仅由字母组成、不包含任何空格字符的最大子字符串。

### [示例 1]

**输入**: `s = "Hello World"`

**输出**: `5`

**解释**: `最后一个单词是“World”，长度为 5。`

### [示例 2]

**输入**: `s = "   fly me   to   the moon  "`

**输出**: `4`

**解释**: `最后一个单词是“moon”，长度为 4。`

### [示例 3]

**输入**: `s = "luffy is still joyboy"`

**输出**: `6`

**解释**: `最后一个单词是长度为 6 的“joyboy”。`

### [约束]

- `1 <= s.length <= 10^4`
- `s` 仅有英文字母和空格 `' '` 组成
- `s` 中至少存在一个单词

## 思路

- 求最后一个单词的长度，我们可以用 `split()`, `last()`, `len()` 这样的方法。
- 不过这种题目其实是想考察程序员对 `index` 的控制能力。
- 最后一个单词在最后，如果从前向后求解，并不是很方便。有什么其它方法吗？

<details><summary>点击查看答案</summary><p>
方法一：可以直接从后往前求解。
方法二：把字符串 `s` 倒序，求第一个单词的长度。
本题采用方法二。在做完方法二后，建议用方法一实现一下。
</p></details>

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `1`.

## Python

```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        s = s[::-1]  # Reverse the string

        start_index = 0

        while start_index < len(s) and s[start_index] == ' ':
            start_index += 1

        end_index = start_index

        while end_index < len(s) and s[end_index] != ' ':
            end_index += 1

        return end_index - start_index
```

## Ruby

```ruby
# @param {String} s
# @return {Integer}
def length_of_last_word(s)
  s.reverse!

  start_index = 0

  while s[start_index] == ' '
    start_index += 1
  end

  end_index = start_index

  while end_index < s.size && s[end_index] != ' '
    end_index += 1
  end

  end_index - start_index
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.to](https://leetcode.to/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[58. 最后一个单词的长度 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.to/zh/leetcode/58-length-of-last-word).

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

