# 345. 反转字符串中的元音字母 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

访问原文链接：[345. 反转字符串中的元音字母 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.to/zh/leetcode/345-reverse-vowels-of-a-string)，体验更佳！

力扣链接：[345. 反转字符串中的元音字母](https://leetcode.cn/problems/reverse-vowels-of-a-string), 难度等级：**简单**。

## LeetCode “345. 反转字符串中的元音字母”问题描述

给你一个字符串 `s` ，仅反转字符串中的所有元音字母，并返回结果字符串。

元音字母包括 `'a'`, `'e'`, `'i'`, `'o'`, `'u'`，且可能以大小写两种形式出现不止一次。

### [示例 1]

**输入**: `s = "IceCreAm"`

**输出**: `"AceCreIm"`

**解释**: 

<p><code>s</code> 中的元音是 <code>[&#39;I&#39;, &#39;e&#39;, &#39;e&#39;, &#39;A&#39;]</code>。反转这些元音，<code>s</code> 变为 <code>&quot;AceCreIm&quot;</code>.</p>


### [示例 2]

**输入**: `"leetcode"`

**输出**: `"leotcede"`

### [约束]

- `1 <= s.length <= 3 * 10^5`
- `s` 由 **可打印的 ASCII** 字符组成

## 思路

双指针交换字符串中的元音字母。左指针从左找元音，右指针从右找元音，找到后交换，直到指针相遇。

## “左右双指针”的模式

代码框架如下：

```java
int r = target.length() - 1;

for (int l = 0; l < target.length(); l++) { // Important
    // ...
    if (l >= r) {
        break;
    }

    // ...
    r--;
}
```

## 步骤

1. 初始化元音集合
2. 某些语言，需要将字符串转字符数组（因字符串不可变） 
3. 左指针`l`从`0`开始，右指针`r`从末尾开始
4. 循环处理：
    - `l`右移直到找到元音
    - `r`左移直到找到元音
    - 当`l < r`时交换这两个元音
5. 返回处理后的字符串

## 复杂度

> 如果转换为字符数组，空间复杂度为 O(N)。

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1) or O(N)`.

## Python

```python
class Solution:
    def reverseVowels(self, s: str) -> str:
        vowels = ['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U']
        s = list(s)
        r = len(s) - 1

        for l in range(len(s)): # Important
            if s[l] not in vowels:
                continue

            while r > 0 and s[r] not in vowels:
                r -= 1

            if l >= r:
                break

            s[l], s[r] = s[r], s[l]
            r -= 1

        return ''.join(s)
```

## Java

```java
class Solution {
    public String reverseVowels(String s) {
        var vowels = new HashSet<>(Arrays.asList('a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'));
        var chars = s.toCharArray();
        int r = chars.length - 1;

        for (int l = 0; l < chars.length; l++) { // important
            if (!vowels.contains(chars[l])) {
                continue;
            }

            while (r > 0 && !vowels.contains(chars[r])) {
                r--;
            }

            if (l >= r) {
                break;
            }

            // Swap the vowels
            char temp = chars[l];
            chars[l] = chars[r];
            chars[r] = temp;
            r--;
        }

        return new String(chars);
    }
}
```

## C++

```cpp
class Solution {
public:
    string reverseVowels(string s) {
        unordered_set<char> vowels = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};
        int r = s.size() - 1;

        for (int l = 0; l < s.size(); l++) { // important
            if (!vowels.contains(s[l])) {
                continue;
            }

            while (r > 0 && !vowels.contains(s[r])) {
                r--;
            }

            if (l >= r) {
                break;
            }

            swap(s[l], s[r]);
            r--;
        }

        return s;
    }
};
```

## JavaScript

```javascript
var reverseVowels = function (s) {
  const vowels = new Set(['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'])
  const chars = s.split('')
  let r = chars.length - 1

  for (let l = 0; l < chars.length; l++) { // important
    if (!vowels.has(chars[l])) {
      continue
    }

    while (r > 0 && !vowels.has(chars[r])) {
      r--
    }

    if (l >= r) {
      break
    }

    [chars[l], chars[r]] = [chars[r], chars[l]]
    r--
  }

  return chars.join('')
};
```

## Ruby

```ruby
def reverse_vowels(s)
  vowels = Set.new(['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'])
  r = s.size - 1

  (0...s.size).each do |l|
    unless vowels.include?(s[l])
      next
    end

    while r > 0 && !vowels.include?(s[r])
      r -= 1
    end

    if l >= r
      break
    end

    s[l], s[r] = s[r], s[l]
    r -= 1
  end

  s
end
```

## C#

```csharp
public class Solution
{
    public string ReverseVowels(string s)
    {
        var vowels = new HashSet<char> {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};
        var chars = s.ToCharArray();
        int r = chars.Length - 1;
        // important
        for (int l = 0; l < chars.Length; l++)
        {
            if (!vowels.Contains(chars[l]))
            {
                continue;
            }

            while (r > 0 && !vowels.Contains(chars[r]))
            {
                r--;
            }

            if (l >= r)
            {
                break;
            }

            (chars[l], chars[r]) = (chars[r], chars[l]);
            r--;
        }

        return new string(chars);
    }
}
```

## Go

```go
func reverseVowels(s string) string {
    vowels := map[byte]bool{
        'a': true, 'e': true, 'i': true, 'o': true, 'u': true,
        'A': true, 'E': true, 'I': true, 'O': true, 'U': true,
    }
    chars := []byte(s)
    r := len(chars) - 1

    for l := 0; l < len(chars); l++ { // important
        if !vowels[chars[l]] {
            continue
        }

        for r > 0 && !vowels[chars[r]] {
            r--
        }

        if l >= r {
            break
        }

        chars[l], chars[r] = chars[r], chars[l]
        r--
    }

    return string(chars)
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.to](https://leetcode.to/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[345. 反转字符串中的元音字母 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.to/zh/leetcode/345-reverse-vowels-of-a-string).

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

