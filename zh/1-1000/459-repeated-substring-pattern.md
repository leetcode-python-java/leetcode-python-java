# 459. 重复的子字符串 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **进阶你的开发者身份**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **专业简历 (Resume)：** 告别平庸，生成一份令猎头和面试官眼前一亮的动态技术简历。
> - 🎨 **作品集 (Portfolio)：** 自动聚合 GitHub 贡献与项目经历，将枯燥的代码转化为极具冲击力的视觉作品集。
> - ✍️ **技术博客 (Blog)：** 在纯净、专注的写作空间分享技术见解，树立你的行业影响力。
>
> [**立即前往 Show.dev 打造你的专属品牌 →**](https://www.show.dev)

---

访问原文链接：[459. 重复的子字符串 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/459-repeated-substring-pattern)，体验更佳！

力扣链接：[459. 重复的子字符串](https://leetcode.cn/problems/repeated-substring-pattern), 难度等级：**简单**。

## LeetCode “459. 重复的子字符串”问题描述

给定一个非空的字符串 `s` ，检查是否可以通过由它的一个子串重复多次构成。

### [示例 1]

**输入**: `s = "abcabcabcabc"`

**输出**: `true`

**解释**: `可由子串 "abc" 重复四次构成。 (或子串 "abcabc" 重复两次构成。)`

### [示例 2]

**输入**: `s = "aba"`

**输出**: `false`

### [约束]

- `1 <= s.length <= 10000`
- `s` consists of lowercase English letters.

## 思路

解决本问题的关键是要看清楚一点：通过子串的重复能得到`s`，那么子串的起始字母一定是`s[0]`。
想明白了这一点，子串的排查范围就大大缩小了。

## 复杂度

- 时间复杂度: `O(N * N)`.
- 空间复杂度: `O(N)`.

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

> 🚀 **进阶你的开发者身份**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **专业简历 (Resume)：** 告别平庸，生成一份令猎头和面试官眼前一亮的动态技术简历。
> - 🎨 **作品集 (Portfolio)：** 自动聚合 GitHub 贡献与项目经历，将枯燥的代码转化为极具冲击力的视觉作品集。
> - ✍️ **技术博客 (Blog)：** 在纯净、专注的写作空间分享技术见解，树立你的行业影响力。
>
> [**立即前往 Show.dev 打造你的专属品牌 →**](https://www.show.dev)

---

访问原文链接：[459. 重复的子字符串 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/459-repeated-substring-pattern)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

