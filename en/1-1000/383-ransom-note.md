# 383. Ransom Note - Best Practices of LeetCode Solutions
LeetCode problem link: [383. Ransom Note](https://leetcode.com/problems/ransom-note),
[383. 赎金信](https://leetcode.cn/problems/ransom-note)

[中文题解](#中文题解)

## LeetCode problem description
Given two strings `ransomNote` and `magazine`, return `true` if `ransomNote` can be constructed by using the letters from `magazine` and `false` otherwise.

Each letter in `magazine` can only be used once in `ransomNote`.

Difficulty: **Easy**

### [Example 1]
**Input**: `ransomNote = "a", magazine = "b"`

**Output**: `false`

### [Example 2]
**Input**: `ransomNote = "aa", magazine = "ab"`

**Output**: `false`

### [Example 3]
**Input**: `ransomNote = "aa", magazine = "aab"`

**Output**: `true`

### [Constraints]
- `1 <= ransomNote.length, magazine.length <= 100000`
- `ransomNote` and `magazine` consist of lowercase English letters.

## Intuition
[中文题解](#中文题解)

1. This question is equivalent to asking whether `magazine` can contain all the characters in `ransomNote`.
2. First count the characters in `magazine`, and store the results in `Map`.
3. Then, traverse `ransomNote` and perform reverse operations on the data in `Map`. If the count of a character is less than 0, return `false`.

## Steps
1. First count the characters in `magazine`, and store the results in `Map`.
```javascript
charToCount = new Map()

for (character in magazine) {
  charToCount[character] += 1
}
```

2. Then, traverse `ransomNote` and perform reverse operations on the data in `Map`. If the count of a character is less than 0, return `false`.
```javascript
charToCount = new Map()

for (character in magazine) {
  charToCount[character] += 1
}

for (character in ransomNote) {
  charToCount[character] -= 1

  if (charToCount[character] < 0) {
    return false
  }
}

return true
```

## Complexity
* Time: `O(n)`.
* Space: `O(n)`.

## Java
```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        var charToCount = new HashMap<Character, Integer>();

        for (var character : magazine.toCharArray()) {
            charToCount.put(character, charToCount.getOrDefault(character, 0) + 1);
        }

        for (var character : ransomNote.toCharArray()) {
            charToCount.put(character, charToCount.getOrDefault(character, 0) - 1);

            if (charToCount.get(character) < 0) {
                return false;
            }
        }

        return true;
    }
}
```

## Python
```python
# from collections import defaultdict

class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        char_to_count = defaultdict(int)

        for char in magazine:
            char_to_count[char] += 1

        for char in ransomNote:
            char_to_count[char] -= 1

            if char_to_count[char] < 0:
                return False

        return True
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
var canConstruct = function (ransomNote, magazine) {
  const charToCount = new Map()

  for (const character of magazine) {
    charToCount.set(character, (charToCount.get(character) || 0) + 1)
  }

  for (const character of ransomNote) {
    charToCount.set(character, (charToCount.get(character) || 0) - 1)

    if (charToCount.get(character) < 0) {
      return false
    }
  }

  return true
};
```

## C#
```c#
public class Solution
{
    public bool CanConstruct(string ransomNote, string magazine)
    {
        var charToCount = new Dictionary<char, int>();

        foreach (char character in magazine)
            charToCount[character] = charToCount.GetValueOrDefault(character, 0) + 1;

        foreach (char character in ransomNote)
        {
            charToCount[character] = charToCount.GetValueOrDefault(character, 0) - 1;

            if (charToCount[character] < 0)
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

## 力扣问题描述
[383. 赎金信](https://leetcode.cn/problems/ransom-note), 难度: **简单**。

给你两个字符串：`ransomNote` 和 `magazine` ，判断 `ransomNote` 能不能由 `magazine` 里面的字符构成。

如果可以，返回 `true` ；否则返回 `false` 。

`magazine` 中的每个字符只能在 `ransomNote` 中使用一次。

### [示例 2]
**输入**: `ransomNote = "aa", magazine = "ab"`

**输出**: `false`

### [示例 3]
**输入**: `ransomNote = "aa", magazine = "aab"`

**输出**: `true`

# 中文题解
## 思路
1. 本题等同于求`magazine`是否能包含`ransomNote`中的所有字符。
2. 先对`magazine`进行字符和字数统计，结果存储在`Map`中。
3. 然后，遍历`ransomNote`，并对`Map`中的数据进行反向操作。如果某个字符的字数小于0，则返回`false`。

## 步骤
1. 先对`magazine`进行字符和字数统计，结果存储在`Map`中。
```javascript
charToCount = new Map()

for (character in magazine) {
  charToCount[character] += 1
}
```

2. 然后，遍历`ransomNote`，并对`Map`中的数据进行反向操作。如果某个字符的字数小于0，则返回`false`。
```javascript
charToCount = new Map()

for (character in magazine) {
  charToCount[character] += 1
}

for (character in ransomNote) {
  charToCount[character] -= 1

  if (charToCount[character] < 0) {
    return false
  }
}

return true
```
