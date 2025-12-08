# 58. 最后一个单词的长度 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **进阶你的开发者身份**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/你的名字` 或 `an.dev/你的名字`。
>
> [**立即前往 Show.dev 打造你的专属品牌 →**](https://www.show.dev)

---

访问原文链接：[58. 最后一个单词的长度 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/58-length-of-last-word)，体验更佳！

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

## Java

```java
class Solution {
    public int lengthOfLastWord(String s) {
        // Reverse the string
        var sb = new StringBuilder(s);
        String reversed = sb.reverse().toString();

        var startIndex = 0;
        // Skip leading spaces (which were trailing spaces in original)
        while (startIndex < reversed.length() && reversed.charAt(startIndex) == ' ') {
            startIndex++;
        }

        var endIndex = startIndex;
        while (endIndex < reversed.length() && reversed.charAt(endIndex) != ' ') {
            endIndex++;
        }

        return endIndex - startIndex;
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **进阶你的开发者身份**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/你的名字` 或 `an.dev/你的名字`。
>
> [**立即前往 Show.dev 打造你的专属品牌 →**](https://www.show.dev)

---

访问原文链接：[58. 最后一个单词的长度 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/58-length-of-last-word)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

