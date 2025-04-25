# 28. 找出字符串中第一个匹配项的下标 - LeetCode Python/Java/C++ 题解

访问原文链接：[28. 找出字符串中第一个匹配项的下标 - LeetCode Python/Java/C++ 题解](https://leetcodepython.com/zh/leetcode/28-find-the-index-of-the-first-occurrence-in-a-string)，体验更佳！

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
- 针对 `heystack`，依次遍历每个字符。可能出现两种情况：
	1. 该字符与`needle`的首字母不相等。这时处理下一个字符。
	2. 该字符与`needle`的首字母相等，则在一个内部循环中继续比较继续比较`heystack`和`needle`的下一个字符，直到不相等或者`needle`已经完全匹配。

- 本题直接看代码比较容易理解。

## 复杂度

- 时间复杂度: `O(N + M)`.
- 空间复杂度: `O(1)`.

## Python

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        for i in range(len(haystack)):
            j = 0
            
            while i + j < len(haystack) and haystack[i + j] == needle[j]:
                j += 1

                if j == len(needle):
                    return i

        return -1
```

## JavaScript

```javascript
var strStr = function (haystack, needle) {
  for (let i = 0; i < haystack.length; i++) {
    let j = 0
            
    while (i + j < haystack.length && haystack[i + j] == needle[j]) {
        j += 1

        if (j == needle.length) {
            return i
        }
    }
  }

  return -1
};
```

## Ruby

```ruby
# @param {String} haystack
# @param {String} needle
# @return {Integer}
def str_str(haystack, needle)
  (0...haystack.length).each do |i|
    j = 0
    
    while i + j < haystack.length && haystack[i + j] == needle[j]
      j += 1
      
      return i if j == needle.length
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

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCodePython.com](https://leetcodepython.com/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[28. 找出字符串中第一个匹配项的下标 - LeetCode Python/Java/C++ 题解](https://leetcodepython.com/zh/leetcode/28-find-the-index-of-the-first-occurrence-in-a-string).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

