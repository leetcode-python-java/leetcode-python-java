# 3612. 用特殊操作处理字符串 I - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[3612. 用特殊操作处理字符串 I - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/3612-process-string-with-special-operations-i)，体验更佳！

力扣链接：[3612. 用特殊操作处理字符串 I](https://leetcode.cn/problems/process-string-with-special-operations-i), 难度等级：**中等**。

## LeetCode “3612. 用特殊操作处理字符串 I”问题描述

给你一个字符串 `s`，它由小写英文字母和特殊字符：`*`、`#` 和 `%` 组成。

请根据以下规则从左到右处理 `s` 中的字符，构造一个新的字符串 `result`：

- 如果字符是 **小写** 英文字母，则将其添加到 `result` 中。
- 字符 `'*'` 会 **删除** `result` 中的最后一个字符（如果存在）。
- 字符 `'#'` 会 **复制** 当前的 `result` 并 **追加** 到其自身后面。
- 字符 `'%'` 会 **反转** 当前的 `result`。

在处理完 `s` 中的所有字符后，返回最终的字符串 `result`。

### [示例 1]

**输入**: `s = "a#b%*"`

**输出**: `"ba"`

**解释**: 

<table><thead>
<tr>
<th><code>i</code></th>
<th><code>s[i]</code></th>
<th>操作</th>
<th>当前 <code>result</code></th>
</tr>
</thead><tbody>
<tr>
<td>0</td>
<td><code>&#39;a&#39;</code></td>
<td>添加 <code>&#39;a&#39;</code></td>
<td><code>&quot;a&quot;</code></td>
</tr>
<tr>
<td>1</td>
<td><code>&#39;#&#39;</code></td>
<td>复制 <code>result</code></td>
<td><code>&quot;aa&quot;</code></td>
</tr>
<tr>
<td>2</td>
<td><code>&#39;b&#39;</code></td>
<td>添加 <code>&#39;b&#39;</code></td>
<td><code>&quot;aab&quot;</code></td>
</tr>
<tr>
<td>3</td>
<td><code>&#39;%&#39;</code></td>
<td>反转 <code>result</code></td>
<td><code>&quot;baa&quot;</code></td>
</tr>
<tr>
<td>4</td>
<td><code>&#39;*&#39;</code></td>
<td>删除最后一个字符</td>
<td><code>&quot;ba&quot;</code></td>
</tr>
</tbody></table>

<p>因此，最终的 <code>result</code> 是 <code>&quot;ba&quot;</code>。</p>


### [示例 2]

**输入**: `s = "z*#"`

**输出**: `""`

**解释**: 

<table><thead>
<tr>
<th><code>i</code></th>
<th><code>s[i]</code></th>
<th>操作</th>
<th>当前 <code>result</code></th>
</tr>
</thead><tbody>
<tr>
<td>0</td>
<td><code>&#39;z&#39;</code></td>
<td>添加 <code>&#39;z&#39;</code></td>
<td><code>&quot;z&quot;</code></td>
</tr>
<tr>
<td>1</td>
<td><code>&#39;*&#39;</code></td>
<td>删除最后一个字符</td>
<td><code>&quot;&quot;</code></td>
</tr>
<tr>
<td>2</td>
<td><code>&#39;#&#39;</code></td>
<td>复制字符串</td>
<td><code>&quot;&quot;</code></td>
</tr>
</tbody></table>

<p>因此，最终的 <code>result</code> 是 <code>&quot;&quot;</code>。</p>


### [约束]

- `1 <= s.length <= 20`
- `s` 只包含小写英文字母和特殊字符 `*`、`#` 和 `%`。

### [Hints]

<details>
  <summary>提示 1</summary>
  Simulate as described

  
</details>

## 思路

与“处理包含特殊操作的字符串 II”一题中 `s.length` 可以达到 `10^5` 且 `k` 高达 `10^{15}` 不同，本题中 `s.length` 非常小（最多 20）。

因为输入长度 `n <= 20`，即使我们在每一步都将字符串长度翻倍（例如，每次都遇到 `'#'`），最大可能长度也只是 `2^{20}`，大约 100 万个字符。这对于现代计算机的内存和处理速度来说，作为单个字符串操作是完全可以接受的。

因此，我们可以使用一种直接的 **模拟（Simulation）** 方法：
我们只需创建一个结果字符串（为了效率可以使用数组或 StringBuilder），然后从左到右逐个处理 `s` 中的字符，完全按照规则执行即可。

我们只需要处理四种情况：
1. **小写字母：** 将其追加到当前结果中。
2. **`'*'`（星号）：** 如果结果不为空，则删除最后一个字符。
3. **`'#'`（井号）：** 将当前整个结果追加到自身后面（复制）。
4. **`'%'`（百分号）：** 反转当前结果中的字符。

## 步骤

1. 初始化一个空字符串/数组 `res` 来构建结果。
2. 遍历给定字符串 `s` 中的每个字符 `ch`。
3. 如果 `ch` 是小写英文字母（`'a'` 到 `'z'`），将其追加到 `res`。
4. 如果 `ch == '*'`，检查 `res` 是否为空。如果不为空，则删除最后一个字符。
5. 如果 `ch == '#'`，将 `res` 当前的内容复制一份并追加到 `res` 中。
6. 如果 `ch == '%'`，反转当前 `res` 中的所有字符。
7. 循环结束后，将 `res` 作为字符串返回。

## 复杂度

> - **时间复杂度：** `O(2^n)`，其中 `n` 是字符串 `s` 的长度。在最坏情况下（字符串在几个字母后全部是 `'#'`），字符串长度每次翻倍，导致 `2^n` 次操作。因为 `n <= 20`，`2^{20} \approx 10^6`，这个计算量非常小。
- **空间复杂度：** `O(2^n)`，用于存储结果字符串，在最坏情况下可能会增长到 `2^{20}` 个字符。

- 时间复杂度: `O(2^n)`.
- 空间复杂度: `O(2^n)`.

## Python

```python
class Solution:
    def processStr(self, s: str) -> str:
        # Use a list to efficiently build the result string
        res = []
        
        # Iterate through each character in the string
        for ch in s:
            if ch.isalpha():
                # If it is a lowercase letter, append it
                res.append(ch)
            elif ch == '*':
                # If it is '*', remove the last character if the list is not empty
                if res:
                    res.pop()
            elif ch == '#':
                # If it is '#', duplicate the current result
                res.extend(res)
            elif ch == '%':
                # If it is '%', reverse the current result
                res.reverse()
                
        # Join the list into a string and return
        return "".join(res)
```

## Java

```java
class Solution {
    public String processStr(String s) {
        // Use StringBuilder for efficient string manipulations
        StringBuilder res = new StringBuilder();
        
        // Iterate through each character in the string
        for (char ch : s.toCharArray()) {
            if (ch >= 'a' && ch <= 'z') {
                // If it is a lowercase letter, append it
                res.append(ch);
            } else if (ch == '*') {
                // If it is '*', remove the last character if not empty
                if (res.length() > 0) {
                    res.deleteCharAt(res.length() - 1);
                }
            } else if (ch == '#') {
                // If it is '#', duplicate the current result
                res.append(res.toString());
            } else if (ch == '%') {
                // If it is '%', reverse the current result
                res.reverse();
            }
        }
        
        // Return the final string
        return res.toString();
    }
}
```

## JavaScript

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var processStr = function(s) {
    // Use an array to efficiently build the result string
    const res = [];
    
    // Iterate through each character in the string
    for (const ch of s) {
        if (ch >= 'a' && ch <= 'z') {
            // If it is a lowercase letter, append it
            res.push(ch);
        } else if (ch === '*') {
            // If it is '*', remove the last character if not empty
            if (res.length > 0) {
                res.pop();
            }
        } else if (ch === '#') {
            // If it is '#', duplicate the current result
            // We use spread syntax or push.apply to append all elements
            res.push(...res);
        } else if (ch === '%') {
            // If it is '%', reverse the current result
            res.reverse();
        }
    }
    
    // Join the array into a string and return
    return res.join('');
};
```

## C++

```cpp
class Solution {
public:
    string processStr(string s) {
        // Use a string to efficiently build the result
        string res = "";
        
        // Iterate through each character in the string
        for (char ch : s) {
            if (isalpha(ch)) {
                // If it is a lowercase letter, append it
                res.push_back(ch);
            } else if (ch == '*') {
                // If it is '*', remove the last character if not empty
                if (!res.empty()) {
                    res.pop_back();
                }
            } else if (ch == '#') {
                // If it is '#', duplicate the current result
                res += res;
            } else if (ch == '%') {
                // If it is '%', reverse the current result
                reverse(res.begin(), res.end());
            }
        }
        
        // Return the final string
        return res;
    }
};
```

## C#

```csharp
public class Solution {
    public string ProcessStr(string s) {
        // Use StringBuilder for efficient string manipulations
        StringBuilder res = new StringBuilder();
        
        // Iterate through each character in the string
        foreach (char ch in s) {
            if (ch >= 'a' && ch <= 'z') {
                // If it is a lowercase letter, append it
                res.Append(ch);
            } else if (ch == '*') {
                // If it is '*', remove the last character if not empty
                if (res.Length > 0) {
                    res.Length--;
                }
            } else if (ch == '#') {
                // If it is '#', duplicate the current result
                res.Append(res.ToString());
            } else if (ch == '%') {
                // If it is '%', reverse the current result
                // C# StringBuilder doesn't have a built-in Reverse, so we do it manually
                int left = 0, right = res.Length - 1;
                while (left < right) {
                    char temp = res[left];
                    res[left] = res[right];
                    res[right] = temp;
                    left++;
                    right--;
                }
            }
        }
        
        // Return the final string
        return res.ToString();
    }
}
```

## Go

```go
func processStr(s string) string {
    // Use a byte slice to efficiently build the result string
    res := []byte{}
    
    // Iterate through each character in the string
    for i := 0; i < len(s); i++ {
        ch := s[i]
        if ch >= 'a' && ch <= 'z' {
            // If it is a lowercase letter, append it
            res = append(res, ch)
        } else if ch == '*' {
            // If it is '*', remove the last character if not empty
            if len(res) > 0 {
                res = res[:len(res)-1]
            }
        } else if ch == '#' {
            // If it is '#', duplicate the current result
            res = append(res, res...)
        } else if ch == '%' {
            // If it is '%', reverse the current result
            left, right := 0, len(res)-1
            for left < right {
                res[left], res[right] = res[right], res[left]
                left++
                right--
            }
        }
    }
    
    // Convert byte slice to string and return
    return string(res)
}
```

## Ruby

```ruby
# @param {String} s
# @return {String}
def process_str(s)
    # Use an array to efficiently build the result string
    res = []
    
    # Iterate through each character in the string
    s.each_char do |ch|
        if ch >= 'a' && ch <= 'z'
            # If it is a lowercase letter, append it
            res << ch
        elsif ch == '*'
            # If it is '*', remove the last character if not empty
            res.pop if !res.empty?
        elsif ch == '#'
            # If it is '#', duplicate the current result
            res.concat(res)
        elsif ch == '%'
            # If it is '%', reverse the current result
            res.reverse!
        end
    end
    
    # Join the array into a string and return
    res.join
end
```

## Rust

```rust
impl Solution {
    pub fn process_str(s: String) -> String {
        // Use a vector of characters to efficiently build the result
        let mut res: Vec<char> = Vec::new();
        
        // Iterate through each character in the string
        for ch in s.chars() {
            if ch.is_ascii_alphabetic() {
                // If it is a lowercase letter, append it
                res.push(ch);
            } else if ch == '*' {
                // If it is '*', remove the last character if not empty
                res.pop();
            } else if ch == '#' {
                // If it is '#', duplicate the current result
                let cloned = res.clone();
                res.extend(cloned);
            } else if ch == '%' {
                // If it is '%', reverse the current result
                res.reverse();
            }
        }
        
        // Collect the vector of chars into a String and return
        res.into_iter().collect()
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun processStr(s: String): String {
        // Use StringBuilder for efficient string manipulations
        val res = java.lang.StringBuilder()
        
        // Iterate through each character in the string
        for (ch in s) {
            if (ch in 'a'..'z') {
                // If it is a lowercase letter, append it
                res.append(ch)
            } else if (ch == '*') {
                // If it is '*', remove the last character if not empty
                if (res.isNotEmpty()) {
                    res.deleteCharAt(res.length - 1)
                }
            } else if (ch == '#') {
                // If it is '#', duplicate the current result
                res.append(res.toString())
            } else if (ch == '%') {
                // If it is '%', reverse the current result
                res.reverse()
            }
        }
        
        // Return the final string
        return res.toString()
    }
}
```

## Swift

```swift
class Solution {
    func processStr(_ s: String) -> String {
        // Use an array of Characters to efficiently build the result
        var res = [Character]()
        
        // Iterate through each character in the string
        for ch in s {
            if ch >= "a" && ch <= "z" {
                // If it is a lowercase letter, append it
                res.append(ch)
            } else if ch == "*" {
                // If it is '*', remove the last character if not empty
                if !res.isEmpty {
                    res.removeLast()
                }
            } else if ch == "#" {
                // If it is '#', duplicate the current result
                res.append(contentsOf: res)
            } else if ch == "%" {
                // If it is '%', reverse the current result
                res.reverse()
            }
        }
        
        // Convert the character array to String and return
        return String(res)
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

访问原文链接：[3612. 用特殊操作处理字符串 I - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/3612-process-string-with-special-operations-i)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

