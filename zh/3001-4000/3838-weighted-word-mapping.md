# 3838. 带权单词映射 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 coder.id 打造你的开发者个人IP →**](https://www.coder.id)

访问原文链接：[3838. 带权单词映射 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/3838-weighted-word-mapping)，体验更佳！

力扣链接：[3838. 带权单词映射](https://leetcode.cn/problems/weighted-word-mapping), 难度等级：**中等**。

## LeetCode “3838. 带权单词映射”问题描述

给你一个字符串数组 `words`，其中每个字符串代表一个包含小写英文字母的单词。

你还被提供了一个长度为 26 的整数数组 `weights`，其中 `weights[i]` 代表第 `i` 个小写英文字母的权重。

一个单词的 **权重** 定义为其字符权重的 **总和**。

对于每个单词，将其权重对 26 取模，并使用反向字母表顺序（`0 -> 'z', 1 -> 'y', ..., 25 -> 'a'`）将结果映射为一个字母。

返回按顺序将所有单词映射后的字符拼接形成的字符串。

### [示例 1]

**输入**: `words = ["abcd","def","xyz"], weights = [5,3,12,14,1,2,3,2,10,6,6,9,7,8,7,10,8,9,6,9,9,8,3,7,7,2]`

**输出**: `"rij"`

**解释**: 

<ul>
<li><code>&quot;abcd&quot;</code> 的权重为 <code>5 + 3 + 12 + 14 = 34</code>。对 26 取模的结果为 <code>34 % 26 = 8</code>，映射为 <code>&#39;r&#39;</code>。</li>
<li><code>&quot;def&quot;</code> 的权重为 <code>14 + 1 + 2 = 17</code>。对 26 取模的结果为 <code>17 % 26 = 17</code>，映射为 <code>&#39;i&#39;</code>。</li>
<li><code>&quot;xyz&quot;</code> 的权重为 <code>7 + 7 + 2 = 16</code>。对 26 取模的结果为 <code>16 % 26 = 16</code>，映射为 <code>&#39;j&#39;</code>。</li>
</ul>

<p>因此，将所有映射字符连接成的字符串是 <code>&quot;rij&quot;</code>。</p>


### [示例 2]

**输入**: `words = ["a","b","c"], weights = [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]`

**输出**: `"yyy"`

**解释**: 

<p>每个单词的权重都是 1。对 26 取模的结果为 <code>1 % 26 = 1</code>，映射为 <code>&#39;y&#39;</code>。<br>
因此，将所有映射字符连接成的字符串是 <code>&quot;yyy&quot;</code>。</p>


### [示例 3]

**输入**: `words = ["abcd"], weights = [7,5,3,4,3,5,4,9,4,2,2,7,10,2,5,10,6,1,2,2,4,1,3,4,4,5]`

**输出**: `"g"`

**解释**: 

<p><code>&quot;abcd&quot;</code> 的权重为 <code>7 + 5 + 3 + 4 = 19</code>。对 26 取模的结果为 <code>19 % 26 = 19</code>，映射为 <code>&#39;g&#39;</code>。<br>
因此，将所有映射字符连接成的字符串是 <code>&quot;g&quot;</code>。</p>


### [约束]

- `1 <= words.length <= 100`
- `1 <= words[i].length <= 10`
- `weights.length == 26`
- `1 <= weights[i] <= 100`
- `words[i]` 仅由小写英文字母组成。

### [Hints]

<details>
  <summary>提示 1</summary>
  For each word, sum character weights using `weights[c - 'a']`

  
</details>

<details>
  <summary>提示 2</summary>
  Take the sum modulo `26`

  
</details>

<details>
  <summary>提示 3</summary>
  Map the value to a character using reverse order: `char = 'z' - value`

  
</details>

<details>
  <summary>提示 4</summary>
  Append all mapped characters in order to form the result string

  
</details>

## 思路

这道题是对映射规则的直接模拟。对于给定的 `words` 数组中的每个字符串，我们需要计算它的“权重”。这个权重是单词中所有字符权重的总和，而字符的权重可以通过将其字母索引映射到 `weights` 数组来确定。

算出总和后，我们对 26 取模。最后，我们使用反向字母表顺序将这个结果值映射为一个字符，在数学上这正好等同于从 `'z'` 的 ASCII 码中减去该值，然后再转换回字符。我们将所有单词对应的结果字符拼接起来并返回最终的字符串。

## 步骤

1. 初始化一个空列表或字符串构建器，用于收集映射后的字符。
2. 遍历 `words` 数组中的每个单词 `word`。
3. 对于每个单词，初始化 `sum` 为 0。遍历单词中的每个字符 `c`，并将 `weights[c - 'a']` 加到 `sum` 中。
4. 将计算出的 `sum` 对 26 取模，得到映射值。
5. 使用反向字母规则将该值转换为字符：`char = 'z' - value`。
6. 将计算得到的字符追加到字符串构建器中。
7. 处理完所有单词后，返回拼接好的字符串。

## 复杂度

> - **时间复杂度：** `O(N * M)`
  我们遍历数组中的所有 `N` 个单词，并且对于每个单词，我们遍历它的 `M` 个字符。因此，时间复杂度严格与所有单词的字符总数成正比。
- **空间复杂度：** `O(N)`
  我们使用字符串构建器或数组来存储每个单词映射后的结果字符。因为有 `N` 个单词，所以结果字符串的长度为 `N`。因此辅助空间为 `O(N)`。

- 时间复杂度: ``.
- 空间复杂度: ``.

## Python

```python
class Solution:
    def weightedWordMapping(self, words: List[str], weights: List[int]) -> str:
        # Array to store the mapped characters for each word
        result = []
        
        # Iterate over each word in the input list
        for word in words:
            # Calculate the sum of weights for the characters in the current word
            word_weight = 0
            for char in word:
                # Get the weight of the character by mapping it to its index (0 for 'a', 1 for 'b', etc.)
                word_weight += weights[ord(char) - ord('a')]
            
            # Take the sum modulo 26 as specified in the problem
            mapped_val = word_weight % 26
            
            # Map the value to a character using reverse alphabetical order ('z' - value)
            mapped_char = chr(ord('z') - mapped_val)
            
            # Append the mapped character to the result list
            result.append(mapped_char)
            
        # Join the characters into a single string and return
        return "".join(result)
```

## Java

```java
class Solution {
    public String weightedWordMapping(String[] words, int[] weights) {
        // Use a StringBuilder for efficient string concatenation
        StringBuilder result = new StringBuilder();
        
        // Iterate through each word in the array
        for (String word : words) {
            int wordWeight = 0;
            
            // Sum the weights of all characters in the current word
            for (char c : word.toCharArray()) {
                // Determine the 0-indexed position of the character
                wordWeight += weights[c - 'a'];
            }
            
            // Modulo 26 operation
            int mappedVal = wordWeight % 26;
            
            // Calculate the mapped character using reverse alphabetical order
            // Since 'z' is the starting point (0 -> 'z'), we subtract the mapped value
            char mappedChar = (char) ('z' - mappedVal);
            
            // Append the mapped character to our result
            result.append(mappedChar);
        }
        
        // Convert the StringBuilder to String and return
        return result.toString();
    }
}
```

## JavaScript

```javascript
/**
 * @param {string[]} words
 * @param {number[]} weights
 * @return {string}
 */
var weightedWordMapping = function(words, weights) {
    // Array to collect the resulting characters
    let result = [];
    
    // Process each word one by one
    for (let word of words) {
        let wordWeight = 0;
        
        // Sum up the weight of each character in the word
        for (let i = 0; i < word.length; i++) {
            // Find the character code difference from 'a'
            let charIndex = word.charCodeAt(i) - 97; // 97 is the ASCII for 'a'
            wordWeight += weights[charIndex];
        }
        
        // Apply modulo 26 to the sum
        let mappedVal = wordWeight % 26;
        
        // Map it back to a character starting backwards from 'z' (ASCII 122)
        let mappedChar = String.fromCharCode(122 - mappedVal);
        
        // Push to the result array
        result.push(mappedChar);
    }
    
    // Join the array into a string and return
    return result.join('');
};
```

## C++

```cpp
class Solution {
public:
    string weightedWordMapping(vector<string>& words, vector<int>& weights) {
        // String to store the concatenated mapped characters
        string result = "";
        
        // Process each word in the input
        for (const string& word : words) {
            int wordWeight = 0;
            
            // Sum the weights corresponding to each character
            for (char c : word) {
                // Find the index by subtracting the ASCII value of 'a'
                wordWeight += weights[c - 'a'];
            }
            
            // Perform the modulo 26 operation
            int mappedVal = wordWeight % 26;
            
            // Deduct the mapped value from 'z' to get the reversed mapped character
            char mappedChar = 'z' - mappedVal;
            
            // Append it to the result string
            result += mappedChar;
        }
        
        return result;
    }
};
```

## C#

```csharp
public class Solution {
    public string WeightedWordMapping(string[] words, int[] weights) {
        // StringBuilder is optimal for creating strings character by character
        System.Text.StringBuilder result = new System.Text.StringBuilder();
        
        // Iterate over each string in words
        foreach (string word in words) {
            int wordWeight = 0;
            
            // Calculate total weight of the word
            foreach (char c in word) {
                // c - 'a' yields the 0-based index of the alphabet
                wordWeight += weights[c - 'a'];
            }
            
            // Modulo 26 ensures the value is between 0 and 25
            int mappedVal = wordWeight % 26;
            
            // Map the value in reverse order (0 -> 'z', 1 -> 'y', etc.)
            char mappedChar = (char)('z' - mappedVal);
            
            // Append the mapped character
            result.Append(mappedChar);
        }
        
        // Return the final concatenated string
        return result.ToString();
    }
}
```

## Go

```go
func weightedWordMapping(words []string, weights []int) string {
    // Use a byte slice to efficiently build the result string
    result := make([]byte, 0, len(words))
    
    // Iterate through all the words
    for _, word := range words {
        wordWeight := 0
        
        // Iterate through each character of the word
        for i := 0; i < len(word); i++ {
            // Find character index (0-25) by subtracting ASCII of 'a'
            charIndex := word[i] - 'a'
            wordWeight += weights[charIndex]
        }
        
        // Take modulo 26
        mappedVal := wordWeight % 26
        
        // Reverse alphabetical mapping: 'z' - mappedVal
        mappedChar := byte('z' - mappedVal)
        
        // Append the character to our byte slice
        result = append(result, mappedChar)
    }
    
    // Convert byte slice back to string
    return string(result)
}
```

## Ruby

```ruby
# @param {String[]} words
# @param {Integer[]} weights
# @return {String}
def weighted_word_mapping(words, weights)
    result = ""
    
    # Process each word individually
    words.each do |word|
        word_weight = 0
        
        # Iterate over each character's byte value
        word.each_byte do |byte|
            # byte of 'a' is 97, so we subtract 97 to get the index
            char_index = byte - 97
            word_weight += weights[char_index]
        end
        
        # Take the weight modulo 26
        mapped_val = word_weight % 26
        
        # Convert the reverse alphabetical mapped value back to a character
        # 'z'.ord is 122
        mapped_char = (122 - mapped_val).chr
        
        # Append the character to the result string
        result << mapped_char
    end
    
    result
end
```

## Rust

```rust
impl Solution {
    pub fn weighted_word_mapping(words: Vec<String>, weights: Vec<i32>) -> String {
        // String to store our concatenated results
        let mut result = String::with_capacity(words.len());
        
        // Iterate over all words
        for word in words {
            let mut word_weight = 0;
            
            // Calculate the total weight of the word
            for c in word.bytes() {
                // b'a' is the byte value of 'a'
                let char_index = (c - b'a') as usize;
                word_weight += weights[char_index];
            }
            
            // Modulo 26 operation
            let mapped_val = word_weight % 26;
            
            // Map the value to reverse alphabetical order (b'z' is 122)
            let mapped_char = (b'z' - mapped_val as u8) as char;
            
            // Push the character to our result string
            result.push(mapped_char);
        }
        
        result
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun weightedWordMapping(words: Array<String>, weights: IntArray): String {
        // StringBuilder is used to concatenate characters efficiently
        val result = java.lang.StringBuilder()
        
        // Loop over each word in the array
        for (word in words) {
            var wordWeight = 0
            
            // Calculate the sum of weights for the characters in the word
            for (c in word) {
                wordWeight += weights[c - 'a']
            }
            
            // Modulo 26 for the mapping rule
            val mappedVal = wordWeight % 26
            
            // Calculate reverse alphabetical character starting from 'z'
            val mappedChar = ('z' - mappedVal).toChar()
            
            // Append the mapped character to the StringBuilder
            result.append(mappedChar)
        }
        
        // Return the accumulated characters as a string
        return result.toString()
    }
}
```

## Swift

```swift
class Solution {
    func weightedWordMapping(_ words: [String], _ weights: [Int]) -> String {
        // String to collect the mapped characters
        var result = ""
        
        // Process each word in the array
        for word in words {
            var wordWeight = 0
            
            // Sum the weights of the characters in the current word
            for char in word {
                // Get the ASCII value of the character and subtract ASCII of 'a'
                let charIndex = Int(char.asciiValue!) - Int(Character("a").asciiValue!)
                wordWeight += weights[charIndex]
            }
            
            // Take the sum modulo 26
            let mappedVal = wordWeight % 26
            
            // Map the value using reverse alphabetical order
            let mappedAscii = Int(Character("z").asciiValue!) - mappedVal
            let mappedChar = Character(UnicodeScalar(mappedAscii)!)
            
            // Append the mapped character
            result.append(mappedChar)
        }
        
        return result
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
> 我的另一个项目 [**coder.id**](https://www.coder.id) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.coder.id`，极具职业含金量的专属域名。

>
> [**立即前往 coder.id 打造你的个人品牌 →**](https://www.coder.id)

---

访问原文链接：[3838. 带权单词映射 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/3838-weighted-word-mapping)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

