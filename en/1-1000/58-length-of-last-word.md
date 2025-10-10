# 58. Length of Last Word - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

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
**Method 1:** Solve it directly by traversing from the end to the beginning.
**Method 2:** Reverse the string `s` and then find the length of the first word.
In this problem, we use **Method 2**. After completing Method 2, it’s recommended to also try implementing Method 1.
</p></details>

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `1`.

## Python

```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        s = s[::-1]  # Reverse the string

        start_index = 0

        while start_index < len(s) and s[start_index] == ' ':
            start_index += 1

        end_index = start_index

        while end_index < len(s) and s[end_index] != ' ':
            end_index += 1

        return end_index - start_index
```

## Ruby

```ruby
# @param {String} s
# @return {Integer}
def length_of_last_word(s)
  s.reverse!

  start_index = 0

  while s[start_index] == ' '
    start_index += 1
  end

  end_index = start_index

  while end_index < s.size && s[end_index] != ' '
    end_index += 1
  end

  end_index - start_index
end
```

## Java

```java
class Solution {
    public int lengthOfLastWord(String s) {
        // Reverse the string
        var sb = new StringBuilder(s);
        String reversed = sb.reverse().toString();

        var startIndex = 0;
        // Skip leading spaces (which were trailing spaces in original)
        while (startIndex < reversed.length() && reversed.charAt(startIndex) == ' ') {
            startIndex++;
        }

        var endIndex = startIndex;
        while (endIndex < reversed.length() && reversed.charAt(endIndex) != ' ') {
            endIndex++;
        }

        return endIndex - startIndex;
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCode.blog](https://leetcode.blog): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [58. Length of Last Word - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/58-length-of-last-word).

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).
