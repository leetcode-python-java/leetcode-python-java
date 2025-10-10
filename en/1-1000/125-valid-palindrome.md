# 125. Valid Palindrome - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

Visit original link: [125. Valid Palindrome - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/125-valid-palindrome) for a better experience!

LeetCode link: [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome), difficulty: **Easy**.

## LeetCode description of "125. Valid Palindrome"

A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` if it is a **palindrome**, or `false` otherwise.

### [Example 1]

**Input**: `s = "A man, a plan, a canal: Panama"`

**Output**: `true`

**Explanation**: `"amanaplanacanalpanama" is a palindrome.`

### [Example 2]

**Input**: `s = "race a car"`

**Output**: `false`

**Explanation**: `"raceacar" is not a palindrome.`

### [Example 3]

**Input**: `s = " "`

**Output**: `true`

**Explanation**: 

<p>s is an empty string &quot;&quot; after removing non-alphanumeric characters.<br>
Since an empty string reads the same forward and backward, it is a palindrome.</p>


### [Constraints]

- `1 <= s.length <= 2 * 10^5`
- `s` consists only of printable ASCII characters.

## Intuition

1. Remove invalid characters.
2. Use `valid_s == valid_s.reverse` to check whether it is a palindrome.

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Ruby

```ruby
# @param {String} s
# @return {Boolean}
def is_palindrome(s)
  valid_chars = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'
  valid_s = ''

  s.downcase.chars.each do |char|
    if valid_chars.include?(char)
      valid_s << char
    end
  end

  valid_s == valid_s.reverse
end
```

## Python

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        valid_chars = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'
        valid_s = ''

        for char in s.lower():
            if char in valid_chars:
                valid_s += char

        return valid_s == valid_s[::-1]
```

## Java

```java
class Solution {
    public boolean isPalindrome(String s) {
        var validChars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
        var validS = new StringBuilder();

        for (char c : s.toLowerCase().toCharArray()) {
            if (validChars.indexOf(c) != -1) {
                validS.append(c);
            }
        }

        var cleaned = validS.toString();
        var reversed = validS.reverse().toString();

        return cleaned.equals(reversed);
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCode.blog](https://leetcode.blog): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [125. Valid Palindrome - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/125-valid-palindrome).

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).
