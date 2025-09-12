# 541. Reverse String II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

Visit original link: [541. Reverse String II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.to/en/leetcode/541-reverse-string-ii) for a better experience!

LeetCode link: [541. Reverse String II](https://leetcode.com/problems/reverse-string-ii), difficulty: **Easy**.

## LeetCode description of "541. Reverse String II"

Given a string `s` and an integer `k`, reverse the first `k` characters for every `2k` characters counting from the start of the string.

- If there are fewer than `k` characters left, reverse all of them.
- If there are less than `2k` but greater than or equal to `k` characters, then reverse the first `k` characters and leave the other as original.

### [Example 1]

**Input**: `s = "abcdefg", k = 2`

**Output**: `bacdfeg`

### [Example 2]

**Input**: `s = "abcd", k = 2`

**Output**: `bacd`

### [Constraints]

- `1 <= s.length <= 10000`
- `s` consists of only lowercase English letters.
- `1 <= k <= 10000`

## Intuition

1. The question does not require `reverse in place`, so using a new string `result` as the return value is easier to operate.
2. In the loop, it is more convenient to use `k` as the step value rather than `2k`, because if `2k` is used, `k` must still be used for judgment.
3. It is required to reverse only the first `k` characters of each `2k` characters, so a `boolean` variable `should_reverse` is needed as a judgment condition for whether to reverse.

## Step-by-Step Solution

1. Use a new string `result` as the return value. In the loop, the step value is `k`.

    ```ruby
    result = ''
    index = 0
    
    while index < s.size
      k_chars = s[index...index + k]
      result += k_chars
      index += k
    end
    
    return result
    ```

2. Use the Boolean variable `should_reverse` as the judgment condition for whether to reverse, and only reverse the first `k` characters of each `2k` characters.

    ```ruby
    result = ''
    should_reverse = true # 1
    index = 0
    
    while index < s.size
      k_chars = s[index...index + k]
    
      if should_reverse # 2
        result += k_chars.reverse # 3
      else # 4
        result += k_chars
      end
    
      index += k
      should_reverse = !should_reverse # 5
    end
    
    return result
    ```

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(N)`.

## Python

```python
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        result = ''
        should_reverse = True
        index = 0

        while index < len(s):
            k_chars = s[index:index + k]

            if should_reverse:
                result += k_chars[::-1]
            else:
                result += k_chars

            index += k
            should_reverse = not should_reverse

        return result
```

## Java

```java
class Solution {
    public String reverseStr(String s, int k) {
        var result = new StringBuffer();
        var shouldReverse = true;
        var index = 0;

        while (index < s.length()) {
            var kChars = s.substring(index, Math.min(index + k, s.length()));

            if (shouldReverse) {
                result.append(new StringBuffer(kChars).reverse());
            } else {
                result.append(kChars);
            }

            index += k;
            shouldReverse = !shouldReverse;
        }

        return result.toString();
    }
}
```

## JavaScript

```javascript
var reverseStr = function (s, k) {
  let result = ''
  let shouldReverse = true
  let index = 0

  while (index < s.length) {
    const kChars = s.substr(index, k)

    if (shouldReverse) {
      result += [...kChars].reverse().join('')
    } else {
      result += kChars
    }

    index += k
    shouldReverse = !shouldReverse
  }

  return result
};
```

## C#

```csharp
public class Solution
{
    public string ReverseStr(string s, int k)
    {
        string result = "";
        bool shouldReverse = true;
        int index = 0;

        while (index < s.Length)
        {
            string kChars = s[index..Math.Min(index + k, s.Length)];

            if (shouldReverse)
            {
                result += new string(kChars.Reverse().ToArray());
            }
            else
            {
                result += kChars;
            }

            index += k;
            shouldReverse = !shouldReverse;
        }

        return result;
    }
}
```

## Ruby

```ruby
def reverse_str(s, k)
  result = ''
  should_reverse = true
  index = 0

  while index < s.size
    k_chars = s[index...index + k]

    if should_reverse
      result += k_chars.reverse
    else
      result += k_chars
    end

    index += k
    should_reverse = !should_reverse
  end

  result
end
```

## C++

```cpp
class Solution {
public:
    string reverseStr(string s, int k) {
        string result = "";
        bool shouldReverse = true;
        int index = 0;

        while (index < s.length()) {
            auto kChars = s.substr(index, k);

            if (shouldReverse) {
                reverse(kChars.begin(), kChars.end());
            }

            result += kChars;
            index += k;
            shouldReverse = !shouldReverse;
        }

        return result;
    }
};
```

## Go

```go
func reverseStr(s string, k int) string {
    var result []rune
    shouldReverse := true
    index := 0

    for index < len(s) {
        end := index + k
        if end > len(s) {
            end = len(s)
        }
        kChars := []rune(s[index:end])

        if shouldReverse {
            for i, j := 0, len(kChars) - 1; i < j; i, j = i + 1, j - 1 {
                kChars[i], kChars[j] = kChars[j], kChars[i]
            }
        }

        result = append(result, kChars...)
        index += k
        shouldReverse = !shouldReverse
    }

    return string(result)
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCode.to](https://leetcode.to): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [541. Reverse String II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.to/en/leetcode/541-reverse-string-ii).

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).
