# 58. Length of Last Word - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

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

Visit original link: [58. Length of Last Word - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/58-length-of-last-word) for a better experience!

LeetCode link: [58. Length of Last Word](https://leetcode.com/problems/length-of-last-word), difficulty: **Easy**.

## LeetCode description of "58. Length of Last Word"

Given a string `s` consisting of words and spaces, return the length of the **last** word in the string.

A **word** is a maximal substring consisting of non-space characters only.

### [Example 1]

**Input**: `s = "Hello World"`

**Output**: `5`

**Explanation**: `The last word is "World" with length 5.`

### [Example 2]

**Input**: `s = "   fly me   to   the moon  "`

**Output**: `4`

**Explanation**: `The last word is "moon" with length 4.`

### [Example 3]

**Input**: `s = "luffy is still joyboy"`

**Output**: `6`

**Explanation**: `The last word is "joyboy" with length 6.`

### [Constraints]

- `1 <= s.length <= 10^4`
- `s` consists of only English letters and spaces `' '`.
- There will be at least one word in `s`.

## Intuition

- To find the length of the last word, we can use methods like `split()`, `last()`, and `len()`.
- However, this kind of problem is actually meant to test a programmer’s ability to control `index`.
- Since the last word is at the end, solving it from the front isn’t very convenient. Is there another way?

<details><summary>Click to view the answer</summary><p>
You can solve this by traversing the string **backwards**. There are only two cases to consider: whether the current character is a space or not.

* **Initially**, if you encounter a space, skip it and move to the next character. If you encounter a non-space character, increment the `length`.
* **If `length > 0`**, it means you have already encountered letters. At this point, if the current character is a space, you can return the result.
</p></details>

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `1`.

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

Visit original link: [58. Length of Last Word - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/58-length-of-last-word) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

