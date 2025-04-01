# 583. 两个字符串的删除操作 - 力扣题解最佳实践

访问原文链接：[583. 两个字符串的删除操作 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/583-delete-operation-for-two-strings)，体验更佳！

力扣链接：[583. 两个字符串的删除操作](https://leetcode.cn/problems/delete-operation-for-two-strings), 难度：**中等**。

## 力扣“583. 两个字符串的删除操作”问题描述

给定两个单词 `word1` 和 `word2` ，返回使得 `word1` 和  `word2` 相同所需的最小步数。

**每步** 可以删除任意一个字符串中的一个字符。

### [示例 1]

**输入**: `word1 = "sea", word2 = "eat"`

**输出**: `2`

**解释**: `第一步将 "sea" 变为 "ea" ，第二步将 "eat "变为 "ea"`

### [示例 2]

**输入**: `word1 = "leetcode", word2 = "etco"`

**输出**: `4`

### [约束]

- `1 <= word1.length, word2.length <= 500`
- `word1` 和 `word2` 只包含小写英文字母

## 思路

这是一道**比较两个字符串**的问题。在多次做过类似的题目之后，我们会形成使用`二维数组动态规划`的直觉。

## 步骤

### “动态规划”的常用步骤

这**五个步骤**是解决`动态规划`问题的一个模式。

1. 确定`dp[i][j]`的**含义**
    - 因为有两个字符串，所以我们可以使用二维数组作为默认选项。
    - 首先尝试使用问题的`return`值作为`dp[i][j]`的值来确定`dp[i][j]`的含义。如果不行，再尝试其他方法。
    - `dp[i][j]`表示使`word1`的前`i`个字母和`word2`的前`j`个字母相同所需的**最少**步数。
    - `dp[i][j]`是一个整数。
2. 确定 `dp` 数组的初值
    - 举例说明：

        ```
        初始化后，'dp' 数组为：
        # e a t
        # 0 1 2 3 # dp[0]
        # s 1 0 0 0
        # e 2 0 0 0
        # a 3 0 0 0
        ```
    - `dp[0][j] = j`，因为 `dp[0]` 表示空字符串，步数就是要删除的字符数。
    - `dp[i][0] = i`，理由和上一行一样，只是从垂直方向看。
3. 确定 `dp` 数组的递归公式
    - 尝试完成网格。在这个过程中，你会得到推导公式的灵感。

        ```
        1. word1 = "s", word2 = "eat"
        # e a t
        # 0 1 2 3
        # s 1 2 3 4 # dp[1]
        ```
        ```
        2. word1 = "se", word2 = "eat"
        # e a t
        # 0 1 2 3
        # s 1 2 3 4
        # e 2 1 2 3
        ```
        ```
        3. word1 = "sea", word2 = "eat"
        # e a t
        # 0 1 2 3
        # s 1 2 3 4
        # e 2 1 2 3
        # a 3 2 1 2
        ```
    - 在分析示例 `dp` 网格时，请记住有三个要点需要特别注意：`dp[i - 1][j - 1]`、`dp[i - 1][j]` 和 `dp[i][j - 1]`。当前的 `dp[i][j]` 通常取决于它们。
    - 如果问题反过来也是正确的（交换 `word1` 和 `word2`），并且我们需要使用 `dp[i - 1][j]` 或 `dp[i][j - 1]`，那么我们可能需要同时使用它们。
    - 我们可以推导出 `递归公式`：

        ```ruby
        if word1[i - 1] == word2[j - 1]
          dp[i][j] = dp[i - 1][j - 1]
        else
          dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + 1
        end
        ```
4. 确定 `dp` 数组的遍历顺序
    - `dp[i][j]` 依赖于 `dp[i - 1][j - 1]`、`dp[i - 1][j]` 和 `dp[i][j - 1]`，所以我们应该从上到下，然后从左到右遍历 `dp` 数组。
5. 检查 `dp` 数组的值
    - 打印 `dp` 以查看它是否符合预期。

## 复杂度

- 时间复杂度: `O(N * M)`.
- 空间复杂度: `O(N * M)`.

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
                    dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - 1]) + 1;
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
                    dp[i, j] = Math.Min(dp[i - 1, j], dp[i, j - 1]) + 1;
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
                    dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + 1

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
                    dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + 1;
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
        dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - 1]) + 1
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
                dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + 1
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
          [ dp[i - 1][j], dp[i][j - 1] ].min + 1
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

亲爱的力扣人，为了您更好的刷题体验，请访问 [leetcoder.net](https://leetcoder.net)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[583. 两个字符串的删除操作 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/583-delete-operation-for-two-strings).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

