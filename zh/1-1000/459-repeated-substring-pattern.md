# 459. 重复的子字符串 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[459. 重复的子字符串 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/459-repeated-substring-pattern)，体验更佳！

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

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**leader.me**](https://www.leader.me) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.leader.me`，极具职业含金量的专属域名。

>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[459. 重复的子字符串 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/459-repeated-substring-pattern)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

