# 345. 反转字符串中的元音字母 - LeetCode Python/Java/C++ 题解

访问原文链接：[345. 反转字符串中的元音字母 - LeetCode Python/Java/C++ 题解](https://leetcode.blog/zh/leetcode/345-reverse-vowels-of-a-string)，体验更佳！

力扣链接：[345. 反转字符串中的元音字母](https://leetcode.cn/problems/reverse-vowels-of-a-string), 难度等级：**简单**。

## LeetCode “345. 反转字符串中的元音字母”问题描述

给你一个字符串 `s` ，仅反转字符串中的所有元音字母，并返回结果字符串。

元音字母包括 `'a'`, `'e'`, `'i'`, `'o'`, `'u'`，且可能以大小写两种形式出现不止一次。

### [示例 1]

**输入**: `s = "IceCreAm"`

**输出**: `"AceCreIm"`

**解释**: 

<p><code>s</code> 中的元音是 <code>[&#39;I&#39;, &#39;e&#39;, &#39;e&#39;, &#39;A&#39;]</code>。反转这些元音，<code>s</code> 变为 <code>&quot;AceCreIm&quot;</code>.</p>


### [示例 2]

**输入**: `"leetcode"`

**输出**: `"leotcede"`

### [约束]

- `1 <= s.length <= 3 * 10^5`
- `s` 由 **可打印的 ASCII** 字符组成

## 思路



## 复杂度

- 时间复杂度: ``.
- 空间复杂度: ``.

## Python

```python
class Solution:
    def reverseVowels(self, s: str) -> str:
        vowels = ['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U']
        s = list(s)
        r = len(s) - 1

        for l in range(len(s)): # Important
            if s[l] not in vowels:
                continue

            while r > 0 and s[r] not in vowels:
                r -= 1

            if l >= r:
                break

            s[l], s[r] = s[r], s[l]
            r -= 1

        return ''.join(s)
```

## SQL

```sql

```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.blog](https://leetcode.blog/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[345. 反转字符串中的元音字母 - LeetCode Python/Java/C++ 题解](https://leetcode.blog/zh/leetcode/345-reverse-vowels-of-a-string).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

