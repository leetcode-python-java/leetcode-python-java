# 72. 编辑距离 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[72. 编辑距离 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/72-edit-distance)，体验更佳！

力扣链接：[72. 编辑距离](https://leetcode.cn/problems/edit-distance), 难度等级：**中等**。

## LeetCode “72. 编辑距离”问题描述

给你两个单词 `word1` 和 `word2`， 请返回将 `word1` 转换成 `word2` 所使用的**最少操作数**。

你可以对一个单词进行如下三种操作：

- 插入一个字符
- 删除一个字符
- 替换一个字符

### [示例 1]

**输入**: `word1 = "horse", word2 = "ros"`

**输出**: `3`

**解释**: 

<p>horse -&gt; rorse (将 &#39;h&#39; 替换为 &#39;r&#39;)<br>
rorse -&gt; rose (删除 &#39;r&#39;)<br>
rose -&gt; ros (删除 &#39;e&#39;)</p>


### [示例 2]

**输入**: `word1 = "intention", word2 = "execution"`

**输出**: `5`

**解释**: 

<p>intention -&gt; inention (删除 &#39;t&#39;)<br>
inention -&gt; enention (将 &#39;i&#39; 替换为 &#39;e&#39;)<br>
enention -&gt; exention (将 &#39;n&#39; 替换为 &#39;x&#39;)<br>
exention -&gt; exection (将 &#39;n&#39; 替换为 &#39;c&#39;)<br>
exection -&gt; execution (插入 &#39;u&#39;)</p>


### [约束]

1. `0 <= word1.length, word2.length <= 500`
2. `word1` 和 `word2` 由小写英文字母组成

## 思路

这是一道比较两个字符串的题目。在多次练习类似的题目之后，我们能培养出使用*二维*数组`dp`的“动态规划”方法解决本问题的直觉。

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

## “子序列问题”的模式

- 由于要比较有两个可互换位置的数组（或字符串），我们使用**二维**数组作为`dp`。
- `dp` 数组的遍历顺序是从上到下，然后从左到右。

## 步骤

1. 确定数组`dp`的每个值代表的**含义**。
    - `dp[i][j]` 表示将 `word1` 的前 `i` 个字母转换为 `word2` 的前 `j` 个字母所需的**最小**操作次数。
    - `dp[i][j]` 是一个整数。
2. 初始化数组`dp`的值。
    - 使用示例：

    ```
    初始化后，dp 数组应为：
    # r o s
    # 0 1 2 3 # dp[0]
    # h 1 0 0 0
    # o 2 0 0 0
    # r 3 0 0 0
    # s 4 0 0 0
    # e 5 0 0 0
    ```
    - `dp[i][0] = i`，因为`dp[i][0]`表示空字符串，操作次数就是需要删除的字符数。
    - `dp[0][j] = j`，原因与上一行相同，只是角度相反：将`word2`转换为`word1`。

3. 根据一个示例，**按顺序**填入`dp`网格数据。

    ```
    1. 将`h`转换为`ros`。
    # r o s
    # 0 1 2 3
    # h 1 1 2 3 # dp[1]
    ```
    ```
    2. 将`ho`转换为`ros`。
    # r o s
    # 0 1 2 3
    # h 1 1 2 3
    # o 2 2 1 2
    ```
    ```
    3. 将`hor`转换为`ros`。
    # r o s
    # 0 1 2 3
    # h 1 1 2 3
    # o 2 2 1 2
    # r 3 2 2 2
    ```
    ```
    4. 将`hors`转换为`ros`。
    # r o s
    # 0 1 2 3
    # h 1 1 2 3
    # o 2 2 1 2
    # r 3 2 2 2
    # s 4 3 3 2
    ```
    ```
    5. 将 `horse` 转换为 `ros`。
    # r o s
    # 0 1 2 3
    # h 1 1 2 3
    # o 2 2 1 2
    # r 3 2 2 2
    # s 4 3 3 2
    # e 5 4 4 3 # dp[5]
    ```
4. 根据`dp`网格数据，推导出**递推公式**。

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
5. 写出程序，并打印`dp`数组，不合预期就调整。

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

访问原文链接：[72. 编辑距离 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/72-edit-distance)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

