# 242. 有效的字母异位词 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

访问原文链接：[242. 有效的字母异位词 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/242-valid-anagram)，体验更佳！

力扣链接：[242. 有效的字母异位词](https://leetcode.cn/problems/valid-anagram), 难度等级：**简单**。

## LeetCode “242. 有效的字母异位词”问题描述

给定两个字符串 `s` 和 `t` ，编写一个函数来判断 `t` 是否是 `s` 的 **字母异位词**。

> *字母异位词*是通过重新排列不同单词或短语的字母而形成的单词或短语，并使用所有原字母一次。

### [示例 1]

**输入**: `s = "anagram", t = "nagaram"`

**输出**: `true`

### [示例 2]

**输入**: `s = "rat", t = "car"`

**输出**: `false`

### [约束]

- `1 <= s.length, t.length <= 5 * 10^4`
- `s` 和 `t` 仅包含小写字母

## 思路

1. 如果两个字符串长度不同，直接返回`false`。
2. 用两个`Hash tables`分别存储对两个字符串的统计数据，`key`为字符，`value`为该字符出现次数。
3. 比较这两个`Hash tables`，看它们是否相等。

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(N)`.

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

```csharp
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
import "reflect"

func isAnagram(s string, t string) bool {
    if len(s) != len(t) {
        return false
    }

    // Create frequency maps for both strings
    sCharCount := make(map[rune]int)
    for _, char := range s {
        sCharCount[char]++
    }

    tCharCount := make(map[rune]int)
    for _, char := range t {
        tCharCount[char]++
    }

    return reflect.DeepEqual(sCharCount, tCharCount)
}
```

## Ruby

```ruby
def is_anagram(s, t)
  return false if s.length != t.length

  s_char_to_count = Hash.new(0)
  t_char_to_count = Hash.new(0)

  s.each_char do |char|
    s_char_to_count[char] += 1
  end

  t.each_char do |char|
    t_char_to_count[char] += 1
  end

  s_char_to_count == t_char_to_count
end
```

## C++

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.length() != t.length()) {
            return false;
        }

        unordered_map<char, int> s_char_to_count;
        for (char character : s) {
            s_char_to_count[character]++;
        }

        unordered_map<char, int> t_char_to_count;
        for (char character : t) {
            t_char_to_count[character]++;
        }

        return s_char_to_count == t_char_to_count;
    }
};
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.blog](https://leetcode.blog/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[242. 有效的字母异位词 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/242-valid-anagram).

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

