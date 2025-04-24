# 459. Repeated Substring Pattern - LeetCode Python/Java/C++/JS code

Visit original link: [459. Repeated Substring Pattern - LeetCode Python/Java/C++/JS code](https://leetcodepython.com/en/leetcode/459-repeated-substring-pattern) for a better experience!

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
  n = s.length

  (1..n / 2).each do |i|
    next unless n % i == 0
    
    pattern = s[0...i]
    repeated = ""
    
    # Simply concatenate the pattern multiple times
    (0...(n / i)).each do
      repeated += pattern
    end
    
    # Compare the constructed string with the original string
    return true if repeated == s
  end

  false
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCodePython.com](https://leetcodepython.com): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [459. Repeated Substring Pattern - LeetCode Python/Java/C++/JS code](https://leetcodepython.com/en/leetcode/459-repeated-substring-pattern).

GitHub repository: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

