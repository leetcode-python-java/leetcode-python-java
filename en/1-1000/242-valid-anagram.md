# 242. Valid Anagram - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.leader.me`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [242. Valid Anagram - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/242-valid-anagram) for a better experience!

LeetCode link: [242. Valid Anagram](https://leetcode.com/problems/valid-anagram), difficulty: **Easy**.

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

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.leader.me`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [242. Valid Anagram - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/242-valid-anagram) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

