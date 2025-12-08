# 541. 反转字符串 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **进阶你的开发者身份**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/你的名字` 或 `an.dev/你的名字`。
>
> [**立即前往 Show.dev 打造你的专属品牌 →**](https://www.show.dev)

---

访问原文链接：[541. 反转字符串 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/541-reverse-string-ii)，体验更佳！

力扣链接：[541. 反转字符串 II](https://leetcode.cn/problems/reverse-string-ii), 难度等级：**简单**。

## LeetCode “541. 反转字符串 II”问题描述

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

> 🚀 **进阶你的开发者身份**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/你的名字` 或 `an.dev/你的名字`。
>
> [**立即前往 Show.dev 打造你的专属品牌 →**](https://www.show.dev)

---

访问原文链接：[541. 反转字符串 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/541-reverse-string-ii)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

