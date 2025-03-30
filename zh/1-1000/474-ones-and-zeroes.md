# 474. 一和零 - 力扣题解最佳实践

访问 原文链接：[474. 一和零 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/474-ones-and-zeroes) 体验更佳！

GitHub 仓库: [fuck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

力扣链接：[474. 一和零](https://leetcode.cn/problems/ones-and-zeroes), 难度：**中等**。

## 力扣“474. 一和零”问题描述

给你一个二进制字符串数组 `strs` 和两个整数 `m` 和 `n` 。

请你找出并返回 `strs` 的最大子集的长度，该子集中 **最多** 有 `m` 个 `0` 和 `n` 个 `1` 。

如果 `x` 的所有元素也是 `y` 的元素，集合 `x` 是集合 `y` 的 **子集** 。

### [示例 1]

**输入**: `strs = ["10","0001","111001","1","0"], m = 5, n = 3`

**输出**: `4`

**解释**: 

<p>最多有 5 个 0 和 3 个 1 的最大子集是 {&quot;10&quot;,&quot;0001&quot;,&quot;1&quot;,&quot;0&quot;} ，因此答案是 4 。<br>
其他满足题意但较小的子集包括 {&quot;0001&quot;,&quot;1&quot;} 和 {&quot;10&quot;,&quot;1&quot;,&quot;0&quot;} 。{&quot;111001&quot;} 不满足题意，因为它含 4 个 1 ，大于 n 的值 3 。</p>


### [示例 2]

**输入**: `strs = ["10","0","1"], m = 1, n = 1`

**输出**: `2`

**解释**: `最大的子集是 {"0", "1"} ，所以答案是 2 。`

### [约束]

- `1 <= strs.length <= 600`
- `1 <= strs[i].length <= 100`
- `'strs[i]' consists only of digits '0' and '1'`
- `1 <= m, n <= 100`

## 思路

本题偏难，建议先完成一个同类的简单题目[416. 分割等和子集](416-partition-equal-subset-sum.md)。

- 在完成了416后，你会发现本题要在两个维度上解决`0/1问题`。
- 解决方法是先在一维上解决问题，然后再将其扩展到二维。
- 没有必要画一个同时考虑两个维度的网格，那太复杂了。我们可以先**只**考虑`0`的数量限制。

## 步骤

### '0/1背包问题'中的常用步骤

这五个步骤是解决`动态规划`问题的模式。

1. 确定`dp[j]`的**含义**
    - 由于我们目前只考虑零计数约束，因此我们可以使用一维`dp`数组。
    - `dp[j]`表示最多可以用`j`个零来选择的最大字符串数。
    - `dp[j]`是一个整数。

2. 确定`dp`数组的初始值
    - 使用一个例子，示例1：`输入：strs = ["10","0001","111001","1","0"]，m = 5，n = 3`。
    - 初始化后：

        ```python
        max_zero_count = m
        dp = [0] * (max_zero_count + 1)
        ```
    - `dp` 数组大小比零计数约束大一。这样，索引值等于约束值，更容易理解。
    - `dp[0] = 0`，表示没有零，我们可以选择 0 个字符串。
    - `dp[j] = 0` 作为初始值，因为我们稍后将使用 `max` 来增加它们。

3. 确定 `dp` 数组的递归公式
    - 我们来一步步分析这个例子：

        ```ruby
        # Initial state
        #    0 1 2 3 4 5
        #    0 0 0 0 0 0

        # After processing "10" (1 zero)
        #    0 1 2 3 4 5
        #    0 1 1 1 1 1

        # After processing "0001" (3 zeros)
        #    0 1 2 3 4 5
        #    0 1 1 1 2 2

        # After processing "111001" (2 zeros)
        #    0 1 2 3 4 5
        #    0 1 1 2 2 2

        # After processing "1" (0 zeros)
        #    0 1 2 3 4 5
        #    0 2 2 3 3 3

        # After processing "0" (1 zero)
        #    0 1 2 3 4 5
        #    0 2 3 3 4 4
        ```
    - 分析示例 `dp` 网格后，我们可以得出 `递归公式`：

        ```cpp
        dp[j] = max(dp[j], dp[j - zero_count] + 1)
        ```
    - 此公式意味着：对于每个字符串，我们可以：
        1. 不选择它（保留当前值 `dp[j]`）
        2. 选择它（将 `dp[j - zero_count]` 处的值加 1）

4. 确定 `dp` 数组的遍历顺序
    - 首先 **遍历字符串**，然后 **遍历零计数**（`以相反的顺序`）。
    - 在遍历零计数时，由于 `dp[j]` 依赖于 `dp[j]` 和 `dp[j - zero_count]`，因此我们应该**从右到左**遍历。
    - 这确保我们不会多次使用相同的字符串。

5. 检查 `dp` 数组的值
    - 打印 `dp` 以查看它是否符合预期。
    - 最终答案将在 `dp[max_zero_count]`。

6. 只考虑`0`数量限制的代码是：

    ```python
    class Solution:
        def findMaxForm(self, strs: List[str], max_zero_count: int, n: int) -> int:
            dp = [0] * (max_zero_count + 1)

            for string in strs:
                zero_count = count_zero(string)

                for j in range(len(dp) - 1, zero_count - 1, -1): # must iterate in reverse order!
                    dp[j] = max(dp[j], dp[j - zero_count] + 1)

            return dp[-1]


    def count_zero(string):
        zero_count = 0

        for bit in string:
            if bit == '0':
                zero_count += 1

        return zero_count
    ```

### 现在，你可以考虑另一个维度：`1`的数量限制。

它应该以与“0”类似的方式处理，但在另一个维度上。请参阅下面的完整代码。

## 复杂度

- 时间复杂度: `O(N∗M∗Len)`.
- 空间复杂度: `O(N∗M)`.

## Python

```python
class Solution:
    def findMaxForm(self, strs: List[str], max_zero_count: int, max_one_count: int) -> int:
        dp = [[0] * (max_one_count + 1) for _ in range(max_zero_count + 1)]

        for string in strs:
            zero_count, one_count = count_zero_one(string)

            for i in range(len(dp) - 1, zero_count - 1, -1):
                for j in range(len(dp[0]) - 1, one_count - 1, -1):
                    dp[i][j] = max(dp[i][j], dp[i - zero_count][j - one_count] + 1)
        
        return dp[-1][-1]


def count_zero_one(string):
    zero_count = 0
    one_count = 0

    for bit in string:
        if bit == '0':
            zero_count += 1
        else:
            one_count += 1

    return zero_count, one_count
```

## C++

```cpp
class Solution {
public:
    int findMaxForm(vector<string>& strs, int max_zero_count, int max_one_count) {
        vector<vector<int>> dp(max_zero_count + 1, vector<int>(max_one_count + 1, 0));

        for (auto& str : strs) {
            auto zero_count = 0;
            auto one_count = 0;

            for (auto bit : str) {
                if (bit == '0') {
                    zero_count++;
                } else {
                    one_count++;
                }
            }

            for (auto i = max_zero_count; i >= zero_count; i--) {
                for (auto j = max_one_count; j >= one_count; j--) {
                    dp[i][j] = max(dp[i][j], dp[i - zero_count][j - one_count] + 1);
                }
            }
        }

        return dp[max_zero_count][max_one_count];
    }
};
```

## Java

```java
class Solution {
    public int findMaxForm(String[] strs, int maxZeroCount, int maxOneCount) {
        var dp = new int[maxZeroCount + 1][maxOneCount + 1];

        for (var str : strs) {
            var zeroCount = 0;
            var oneCount = 0;

            for (var bit : str.toCharArray()) {
                if (bit == '0') {
                    zeroCount++;
                } else {
                    oneCount++;
                }
            }

            for (var i = maxZeroCount; i >= zeroCount; i--) {
                for (var j = maxOneCount; j >= oneCount; j--) {
                    dp[i][j] = Math.max(dp[i][j], dp[i - zeroCount][j - oneCount] + 1);
                }
            }
        }

        return dp[maxZeroCount][maxOneCount];
    }
}
```

## C#

```csharp
public class Solution
{
    public int FindMaxForm(string[] strs, int maxZeroCount, int maxOneCount)
    {
        var dp = new int[maxZeroCount + 1, maxOneCount + 1];

        foreach (var str in strs)
        {
            var (zeroCount, oneCount) = CountZeroOne(str);

            for (var i = maxZeroCount; i >= zeroCount; i--)
            {
                for (var j = maxOneCount; j >= oneCount; j--)
                {
                    dp[i, j] = Math.Max(dp[i, j], dp[i - zeroCount, j - oneCount] + 1);
                }
            }
        }

        return dp[maxZeroCount, maxOneCount];
    }

    (int, int) CountZeroOne(string str)
    {
        var zeroCount = 0;
        var oneCount = 0;

        foreach (var bit in str)
        {
            if (bit == '0')
            {
                zeroCount++;
            }
            else
            {
                oneCount++;
            }
        }

        return (zeroCount, oneCount);
    }
}
```

## JavaScript

```javascript
var findMaxForm = function (strs, maxZeroCount, maxOneCount) {
  const dp = Array(maxZeroCount + 1).fill().map(
    () => Array(maxOneCount + 1).fill(0)
  )

  for (const str of strs) {
    const [zeroCount, oneCount] = countZeroOne(str)

    for (let i = dp.length - 1; i >= zeroCount; i--) {
      for (let j = dp[0].length - 1; j >= oneCount; j--) {
        dp[i][j] = Math.max(dp[i][j], dp[i - zeroCount][j - oneCount] + 1)
      }
    }
  }

  return dp.at(-1).at(-1)
};

function countZeroOne(str) {
  let zeroCount = 0
  let oneCount = 0

  for (const bit of str) {
    if (bit === '0') {
      zeroCount++
    } else {
      oneCount++
    }
  }

  return [zeroCount, oneCount]
}
```

## Go

```go
func findMaxForm(strs []string, maxZeroCount int, maxOneCount int) int {
    dp := make([][]int, maxZeroCount + 1)
    for i := range dp {
        dp[i] = make([]int, maxOneCount + 1)
    }

    for _, str := range strs {
        zeroCount, oneCount := countZeroOne(str)

        for i := len(dp) - 1; i >= zeroCount; i-- {
            for j := len(dp[0]) - 1; j >= oneCount; j-- {
                dp[i][j] = max(dp[i][j], dp[i - zeroCount][j - oneCount] + 1)
            }
        }
    }

    return dp[maxZeroCount][maxOneCount]
}

func countZeroOne(str string) (int, int) {
    zeroCount := 0
    oneCount := 0

    for _, bit := range str {
        if bit == '0' {
            zeroCount++
        } else {
            oneCount++
        }
    }

    return zeroCount, oneCount
}
```

## Ruby

```ruby
def find_max_form(strs, max_zero_count, max_one_count)
  dp = Array.new(max_zero_count + 1) do
    Array.new(max_one_count + 1, 0)
  end

  strs.each do |string|
    zero_count, one_count = count_zero_one(string)

    (zero_count...dp.size).reverse_each do |i|
      (one_count...dp[0].size).reverse_each do |j|
        dp[i][j] = [ dp[i][j], dp[i - zero_count][j - one_count] + 1 ].max
      end
    end
  end

  dp[-1][-1]
end

def count_zero_one(string)
  zero_count = 0
  one_count = 0

  string.each_char do |bit|
    if bit == '0'
      zero_count += 1
    else
      one_count += 1
    end
  end

  [ zero_count, one_count ]
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [leetcoder.net](https://leetcoder.net)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[474. 一和零 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/474-ones-and-zeroes).

GitHub 仓库: [fuck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).
