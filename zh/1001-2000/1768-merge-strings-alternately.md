# 1768. 交替合并字符串 - LeetCode Python/Java/C++ 题解

访问原文链接：[1768. 交替合并字符串 - LeetCode Python/Java/C++ 题解](https://leetcode.blog/zh/leetcode/1768-merge-strings-alternately)，体验更佳！

力扣链接：[1768. 交替合并字符串](https://leetcode.cn/problems/merge-strings-alternately), 难度等级：**简单**。

## LeetCode “1768. 交替合并字符串”问题描述

给你两个字符串 `word1` 和 `word2` 。请你从 `word1` 开始，通过交替添加字母来合并字符串。如果一个字符串比另一个字符串长，就将多出来的字母追加到合并后字符串的末尾。

返回 **合并后的字符串** 。

### [示例 1]

**输入**: `word1 = "abc", word2 = "pqr"`

**输出**: `"apbqcr"`

**解释**: 

<div class="highlight"><pre class="highlight plaintext"><code>The merged string will be merged as so:
word1:  a   b   c
word2:    p   q   r
merged: a p b q c r
</code></pre></div>

### [示例 2]

**输入**: `word1 = "ab", word2 = "pqrs"`

**输出**: `"apbqrs"`

**解释**: 

<div class="highlight"><pre class="highlight plaintext"><code>Notice that as word2 is longer, "rs" is appended to the end.
word1:  a   b 
word2:    p   q   r   s
merged: a p b q   r   s
</code></pre></div>

### [示例 3]

**输入**: `word1 = "abcd", word2 = "pq"`

**输出**: `"apbqcd"`

**解释**: 

<div class="highlight"><pre class="highlight plaintext"><code>Notice that as word1 is longer, "cd" is appended to the end.
word1:  a   b   c   d
word2:    p   q 
merged: a p b q c   d
</code></pre></div>

### [约束]

- `1 <= word1.length, word2.length <= 100`
- `word1` 和 `word2` 由小写英文字母组成


### [Hints]

<details>
  <summary>提示 1</summary>
  Use two pointers, one pointer for each string. Alternately choose the character from each pointer, and move the pointer upwards.

  
</details>

## 思路

这个问题要求我们合并两个字符串 `word1` 和 `word2`，方法是交替选取字符，从 `word1` 开始。如果一个字符串比另一个长，那么较长字符串中多余的字符应该追加到合并结果的末尾。

核心思路是同时遍历两个字符串，从 `word1` 中取一个字符，然后从 `word2` 中取一个字符，并将它们添加到我们的结果中。只要两个字符串中都还有可用的字符，这个过程就会继续。

一旦较短字符串的字符用完，我们就简单地从较长字符串中取出所有剩余的字符，并将它们追加到我们的结果中。

## 步骤

1.  初始化一个空字符串（或字符列表、字符串构建器）来存储合并后的结果。
2.  确定 `word1` 和 `word2` 的长度。设它们分别为 `n1` 和 `n2`。
3.  找出这两个长度中的较小值，称其为 `min_len = min(n1, n2)`。这个 `min_len` 是我们可以从两个字符串中交替选取的字符数。
4.  从 `i = 0` 迭代到 `min_len - 1`：
    *   将 `word1` 的第 `i` 个字符追加到结果中。
    *   将 `word2` 的第 `i` 个字符追加到结果中。
5.  循环结束后，我们已经处理了两个字符串中的 `min_len` 个字符。
6.  确定哪个字符串可能有多余的字符。设其为 `longer_word`。
    *   如果 `word1` 的长度 (`n1`) 大于 `min_len`，则 `longer_word` 是 `word1`。
    *   否则，`longer_word` 是 `word2`。
7.  将 `longer_word` 的剩余部分（即从索引 `min_len` 开始的 `longer_word`）追加到 `result` 中。8.  返回最终合并的字符串。

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(N)`.

## Python

```python
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        min_size = min(len(word1), len(word2))
        result = ""

        for i in range(min_size):
            result += f'{word1[i]}{word2[i]}'

        longer_word = word1 if len(word1) > min_size else word2

        return result + longer_word[min_size:]
```

## Java

```java
class Solution {
    public String mergeAlternately(String word1, String word2) {
        int minSize = Math.min(word1.length(), word2.length());
        StringBuilder result = new StringBuilder();

        for (int i = 0; i < minSize; i++) {
            result.append(word1.charAt(i)).append(word2.charAt(i));
        }

        String longerWord = (word1.length() > word2.length()) ? word1 : word2;
        result.append(longerWord.substring(minSize));

        return result.toString();
    }
}
```

## C++

```cpp
class Solution {
public:
    string mergeAlternately(string word1, string word2) {
        int min_size = min(word1.length(), word2.length());
        string result;

        for (int i = 0; i < min_size; ++i) {
            result += word1[i];
            result += word2[i];
        }

        auto& longer_word = (word1.length() > min_size) ? word1 : word2;
        result += longer_word.substr(min_size);

        return result;
    }
};
```

## JavaScript

```javascript
var mergeAlternately = function(word1, word2) {
  const minSize = Math.min(word1.length, word2.length);
  let result = "";

  for (let i = 0; i < minSize; i++) {
    result += word1[i] + word2[i];
  }

  const longerWord = word1.length > word2.length ? word1 : word2;
  result += longerWord.slice(minSize);

  return result;
};
```

## Go

```go
func mergeAlternately(word1, word2 string) string {
	minSize := int(math.Min(float64(len(word1)), float64(len(word2))))
	var result strings.Builder

	for i := 0; i < minSize; i++ {
		result.WriteByte(word1[i])
		result.WriteByte(word2[i])
	}

	longerWord := word1
	if len(word2) > len(word1) {
		longerWord = word2
	}
	result.WriteString(longerWord[minSize:])

	return result.String()
}
```

## C#

```csharp
public class Solution
{
    public string MergeAlternately(string word1, string word2)
    {
        int minSize = Math.Min(word1.Length, word2.Length);
        var result = new StringBuilder();

        for (int i = 0; i < minSize; i++)
            result.Append(word1[i]).Append(word2[i]);

        string longerWord = word1.Length > word2.Length ? word1 : word2;
        result.Append(longerWord.Substring(minSize));

        return result.ToString();
    }
}
```

## Ruby

```ruby
def merge_alternately(word1, word2)
  min_size = [ word1.size, word2.size ].min
  result = ""

  min_size.times { |i| result << word1[i] << word2[i] }

  longer_word = word1.size > word2.size ? word1 : word2
  result << longer_word[min_size..]

  result
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.blog](https://leetcode.blog/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[1768. 交替合并字符串 - LeetCode Python/Java/C++ 题解](https://leetcode.blog/zh/leetcode/1768-merge-strings-alternately).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

