# 345. Reverse Vowels of a String - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired. We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [345. Reverse Vowels of a String - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/345-reverse-vowels-of-a-string) for a better experience!

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

Use two pointers to swap vowels in the string. The left pointer finds vowels from the start, the right pointer finds vowels from the end, and they swap until the pointers meet.

## Pattern of "left & right pointers"

The code framework is as follows:

```java
int r = target.length() - 1;

for (int l = 0; l < target.length(); l++) { // Important
    // ...
    if (l >= r) {
        break;
    }

    // ...
    r--;
}
```

## Step-by-Step Solution

1. Initialize a set of vowels
2. For some languages, convert the string to a character array (since strings are immutable)
3. Left pointer `l` starts at `0`, right pointer `r` starts at the end
4. Loop processing:
    - Move `l` right until a vowel is found
    - Move `r` left until a vowel is found
    - Swap the two vowels when `l < r`
5. Return the processed string

## Complexity

> Space complexity is O(N) if converting to a character array

- Time complexity: `O(N)`.
- Space complexity: `O(1) or O(N)`.

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

## Java

```java
class Solution {
    public String reverseVowels(String s) {
        var vowels = new HashSet<>(Arrays.asList('a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'));
        var chars = s.toCharArray();
        int r = chars.length - 1;

        for (int l = 0; l < chars.length; l++) { // important
            if (!vowels.contains(chars[l])) {
                continue;
            }

            while (r > 0 && !vowels.contains(chars[r])) {
                r--;
            }

            if (l >= r) {
                break;
            }

            // Swap the vowels
            char temp = chars[l];
            chars[l] = chars[r];
            chars[r] = temp;
            r--;
        }

        return new String(chars);
    }
}
```

## C++

```cpp
class Solution {
public:
    string reverseVowels(string s) {
        unordered_set<char> vowels = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};
        int r = s.size() - 1;

        for (int l = 0; l < s.size(); l++) { // important
            if (!vowels.contains(s[l])) {
                continue;
            }

            while (r > 0 && !vowels.contains(s[r])) {
                r--;
            }

            if (l >= r) {
                break;
            }

            swap(s[l], s[r]);
            r--;
        }

        return s;
    }
};
```

## JavaScript

```javascript
var reverseVowels = function (s) {
  const vowels = new Set(['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'])
  const chars = s.split('')
  let r = chars.length - 1

  for (let l = 0; l < chars.length; l++) { // important
    if (!vowels.has(chars[l])) {
      continue
    }

    while (r > 0 && !vowels.has(chars[r])) {
      r--
    }

    if (l >= r) {
      break
    }

    [chars[l], chars[r]] = [chars[r], chars[l]]
    r--
  }

  return chars.join('')
};
```

## Ruby

```ruby
def reverse_vowels(s)
  vowels = Set.new(['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'])
  r = s.size - 1

  (0...s.size).each do |l|
    unless vowels.include?(s[l])
      next
    end

    while r > 0 && !vowels.include?(s[r])
      r -= 1
    end

    if l >= r
      break
    end

    s[l], s[r] = s[r], s[l]
    r -= 1
  end

  s
end
```

## C#

```csharp
public class Solution
{
    public string ReverseVowels(string s)
    {
        var vowels = new HashSet<char> {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};
        var chars = s.ToCharArray();
        int r = chars.Length - 1;
        // important
        for (int l = 0; l < chars.Length; l++)
        {
            if (!vowels.Contains(chars[l]))
            {
                continue;
            }

            while (r > 0 && !vowels.Contains(chars[r]))
            {
                r--;
            }

            if (l >= r)
            {
                break;
            }

            (chars[l], chars[r]) = (chars[r], chars[l]);
            r--;
        }

        return new string(chars);
    }
}
```

## Go

```go
func reverseVowels(s string) string {
    vowels := map[byte]bool{
        'a': true, 'e': true, 'i': true, 'o': true, 'u': true,
        'A': true, 'E': true, 'I': true, 'O': true, 'U': true,
    }
    chars := []byte(s)
    r := len(chars) - 1

    for l := 0; l < len(chars); l++ { // important
        if !vowels[chars[l]] {
            continue
        }

        for r > 0 && !vowels[chars[r]] {
            r--
        }

        if l >= r {
            break
        }

        chars[l], chars[r] = chars[r], chars[l]
        r--
    }

    return string(chars)
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired. We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [345. Reverse Vowels of a String - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/345-reverse-vowels-of-a-string) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

