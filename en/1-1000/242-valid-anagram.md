Original link: [leetcoder.net - LeetCoder: Fucking Good LeetCode Solutions](https://leetcoder.net/en/leetcode/242-valid-anagram)

# 242. Valid Anagram - LeetCoder: Fucking Good LeetCode Solutions

LeetCode link: [242. Valid Anagram](https://leetcode.com/problems/valid-anagram), Difficulty: **Easy**.

## LeetCode description of "242. Valid Anagram"

Given two strings `s` and `t`, return `true` if `t` is an **anagram** of `s`, and `false` otherwise.

> An **anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, using all the original letters exactly once.

### [Example 1]

**Input**: `s = "anagram", t = "nagaram"`

**Output**: `true`

### [Example 2]

**Input**: `s = "rat", t = "car"`

**Output**: `false`

### [Constraints]

- `1 <= s.length, t.length <= 5 * 10^4`
- `s` and `t` consist of lowercase English letters.

## Intuition

1. If the lengths of the two strings are different, return `false` directly.
2. Use two `hash tables` to store the statistics of the two strings respectively, with the `key` being the character and the `value` being the number of characters.
3. Compare the two `hash tables` to see if they are equal.

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(N)`.

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

## JavaScript

```javascript
var isAnagram = function (s, t) {
  if (s.length != t.length) {
    return false;
  }

  const sCharToCount = new Map()
  const tCharToCount = new Map()

  for (const char of s) {
    sCharToCount.set(char, (sCharToCount.get(char) || 0) + 1)
  }

  for (const char of t) {
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

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

