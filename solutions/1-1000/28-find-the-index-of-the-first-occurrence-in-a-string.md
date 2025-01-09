# 28. Find the Index of the First Occurrence in a String - LeetCode Solution
LeetCode English link: [28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string),

LeetCode Chinese link: [28. 找出字符串中第一个匹配项的下标](https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string)
([中文题解](#中文题解))

## LeetCode problem description
Given two strings `needle` and `haystack`, return the **index** of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

Difficulty: **Easy**

### [Example 1]
**Input**: `haystack = "sadbutsad", needle = "sad"`

**Output**: `0`

**Explanation**:
```
"sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.
```

### [Example 2]
**Input**: `haystack = "leetcode", needle = "leeto"`

**Output**: `-1`

**Explanation**: `"leeto" did not occur in "leetcode", so we return -1.`

### [Constraints]
- `1 <= haystack.length, needle.length <= 10000`
- `haystack` and `needle` consist of only lowercase English characters.

## Intuition behind the Solution
[中文题解](#中文题解)

Traverse the string once, and if the `needle.length` characters after the current position are equal to `needle`, return the current `index`.

## Complexity
* Time: `O(m * n)`.
* Space: `O(n)`.

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

## 力扣“28. 找出字符串中第一个匹配项的下标”问题描述
力扣链接：[28. 找出字符串中第一个匹配项的下标](https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string), 难度: **简单**。

给你两个字符串 `haystack` 和 `needle` ，请你在 `haystack` 字符串中找出 `needle` 字符串的第一个匹配项的下标（下标从 `0` 开始）。如果 `needle` 不是 `haystack` 的一部分，则返回 `-1` 。

### [示例 1]
**输入**: `haystack = "sadbutsad", needle = "sad"`

**输出**: `0`

### [示例 1]
**输入**: `haystack = "leetcode", needle = "leeto"`

**输出**: `-1`

# 中文题解
## 思路
遍历一遍字符串，如果从当前位置起的后的`needle.length`个字符等于`needle`，则返回当前的`index`。
