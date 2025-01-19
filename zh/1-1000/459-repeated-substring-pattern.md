# 459. 重复的子字符串 - 力扣题解最佳实践
力扣链接：[459. 重复的子字符串](https://leetcode.cn/problems/repeated-substring-pattern), 难度: **简单**。

## 力扣“459. 重复的子字符串”问题描述
给定一个非空的字符串 `s` ，检查是否可以通过由它的一个子串重复多次构成。

### [示例 1]
**输入**: `s = "abcabcabcabc"`

**输出**: `true`

**解释**: `可由子串 "abc" 重复四次构成。 (或子串 "abcabc" 重复两次构成。)`

### [示例 2]
**输入**: `s = "aba"`

**输出**: `false`

### [约束]
- `1 <= s.length <= 10000`
- `s` 由小写英文字母组成

## 思路
解决本问题的关键是要看清楚一点：通过子串的重复能得到`s`，那么子串的起始字母一定是`s[0]`。想明白了这一点，子串的排查范围就大大缩小了。

## 复杂度
* 时间：`O(N * N)`。
* 空间：`O(N)`。

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
