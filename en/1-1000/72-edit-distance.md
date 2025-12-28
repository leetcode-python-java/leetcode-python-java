# 72. Edit Distance - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [72. Edit Distance - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/72-edit-distance) for a better experience!

LeetCode link: [72. Edit Distance](https://leetcode.com/problems/edit-distance), difficulty: **Medium**.

## LeetCode description of "72. Edit Distance"

Given two strings `word1` and `word2`, return the **minimum** number of operations required to convert `word1` to `word2`.

You have the following three operations permitted on a word:

- Insert a character
- Delete a character
- Replace a character

### [Example 1]

**Input**: `word1 = "horse", word2 = "ros"`

**Output**: `3`

**Explanation**: 

<p>horse -&gt; rorse (replace &#39;h&#39; with &#39;r&#39;)<br>
rorse -&gt; rose (remove &#39;r&#39;)<br>
rose -&gt; ros (remove &#39;e&#39;)</p>


### [Example 2]

**Input**: `word1 = "intention", word2 = "execution"`

**Output**: `5`

**Explanation**: 

<p>intention -&gt; inention (remove &#39;t&#39;)<br>
inention -&gt; enention (replace &#39;i&#39; with &#39;e&#39;)<br>
enention -&gt; exention (replace &#39;n&#39; with &#39;x&#39;)<br>
exention -&gt; exection (replace &#39;n&#39; with &#39;c&#39;)<br>
exection -&gt; execution (insert &#39;u&#39;)</p>


### [Constraints]

1. `0 <= word1.length, word2.length <= 500`
2. `word1` and `word2` consist of lowercase English letters.

## Intuition

It is a question of comparing two strings. After doing similar questions many times, we will develop an intuition to use Dynamic Programming with *two-dimensional* arrays.

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

## Pattern of "Subsequence Problems"

- Since there are two swappable arrays (or strings) to compare, we can use **two-dimensional** arrays as `dp`.
- The traversal order of `dp` array is from top to bottom, then from left to right.

## Step-by-Step Solution

1. Determine the **meaning** of each value of the array `dp`.
    - `dp[i][j]` represents the **minimum** number of operations required to convert `word1`'s first `i` letters to `word2`'s first `j` letters.
    - `dp[i][j]` is an integer.
2. Initialize the value of the array `dp`.
    - Use an example:

    ```
    After initialization, the 'dp' array would be:  
    #     r o s
    #   0 1 2 3 # dp[0]
    # h 1 0 0 0
    # o 2 0 0 0
    # r 3 0 0 0
    # s 4 0 0 0
    # e 5 0 0 0
    ```
    - `dp[i][0] = i`, because `dp[i][0]` represents the empty string, and the number of operations is just the number of chars to be deleted.
    - `dp[0][j] = j`, the reason is the same as the previous line, just viewed from the opposite angle: convert `word2` to `word1`.

3. Fill in the `dp` grid data **in order** according to an example.

    ```
    1. Convert `h` to `ros`. 
    #     r o s
    #   0 1 2 3
    # h 1 1 2 3 # dp[1]
    ```
    ```
    2. Convert `ho` to `ros`. 
    #     r o s
    #   0 1 2 3
    # h 1 1 2 3
    # o 2 2 1 2
    ```
    ```
    3. Convert `hor` to `ros`. 
    #     r o s
    #   0 1 2 3
    # h 1 1 2 3
    # o 2 2 1 2
    # r 3 2 2 2
    ```
    ```
    4. Convert `hors` to `ros`. 
    #     r o s
    #   0 1 2 3
    # h 1 1 2 3
    # o 2 2 1 2
    # r 3 2 2 2
    # s 4 3 3 2
    ```
    ```
    5. Convert `horse` to `ros`. 
    #     r o s
    #   0 1 2 3
    # h 1 1 2 3
    # o 2 2 1 2
    # r 3 2 2 2
    # s 4 3 3 2
    # e 5 4 4 3 # dp[5]
    ```
4. Based on the `dp` grid data, derive the **recursive formula**.

    ```python
    if word1[i - 1] == word2[j - 1]:
        dp[i][j] = dp[i - 1][j - 1]
    else:
        dp[i][j] = min(
          dp[i - 1][j - 1],
          dp[i - 1][j],
          dp[i][j - 1],
        ) + 1
    ```
5. Write a program and print the `dp` array. If it is not as expected, adjust it.

## Complexity

- Time complexity: `O(N * M)`.
- Space complexity: `O(N * M)`.

## Java

```java
class Solution {
    public int minDistance(String word1, String word2) {
        var dp = new int[word1.length() + 1][word2.length() + 1];
        for (var i = 0; i < dp.length; i++) {
            dp[i][0] = i;
        }
        for (var j = 0; j < dp[0].length; j++) {
            dp[0][j] = j;
        }

        for (var i = 1; i < dp.length; i++) {
            for (var j = 1; j < dp[0].length; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = Math.min(dp[i - 1][j - 1], Math.min(dp[i - 1][j], dp[i][j - 1])) + 1;
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
    public int MinDistance(string word1, string word2)
    {
        var dp = new int[word1.Length + 1, word2.Length + 1];
        
        for (var i = 0; i < dp.GetLength(0); i++)
            dp[i, 0] = i;
        
        for (var j = 0; j < dp.GetLength(1); j++)
            dp[0, j] = j;

        for (var i = 1; i < dp.GetLength(0); i++)
        {
            for (var j = 1; j < dp.GetLength(1); j++)
            {
                if (word1[i - 1] == word2[j - 1])
                {
                    dp[i, j] = dp[i - 1, j - 1];
                }
                else
                {
                    dp[i, j] = Math.Min(dp[i - 1, j - 1], Math.Min(dp[i - 1, j], dp[i, j - 1])) + 1;
                }
            }
        }

        return dp[dp.GetUpperBound(0), dp.GetUpperBound(1)];
    }
}
```

## Python

```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        dp = [[0] * (len(word2) + 1) for _ in range(len(word1) + 1)]
        for i in range(len(dp)):
            dp[i][0] = i
        for j in range(len(dp[0])):
            dp[0][j] = j
        
        for i in range(1, len(dp)):
            for j in range(1, len(dp[0])):
                if word1[i - 1] == word2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1]
                else:
                    dp[i][j] = min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1
        
        return dp[-1][-1]
```

## C++

```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        vector<vector<int>> dp(word1.size() + 1, vector<int>(word2.size() + 1));
        for (auto i = 0; i < dp.size(); i++) {
            dp[i][0] = i;
        }
        for (auto j = 0; j < dp[0].size(); j++) {
            dp[0][j] = j;
        }

        for (auto i = 1; i < dp.size(); i++) {
            for (auto j = 1; j < dp[0].size(); j++) {
                if (word1[i - 1] == word2[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = min({dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]}) + 1;
                }
            }
        }

        return dp[dp.size() - 1][dp[0].size() - 1];
    }
};
```

## JavaScript

```javascript
var minDistance = function (word1, word2) {
  const dp = Array(word1.length + 1).fill().map(
    () => Array(word2.length + 1).fill(0)
  )
  dp.forEach((_, i) => { dp[i][0] = i })
  dp[0].forEach((_, j) => { dp[0][j] = j })

  for (let i = 1; i < dp.length; i++) {
    for (let j = 1; j < dp[0].length; j++) {
      if (word1[i - 1] == word2[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1]
      } else {
        dp[i][j] = Math.min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1
      }
    }
  }

  return dp.at(-1).at(-1)
};
```

## Go

```go
func minDistance(word1 string, word2 string) int {
    dp := make([][]int, len(word1) + 1)
    for i := range dp {
        dp[i] = make([]int, len(word2) + 1)
        dp[i][0] = i
    }
    for j := range dp[0] {
        dp[0][j] = j
    }

    for i := 1; i < len(dp); i++ {
        for j := 1; j < len(dp[0]); j++ {
            if word1[i - 1] == word2[j - 1] {
                dp[i][j] = dp[i - 1][j - 1]
            } else {
                dp[i][j] = min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1
            }
        }
    }

    return dp[len(dp) - 1][len(dp[0]) - 1]
}
```

## Ruby

```ruby
def min_distance(word1, word2)
  dp = Array.new(word1.size + 1) do
    Array.new(word2.size + 1, 0)
  end
  dp.each_with_index do |_, i|
    dp[i][0] = i
  end
  dp[0].each_with_index do |_, j|
    dp[0][j] = j
  end

  (1...dp.size).each do |i|
    (1...dp[0].size).each do |j|
      dp[i][j] =
        if word1[i - 1] == word2[j - 1]
          dp[i - 1][j - 1]
        else
          [ dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1] ].min + 1
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
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [72. Edit Distance - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/72-edit-distance) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

