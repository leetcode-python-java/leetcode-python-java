# 3614. Process String with Special Operations II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

Visit original link: [3614. Process String with Special Operations II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/3614-process-string-with-special-operations-ii) for a better experience!

LeetCode link: [3614. Process String with Special Operations II](https://leetcode.com/problems/process-string-with-special-operations-ii), difficulty: **Hard**.

## LeetCode description of "3614. Process String with Special Operations II"

You are given a string `s` consisting of lowercase English letters and the special characters: `'*'`, `'#'`, and `'%'`.

You are also given an integer `k`.

Build a new string `result` by processing `s` according to the following rules from left to right:

- If the letter is a **lowercase** English letter append it to `result`.
- A `'*'` **removes** the last character from `result`, if it exists.
- A `'#'` **duplicates** the current `result` and **appends** it to itself.
- A `'%'` **reverses** the current `result`.

Return the `k^{th}` character of the final string `result`. If `k` is out of the bounds of `result`, return `'.'`.

### [Example 1]

**Input**: `s = "a#b%*", k = 1`

**Output**: `"a"`

**Explanation**: 

<table><thead>
<tr>
<th><code>i</code></th>
<th><code>s[i]</code></th>
<th>Operation</th>
<th>Current <code>result</code></th>
</tr>
</thead><tbody>
<tr>
<td>0</td>
<td><code>&#39;a&#39;</code></td>
<td>Append <code>&#39;a&#39;</code></td>
<td><code>&quot;a&quot;</code></td>
</tr>
<tr>
<td>1</td>
<td><code>&#39;#&#39;</code></td>
<td>Duplicate <code>result</code></td>
<td><code>&quot;aa&quot;</code></td>
</tr>
<tr>
<td>2</td>
<td><code>&#39;b&#39;</code></td>
<td>Append <code>&#39;b&#39;</code></td>
<td><code>&quot;aab&quot;</code></td>
</tr>
<tr>
<td>3</td>
<td><code>&#39;%&#39;</code></td>
<td>Reverse <code>result</code></td>
<td><code>&quot;baa&quot;</code></td>
</tr>
<tr>
<td>4</td>
<td><code>&#39;*&#39;</code></td>
<td>Remove the last character</td>
<td><code>&quot;ba&quot;</code></td>
</tr>
</tbody></table>

<p>The final <code>result</code> is <code>&quot;ba&quot;</code>. The character at index <code>k = 1</code> is <code>&#39;a&#39;</code>.</p>


### [Example 2]

**Input**: `s = "cd%#*#", k = 3`

**Output**: `"d"`

**Explanation**: 

<table><thead>
<tr>
<th><code>i</code></th>
<th><code>s[i]</code></th>
<th>Operation</th>
<th>Current <code>result</code></th>
</tr>
</thead><tbody>
<tr>
<td>0</td>
<td><code>&#39;c&#39;</code></td>
<td>Append <code>&#39;c&#39;</code></td>
<td><code>&quot;c&quot;</code></td>
</tr>
<tr>
<td>1</td>
<td><code>&#39;d&#39;</code></td>
<td>Append <code>&#39;d&#39;</code></td>
<td><code>&quot;cd&quot;</code></td>
</tr>
<tr>
<td>2</td>
<td><code>&#39;%&#39;</code></td>
<td>Reverse <code>result</code></td>
<td><code>&quot;dc&quot;</code></td>
</tr>
<tr>
<td>3</td>
<td><code>&#39;#&#39;</code></td>
<td>Duplicate <code>result</code></td>
<td><code>&quot;dcdc&quot;</code></td>
</tr>
<tr>
<td>4</td>
<td><code>&#39;*&#39;</code></td>
<td>Remove the last character</td>
<td><code>&quot;dcd&quot;</code></td>
</tr>
<tr>
<td>5</td>
<td><code>&#39;#&#39;</code></td>
<td>Duplicate <code>result</code></td>
<td><code>&quot;dcddcd&quot;</code></td>
</tr>
</tbody></table>

<p>The final <code>result</code> is <code>&quot;dcddcd&quot;</code>. The character at index <code>k = 3</code> is <code>&#39;d&#39;</code>.</p>


### [Example 3]

**Input**: `s = "z*#", k = 0`

**Output**: `"."`

**Explanation**: 

<table><thead>
<tr>
<th><code>i</code></th>
<th><code>s[i]</code></th>
<th>Operation</th>
<th>Current <code>result</code></th>
</tr>
</thead><tbody>
<tr>
<td>0</td>
<td><code>&#39;z&#39;</code></td>
<td>Append <code>&#39;z&#39;</code></td>
<td><code>&quot;z&quot;</code></td>
</tr>
<tr>
<td>1</td>
<td><code>&#39;*&#39;</code></td>
<td>Remove the last character</td>
<td><code>&quot;&quot;</code></td>
</tr>
<tr>
<td>2</td>
<td><code>&#39;#&#39;</code></td>
<td>Duplicate the string</td>
<td><code>&quot;&quot;</code></td>
</tr>
</tbody></table>

<p>The final <code>result</code> is <code>&quot;&quot;</code>. Since index <code>k = 0</code> is out of bounds, the output is <code>&#39;.&#39;</code>.</p>


### [Constraints]

- `1 <= s.length <= 10^5`
- `s` consists of only lowercase English letters and special characters `'*'`, `'#'`, and `'%'`.
- `0 <= k <= 10^{15}`
- The length of `result` after processing `s` will not exceed `10^{15}`.

### [Hints]

<details>
  <summary>Hint 1</summary>
  Track the length of the string after each operation on `s`.

  
</details>

<details>
  <summary>Hint 2</summary>
  Walk backwards through `s`, undoing each # by using modulus on the tracked lengths, and undoing each % by mirroring across the midpoint, to pinpoint the `k`th character.

  
</details>

## Intuition

Since `k` can be up to `10^{15}`, we cannot simulate the string construction directly as it would result in Memory Limit Exceeded (MLE) or Time Limit Exceeded (TLE).

Instead, we can use a **Backward Simulation** approach:

1. First, compute the length of the string at each step of processing `s`.
2. If the final length is less than or equal to `k`, the index is out of bounds, so we return `'.'`.
3. Otherwise, we traverse the string backwards. At each step `i`:
   - If `s[i]` is a letter: Check if it's the character we are looking for (`lens[i] - 1 == k`). If so, return it.
   - If `s[i] == '#'` (duplicate): The string was duplicated. If `k` falls in the second half, it corresponds to the same character in the first half. So we update `k = k % (lens[i] / 2)`.
   - If `s[i] == '%'` (reverse): The string was reversed. We update `k` to its corresponding index before the reverse: `k = lens[i] - 1 - k`.
   - If `s[i] == '*'` (delete): We don't need to change `k`. Since `k` is a valid index in the current string, and `*` just removed a character at the very end, our current `k` naturally points to a character added before this `*`.

This logic guarantees that `k` is always a valid index in the string at the current step.

## Step-by-Step Solution

1. Create an array `lens` of size `n` to store the length of the string at each step.
2. Initialize `curr_len = 0`.
3. Iterate through `s` from left to right:
   - If `s[i]` is a letter, increment `curr_len`.
   - If `s[i] == '*'`, decrement `curr_len` (minimum 0).
   - If `s[i] == '#'`, double `curr_len`.
   - Store `curr_len` in `lens[i]`.
4. If `curr_len <= k`, return `'.'`.
5. Iterate through `s` from right to left:
   - If `s[i]` is a letter and `lens[i] - 1 == k`, return `s[i]`.
   - If `s[i] == '#'` and `k >= lens[i] / 2`, update `k %= (lens[i] / 2)`.
   - If `s[i] == '%'`, update `k = lens[i] - 1 - k`.

## Complexity

> - **Time Complexity:** `O(n)`, where `n` is the length of string `s`. We make two passes over the string.
- **Space Complexity:** `O(n)` to store the lengths at each step in the `lens` array.

- Time complexity: `O(n)`.
- Space complexity: `O(n)`.

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

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.leader.me`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [3614. Process String with Special Operations II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/3614-process-string-with-special-operations-ii) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

