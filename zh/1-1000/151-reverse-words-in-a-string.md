# 151. 反转字符串中的单词 - LeetCode Python/Java/C++ 题解

访问原文链接：[151. 反转字符串中的单词 - LeetCode Python/Java/C++ 题解](https://leetcode.blog/zh/leetcode/151-reverse-words-in-a-string)，体验更佳！

力扣链接：[151. 反转字符串中的单词](https://leetcode.cn/problems/reverse-words-in-a-string), 难度等级：**中等**。

## LeetCode “151. 反转字符串中的单词”问题描述

给你一个字符串 `s` ，请你反转字符串中 **单词** 的顺序。

**单词** 是由非空格字符组成的字符串。`s` 中使用至少一个空格将字符串中的 **单词** 分隔开。

返回 **单词** 顺序颠倒且 **单词** 之间用单个空格连接的结果字符串。

**注意**：输入字符串 `s` 中可能会存在前导空格、尾随空格或者单词间的多个空格。返回的结果字符串中，单词间应当仅用单个空格分隔，且不包含任何额外的空格。

### [示例 1]

**输入**: `s = "the sky is blue"`

**输出**: `"blue is sky the"`

### [示例 2]

**输入**: `s = "  hello world  "`

**输出**: `"world hello"`

### [示例 3]

**输入**: `"a good   example"`

**输出**: `"example good a"`

### [约束]

- `1 <= s.length <= 10^4`
- `s` 包含英文大小写字母、数字和空格 `' '`
- `s` 中 **至少存在一个** 单词

**进阶**：如果字符串在你使用的编程语言中是一种可变数据类型，请尝试使用 `O(1)` 额外空间复杂度的 **原地** 解法。

## 思路

1. 拆分字符串为单词数组（需删除空字符串）
2. 反转单词顺序
3. 用单空格连接单词

## 步骤

1. 用 split(' ') 分割字符串
2. 删除空字符串
3. 对得到的单词数组调用 `reverse` 反转
4. 用 `join(' ')` 合并为最终字符串

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(N)`.

## Python

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        words = [word for word in s.split(' ') if word]
        return ' '.join(words[::-1])
```

## Java

```java
class Solution {
    public String reverseWords(String s) {
        var wordList = new ArrayList<String>();
        var words = s.split(" ");

        for (var word : words) {
            if (!word.isEmpty()) {
                wordList.add(word);
            }
        }

        int left = 0;
        int right = wordList.size() - 1;
        while (left < right) {
            Collections.swap(wordList, left, right);
            left++;
            right--;
        }

        return String.join(" ", wordList);
    }
}
```

## C++

```cpp
class Solution {
public:
    string reverseWords(string s) {
        istringstream iss(s);
        string word;
        vector<string> word_list;

        // 1. Extract words from the string.
        // The istringstream >> operator automatically handles
        // multiple spaces between words and leading/trailing spaces.
        while (iss >> word) {
            word_list.push_back(word);
        }

        reverse(word_list.begin(), word_list.end());

        // 2. Join the words with a single space.
        string result = "";
        result = word_list[0];
        for (auto i = 1; i < word_list.size(); ++i) {
            result += " ";
            result += word_list[i];
        }

        return result;
    }
};

```

## JavaScript

```javascript
var reverseWords = function(s) {
  const words = s.split(' ').filter((word) => word !== '');
  return words.reverse().join(' ');
};
```

## Go

```go
func reverseWords(s string) string {
    words := strings.Fields(s) // Fields splits on whitespace and ignores multiple spaces

    // Reverse the words
    for i, j := 0, len(words) - 1; i < j; {
        words[i], words[j] = words[j], words[i]
        i += 1
        j -= 1
    }

    return strings.Join(words, " ")
}
```

## C#

```csharp
public class Solution {
    public string ReverseWords(string s) {
        // Split into words, remove empty entries, reverse
        var words = s.Split(new[] {' '}, StringSplitOptions.RemoveEmptyEntries).Reverse();
        return string.Join(" ", words);
    }
}
```

## Ruby

```ruby
def reverse_words(s)
  s.split(' ').reject(&:empty?).reverse.join(' ')
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.blog](https://leetcode.blog/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[151. 反转字符串中的单词 - LeetCode Python/Java/C++ 题解](https://leetcode.blog/zh/leetcode/151-reverse-words-in-a-string).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

