# 28. 找出字符串中第一个匹配项的下标 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[28. 找出字符串中第一个匹配项的下标 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/28-find-the-index-of-the-first-occurrence-in-a-string)，体验更佳！

力扣链接：[28. 找出字符串中第一个匹配项的下标](https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string), 难度等级：**简单**。

## LeetCode “28. 找出字符串中第一个匹配项的下标”问题描述

给你两个字符串 `haystack` 和 `needle` ，请你在 `haystack` 字符串中找出 `needle` 字符串的第一个匹配项的下标（下标从 `0` 开始）。如果 `needle` 不是 `haystack` 的一部分，则返回 `-1` 。

### [示例 1]

**输入**: `haystack = "sadbutsad", needle = "sad"`

**输出**: `0`

**解释**: `"sad" 在下标 0 和 6 处匹配。
第一个匹配项的下标是 0 ，所以返回 0 。`

### [示例 2]

**输入**: `haystack = "leetcode", needle = "leeto"`

**输出**: `-1`

**解释**: `"leeto" 没有在 "leetcode" 中出现，所以返回 -1 。`

### [约束]

- `1 <= haystack.length, needle.length <= 10^4`
- `haystack` 和 `needle` 仅由小写英文字符组成

## 思路

- 这样的题目，如果用内置的`index()`，一行代码就可以实现。显然，出题人是想考察我们对循环的控制能力。
- 针对 `heystack`，依次遍历每个字符。如果从当前字符开始到`needle`长度的子串与`needle`相同，则返回当前字符的位置。

- 本题直接看代码比较容易理解。

## 复杂度

- 时间复杂度: `O(N * M)`.
- 空间复杂度: `O(1)`.

## Python

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        n = len(haystack)
        m = len(needle)
        
        for i in range(n - m + 1):
            if haystack[i:i + m] == needle:
                return i
        
        return -1
```

## JavaScript

```javascript
/**
 * @param {string} haystack
 * @param {string} needle
 * @return {number}
 */
var strStr = function(haystack, needle) {
  const n = haystack.length;
  const m = needle.length;
    
  for (let i = 0; i <= n - m; i++) {
    if (haystack.substring(i, i + m) === needle) {
      return i;
    }
  }
    
  return -1;
};

```

## Ruby

```ruby
# @param {String} haystack
# @param {String} needle
# @return {Integer}
def str_str(haystack, needle)
  (0..haystack.size - needle.size).each do |i|
    if haystack[i...i + needle.size] == needle
      return i  
    end
  end

  -1
end
```

## C++

```cpp
class Solution {
public:
    int strStr(string haystack, string needle) {
        for (int i = 0; i < haystack.length(); i++) {
            int j = 0;
            
            while (i + j < haystack.length() && haystack[i + j] == needle[j]) {
                j++;
                
                if (j == needle.length()) {
                    return i;
                }
            }
        }
        
        return -1;
    }
};
```

## Java

```java
class Solution {
    public int strStr(String haystack, String needle) {
        for (int i = 0; i < haystack.length(); i++) {
            int j = 0;

            while (i + j < haystack.length() && haystack.charAt(i + j) == needle.charAt(j)) {
                j++;

                if (j == needle.length()) {
                    return i;
                }
            }
        }

        return -1;
    }
}
```

## Go

```go
func strStr(haystack string, needle string) int {
    for i := 0; i < len(haystack); i++ {
        j := 0

        for i+j < len(haystack) && haystack[i+j] == needle[j] {
            j++

            if j == len(needle) {
                return i
            }
        }
    }

    return -1
}
```

## C#

```csharp
public class Solution {
    public int StrStr(string haystack, string needle) {
        for (int i = 0; i < haystack.Length; i++) {
            int j = 0;

            while (i + j < haystack.Length && haystack[i + j] == needle[j]) {
                j++;

                if (j == needle.Length) {
                    return i;
                }
            }
        }

        return -1;
    }
}
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

访问原文链接：[28. 找出字符串中第一个匹配项的下标 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/28-find-the-index-of-the-first-occurrence-in-a-string)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

