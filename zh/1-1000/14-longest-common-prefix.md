# 14. 最长公共前缀 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[14. 最长公共前缀 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/14-longest-common-prefix)，体验更佳！

力扣链接：[14. 最长公共前缀](https://leetcode.cn/problems/longest-common-prefix), 难度等级：**简单**。

## LeetCode “14. 最长公共前缀”问题描述

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 `""`。

### [示例 1]

**输入**: `strs = ["flower","flow","flight"]`

**输出**: `"fl"`

### [示例 2]

**输入**: `strs = ["dog","racecar","car"]`

**输出**: `""`

**解释**: `输入不存在公共前缀。`

### [约束]

- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` 如果非空，则仅由小写英文字母组成

## 思路

1. 查找最长公共前缀，可以从左向右，以第一个字符串的字符为基准。
1. 如果后面的字符串的当前字符不等于基准字符，则返回结果。每一轮循环下来，都把基准字符加入到公共前缀中。

## 复杂度

- 时间复杂度: `O(M * N)`.
- 空间复杂度: `O(1)`.

## Ruby

```ruby
# @param {String[]} strs
# @return {String}
def longest_common_prefix(strs)
  result = ''

  (0...strs[0].size).each do |i|
    char = strs[0][i]

    strs[1..].each do |str|
      if str[i] != char
        return result
      end
    end

    result << char
  end

  result
end

```

## Python

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        result = ''

        for i in range(len(strs[0])):
            char = strs[0][i]

            for string in strs[1:]:
                if i >= len(string) or string[i] != char:
                    return result

            result += char

        return result
```

## Java

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        var result = "";

        for (var i = 0; i < strs[0].length(); i++) {
            var c = strs[0].charAt(i);
            
            for (var j = 1; j < strs.length; j++) {
                if (i >= strs[j].length() || strs[j].charAt(i) != c) {
                    return result;
                }
            }
            
            result += c;
        }

        return result;
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

访问原文链接：[14. 最长公共前缀 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/14-longest-common-prefix)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

