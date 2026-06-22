# 3612. Process String with Special Operations I - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

Visit original link: [3612. Process String with Special Operations I - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/3612-process-string-with-special-operations-i) for a better experience!

LeetCode link: [3612. Process String with Special Operations I](https://leetcode.com/problems/process-string-with-special-operations-i), difficulty: **Medium**.

## LeetCode description of "3612. Process String with Special Operations I"

You are given a string `s` consisting of lowercase English letters and the special characters: `*`, `#`, and `%`.

Build a new string `result` by processing `s` according to the following rules from left to right:

- If the letter is a **lowercase** English letter append it to `result`.
- A `'*'` **removes** the last character from `result`, if it exists.
- A `'#'` **duplicates** the current `result` and **appends** it to itself.
- A `'%'` **reverses** the current `result`.

Return the final string `result` after processing all characters in `s`.

### [Example 1]

**Input**: `s = "a#b%*"`

**Output**: `"ba"`

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

<p>Thus, the final <code>result</code> is <code>&quot;ba&quot;</code>.</p>


### [Example 2]

**Input**: `s = "z*#"`

**Output**: `""`

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

<p>Thus, the final <code>result</code> is <code>&quot;&quot;</code>.</p>


### [Constraints]

- `1 <= s.length <= 20`
- `s` consists of only lowercase English letters and special characters `*`, `#`, and `%`.

### [Hints]

<details>
  <summary>Hint 1</summary>
  Simulate as described

  
</details>

## Intuition

Unlike the "Process String with Special Operations II" problem where `s.length` could be `10^5` and `k` could be `10^{15}`, here `s.length` is extremely small (at most 20).

Because the input length is `n <= 20`, even if we double the string length at every step (e.g., using `'#'`), the maximum possible length is `2^{20}`, which is about 1 million characters. This is well within the limits of modern computer memory and processing speed for a single string operation.

Therefore, we can use a straightforward **Simulation** approach:
We simply create a result string (or array/StringBuilder for efficiency) and process each character of `s` one by one from left to right exactly as the rules describe.

We just need to handle four cases:
1. **Lowercase letter:** Append it to the current result.
2. **`'*'` (Asterisk):** If the result is not empty, remove the last character.
3. **`'#'` (Hash):** Append the entire current result to itself (duplicate).
4. **`'%'` (Percent):** Reverse the characters in the current result.

## Step-by-Step Solution

1. Initialize an empty string/array `res` to build the result.
2. Iterate through each character `ch` in the given string `s`.
3. If `ch` is a lowercase English letter (`'a'` to `'z'`), append it to `res`.
4. If `ch == '*'`, check if `res` is not empty. If it's not empty, remove the last character.
5. If `ch == '#'`, duplicate the current contents of `res` and append them to `res`.
6. If `ch == '%'`, reverse all the characters currently in `res`.
7. After the loop finishes, return `res` as a string.

## Complexity

> - **Time Complexity:** `O(2^n)`, where `n` is the length of string `s`. In the worst case (a string consisting entirely of `'#'` after some letters), the string length doubles each time, leading to `2^n` operations. Since `n <= 20`, `2^{20} \approx 10^6`, which is very fast.
- **Space Complexity:** `O(2^n)` to store the result string, which can grow up to `2^{20}` characters in the worst case.

- Time complexity: `O(2^n)`.
- Space complexity: `O(2^n)`.

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

Visit original link: [3612. Process String with Special Operations I - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/3612-process-string-with-special-operations-i) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

