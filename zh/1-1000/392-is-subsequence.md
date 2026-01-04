# 392. 判断子序列 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**leader.me**](https://www.leader.me) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.leader.me`，极具职业含金量的专属域名。
>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[392. 判断子序列 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/392-is-subsequence)，体验更佳！

力扣链接：[392. 判断子序列](https://leetcode.cn/problems/is-subsequence), 难度等级：**中等**。

## LeetCode “392. 判断子序列”问题描述

给定字符串 **s** 和 **t** ，判断 **s** 是否为 **t** 的子序列。

字符串的一个**子序列**是原始字符串删除一些（也可以不删除）字符而不改变剩余字符相对位置形成的新字符串。（例如，`"ace"`是`"abcde"`的一个子序列，而`"aec"`不是）。

**进阶**：

如果有大量输入的 `S`，称作 `S1, S2, ... , Sk` 其中 `k >= 10亿`，你需要依次检查它们是否为 `T` 的子序列。在这种情况下，你会怎样改变代码？

### [示例 1]

**输入**: `s = "abc", t = "ahbgdc"`

**输出**: `true`

### [示例 2]

**输入**: `s = "axc", t = "ahbgdc"`

**输出**: `false`

### [约束]

- `0 <= s.length <= 100`
- `0 <= t.length <= 10^4`
- `s` and `t` consist only of lowercase English letters.

## 思路 1

- 定义两个指针，最初分别指向两个字符串的头部，字符用`t[i]`, `s[j]`引用。
- 在对`t`的遍历过程中，`i`自动加1，如果`t[i] == s[j]`，则`j += 1`。
- 如果`j >= s.length`，返回`true`。如果遍历完`t`了，仍然没有提前返回`true`，则返回`false`。

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

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

## 思路 2

- `题解1`本质上是用`滚动变量`实现的“动态规划”算法。它很好理解，并且空间复杂度降到了`O(1)`。
- 但现在，我们不仅不做降维，还要升维。理解和实现起来都会更困难些。那为什么还要做这种吃力不讨好的事情呢？
    <details><summary>点击查看答案</summary><p> 因为它能处理一类在动态规划中常见的、更为复杂的场景。比如：[583. 两个字符串的删除操作](583-delete-operation-for-two-strings.md) 等。</p></details>
- 本题用一维的滚动数组实现“动态规划”算法，可以吗？
    <details><summary>点击查看答案</summary><p> 当然可以，但考虑本题`一维的滚动数组`不如`二维数组`好理解，实现的过程也容易出错，所以我没有给出相关的代码实现。如何你有兴趣，可以尝试下。</p></details>
- **比较两个字符串**的题目，属于处理“两个对等数组”，类似的题目做过多次后，我们会形成使用`二维数组`进行动态规划的直觉。

## “动态规划”的模式

“动态规划”，需要用`dp`数组来保存结果。`dp[i][j]`的值可以由它的前一个（或多个）值通过公式转化出来。因此，`dp[i][j]`值是一步一步推导出来的，它和先前的`dp`记录值都有联系。

#### “动态规划”分为五步

1. 确定数组`dp`的每个值代表的**含义**。
2. 初始化数组`dp`的值。
3. 根据一个示例，**按顺序**填入`dp`网格数据。
4. 根据`dp`网格数据，推导出**递推公式**。
5. 写出程序，并打印`dp`数组，不合预期就调整。

#### 细说这五步

1. 确定数组`dp`的每个值代表的**含义**。
    - 先确定`dp`是一维数组还是二维数组。“一维滚动数组”意味着每次迭代时都会覆盖数组的值。大多时候，用“一维滚动数组”代替“二维数组”可以简化代码；但有些题目，比如要操作“两个位置可互换的数组”，为了理解方便，还是使用“二维数组”。
    - 尝试使用问题所求的`返回值`的含义作为 `dp[i]`（一维）或`dp[i][j]`（二维）的含义，约60%的概率能行。如果不行，再尝试其他含义。
    - 设计上尽量考虑保存更丰富的信息，重复信息只在某个`dp[i]`中保存一次就够了。
    - 使用简化的含义。如果用`布尔值`可以解决问题，就不要用`数值`。
2. 初始化数组`dp`的值。`dp`的值涉及两个层面：
    1. `dp`的长度。通常是：`条件数组长度加1`或`条件数组长度`。
    2. `dp[i]`或`dp[i][j]`的值。`dp[0]`或`dp[0][0]`有时需要特殊处理。
3. 根据一个示例，**按顺序**填入`dp`网格数据。
    - “递推公式”是“动态规划”算法的核心。但“递推公式”是隐晦的，想得到它，就需要制表，用数据启发自己。
    - 如果原示例不够好，需要自己重新设计一个。
    - 根据示例，填入`dp`网格数据，需要“按顺序”填，这是很重要的，因为它决定了代码的遍历顺序。
    - 大多时候，从左到右，从上到下。但有时需要从右向左、由下而上、从中间向右（或左），如“回文串”问题。有时，还需要一行遍历两次，先正向，再反向。
    - 当顺序决定对了，起点就决定好了，从起点出发，“按顺序”填写`dp`网格数据，这也是在模拟程序处理的过程。
    - 在此过程中，您将获得写出“递推公式”的灵感。如果您已经能推导出公式，不需要填完网格。
4. 根据`dp`网格数据，推导出**递推公式**。
    - 有三个特别的位置需要注意： `dp[i - 1][j - 1]`、`dp[i - 1][j]`和`dp[i][j - 1]`，当前的 `dp[i][j]`往往取决于它们。
    - 操作“两个位置可互换的数组”时，因为对称性，我们可能需要同时使用`dp[i - 1][j]`和`dp[i][j - 1]`。
5. 写出程序，并打印`dp`数组，不合预期就调整。
    - 重点分析那些不合预期的数值。

读完了上面的内容，是不是感觉“动态规划”也没有那么难了？试着解出这道题吧。🤗

## 步骤

1. 确定 `dp[i][j]` 的**含义**。
    - `dp[i][j]` 表示 `s` 的前 `i` 个字母是否是 `t` 的前 `j` 个字母的子序列。
    - `dp[i][j]` 为 `true` 或 `false`。
2. 确定 `dp` 数组的初始值。
    - 使用示例：

        ```
        After initialization, the 'dp' array would be:
        s = "abc", t = "ahbgdc"
        #     a h b g d c
        #   T T T T T T T # dp[0]
        # a F F F F F F F
        # b F F F F F F F
        # c F F F F F F F
        ```
    - `dp[0][j] = true` 因为 `dp[0]` 表示空字符串，而空字符串是任何字符串的子序列。
    - `dp[i][j] = false (i != 0)`。
3. 根据一个示例，“按顺序”填入`dp`网格数据。

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
4. 根据`dp`网格数据，推导出“递推公式”。

    ```ruby
    if s[i - 1] == t[j - 1]
      dp[i][j] = dp[i - 1][j - 1]
    else
      dp[i][j] = dp[i][j - 1]
    end
    ```
5. 检查 `dp` 数组的值
    - 打印 `dp` 以查看它是否符合预期。

## 复杂度

- 时间复杂度: `O(N * M)`.
- 空间复杂度: `O(N * M)`.

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

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**leader.me**](https://www.leader.me) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.leader.me`，极具职业含金量的专属域名。

>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[392. 判断子序列 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/392-is-subsequence)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

