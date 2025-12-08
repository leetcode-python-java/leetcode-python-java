# 392. Is Subsequence - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
> We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [392. Is Subsequence - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/392-is-subsequence) for a better experience!

LeetCode link: [392. Is Subsequence](https://leetcode.com/problems/is-subsequence), difficulty: **Medium**.

## LeetCode description of "392. Is Subsequence"

Given two strings `s` and `t`, return `true` if `s` is a **subsequence** of `t`, or `false` otherwise.

A **subsequence** of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., `"ace"` is a subsequence of `"abcde"` while `"aec"` is not).


**Follow up**: Suppose there are lots of incoming `s`, say `s1, s2, ..., sk` where `k >= 10^9`, and you want to check one by one to see if `t` has its subsequence. In this scenario, how would you change your code?

### [Example 1]

**Input**: `s = "abc", t = "ahbgdc"`

**Output**: `true`

### [Example 2]

**Input**: `s = "axc", t = "ahbgdc"`

**Output**: `false`

### [Constraints]

- `0 <= s.length <= 100`
- `0 <= t.length <= 10^4`
- `s` and `t` consist only of lowercase English letters.

## Intuition 1

- Define two pointers, initially pointing to the heads of two strings respectively, and reference characters with `t[i]` and `s[j]`.
- During the traversal of `t`, `i` is automatically incremented by 1, and if `t[i] == s[j]`, then `j += 1`.
- If `j >= s.length`, return `true`. If `t` is traversed and still not returned in advance, return `false`.

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Python

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        if s == "":
            return True

        s_index = 0

        for i in range(len(t)):
            if t[i] == s[s_index]:
                s_index += 1

                if s_index >= len(s):
                    return True

        return False
```

## C++

```cpp
class Solution {
public:
    bool isSubsequence(string s, string t) {
        if (s.empty()) {
            return true;
        }

        int s_index = 0;

        for (int i = 0; i < t.length(); i++) {
            if (t[i] == s[s_index]) {
                s_index++;

                if (s_index >= s.length()) {
                    return true;
                }
            }
        }

        return false;
    }
};
```

## Java

```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        if (s.isEmpty()) {
            return true;
        }

        int sIndex = 0;

        for (int i = 0; i < t.length(); i++) {
            if (t.charAt(i) == s.charAt(sIndex)) {
                sIndex++;

                if (sIndex >= s.length()) {
                    return true;
                }
            }
        }

        return false;
    }
}
```

## C#

```csharp
public class Solution
{
    public bool IsSubsequence(string s, string t)
    {
        if (string.IsNullOrEmpty(s))
        {
            return true;
        }

        int sIndex = 0;

        for (int i = 0; i < t.Length; i++)
        {
            if (t[i] == s[sIndex])
            {
                sIndex++;

                if (sIndex >= s.Length)
                {
                    return true;
                }
            }
        }

        return false;
    }
}
```

## Go

```go
func isSubsequence(s string, t string) bool {
    if len(s) == 0 {
        return true
    }

    sIndex := 0

    for i := 0; i < len(t); i++ {
        if t[i] == s[sIndex] {
            sIndex++

            if sIndex >= len(s) {
                return true
            }
        }
    }

    return false
}
```

## JavaScript

```javascript
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isSubsequence = function(s, t) {
    if (s.length === 0) {
        return true;
    }

    let sIndex = 0;

    for (let i = 0; i < t.length; i++) {
        if (t[i] === s[sIndex]) {
            sIndex++;

            if (sIndex >= s.length) {
                return true;
            }
        }
    }

    return false;
};
```

## Ruby

```ruby
# @param {String} s
# @param {String} t
# @return {Boolean}
def is_subsequence(s, t)
  return true if s.empty?

  s_index = 0

  t.each_char.with_index do |char, i|
    if char == s[s_index]
      s_index += 1
      return true if s_index >= s.length
    end
  end

  false
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## Intuition 2

- `Solution 1` is essentially a "dynamic programming" algorithm implemented with `rolling variables`. It is easy to understand, and the space complexity is reduced to `O(1)`.
- But now, not only do we not reduce the dimension, but we also increase the dimension. It will be more difficult to understand and implement. So why do this thankless task?
    <details><summary>Click to view the answer</summary><p> Because it can handle a more complex scenario (e.g. [583. Delete Operation for Two Strings](583-delete-operation-for-two-strings.md)) that is common in dynamic programming. </p></details>
- In this question, can we use a `one-dimensional rolling array` to implement the "dynamic programming" algorithm?
    <details><summary>Click to view the answer</summary><p> Of course, but considering that for this problem a `one-dimensional rolling array` is not as easy to understand as a `two-dimensional array`, and the implementation process is also prone to errors, so here I didn't give the relevant code implementation. If you are interested, you can try it. </p></details>
- The **compare two strings** question is about dealing with "two swappable arrays". After doing similar questions many times, we will form the intuition of using `two-dimensional arrays` for dynamic programming.

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

## Step-by-Step Solution

1. Determine the **meaning** of the `dp[i][j]`.
    - `dp[i][j]` represents whether the first `i` letters of `s` are a subsequence of `t`'s first `j` letters.
    - `dp[i][j]` is `true` or `false`.
2. Determine the `dp` array's initial value.
    - Use an example:

        ```
        After initialization, the 'dp' array would be:
        s = "abc", t = "ahbgdc"
        #     a h b g d c
        #   T T T T T T T # dp[0]
        # a F F F F F F F
        # b F F F F F F F
        # c F F F F F F F
        ```
    - `dp[0][j] = true` because `dp[0]` represents the empty string, and empty string is a subsequence of any string.
    - `dp[i][j] = false (i != 0)`.
3. Fill in the `dp` grid data "in order" according to an example.

    ```
    1. s = "a", t = "ahbgdc" 
    #     a h b g d c
    #   T T T T T T T
    # a F T T T T T T # dp[1]
    ```
    ```
    2. s = "ab", t = "ahbgdc" 
    #     a h b g d c
    #   T T T T T T T
    # a F T T T T T T
    # b F F F T T T T
    ```
    ```
    3. s = "abc", t = "ahbgdc"
    #     a h b g d c
    #   T T T T T T T
    # a F T T T T T T
    # b F F F T T T T
    # c F F F F F F T # dp[3]
    ```
4. Based on the `dp` grid data, derive the "recursive formula".

    ```ruby
    if s[i - 1] == t[j - 1]
      dp[i][j] = dp[i - 1][j - 1]
    else
      dp[i][j] = dp[i][j - 1]
    end
    ```
5. Write a program and print the `dp` array. If it is not as expected, adjust it.

## Complexity

- Time complexity: `O(N * M)`.
- Space complexity: `O(N * M)`.

## Python

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        column_count = len(t) + 1
        dp = [[True] * column_count]
        for _ in s:
            dp.append([False] * column_count)
        
        for i in range(1, len(dp)):
            for j in range(1, len(dp[0])):
                if s[i - 1] == t[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1]
                else:
                    dp[i][j] = dp[i][j - 1]
        
        return dp[-1][-1]
```

## C++

```cpp
class Solution {
public:
    bool isSubsequence(string s, string t) {
        vector<vector<bool>> dp(s.size() + 1, vector<bool>(t.size() + 1));
        fill(dp[0].begin(), dp[0].end(), true);

        for (auto i = 1; i < dp.size(); i++) {
            for (auto j = 1; j < dp[0].size(); j++) {
                if (s[i - 1] == t[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = dp[i][j - 1];
                }
            }
        }

        return dp[dp.size() - 1][dp[0].size() - 1];
    }
};
```

## JavaScript

```javascript
var isSubsequence = function (s, t) {
  const dp = Array(s.length + 1).fill().map(
    () => Array(t.length + 1).fill(false)
  )
  dp[0].fill(true)

  for (let i = 1; i < dp.length; i++) {
    for (let j = 1; j < dp[0].length; j++) {
      if (s[i - 1] == t[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1]
      } else {
        dp[i][j] = dp[i][j - 1]
      }
    }
  }

  return dp.at(-1).at(-1)
};
```

## Go

```go
func isSubsequence(s string, t string) bool {
    dp := make([][]bool, len(s) + 1)
    columnSize := len(t) + 1
    dp[0] = slices.Repeat([]bool{true}, columnSize)
    for i := 1; i < len(dp); i++ {
        dp[i] = make([]bool, columnSize)
    }

    for i := 1; i < len(dp); i++ {
        for j := 1; j < len(dp[0]); j++ {
            if s[i - 1] == t[j - 1] {
                dp[i][j] = dp[i - 1][j - 1]
            } else {
                dp[i][j] = dp[i][j - 1]
            }
        }
    }

    return dp[len(dp) - 1][len(dp[0]) - 1]
}
```

## Java

```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        var dp = new boolean[s.length() + 1][t.length() + 1];
        Arrays.fill(dp[0], true);

        for (var i = 1; i < dp.length; i++) {
            for (var j = 1; j < dp[0].length; j++) {
                if (s.charAt(i - 1) == t.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = dp[i][j - 1];
                }
            }
        }

        return dp[dp.length - 1][dp[0].length - 1];
    }
}
```

## C#

```csharp
public class Solution
{
    public bool IsSubsequence(string s, string t)
    {
        var dp = new bool[s.Length + 1, t.Length + 1];
        for (var j = 0; j < dp.GetLength(1); j++)
            dp[0, j] = true;
        
        for (var i = 1; i < dp.GetLength(0); i++)
        {
            for (var j = 1; j < dp.GetLength(1); j++)
            {
                if (s[i - 1] == t[j - 1])
                {
                    dp[i, j] = dp[i - 1, j - 1];
                }
                else
                {
                    dp[i, j] = dp[i, j - 1];
                }
            }
        }

        return dp[dp.GetUpperBound(0), dp.GetUpperBound(1)];
    }
}
```

## Ruby

```ruby
def is_subsequence(s, t)
  dp = Array.new(s.size + 1) do |i|
    Array.new(t.size + 1, i == 0 ? true : false)
  end

  (1...dp.size).each do |i|
    (1...dp[0].size).each do |j|
      dp[i][j] =
        if s[i - 1] == t[j - 1]
          dp[i - 1][j - 1]
        else
          dp[i][j - 1]
        end
    end
  end

  dp[-1][-1]
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
> We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [392. Is Subsequence - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/392-is-subsequence) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

