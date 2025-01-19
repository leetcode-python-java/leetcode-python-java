# 242. Valid Anagram - LeetCode Solution
LeetCode problem link: [242. Valid Anagram](https://leetcode.com/problems/valid-anagram),
[242. 有效的字母异位词](https://leetcode.cn/problems/valid-anagram)

[中文题解](#中文题解)

## LeetCode problem description
Given two strings `s` and `t`, return `true` if `t` is an **anagram** of `s`, and `false` otherwise.

An **anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, using all the original letters exactly once.

Difficulty: **Easy**

### [Example 1]
**Input**: `s = "anagram", t = "nagaram"`

**Output**: `true`

### [Example 2]
**Input**: `s = "rat", t = "car"`

**Output**: `false`

### [Constraints]
- `1 <= s.length, t.length <= 5 * 10000`
- `s` and `t` consist of lowercase English letters.

## Intuition
[中文题解](#中文题解)

1. If the lengths of the two strings are different, return `false` directly.
2. Use two `hash tables` to store the statistics of the two strings respectively, with the `key` being the character and the `value` being the number of characters.
3. Compare the two `hash tables` to see if they are equal.

## Complexity
* Time: `O(n)`.
* Space: `O(n)`.

## Java
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        var sCharToCount = new HashMap<Character, Integer>();
        for (var character : s.toCharArray()) {
            sCharToCount.put(character, sCharToCount.getOrDefault(character, 0) + 1);
        }

        var tCharToCount = new HashMap<Character, Integer>();
        for (var character : t.toCharArray()) {
            tCharToCount.put(character, tCharToCount.getOrDefault(character, 0) + 1);
        }

        return sCharToCount.equals(tCharToCount);
    }
}
```

## Python
```python
# from collections import defaultdict

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        s_char_to_count = defaultdict(int)
        for char in s:
            s_char_to_count[char] += 1

        t_char_to_count = defaultdict(int)
        for char in t:
            t_char_to_count[char] += 1

        return s_char_to_count == t_char_to_count
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
var isAnagram = function (s, t) {
  if (s.length != t.length) {
    return false;
  }

  const sCharToCount = new Map()
  const tCharToCount = new Map()

  for (let char of s) {
    sCharToCount.set(char, (sCharToCount.get(char) || 0) + 1)
  }

  for (let char of t) {
    tCharToCount.set(char, (tCharToCount.get(char) || 0) + 1)
  }

  return _.isEqual(sCharToCount, tCharToCount)
};
```

## C#
```c#
public class Solution
{
    public bool IsAnagram(string s, string t)
    {
        if (s.Length != t.Length)
            return false;

        var sCharToCount = new Dictionary<char, int>();
        var tCharToCount = new Dictionary<char, int>();

        foreach (char character in s)
            sCharToCount[character] = sCharToCount.GetValueOrDefault(character, 0) + 1;

        foreach (char character in t)
            tCharToCount[character] = tCharToCount.GetValueOrDefault(character, 0) + 1;

        foreach (var entry in sCharToCount)
        {
            if (entry.Value != tCharToCount.GetValueOrDefault(entry.Key))
            {
                return false;
            }
        }

        return true;
    }
}
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

## 问题描述
给定两个字符串 `s` 和 `t` ，编写一个函数来判断 `t` 是否是 `s` 的 **字母异位词** 。

**字母异位词**是通过重新排列不同单词或短语的字母而形成的单词或短语，并使用所有原字母一次。

难度: **容易**

### [Example 1]
**输入**: `s = "anagram", t = "nagaram"`

**输出**: `true`

### [Example 2]
**输入**: `s = "rat", t = "car"`

**输出**: `false`

# 中文题解
## 思路
1. 如果两个字符串长度不同，直接返回`false`。
2. 用两个`Hash tables`分别存储对两个字符串的统计数据，`key`为字符，`value`为该字符出现次数。
3. 比较这两个`Hash tables`，看它们是否相等。
