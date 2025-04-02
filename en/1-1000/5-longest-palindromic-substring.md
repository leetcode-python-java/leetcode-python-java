# 5. Longest Palindromic Substring - LeetCode Best Practices

Visit original link: [5. Longest Palindromic Substring - LeetCode Best Practices](https://leetcoder.net/en/leetcode/5-longest-palindromic-substring) for a better experience!

LeetCode link: [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring), difficulty: **Medium**.

## LeetCode description of "5. Longest Palindromic Substring"

Given a string `s`, return *the longest palindromic substring in `s`*.

- A string is **palindromic** if it reads the same forward and backward.
- A **substring** is a contiguous **non-empty** sequence of characters within a string.

### [Example 1]

**Input**: `s = "babad"`

**Output**: `"bab"`

**Explanation**: `"aba" is also a valid answer.`

### [Example 2]

**Input**: `s = "cbbd"`

**Output**: `"bb"`

### [Constraints]

- `1 <= s.length <= 1000`
- `s` consist of only digits and English letters.

### [Hints]

<details>
  <summary>Hint 1</summary>
  How can we reuse a previously computed palindrome to compute a larger palindrome?

  
</details>

<details>
  <summary>Hint 2</summary>
  If “aba” is a palindrome, is “xabax” a palindrome? Similarly is “xabay” a palindrome?

  
</details>

<details>
  <summary>Hint 3</summary>
  Complexity based hint:
If we use brute-force and check whether for every start and end position a substring is a palindrome we have O(n^2) start - end pairs and O(n) palindromic checks. Can we reduce the time for palindromic checks to O(1) by reusing some previous computation.

  
</details>

## Intuition



## Complexity

- Time complexity: ``.
- Space complexity: ``.

## Ruby

```ruby
# @param {String} s
# @return {String}
def longest_palindrome(s)
  longest = s[0]
  s = s.chars.join("#")

  s.size.times do |i|
    j = 1

    while j <= i and i + j < s.size
      break if s[i - j] != s[i + j]

      if s[i - j] == '#'
        j += 1
        next
      end
      
      length = j * 2 + 1

      if length > longest.size
        longest = s[i - j..i + j]
      end
      
      j += 1
    end
  end
  
  longest.gsub('#', '')
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [leetcoder.net](https://leetcoder.net): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [5. Longest Palindromic Substring - LeetCode Best Practices](https://leetcoder.net/en/leetcode/5-longest-palindromic-substring).

GitHub repository: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

