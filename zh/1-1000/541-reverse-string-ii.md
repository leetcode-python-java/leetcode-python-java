# 541. 反转字符串 II - 力扣题解最佳实践

访问原文链接：[541. 反转字符串 II - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/541-reverse-string-ii)，体验更佳！

力扣链接：[541. 反转字符串 II](https://leetcode.cn/problems/reverse-string-ii), 难度：**简单**。

## 力扣“541. 反转字符串 II”问题描述

给定一个字符串 `s` 和一个整数 `k`，从字符串开头算起，每计数至 `2k` 个字符，就反转这 `2k` 字符中的前 `k` 个字符。

- 如果剩余字符少于 `k` 个，则将剩余字符全部反转。
- 如果剩余字符小于 `2k` 但大于或等于 `k` 个，则反转前 `k` 个字符，其余字符保持原样。

### [示例 1]

**输入**: `s = "abcdefg", k = 2`

**输出**: `bacdfeg`

### [示例 2]

**输入**: `s = "abcd", k = 2`

**输出**: `bacd`

### [约束]

- `1 <= s.length <= 10000`
- `s` consists of only lowercase English letters.
- `1 <= k <= 10000`

## 思路

1. 题目没有要求`原地反转`，所以用一个新的字符串`result`作为返回值，操作起来容易些。
2. 在循环中，步进值用`k`比`2k`更方便，因为如果用`2k`，还是要再用`k`做判断。
3. 要求只反转`2k`字符中前`k`个字符，所以需要一个布尔类型变量`should_reverse`作为是否要反转判断条件。

## 步骤

1. 用一个新的字符串`result`作为返回值。在循环中，步进值用`k`。

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

2. 用布尔类型变量`should_reverse`作为是否要反转判断条件，并只反转`2k`字符中前`k`个字符。

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

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(N)`.

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

亲爱的力扣人，为了您更好的刷题体验，请访问 [leetcoder.net](https://leetcoder.net/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[541. 反转字符串 II - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/541-reverse-string-ii).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

