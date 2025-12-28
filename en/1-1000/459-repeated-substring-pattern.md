# 459. Repeated Substring Pattern - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [459. Repeated Substring Pattern - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/459-repeated-substring-pattern) for a better experience!

LeetCode link: [459. Repeated Substring Pattern](https://leetcode.com/problems/repeated-substring-pattern), difficulty: **Easy**.

## LeetCode description of "459. Repeated Substring Pattern"

Given a string `s`, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.

### [Example 1]

**Input**: `s = "abcabcabcabc"`

**Output**: `true`

**Explanation**: 

<p>It is the substring &quot;abc&quot; four times or the substring &quot;abcabc&quot; twice.</p>


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

- Time complexity: `O(N * N)`.
- Space complexity: `O(N)`.

## Python

```python
class Solution:
    def repeatedSubstringPattern(self, s: str) -> bool:
        for i in range(1, int(len(s) / 2) + 1):
            if len(s) % i == 0 and s[:i] * int(len(s) / i) == s:
                return True

        return False
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

## Go

```go
func repeatedSubstringPattern(s string) bool {
    n := len(s)

    for i := 1; i <= n/2; i++ {
        if n%i == 0 {
            substring := s[:i]
            repeated := strings.Repeat(substring, n/i)

            if repeated == s {
                return true
            }
        }
    }

    return false
}
```

## C++

```cpp
class Solution {
public:
    bool repeatedSubstringPattern(string s) {
        int n = s.length();

        for (int i = 1; i <= n / 2; i++) {
            if (n % i != 0) {
                continue;
            }

            string pattern = s.substr(0, i);
            string repeated = "";

            for (int j = 0; j < n / i; j++) {
                repeated += pattern;
            }

            if (repeated == s) {
                return true;
            }
        }

        return false;
    }
};
```

## Java

```java
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        int n = s.length();

        for (var i = 1; i <= n / 2; i++) {
            if (n % i != 0) {
                continue;
            }

            var pattern = s.substring(0, i);
            var repeated = new StringBuilder();

            // Simply concatenate the pattern multiple times
            for (var j = 0; j < n / i; j++) {
                repeated.append(pattern);
            }

            // Compare the constructed string with the original string
            if (repeated.toString().equals(s)) {
                return true;
            }
        }

        return false;
    }
}
```

## C#

```csharp
public class Solution
{
    public bool RepeatedSubstringPattern(string s)
    {
        int n = s.Length;

        for (int i = 1; i <= n / 2; i++)
        {
            if (n % i != 0)
            {
                continue;
            }

            // Get the potential substring pattern
            string pattern = s.Substring(0, i);
            StringBuilder repeated = new StringBuilder();

            // Simply concatenate the pattern multiple times
            for (int j = 0; j < n / i; j++)
            {
                repeated.Append(pattern);
            }

            // Compare the constructed string with the original string
            if (repeated.ToString() == s)
            {
                return true;
            }
        }

        return false;
    }
}
```

## Ruby

```ruby
# @param {String} s
# @return {Boolean}
def repeated_substring_pattern(s)
  (0...s.size / 2).each do |i|
    next unless s.size % (i + 1) == 0

    if s[0..i] * (s.size / (i + 1)) == s
      return true
    end
  end

  false
end
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
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [459. Repeated Substring Pattern - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/459-repeated-substring-pattern) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

