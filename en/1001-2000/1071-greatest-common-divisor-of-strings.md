# 1071. Greatest Common Divisor of Strings - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

Visit original link: [1071. Greatest Common Divisor of Strings - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/1071-greatest-common-divisor-of-strings) for a better experience!

LeetCode link: [1071. Greatest Common Divisor of Strings](https://leetcode.com/problems/greatest-common-divisor-of-strings), difficulty: **Easy**.

## LeetCode description of "1071. Greatest Common Divisor of Strings"

For two strings `s` and `t`, we say "`t` divides `s`" if and only if `s = t + t + t + ... + t + t` (i.e., `t` is concatenated with itself one or more times).

Given two strings `str1` and `str2`, return the **largest string** `x` such that `x` divides both `str1` and `str2`.

### [Example 1]

**Input**: `str1 = "ABCABC", str2 = "ABC"`

**Output**: `"ABC"`

### [Example 2]

**Input**: `str1 = "ABABAB", str2 = "ABAB"`

**Output**: `"AB"`

### [Example 3]

**Input**: `str1 = "LEET", str2 = "CODE"`

**Output**: `""`

### [Constraints]

- `1 <= str1.length, str2.length <= 1000`
- `str1` and `str2` consist of English uppercase letters.

### [Hints]

<details>
  <summary>Hint 1</summary>
  The greatest common divisor must be a prefix of each string, so we can try all prefixes.

  
</details>

## Intuition

The greatest common divisor must be a prefix of each string, so we can try all prefixes.

Enumerate all possible prefixes and check whether repeating the prefix several times can form the original strings.

Return the longest one that satisfies the condition.


## Step-by-Step Solution

1. Get the minimum length `min_size` of the two strings.
2. For length `i` from `1` to `min_size`, enumerate the prefix `candidate`.
3. If the length of `candidate` can divide both `str1` and `str2`, and repeating `candidate` the corresponding times equals `str1` and `str2`, update the result.
4. Finally, return the longest valid `candidate`.

## Complexity

- Time complexity: `O(N * (N + M))`.
- Space complexity: `O(N)`.

## Python

```python
class Solution:
    def gcdOfStrings(self, str1: str, str2: str) -> str:
        result = ""
        min_size = min(len(str1), len(str2))

        for i in range(1, min_size + 1):
            if len(str1) % i == 0 and len(str2) % i == 0:
                candidate = str1[:i]

                if candidate * (len(str1) // i) == str1 and candidate * (len(str2) // i) == str2:
                    result = candidate

        return result
```

## Java

```java
class Solution {
    public String gcdOfStrings(String str1, String str2) {
        String result = "";
        int minSize = Math.min(str1.length(), str2.length());

        for (int i = 1; i <= minSize; i++) {
            if (str1.length() % i == 0 && str2.length() % i == 0) {
                String candidate = str1.substring(0, i);
                if (isValid(candidate, str1) && isValid(candidate, str2)) {
                    result = candidate;
                }
            }
        }
        
        return result;
    }

    private boolean isValid(String candidate, String s) {
        int count = s.length() / candidate.length();
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < count; i++) {
            sb.append(candidate);
        }
        return sb.toString().equals(s);
    }
}
```

## C++

```cpp
class Solution {
public:
    string gcdOfStrings(string str1, string str2) {
        string result;
        int min_size = min(str1.size(), str2.size());

        for (int i = 1; i <= min_size; i++) {
            if (str1.size() % i == 0 && str2.size() % i == 0) {
                string candidate = str1.substr(0, i);
                if (isValid(candidate, str1) && isValid(candidate, str2)) {
                    result = candidate;
                }
            }
        }

        return result;
    }

private:
    bool isValid(const string& candidate, const string& s) {
        int count = s.size() / candidate.size();
        string temp;
        for (int i = 0; i < count; i++) {
            temp += candidate;
        }
        return temp == s;
    }
};
```

## C#

```csharp
public class Solution
{
    public string GcdOfStrings(string str1, string str2)
    {
        string result = "";
        int minSize = Math.Min(str1.Length, str2.Length);

        for (int i = 1; i <= minSize; i++)
        {
            if (str1.Length % i == 0 && str2.Length % i == 0)
            {
                string candidate = str1.Substring(0, i);
                if (IsValid(candidate, str1) && IsValid(candidate, str2))
                {
                    result = candidate;
                }
            }
        }
        
        return result;
    }
    
    private bool IsValid(string candidate, string s)
    {
        return string.Concat(Enumerable.Repeat(candidate, s.Length / candidate.Length)) == s;
    }
}
```

## JavaScript

```javascript
var gcdOfStrings = function (str1, str2) {
  let result = "";
  const minSize = Math.min(str1.length, str2.length);

  const isValid = (candidate, s) => {
    return candidate.repeat(s.length / candidate.length) === s;
  };

  for (let i = 1; i <= minSize; i++) {
    if (str1.length % i === 0 && str2.length % i === 0) {
      const candidate = str1.substring(0, i);
      if (isValid(candidate, str1) && isValid(candidate, str2)) {
        result = candidate;
      }
    }
  }

  return result;
}

```

## Go

```go
func gcdOfStrings(str1 string, str2 string) string {
    result := ""
    minSize := len(str1)
    if len(str2) < minSize {
        minSize = len(str2)
    }

    for i := 1; i <= minSize; i++ {
        if len(str1) % i == 0 && len(str2) % i == 0 {
            candidate := str1[:i]
            if isValid(candidate, str1) && isValid(candidate, str2) {
                result = candidate
            }
        }
    }

    return result
}

func isValid(candidate, s string) bool {
    return strings.Repeat(candidate, len(s)/len(candidate)) == s
}
```

## Ruby

```ruby
def gcd_of_strings(str1, str2)
  result = ""
  min_size = [ str1.size, str2.size ].min

  (1..min_size).each do |i|
    next unless (str1.size % i).zero? && (str2.size % i).zero?

    candidate = str1[0...i]
    next unless candidate * (str1.size / i) == str1
    next unless candidate * (str2.size / i) == str2

    result = candidate
  end

  result
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCode.blog](https://leetcode.blog): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [1071. Greatest Common Divisor of Strings - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/1071-greatest-common-divisor-of-strings).

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).
