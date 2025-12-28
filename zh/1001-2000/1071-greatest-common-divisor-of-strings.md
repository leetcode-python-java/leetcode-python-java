# 1071. 字符串的最大公因子 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**leader.me**](https://www.leader.me) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[1071. 字符串的最大公因子 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/1071-greatest-common-divisor-of-strings)，体验更佳！

力扣链接：[1071. 字符串的最大公因子](https://leetcode.cn/problems/greatest-common-divisor-of-strings), 难度等级：**简单**。

## LeetCode “1071. 字符串的最大公因子”问题描述

对于字符串 `s` 和 `t`，只有在 `s = t + t + t + ... + t + t`（`t` 自身连接 `1` 次或多次）时，我们才认定 “`t` 能除尽 `s`”。

给定两个字符串 `str1` 和 `str2` 。返回 最长字符串 `x`，要求满足 `x` 能除尽 `str1` 且 `x` 能除尽 `str2` 。

### [示例 1]

**输入**: `str1 = "ABCABC", str2 = "ABC"`

**输出**: `"ABC"`

### [示例 2]

**输入**: `str1 = "ABABAB", str2 = "ABAB"`

**输出**: `"AB"`

### [示例 3]

**输入**: `str1 = "LEET", str2 = "CODE"`

**输出**: `""`

### [约束]

- `1 <= str1.length, str2.length <= 1000`
- `str1` 和 `str2` 由大写英文字母组成

### [Hints]

<details>
  <summary>提示 1</summary>
  The greatest common divisor must be a prefix of each string, so we can try all prefixes.

  
</details>

## 思路

- 最大公约数一定是每个字符串的前缀，所以我们可以尝试所有前缀。

- 枚举所有可能的前缀，判断该前缀重复若干次后能否等于原字符串。

- 返回最长的那个。

## 步骤

1. 取两个字符串的最小长度 `min_size`。
2. 从长度 `1` 到 `min_size`，依次枚举前缀 `candidate`。
3. 如果 `candidate` 的长度能同时整除 `str1` 和 `str2` 的长度，且 `candidate` 重复相应次数后等于 `str1` 和 `str2`，则更新结果。
4. 最后返回最长的满足条件的 `candidate`。

## 复杂度

- 时间复杂度: `O(N * (N + M))`.
- 空间复杂度: `O(N)`.

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

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**leader.me**](https://www.leader.me) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[1071. 字符串的最大公因子 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/1071-greatest-common-divisor-of-strings)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

