# 5. 最长回文子串 - 力扣题解最佳实践

访问原文链接：[5. 最长回文子串 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/5-longest-palindromic-substring)，体验更佳！

力扣链接：[5. 最长回文子串](https://leetcode.cn/problems/longest-palindromic-substring), 难度：**中等**。

## 力扣“5. 最长回文子串”问题描述

给你一个字符串 `s`，找到 `s` 中最长的 **回文子串**。

- **回文性**：如果字符串向前和向后读都相同，则它满足 **回文性**。
- **子字符串** 是字符串中连续的 **非空** 字符序列。

### [示例 1]

**输入**: `s = "babad"`

**输出**: `"bab"`

**解释**: `"aba" 同样是符合题意的答案。`

### [示例 2]

**输入**: `s = "cbbd"`

**输出**: `"bb"`

### [约束]

- `1 <= s.length <= 1000`
- `s` 仅由数字和英文字母组成

### [Hints]

<details>
  <summary>提示 1</summary>
  How can we reuse a previously computed palindrome to compute a larger palindrome?

  
</details>

<details>
  <summary>提示 2</summary>
  If “aba” is a palindrome, is “xabax” a palindrome? Similarly is “xabay” a palindrome?

  
</details>

<details>
  <summary>提示 3</summary>
  Complexity based hint:
If we use brute-force and check whether for every start and end position a substring is a palindrome we have O(n^2) start - end pairs and O(n) palindromic checks. Can we reduce the time for palindromic checks to O(1) by reusing some previous computation.

  
</details>

## 思路



## 复杂度

- 时间复杂度: ``.
- 空间复杂度: ``.

## Ruby

```ruby
# @param {String} s
# @return {String}
def longest_palindrome(s)
  longest = s[0]
  s = s.chars.join("#")

  s.size.times do |i|
    j = 1

    while j <= i and i + j < s.size
      break if s[i - j] != s[i + j]

      if s[i - j] == '#'
        j += 1
        next
      end
      
      length = j * 2 + 1

      if length > longest.size
        longest = s[i - j..i + j]
      end
      
      j += 1
    end
  end
  
  longest.gsub('#', '')
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [leetcoder.net](https://leetcoder.net/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[5. 最长回文子串 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/5-longest-palindromic-substring).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

