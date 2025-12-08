# 3494. Find the Minimum Amount of Time to Brew Potions - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired. We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform designed specifically for programmers.
>
> **The All-In-One Powerhouse for Your Career:**
> - 📄 **Professional Resume:** Create a dynamic, tech-focused resume that stands out to recruiters.
> - 🎨 **Visual Portfolio:** Automatically aggregate your GitHub contributions and projects into a stunning showcase.
> - ✍️ **Tech Blog:** Share your knowledge and build authority with a clean, distraction-free blogging space.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [3494. Find the Minimum Amount of Time to Brew Potions - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/3494-find-the-minimum-amount-of-time-to-brew-potions) for a better experience!

LeetCode link: [3494. Find the Minimum Amount of Time to Brew Potions](https://leetcode.com/problems/find-the-minimum-amount-of-time-to-brew-potions), difficulty: **Medium**.

## LeetCode description of "3494. Find the Minimum Amount of Time to Brew Potions"

You are given two integer arrays, `skill` and `mana`, of length `n` and `m`, respectively.

In a laboratory, `n` wizards must brew `m` potions in order. Each potion has a mana capacity `mana[j]` and **must** pass through **all** the wizards sequentially to be brewed properly. The time taken by the ith wizard on the *j<sup>th</sup>* potion is *time<sub>ij</sub>* = `skill[i] * mana[j]`.

Since the brewing process is delicate, a potion **must** be passed to the next wizard immediately after the current wizard completes their work. This means the timing must be synchronized so that each wizard begins working on a potion **exactly** when it arrives.

Return the **minimum** amount of time required for the potions to be brewed properly.

### [Example 1]

**Input**: `skill = [1,5,2,4], mana = [5,1,4,2]`

**Output**: `110`

**Explanation**: 

<table><thead>
<tr>
<th>Potion ID</th>
<th>Start Time</th>
<th>Wizard 0 Done Time</th>
<th>Wizard 1 Done Time</th>
<th>Wizard 2 Done Time</th>
<th>Wizard 3 Done Time</th>
</tr>
</thead><tbody>
<tr>
<td>0</td>
<td>0</td>
<td>5</td>
<td>30</td>
<td>40</td>
<td>60</td>
</tr>
<tr>
<td>1</td>
<td>52</td>
<td>53</td>
<td>58</td>
<td>60</td>
<td>64</td>
</tr>
<tr>
<td>2</td>
<td>54</td>
<td>58</td>
<td>78</td>
<td>86</td>
<td>102</td>
</tr>
<tr>
<td>3</td>
<td>86</td>
<td>88</td>
<td>98</td>
<td>102</td>
<td>110</td>
</tr>
</tbody></table>

<p>As an example for why wizard 0 cannot start working on the 1st potion before time <code>t = 52</code>, consider the case where the wizards started preparing the 1st potion at time <code>t = 50</code>. At time <code>t = 58</code>, wizard 2 is done with the 1st potion, but wizard 3 will still be working on the 0th potion till time <code>t = 60</code>.</p>


### [Example 2]

**Input**: `skill = [1,1,1], mana = [1,1,1]`

**Output**: `5`

**Explanation**: 

<ol>
<li>Preparation of the 0<sup>th</sup> potion begins at time <code>t = 0</code>, and is completed by time <code>t = 3</code>.</li>
<li>Preparation of the 1<sup>st</sup> potion begins at time <code>t = 1</code>, and is completed by time <code>t = 4</code>.</li>
<li>Preparation of the 2<sup>nd</sup> potion begins at time <code>t = 2</code>, and is completed by time <code>t = 5</code>.</li>
</ol>


### [Example 3]

**Input**: `skill = [1,2,3,4], mana = [1,2]`

**Output**: `21`

### [Constraints]

- `n == skill.length`
- `m == mana.length`
- `1 <= n, m <= 5000`
- `1 <= mana[i], skill[i] <= 5000`

### [Hints]

<details>
  <summary>Hint 1</summary>
  Maintain each wizard's earliest free time (for the last potion) as `f[i]`.

  
</details>

<details>
  <summary>Hint 2</summary>
  Let `x` be the current mana value. Starting from `now = f[0]`, update `now = max(now + skill[i - 1] * x, f[i])` for `i in [1..n]`. Then, the final `f[n - 1] = now + skill[n - 1] * x` for this potion.

  
</details>

<details>
  <summary>Hint 3</summary>
  Update all other `f` values by `f[i] = f[i + 1] - skill[i + 1] * x` for `i in [0..n - 2]` (in reverse order).

  
</details>

## Intuition

- The first step to solve this problem is to determine what algorithm to use. Because the production of each bottle of potion depends on the completion of the previous bottle of potion in the hands of some wizards, and the potion itself needs to be produced bottle by bottle, so what algorithm should be used?
    <details><summary>Click to view the answer</summary><p> Dynamic Programming. </p></details>

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

1. Determine the meaning of each value of the array `dp`. So what does each `dp[i][j]`  represent?
    mark-detail The row represents the potion, and the column represents the wizard, which has been hinted in the question. <br>The meaning is: the time it takes for the `j`<sup>th</sup> wizard to complete the `i`<sup>th</sup> bottle of potion. I deliberately did not add the word "shortest" because the potion cannot be separated from the hands of the wizard during the manufacturing process! mark-detail
2. How to initialize the group value?
    mark-detail Just set all the values to `0`. mark-detail
3. Fill in the `dp` grid data "in order" according to an example. How to do it?
    mark-detail The data in the table given in "Example 1" fully meets our needs, so just use it directly. mark-detail
4. Based on the `dp` grid data, derive the "recursive formula". What it the "recursive formula"?
    mark-detail Condition 1: After the `j-1`<sup>th</sup> wizard has finished his work on the `i`<sup>th</sup> bottle of potion, the `j`<sup>th</sup> wizard can start his work on the `i`<sup>th</sup> bottle of potion. <br>Condition 2: After the `j`<sup>th</sup> wizard has finished his work on the `i-1`<sup>th</sup> bottle of potion, he can start his work on the `i`<sup>th</sup> bottle of potion. <br>Condition 3: After the `j`<sup>th</sup> wizard finishes his work on the `i`<sup>th</sup> potion, the `j+1`<sup>th</sup> wizard must immediately start his work on the `i`<sup>th</sup> potion. That is, the potion cannot wait for anyone, and the `j`<sup>th</sup> wizard **cannot start working too early**.mark-detail
5. Write a program and print the `dp` array. If it is not as expected, adjust it. What did you find?
    - As a result, you find that some values are smaller than expected. At this time, you need to think about whether there is a logical loophole based on those "abnormal" values. Where is the loophole?
        mark-detail The logical loophole is: some wizards still start working too early, causing the potion to wait for people. mark-detail
    - How to fix the logic loophole?
        mark-detail **Process again from the back to the front**, because the last wizard no longer has the problem of starting work too early. This shows the importance of traversal order. It may be from front to back, or from back to front, or both. mark-detail

## Complexity

- Time complexity: `O(M * N)`.
- Space complexity: `O(N)`.

## Ruby

```ruby
# It may fail, but its not the problem of algorithm because same code can be accepted in other languages
# @param {Integer[]} skill
# @param {Integer[]} mana
# @return {Integer}
def min_time(skill, mana)
  n = skill.size
  m = mana.size
  dp = Array.new(n, 0)

  m.times do |i|
    n.times do |j|
      dp[j] = [dp[j], dp[j - 1]].max if j >= 1 # condition 1 and 2
      time_consuming = mana[i] * skill[j]
      dp[j] = [dp[j], dp[j + 1] - time_consuming].max if j < n - 1 # condition 3
      dp[j] += time_consuming
    end

    # Process again from back to front to prevent any wizard from starting work too early.
    (1...n).to_a.reverse.each do |j|
      dp[j - 1] = dp[j] - mana[i] * skill[j]
    end
  end

  dp[-1]
end
```

## Python

```python
# It may fail, but its not the problem of algorithm because same code can be accepted in other languages
class Solution:
    def minTime(self, skill: List[int], mana: List[int]) -> int:
        n = len(skill)
        m = len(mana)
        dp = [0] * n

        for i in range(m):
            for j in range(n):
                # condition 1 and 2
                if j >= 1:
                    dp[j] = max(dp[j], dp[j - 1])

                time_consuming = mana[i] * skill[j]

                # condition 3
                if j < n - 1:
                    dp[j] = max(dp[j], dp[j + 1] - time_consuming)
                dp[j] += time_consuming

            # Process again from back to front to prevent any wizard from starting work too early.
            for j in range(n - 1, 0, -1):
                dp[j - 1] = dp[j] - mana[i] * skill[j]

        return dp[-1]
```

## JavaScript

```javascript
/**
 * @param {number[]} skill
 * @param {number[]} mana
 * @return {number}
 */
var minTime = function (skill, mana) {
    const n = skill.length;
    const m = mana.length;
    const dp = new Array(n).fill(0);
    
    for (let i = 0; i < m; i++) {
        for (let j = 0; j < n; j++) {
            // condition 1 and 2
            if (j >= 1) {
                dp[j] = Math.max(dp[j], dp[j - 1]);
            }
            const timeConsuming = mana[i] * skill[j];
            // condition 3
            if (j < n - 1) {
                dp[j] = Math.max(dp[j], dp[j + 1] - timeConsuming);
            }
            dp[j] += timeConsuming;
        }
        
        // Process again from back to front to prevent any wizard from starting work too early.
        for (let j = n - 1; j > 0; j--) {
            dp[j - 1] = dp[j] - mana[i] * skill[j];
        }
    }

    return dp[dp.length - 1];
};
```

## Java

```java
class Solution {
    public long minTime(int[] skill, int[] mana) {
        int n = skill.length;
        int m = mana.length;
        long[] dp = new long[n];

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                // condition 1 and 2
                if (j >= 1) {
                    dp[j] = Math.max(dp[j], dp[j - 1]);
                }
                long timeConsuming = (long) mana[i] * skill[j];
                // condition 3
                if (j < n - 1) {
                    dp[j] = Math.max(dp[j], dp[j + 1] - timeConsuming);
                }
                dp[j] += timeConsuming;
            }

            // Process again from back to front to prevent any wizard from starting work too
            // early
            for (int j = n - 1; j > 0; j--) {
                dp[j - 1] = dp[j] - (long) mana[i] * skill[j];
            }
        }

        return dp[n - 1];
    }
}
```

## C#

```csharp
public class Solution
{
    public long MinTime(int[] skill, int[] mana)
    {
        int n = skill.Length;
        int m = mana.Length;
        long[] dp = new long[n];

        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                // condition 1 and 2
                if (j >= 1)
                {
                    dp[j] = Math.Max(dp[j], dp[j - 1]);
                }
                long timeConsuming = (long)mana[i] * skill[j];
                // condition 3
                if (j < n - 1)
                {
                    dp[j] = Math.Max(dp[j], dp[j + 1] - timeConsuming);
                }
                dp[j] += timeConsuming;
            }

            // Process again from back to front to prevent any wizard from starting work too early
            for (int j = n - 1; j > 0; j--)
            {
                dp[j - 1] = dp[j] - (long)mana[i] * skill[j];
            }
        }

        return dp[n - 1];
    }
}
```

## C++

```cpp
class Solution {
public:
    long long minTime(vector<int>& skill, vector<int>& mana) {
        int n = skill.size();
        int m = mana.size();
        vector<long long> dp(n, 0);

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                // condition 1 and 2
                if (j >= 1) {
                    dp[j] = max(dp[j], dp[j - 1]);
                }
                long long time_consuming = (long long)mana[i] * skill[j];
                // condition 3
                if (j < n - 1) {
                    dp[j] = max(dp[j], dp[j + 1] - time_consuming);
                }
                dp[j] += time_consuming;
            }

            // Process again from back to front to prevent any wizard from
            // starting work too early
            for (int j = n - 1; j > 0; j--) {
                dp[j - 1] = dp[j] - (long long)mana[i] * skill[j];
            }
        }

        return dp[n - 1];
    }
};
```

## Go

```go
func minTime(skill []int, mana []int) int64 {
    n := len(skill)
    m := len(mana)
    dp := make([]int64, n)

    for i := 0; i < m; i++ {
        for j := 0; j < n; j++ {
            // condition 1 and 2
            if j >= 1 && dp[j-1] > dp[j] {
                dp[j] = dp[j-1]
            }
            timeConsuming := int64(mana[i]) * int64(skill[j])
            // condition 3
            if j < n-1 {
                if dp[j+1]-timeConsuming > dp[j] {
                    dp[j] = dp[j+1] - timeConsuming
                }
            }
            dp[j] += timeConsuming
        }

        // Process again from back to front to prevent any wizard from starting work too early
        for j := n - 1; j > 0; j-- {
            dp[j-1] = dp[j] - int64(mana[i])*int64(skill[j])
        }
    }

    return dp[n-1]
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired. We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform designed specifically for programmers.
>
> **The All-In-One Powerhouse for Your Career:**
> - 📄 **Professional Resume:** Create a dynamic, tech-focused resume that stands out to recruiters.
> - 🎨 **Visual Portfolio:** Automatically aggregate your GitHub contributions and projects into a stunning showcase.
> - ✍️ **Tech Blog:** Share your knowledge and build authority with a clean, distraction-free blogging space.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [3494. Find the Minimum Amount of Time to Brew Potions - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/3494-find-the-minimum-amount-of-time-to-brew-potions) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

