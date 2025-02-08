# 459. Repeated Substring Pattern - Best Practices of LeetCode Solutions
LeetCode link: [459. Repeated Substring Pattern](https://leetcode.com/problems/repeated-substring-pattern), difficulty: **Easy**.

## LeetCode description of "459. Repeated Substring Pattern"
Given a string `s`, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.

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

## Intuition
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
