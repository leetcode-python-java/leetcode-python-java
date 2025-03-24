Original link: [leetcoder.net - Fucking Good LeetCode Solutions](https://leetcoder.net/en/leetcode/28-find-the-index-of-the-first-occurrence-in-a-string)

# 28. Find the Index of the First Occurrence in a String - Fucking Good LeetCode Solutions
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

- This kind of question can be solved with one line of code using the built-in `index()`. Obviously, the questioner wants to test our ability to control the loop.

- For `heystack`, traverse each character in turn. There may be two situations:
    1. First, the character is not equal to the first letter of `needle`. Then process the next character.
    2. Second, if the character is equal to the first letter of `needle`, continue to compare the next character of `heystack` and `needle` in an internal loop until they are not equal or `needle` has completely matched.

- This question is easier to understand by looking at the code directly.

## Complexity
* Time: `O(m + n)`.
* Space: `O(n)`.

## Python
```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        for i in range(len(haystack)):
            j = 0
            
            while i + j < len(haystack) and haystack[i + j] == needle[j]:
                j += 1

                if j == len(needle):
                    return i

        return -1
```

## JavaScript
```javascript
var strStr = function (haystack, needle) {
  for (let i = 0; i < haystack.length; i++) {
    let j = 0

    while (i + j < haystack.length && haystack[i + j] == needle[j]) {
      j += 1

      if (j == needle.length) {
        return i
      }
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

## C
```c
// Welcome to create a PR to complete the code of this language, thanks!
```

## Kotlin
```kotlin
// Welcome to create a PR to complete the code of this language, thanks!
```

## Swift
```swift
// Welcome to create a PR to complete the code of this language, thanks!
```

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
