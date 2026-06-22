# 3614. 处理包含特殊操作的字符串 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[3614. 处理包含特殊操作的字符串 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/3614-process-string-with-special-operations-ii)，体验更佳！

力扣链接：[3614. 处理包含特殊操作的字符串 II](https://leetcode.cn/problems/process-string-with-special-operations-ii), 难度等级：**困难**。

## LeetCode “3614. 处理包含特殊操作的字符串 II”问题描述

给你一个由小写英文字母和特殊字符 `'*'`、`'#'` 和 `'%'` 组成的字符串 `s`。

同时给你一个整数 `k`。

通过从左到右处理 `s` ，按照以下规则构建一个新字符串 `result` ：

- 如果字符是**小写**英文字母，将其追加到 `result` 的末尾。
- `'*'` **删除** `result` 的最后一个字符（如果存在）。
- `'#'` **复制** 当前的 `result` 并将其**追加**到自身末尾。
- `'%'` **反转** 当前的 `result`。

返回最终字符串 `result` 的第 `k` 个字符（从 0 开始计数，或者根据题意如果是0-indexed，请视同 0-indexed）。如果 `k` 超出 `result` 的边界，则返回 `'.'`。

### [示例 1]

**输入**: `s = "a#b%*", k = 1`

**输出**: `"a"`

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
<td>追加 <code>&#39;a&#39;</code></td>
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
<td>追加 <code>&#39;b&#39;</code></td>
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

<p>最终的 <code>result</code> 是 <code>&quot;ba&quot;</code>。索引 <code>k = 1</code> 处的字符是 <code>&#39;a&#39;</code>。</p>


### [示例 2]

**输入**: `s = "cd%#*#", k = 3`

**输出**: `"d"`

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
<td><code>&#39;c&#39;</code></td>
<td>追加 <code>&#39;c&#39;</code></td>
<td><code>&quot;c&quot;</code></td>
</tr>
<tr>
<td>1</td>
<td><code>&#39;d&#39;</code></td>
<td>追加 <code>&#39;d&#39;</code></td>
<td><code>&quot;cd&quot;</code></td>
</tr>
<tr>
<td>2</td>
<td><code>&#39;%&#39;</code></td>
<td>反转 <code>result</code></td>
<td><code>&quot;dc&quot;</code></td>
</tr>
<tr>
<td>3</td>
<td><code>&#39;#&#39;</code></td>
<td>复制 <code>result</code></td>
<td><code>&quot;dcdc&quot;</code></td>
</tr>
<tr>
<td>4</td>
<td><code>&#39;*&#39;</code></td>
<td>删除最后一个字符</td>
<td><code>&quot;dcd&quot;</code></td>
</tr>
<tr>
<td>5</td>
<td><code>&#39;#&#39;</code></td>
<td>复制 <code>result</code></td>
<td><code>&quot;dcddcd&quot;</code></td>
</tr>
</tbody></table>

<p>最终的 <code>result</code> 是 <code>&quot;dcddcd&quot;</code>。索引 <code>k = 3</code> 处的字符是 <code>&#39;d&#39;</code>。</p>


### [示例 3]

**输入**: `s = "z*#", k = 0`

**输出**: `"."`

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
<td>追加 <code>&#39;z&#39;</code></td>
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

<p>最终的 <code>result</code> 是 <code>&quot;&quot;</code>。因为索引 <code>k = 0</code> 越界，输出为 <code>&#39;.&#39;</code>。</p>


### [约束]

- `1 <= s.length <= 10^5`
- `s` 仅由小写英文字母和特殊字符 `'*'`、`'#'` 以及 `'%'` 组成。
- `0 <= k <= 10^{15}`
- 处理 `s` 后 `result` 的长度不会超过 `10^{15}`。

### [Hints]

<details>
  <summary>提示 1</summary>
  Track the length of the string after each operation on `s`.

  
</details>

<details>
  <summary>提示 2</summary>
  Walk backwards through `s`, undoing each # by using modulus on the tracked lengths, and undoing each % by mirroring across the midpoint, to pinpoint the `k`th character.

  
</details>

## 思路

由于 `k` 的最大值可以达到 `10^{15}`，我们无法直接模拟字符串的构建过程，否则会导致内存超限（MLE）或时间超限（TLE）。

相反，我们可以使用**反向模拟法**：

1. 首先，计算在处理 `s` 的每一步时字符串的长度。
2. 如果最终长度小于或等于 `k`，说明索引越界，直接返回 `'.'`。
3. 否则，我们从后往前遍历字符串。在每一步 `i`：
   - 如果 `s[i]` 是字母：检查它是否是我们要找的字符（即 `lens[i] - 1 == k`）。如果是，则返回它。
   - 如果 `s[i] == '#'`（复制）：字符串被复制了一份。如果 `k` 落在后半部分，它对应于前半部分的同一个字符。所以我们更新 `k = k % (lens[i] / 2)`。
   - 如果 `s[i] == '%'`（反转）：字符串被反转了。我们将 `k` 更新为反转前的对应索引：`k = lens[i] - 1 - k`。
   - 如果 `s[i] == '*'`（删除）：我们不需要改变 `k`。因为 `k` 是当前字符串中的一个有效索引，而 `*` 只是删除了最末尾的一个字符，我们当前的 `k` 自然指向在此 `*` 之前添加的字符。

这个逻辑保证了 `k` 始终是当前步骤字符串中的一个有效索引。

## 步骤

1. 创建一个大小为 `n` 的数组 `lens`，用于存储每一步的字符串长度。
2. 初始化 `curr_len = 0`。
3. 从左到右遍历 `s`：
   - 如果 `s[i]` 是字母，`curr_len` 加 1。
   - 如果 `s[i] == '*'`，`curr_len` 减 1（最小为 0）。
   - 如果 `s[i] == '#'`，`curr_len` 乘以 2。
   - 将 `curr_len` 存入 `lens[i]`。
4. 如果 `curr_len <= k`，返回 `'.'`。
5. 从右到左遍历 `s`：
   - 如果 `s[i]` 是字母且 `lens[i] - 1 == k`，返回 `s[i]`。
   - 如果 `s[i] == '#'` 且 `k >= lens[i] / 2`，更新 `k %= (lens[i] / 2)`。
   - 如果 `s[i] == '%'`，更新 `k = lens[i] - 1 - k`。

## 复杂度

> - **时间复杂度：** `O(n)`，其中 `n` 是字符串 `s` 的长度。我们对字符串进行了两次遍历。
- **空间复杂度：** `O(n)`，用于在 `lens` 数组中存储每一步的长度。

- 时间复杂度: `O(n)`.
- 空间复杂度: `O(n)`.

## Python

```python
class Solution:
    def processStr(self, s: str, k: int) -> str:
        lens = []
        curr_len = 0
        for ch in s:
            if ch.isalpha():
                curr_len += 1
            elif ch == '*':
                curr_len = max(0, curr_len - 1)
            elif ch == '#':
                curr_len *= 2
            elif ch == '%':
                pass
            lens.append(curr_len)
            
        if curr_len <= k:
            return '.'
            
        for i in range(len(s) - 1, -1, -1):
            if s[i].isalpha():
                if lens[i] - 1 == k:
                    return s[i]
            elif s[i] == '#':
                half = lens[i] // 2
                if half > 0 and k >= half:
                    k %= half
            elif s[i] == '%':
                if lens[i] > 0:
                    k = lens[i] - 1 - k
                    
        return '.'
```

## Java

```java
class Solution {
    public char processStr(String s, long k) {
        int n = s.length();
        long[] lens = new long[n];
        long currLen = 0;
        
        for (int i = 0; i < n; i++) {
            char ch = s.charAt(i);
            if (ch >= 'a' && ch <= 'z') {
                currLen++;
            } else if (ch == '*') {
                currLen = Math.max(0L, currLen - 1);
            } else if (ch == '#') {
                currLen *= 2;
            }
            lens[i] = currLen;
        }
        
        if (currLen <= k) {
            return '.';
        }
        
        for (int i = n - 1; i >= 0; i--) {
            char ch = s.charAt(i);
            if (ch >= 'a' && ch <= 'z') {
                if (lens[i] - 1 == k) {
                    return ch;
                }
            } else if (ch == '#') {
                long half = lens[i] / 2;
                if (half > 0 && k >= half) {
                    k %= half;
                }
            } else if (ch == '%') {
                if (lens[i] > 0) {
                    k = lens[i] - 1 - k;
                }
            }
        }
        
        return '.';
    }
}
```

## JavaScript

```javascript
/**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var processStr = function(s, k) {
    const n = s.length;
    const lens = new Array(n);
    let currLen = 0n;
    let bigK = BigInt(k);
    
    for (let i = 0; i < n; i++) {
        const ch = s[i];
        if (ch >= 'a' && ch <= 'z') {
            currLen++;
        } else if (ch === '*') {
            if (currLen > 0n) currLen--;
        } else if (ch === '#') {
            currLen *= 2n;
        }
        lens[i] = currLen;
    }
    
    if (currLen <= bigK) {
        return '.';
    }
    
    for (let i = n - 1; i >= 0; i--) {
        const ch = s[i];
        if (ch >= 'a' && ch <= 'z') {
            if (lens[i] - 1n === bigK) {
                return ch;
            }
        } else if (ch === '#') {
            const half = lens[i] / 2n;
            if (half > 0n && bigK >= half) {
                bigK %= half;
            }
        } else if (ch === '%') {
            if (lens[i] > 0n) {
                bigK = lens[i] - 1n - bigK;
            }
        }
    }
    
    return '.';
};
```

## C++

```cpp
class Solution {
public:
    char processStr(string s, long long k) {
        int n = s.length();
        vector<long long> lens(n);
        long long curr_len = 0;
        
        for (int i = 0; i < n; ++i) {
            char ch = s[i];
            if (ch >= 'a' && ch <= 'z') {
                curr_len++;
            } else if (ch == '*') {
                curr_len = max(0LL, curr_len - 1);
            } else if (ch == '#') {
                curr_len *= 2;
            }
            lens[i] = curr_len;
        }
        
        if (curr_len <= k) return '.';
        
        for (int i = n - 1; i >= 0; --i) {
            char ch = s[i];
            if (ch >= 'a' && ch <= 'z') {
                if (lens[i] - 1 == k) return ch;
            } else if (ch == '#') {
                long long half = lens[i] / 2;
                if (half > 0 && k >= half) k %= half;
            } else if (ch == '%') {
                if (lens[i] > 0) k = lens[i] - 1 - k;
            }
        }
        
        return '.';
    }
};
```

## C#

```csharp
public class Solution {
    public char ProcessStr(string s, long k) {
        int n = s.Length;
        long[] lens = new long[n];
        long currLen = 0;
        
        for (int i = 0; i < n; i++) {
            char ch = s[i];
            if (ch >= 'a' && ch <= 'z') {
                currLen++;
            } else if (ch == '*') {
                currLen = Math.Max(0L, currLen - 1);
            } else if (ch == '#') {
                currLen *= 2;
            }
            lens[i] = currLen;
        }
        
        if (currLen <= k) return '.';
        
        for (int i = n - 1; i >= 0; i--) {
            char ch = s[i];
            if (ch >= 'a' && ch <= 'z') {
                if (lens[i] - 1 == k) return ch;
            } else if (ch == '#') {
                long half = lens[i] / 2;
                if (half > 0 && k >= half) k %= half;
            } else if (ch == '%') {
                if (lens[i] > 0) k = lens[i] - 1 - k;
            }
        }
        
        return '.';
    }
}
```

## Go

```go
func processStr(s string, k int64) byte {
    n := len(s)
    lens := make([]int64, n)
    var currLen int64 = 0
    
    for i := 0; i < n; i++ {
        ch := s[i]
        if ch >= 'a' && ch <= 'z' {
            currLen++
        } else if ch == '*' {
            if currLen > 0 {
                currLen--
            }
        } else if ch == '#' {
            currLen *= 2
        }
        lens[i] = currLen
    }
    
    if currLen <= k {
        return '.'
    }
    
    for i := n - 1; i >= 0; i-- {
        ch := s[i]
        if ch >= 'a' && ch <= 'z' {
            if lens[i] - 1 == k {
                return ch
            }
        } else if ch == '#' {
            half := lens[i] / 2
            if half > 0 && k >= half {
                k %= half
            }
        } else if ch == '%' {
            if lens[i] > 0 {
                k = lens[i] - 1 - k
            }
        }
    }
    
    return '.'
}
```

## Ruby

```ruby
# @param {String} s
# @param {Integer} k
# @return {String}
def process_str(s, k)
    n = s.length
    lens = Array.new(n)
    curr_len = 0
    
    (0...n).each do |i|
        ch = s[i]
        if ch >= 'a' && ch <= 'z'
            curr_len += 1
        elsif ch == '*'
            curr_len = [0, curr_len - 1].max
        elsif ch == '#'
            curr_len *= 2
        end
        lens[i] = curr_len
    end
    
    return '.' if curr_len <= k
    
    (n - 1).downto(0) do |i|
        ch = s[i]
        if ch >= 'a' && ch <= 'z'
            return ch if lens[i] - 1 == k
        elsif ch == '#'
            half = lens[i] / 2
            k %= half if half > 0 && k >= half
        elsif ch == '%'
            k = lens[i] - 1 - k if lens[i] > 0
        end
    end
    
    '.'
end
```

## Rust

```rust
impl Solution {
    pub fn process_str(s: String, mut k: i64) -> char {
        let n = s.len();
        let mut lens = vec![0i64; n];
        let mut curr_len = 0i64;
        let bytes = s.as_bytes();
        
        for i in 0..n {
            let ch = bytes[i];
            if ch >= b'a' && ch <= b'z' {
                curr_len += 1;
            } else if ch == b'*' {
                if curr_len > 0 { curr_len -= 1; }
            } else if ch == b'#' {
                curr_len *= 2;
            }
            lens[i] = curr_len;
        }
        
        if curr_len <= k {
            return '.';
        }
        
        for i in (0..n).rev() {
            let ch = bytes[i];
            if ch >= b'a' && ch <= b'z' {
                if lens[i] - 1 == k {
                    return ch as char;
                }
            } else if ch == b'#' {
                let half = lens[i] / 2;
                if half > 0 && k >= half {
                    k %= half;
                }
            } else if ch == b'%' {
                if lens[i] > 0 {
                    k = lens[i] - 1 - k;
                }
            }
        }
        
        '.'
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun processStr(s: String, k: Long): Char {
        var mutableK = k
        val n = s.length
        val lens = LongArray(n)
        var currLen = 0L
        
        for (i in 0 until n) {
            val ch = s[i]
            if (ch in 'a'..'z') {
                currLen++
            } else if (ch == '*') {
                if (currLen > 0) currLen--
            } else if (ch == '#') {
                currLen *= 2
            }
            lens[i] = currLen
        }
        
        if (currLen <= mutableK) return '.'
        
        for (i in n - 1 downTo 0) {
            val ch = s[i]
            if (ch in 'a'..'z') {
                if (lens[i] - 1 == mutableK) return ch
            } else if (ch == '#') {
                val half = lens[i] / 2
                if (half > 0 && mutableK >= half) mutableK %= half
            } else if (ch == '%') {
                if (lens[i] > 0) mutableK = lens[i] - 1 - mutableK
            }
        }
        
        return '.'
    }
}
```

## Swift

```swift
class Solution {
    func processStr(_ s: String, _ k: Int) -> Character {
        var mutableK = k
        let chars = Array(s)
        let n = chars.count
        var lens = [Int](repeating: 0, count: n)
        var currLen = 0
        
        for i in 0..<n {
            let ch = chars[i]
            if ch >= "a" && ch <= "z" {
                currLen += 1
            } else if ch == "*" {
                currLen = max(0, currLen - 1)
            } else if ch == "#" {
                currLen *= 2
            }
            lens[i] = currLen
        }
        
        if currLen <= mutableK {
            return "."
        }
        
        for i in stride(from: n - 1, through: 0, by: -1) {
            let ch = chars[i]
            if ch >= "a" && ch <= "z" {
                if lens[i] - 1 == mutableK {
                    return ch
                }
            } else if ch == "#" {
                let half = lens[i] / 2
                if half > 0 && mutableK >= half {
                    mutableK %= half
                }
            } else if ch == "%" {
                if lens[i] > 0 {
                    mutableK = lens[i] - 1 - mutableK
                }
            }
        }
        
        return "."
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

访问原文链接：[3614. 处理包含特殊操作的字符串 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/3614-process-string-with-special-operations-ii)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

