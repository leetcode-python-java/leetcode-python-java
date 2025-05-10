# 345. Reverse Vowels of a String - LeetCode Python/Java/C++/JS code

Visit original link: [345. Reverse Vowels of a String - LeetCode Python/Java/C++/JS code](https://leetcode.blog/en/leetcode/345-reverse-vowels-of-a-string) for a better experience!

LeetCode link: [345. Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string), difficulty: **Easy**.

## LeetCode description of "345. Reverse Vowels of a String"

Given a string `s`, reverse only all the vowels in the string and return it.

The vowels are `'a'`, `'e'`, `'i'`, `'o'`, and `'u'`, and they can appear in both lower and upper cases, more than once.

### [Example 1]

**Input**: `s = "IceCreAm"`

**Output**: `"AceCreIm"`

**Explanation**: 

<p>The vowels in <code>s</code> are <code>[&#39;I&#39;, &#39;e&#39;, &#39;e&#39;, &#39;A&#39;]</code>. On reversing the vowels, <code>s</code> becomes <code>&quot;AceCreIm&quot;</code>.</p>


### [Example 2]

**Input**: `"leetcode"`

**Output**: `"leotcede"`

### [Constraints]

- `1 <= s.length <= 3 * 10^5`
- `s` consist of **printable ASCII** characters.

## Intuition



## Complexity

- Time complexity: ``.
- Space complexity: ``.

## Python

```python
class Solution:
    def reverseVowels(self, s: str) -> str:
        vowels = ['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U']
        s = list(s)
        r = len(s) - 1

        for l in range(len(s)): # Important
            if s[l] not in vowels:
                continue

            while r > 0 and s[r] not in vowels:
                r -= 1

            if l >= r:
                break

            s[l], s[r] = s[r], s[l]
            r -= 1

        return ''.join(s)
```

## SQL

```sql

```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCode.blog](https://leetcode.blog): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [345. Reverse Vowels of a String - LeetCode Python/Java/C++/JS code](https://leetcode.blog/en/leetcode/345-reverse-vowels-of-a-string).

GitHub repository: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

