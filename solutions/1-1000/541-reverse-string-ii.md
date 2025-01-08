# 541. Reverse String II - LeetCode Solution
LeetCode problem link: [541. Reverse String II](https://leetcode.com/problems/reverse-string-ii),
[541. 反转字符串 II](https://leetcode.cn/problems/reverse-string-ii)

[中文题解](#中文题解)

## LeetCode problem description
Given a string `s` and an integer `k`, reverse the first `k` characters for every `2k` characters counting from the start of the string.

If there are fewer than `k` characters left, reverse all of them. If there are less than `2k` but greater than or equal to `k` characters, then reverse the first `k` characters and leave the other as original.

Difficulty: **Medium**

### [Example 1]
**Input**: `s = "abcdefg", k = 2`

**Output**: `"bacdfeg"`

### [Example 2]
**Input**: `s = "abcd", k = 2`

**Output**: `"bacd"`

### [Constraints]
- `1 <= s.length <= 10000`
- `s` consists of only lowercase English letters.
- `1 <= k <= 10000`

## Intuition behind the Solution
[中文题解](#中文题解)

1. The question does not require `reverse in place`, so using a new string `result` as the return value is easier to operate.
2. In the loop, it is more convenient to use `k` as the step value rather than `2k`, because if `2k` is used, `k` must still be used for judgment.
3. It is required to reverse only the first `k` characters of each `2k` characters, so a `Boolean` variable `should_reverse` is needed as a judgment condition for whether to reverse.

## Approach
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
* Time: `O(n)`.
* Space: `O(n)`.

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

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
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
```c#
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

## Go
```go
// Welcome to create a PR to complete the code of this language, thanks!
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

## C, Kotlin, Swift, Rust or other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```

## 力扣“541. 反转字符串 II”问题描述
力扣链接：[541. 反转字符串 II](https://leetcode.cn/problems/reverse-string-ii), 难度: **简单**。

给定一个字符串 `s` 和一个整数 `k`，从字符串开头算起，每计数至 `2k` 个字符，就反转这 `2k` 字符中的前 `k` 个字符。

* 如果剩余字符少于 `k` 个，则将剩余字符全部反转。

* 如果剩余字符小于 `2k` 但大于或等于 `k` 个，则反转前 `k` 个字符，其余字符保持原样。

### [示例 1]
**输入**: `s = "abcdefg", k = 2`

**输出**: `"bacdfeg"`

# 中文题解
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
