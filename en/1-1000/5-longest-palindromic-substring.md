# 5. Longest Palindromic Substring - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**Like.dev**](https://www.like.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Like.dev →**](https://www.like.dev)

---

Visit original link: [5. Longest Palindromic Substring - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/5-longest-palindromic-substring) for a better experience!

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



## Pattern of "Dynamic Programming"

"Dynamic Programming" requires the use of the `dp` array to store the results. The value of `dp[i][j]` can be converted from its previous (or multiple) values ​​through a formula. Therefore, the value of `dp[i][j]` is derived step by step, and it is related to the previous `dp` record value.

#### "Dynamic programming" is divided into five steps

1. Determine the **meaning** of each value of the array `dp`.
2. Initialize the value of the array `dp`.
3. Fill in the `dp` grid data **in order** according to an example.
4. Based on the `dp` grid data, derive the **recursive formula**.
5. Write a program and print the `dp` array. If it is not as expected, adjust it.

#### Detailed description of these five steps

1. Determine the **meaning** of each value of the array `dp`.
    - First determine whether `dp` is a one-dimensional array or a two-dimensional array. A `one-dimensional rolling array` means that the values ​​of the array are overwritten at each iteration. Most of the time, using `one-dimensional rolling array` instead of `two-dimensional array` can simplify the code; but for some problems, such as operating "two swappable arrays", for the sake of ease of understanding, it is better to use `two-dimensional array`.
    - Try to use the meaning of the `return value` required by the problem as the meaning of `dp[i]` (one-dimensional) or `dp[i][j]` (two-dimensional). It works about 60% of the time. If it doesn't work, try other meanings.
    - Try to save more information in the design. Repeated information only needs to be saved once in a `dp[i]`.
    - Use simplified meanings. If the problem can be solved with `boolean value`, don't use `numeric value`.
2. Initialize the value of the array `dp`. The value of `dp` involves two levels:
    1. The length of `dp`. Usually: `condition array length plus 1` or `condition array length`.
    2. The value of `dp[i]` or `dp[i][j]`. `dp[0]` or `dp[0][0]` sometimes requires special treatment.
3. Fill in the `dp` grid data **in order** according to an example.
    - The "recursive formula" is the core of the "dynamic programming" algorithm. But the "recursive formula" is obscure. If you want to get it, you need to make a table and use data to inspire yourself.
    - If the original example is not good enough, you need to redesign one yourself.
    - According to the example, fill in the `dp` grid data "in order", which is very important because it determines the traversal order of the code.
    - Most of the time, from left to right, from top to bottom. But sometimes it is necessary to traverse from right to left, from bottom to top, from the middle to the right (or left), such as the "palindrome" problems. Sometimes, it is necessary to traverse a line twice, first forward and then backward.
    - When the order is determined correctly, the starting point is determined. Starting from the starting point, fill in the `dp` grid data "in order". This order is also the order in which the program processes.
    - In this process, you will get inspiration to write a "recursive formula". If you can already derive the formula, you do not need to complete the grid.
4. Based on the `dp` grid data, derive the **recursive formula**.
    - There are three special positions to pay attention to: `dp[i - 1][j - 1]`, `dp[i - 1][j]` and `dp[i][j - 1]`, the current `dp[i][j]` often depends on them.
    - When operating "two swappable arrays", due to symmetry, we may need to use `dp[i - 1][j]` and `dp[i][j - 1]` at the same time.
5. Write a program and print the `dp` array. If it is not as expected, adjust it.
    - Focus on analyzing those values that are not as expected.

After reading the above, do you feel that "dynamic programming" is not that difficult? Try to solve this problem. 🤗

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

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**Like.dev**](https://www.like.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Like.dev →**](https://www.like.dev)

---

Visit original link: [5. Longest Palindromic Substring - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/5-longest-palindromic-substring) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

