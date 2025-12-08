# 125. 验证回文串 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 Show.dev 打造你的个人品牌 →**](https://www.show.dev)

---

访问原文链接：[125. 验证回文串 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/125-valid-palindrome)，体验更佳！

力扣链接：[125. 验证回文串](https://leetcode.cn/problems/valid-palindrome), 难度等级：**简单**。

## LeetCode “125. 验证回文串”问题描述

如果在将所有大写字符转换为小写字符、并移除所有非字母数字字符之后，短语正着读和反着读都一样。则可以认为该短语是一个 **回文串** 。

字母和数字都属于字母数字字符。

给你一个字符串 `s`，如果它是 **回文串** ，返回 `true` ；否则，返回 `false` 。

### [示例 1]

**输入**: `s = "A man, a plan, a canal: Panama"`

**输出**: `true`

**解释**: `"amanaplanacanalpanama" 是回文串。`

### [示例 2]

**输入**: `s = "race a car"`

**输出**: `false`

**解释**: `"raceacar" 不是回文串。`

### [示例 3]

**输入**: `s = " "`

**输出**: `true`

**解释**: 

<p>在移除非字母数字字符之后，s 是一个空字符串 &quot;&quot; 。<br>
由于空字符串正着反着读都一样，所以是回文串。</p>


### [约束]

- `1 <= s.length <= 2 * 10^5`
- `s` 仅由可打印的 ASCII 字符组成

## 思路

1. 去掉非法字符。
2. 用 `valid_s == valid_s.reverse` 来验证是否为回文串。

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Ruby

```ruby
# @param {String} s
# @return {Boolean}
def is_palindrome(s)
  valid_chars = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'
  valid_s = ''

  s.downcase.chars.each do |char|
    if valid_chars.include?(char)
      valid_s << char
    end
  end

  valid_s == valid_s.reverse
end
```

## Python

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        valid_chars = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'
        valid_s = ''

        for char in s.lower():
            if char in valid_chars:
                valid_s += char

        return valid_s == valid_s[::-1]
```

## Java

```java
class Solution {
    public boolean isPalindrome(String s) {
        var validChars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
        var validS = new StringBuilder();

        for (char c : s.toLowerCase().toCharArray()) {
            if (validChars.indexOf(c) != -1) {
                validS.append(c);
            }
        }

        var cleaned = validS.toString();
        var reversed = validS.reverse().toString();

        return cleaned.equals(reversed);
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 Show.dev 打造你的个人品牌 →**](https://www.show.dev)

---

访问原文链接：[125. 验证回文串 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/125-valid-palindrome)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

