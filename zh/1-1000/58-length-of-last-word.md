# 58. 最后一个单词的长度 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

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

访问原文链接：[58. 最后一个单词的长度 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/58-length-of-last-word)，体验更佳！

力扣链接：[58. 最后一个单词的长度](https://leetcode.cn/problems/length-of-last-word), 难度等级：**简单**。

## LeetCode “58. 最后一个单词的长度”问题描述

给你一个字符串 `s`，由若干单词组成，单词前后用一些空格字符隔开。返回字符串中 **最后一个** 单词的长度。

**单词** 是指仅由字母组成、不包含任何空格字符的最大子字符串。

### [示例 1]

**输入**: `s = "Hello World"`

**输出**: `5`

**解释**: `最后一个单词是“World”，长度为 5。`

### [示例 2]

**输入**: `s = "   fly me   to   the moon  "`

**输出**: `4`

**解释**: `最后一个单词是“moon”，长度为 4。`

### [示例 3]

**输入**: `s = "luffy is still joyboy"`

**输出**: `6`

**解释**: `最后一个单词是长度为 6 的“joyboy”。`

### [约束]

- `1 <= s.length <= 10^4`
- `s` 仅有英文字母和空格 `' '` 组成
- `s` 中至少存在一个单词

## 思路

- 求最后一个单词的长度，我们可以用 `split()`, `last()`, `len()` 这样的方法。
- 不过这种题目其实是想考察程序员对 `index` 的控制能力。
- 最后一个单词在最后，如果从前向后求解，并不是很方便。有什么其它方法吗？

<details><summary>点击查看答案</summary><p>
可以直接从后往前求解。只要考虑两种情况：当前字符是空还是非空。
起初，如果看到空字符就处理下一个字符，看到非空字符length就加1。
如果length > 0，说明之间已经遇到字符了，这时，如果当前字符是空，就可以返回结果了。
</p></details>

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `1`.

## Python

```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        length = 0
    
        for i in range(len(s) - 1, -1, -1):
            if s[i] == " ":
                if length > 0:
                    return length
                continue
            
            length += 1
                
        return length
```

## Ruby

```ruby
# @param {String} s
# @return {Integer}
def length_of_last_word(s)
  length = 0

  (s.size - 1).downto(0) do |i|
    if s[i] == " "
      return length if length > 0
      next
    end

    length += 1
  end

  length
end
```

## Java

```java
class Solution {
    public int lengthOfLastWord(String s) {
        int length = 0;
    
        for (int i = s.length() - 1; i >= 0; i--) {
            if (s.charAt(i) == ' ') {
                if (length > 0) {
                    return length;
                }
                continue;
            }
            
            length++;
        }
        
        return length;
    }
}

```

## C++

```cpp
class Solution {
public:
    int lengthOfLastWord(string s) {
        int length = 0;
        int n = s.size();

        for (int i = n - 1; i >= 0; i--) {
            if (s[i] == ' ') {
                if (length > 0) {
                    return length;
                }
                continue;
            }

            length++;
        }

        return length;
    }
};
```

## C#

```csharp
public class Solution {
    public int LengthOfLastWord(string s) {
        int length = 0;

        for (int i = s.Length - 1; i >= 0; i--) {
            if (s[i] == ' ') {
                if (length > 0) {
                    return length;
                }
                continue;
            }

            length++;
        }

        return length;
    }
}

```

## JavaScript

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLastWord = function (s) {
    let length = 0;

    for (let i = s.length - 1; i >= 0; i--) {
        if (s[i] === " ") {
            if (length > 0) {
                return length;
            }
            continue;
        }

        length++;
    }

    return length;
};


```

## Go

```go
func lengthOfLastWord(s string) int {
    length := 0
    
    for i := len(s) - 1; i >= 0; i-- {
        if s[i] == ' ' {
            if length > 0 {
                return length
            }
            continue
        }
        
        length++
    }
    
    return length
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
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[58. 最后一个单词的长度 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/58-length-of-last-word)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

