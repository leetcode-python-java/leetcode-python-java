# 28. 找出字符串中第一个匹配项的下标 - 力扣题解最佳实践
力扣链接：[28. 找出字符串中第一个匹配项的下标](https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string), 难度: **简单**。

## 力扣“28. 找出字符串中第一个匹配项的下标”问题描述
给你两个字符串 `haystack` 和 `needle` ，请你在 `haystack` 字符串中找出 `needle` 字符串的第一个匹配项的下标（下标从 `0` 开始）。如果 `needle` 不是 `haystack` 的一部分，则返回 `-1` 。

### [示例 1]
**输入**: `haystack = "sadbutsad", needle = "sad"`

**输出**: `0`

**解释**:
```
"sad" 在下标 0 和 6 处匹配。
第一个匹配项的下标是 0 ，所以返回 0 。
```

### [示例 2]
**输入**: `haystack = "leetcode", needle = "leeto"`

**输出**: `-1`

**解释**: `"leeto" 没有在 "leetcode" 中出现，所以返回 -1 。`

### [约束]
- `1 <= haystack.length, needle.length <= 10000`
- `haystack` 和 `needle` 仅由小写英文字符组成

## 思路
遍历一遍字符串，如果从当前位置起的后的`needle.length`个字符等于`needle`，则返回当前的`index`。

## 复杂度
* 时间：`O(m * n)`。
* 空间：`O(n)`。

## Python
```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        for i in range(len(haystack)):
            if haystack[i:i + len(needle)] == needle:
                return i

        return -1
```

## JavaScript
```javascript
var strStr = function (haystack, needle) {
  for (let i = 0; i < haystack.length; i++) {
    if (haystack.slice(i, i + needle.length) == needle) {
      return i
    }
  }

  return -1
};
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
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
