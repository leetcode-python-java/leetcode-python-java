# 459. Repeated Substring Pattern - LeetCode Solution
LeetCode English link: [459. Repeated Substring Pattern](https://leetcode.com/problems/repeated-substring-pattern)

LeetCode Chinese link: [459. 重复的子字符串](https://leetcode.cn/problems/repeated-substring-pattern)

[中文题解](#中文题解)

## LeetCode problem description
Given a string `s`, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.

Difficulty: **Easy**

### [Example 1]
**Input**: `s = "abcabcabcabc"`

**Output**: `true`

**Explanation**: `It is the substring "abc" four times or the substring "abcabc" twice.`

### [Example 2]
**Input**: `s = "aba"`

**Output**: `false`

### [Constraints]
- `1 <= s.length <= 10000`
- `s` consists of lowercase English letters.

## Intuition behind the Solution
[中文题解](#中文题解)

The key to solving this problem is to see clearly that if `s` can be obtained by repeating the substring, then the starting letter of the substring must be `s[0]`.
Once you understand this, the scope of substring investigation is greatly narrowed.

## Complexity
* Time: `O(N * N)`.
* Space: `O(N)`.

## Python
```python
class Solution:
    def repeatedSubstringPattern(self, s: str) -> bool:
        for i in range(1, int(len(s) / 2) + 1):
            if len(s) % i == 0 and s[:i] * int(len(s) / i) == s:
                return True

        return False
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
var repeatedSubstringPattern = function (s) {
  for (let i = 1; i <= s.length / 2; i++) {
    if (s.length % i != 0) {
      continue
    }

    if (s.slice(0, i).repeat(s.length / i) == s) {
      return true
    }
  }

  return false
};
```

## Java
```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## C#
```c#
// Welcome to create a PR to complete the code of this language, thanks!
```

## Go
```go
// Welcome to create a PR to complete the code of this language, thanks!
```

## Ruby
```ruby
# Welcome to create a PR to complete the code of this language, thanks!
```

## C, Kotlin, Swift, Rust or other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```

## 力扣“459. 重复的子字符串”问题描述
力扣链接：[459. 重复的子字符串](https://leetcode.cn/problems/repeated-substring-pattern), 难度: **简单**。

给定一个非空的字符串 `s` ，检查是否可以通过由它的一个子串重复多次构成。

### [示例 1]
**输入**: `s = "abcabcabcabc"`

**输出**: `true`

**解释**: `可由子串 "abc" 重复四次构成。 (或子串 "abcabc" 重复两次构成。)`

### [示例 2]
**输入**: `s = "aba"`

**输出**: `false`

# 中文题解
## 思路
解决本问题的关键是要看清楚一点：通过子串的重复能得到`s`，那么子串的起始字母一定是`s[0]`。想明白了这一点，子串的排查范围就大大缩小了。
