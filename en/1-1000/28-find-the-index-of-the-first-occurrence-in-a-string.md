# 28. Find the Index of the First Occurrence in a String - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

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

Visit original link: [28. Find the Index of the First Occurrence in a String - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/28-find-the-index-of-the-first-occurrence-in-a-string) for a better experience!

LeetCode link: [28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string), difficulty: **Easy**.

## LeetCode description of "28. Find the Index of the First Occurrence in a String"

Given two strings `needle` and `haystack`, return the **index** of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

### [Example 1]

**Input**: `haystack = "sadbutsad", needle = "sad"`

**Output**: `0`

**Explanation**: 

<p>&quot;sad&quot; occurs at index 0 and 6.<br>
The first occurrence is at index 0, so we return 0.</p>


### [Example 2]

**Input**: `haystack = "leetcode", needle = "leeto"`

**Output**: `-1`

**Explanation**: 

<p>&quot;leeto&quot; did not occur in &quot;leetcode&quot;, so we return -1.</p>


### [Constraints]

- `1 <= haystack.length, needle.length <= 10000`
- `haystack` and `needle` consist of only lowercase English characters.

## Intuition

- This kind of question can be solved with one line of code using the built-in `index()`. Obviously, the questioner wants to test our ability to control the loop.

- For `heystack`, iterate through each character in turn. If the substring from the current character to `needle` is the same as `needle`, return the position of the current character.

- This question is easier to understand by looking at the code directly.

## Complexity

- Time complexity: `O(N * M)`.
- Space complexity: `O(1)`.

## Python

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        n = len(haystack)
        m = len(needle)
        
        for i in range(n - m + 1):
            if haystack[i:i + m] == needle:
                return i
        
        return -1
```

## JavaScript

```javascript
/**
 * @param {string} haystack
 * @param {string} needle
 * @return {number}
 */
var strStr = function(haystack, needle) {
  const n = haystack.length;
  const m = needle.length;
    
  for (let i = 0; i <= n - m; i++) {
    if (haystack.substring(i, i + m) === needle) {
      return i;
    }
  }
    
  return -1;
};

```

## Ruby

```ruby
# @param {String} haystack
# @param {String} needle
# @return {Integer}
def str_str(haystack, needle)
  (0..haystack.size - needle.size).each do |i|
    if haystack[i...i + needle.size] == needle
      return i  
    end
  end

  -1
end
```

## C++

```cpp
class Solution {
public:
    int strStr(string haystack, string needle) {
        for (int i = 0; i < haystack.length(); i++) {
            int j = 0;
            
            while (i + j < haystack.length() && haystack[i + j] == needle[j]) {
                j++;
                
                if (j == needle.length()) {
                    return i;
                }
            }
        }
        
        return -1;
    }
};
```

## Java

```java
class Solution {
    public int strStr(String haystack, String needle) {
        for (int i = 0; i < haystack.length(); i++) {
            int j = 0;

            while (i + j < haystack.length() && haystack.charAt(i + j) == needle.charAt(j)) {
                j++;

                if (j == needle.length()) {
                    return i;
                }
            }
        }

        return -1;
    }
}
```

## Go

```go
func strStr(haystack string, needle string) int {
    for i := 0; i < len(haystack); i++ {
        j := 0

        for i+j < len(haystack) && haystack[i+j] == needle[j] {
            j++

            if j == len(needle) {
                return i
            }
        }
    }

    return -1
}
```

## C#

```csharp
public class Solution {
    public int StrStr(string haystack, string needle) {
        for (int i = 0; i < haystack.Length; i++) {
            int j = 0;

            while (i + j < haystack.Length && haystack[i + j] == needle[j]) {
                j++;

                if (j == needle.Length) {
                    return i;
                }
            }
        }

        return -1;
    }
}
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

Visit original link: [28. Find the Index of the First Occurrence in a String - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/28-find-the-index-of-the-first-occurrence-in-a-string) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

