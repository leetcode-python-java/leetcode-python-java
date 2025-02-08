# 28. Find the Index of the First Occurrence in a String - Best Practices of LeetCode Solutions
LeetCode link: [28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string), difficulty: **Easy**.

## LeetCode description of "28. Find the Index of the First Occurrence in a String"
Given two strings `needle` and `haystack`, return the **index** of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

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

## Intuition
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
