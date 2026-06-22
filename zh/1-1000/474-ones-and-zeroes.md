# 474. 一和零 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[474. 一和零 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/474-ones-and-zeroes)，体验更佳！

力扣链接：[474. 一和零](https://leetcode.cn/problems/ones-and-zeroes), 难度等级：**中等**。

## LeetCode “474. 一和零”问题描述

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

## “0/1背包问题”的模式

典型的“0/1背包问题”，指每个“物品”只能使用一次，来填充“背包”。“物品”有“重量”和“价值”属性，求“背包”能存放的“物品”的最大价值。

其特点是：有**一组数字**，每个数字只能被使用一次，通过某种计算得到**另一个数字**。问题也可以变成能否得到？有多少种变化？等。

因为“0/1背包问题”属于“动态规划”，所以我会用“动态规划”的模式讲解。

1. 确定数组`dp`的每个值代表的含义。
    - 首选**一维滚动数组**，代码简洁。
    - 确定什么是“物品”，什么是“背包”。
    - 如果`dp[j]`是一个布尔值，则`dp[j]`表示是否可以前`i`个`物品`的`和`得到`j`。
    - 如果`dp[j]`是一个数值，则`dp[j]`表示是利用前`i`个`物品`，`dp[j]`能达到的所求问题的极限值。
2. 初始化数组`dp`的值。
    - 确定“背包”的大小。需要让背包大小再加1，即插入`dp[0]`做为起始点，方便理解和引用。
    - `dp[0]`有时需要特殊处理。
3. 根据一个示例，“按顺序”填入`dp`网格数据。
    - 先在外层循环中，**遍历物品**。
    - 后在内层循环中，**遍历背包大小**。
       - 在遍历背包大小时，由于`dp[j]`取决于`dp[j]`和`dp[j - weights[i]]`，因此我们应该**从右到左**遍历`dp`数组。
       - 请思考是否可以从`从左到右`遍历`dp`数组？
4. 根据`dp`网格数据，推导出“递推公式”。
    - 如果`dp[j]`是一个布尔值：

    ```cpp
    dp[j] = dp[j] || dp[j - weights[i]]
    ```
    - 如果`dp[j]`是一个数值：

    ```cpp
    dp[j] = min_or_max(dp[j], dp[j - weights[i]] + values[i])
    ```
5. 写出程序，并打印`dp`数组，不合预期就调整。

## 步骤

1. 确定`dp[j]`的**含义**
    - 由于我们目前只考虑零计数约束，因此我们可以使用一维`dp`数组。
    - `物品`是`strs`，`背包`是`max_zero_count`。
    - `dp[j]`表示最多可以用`j`个零来选择的最大字符串数。
    - `dp[j]`是一个整数。

2. 确定`dp`数组的初始值
    - 使用一个例子，示例1：`输入：strs = ["10","0001","111001","1","0"]，m = 5，n = 3`。
    - 初始化后：

        ```python
        max_zero_count = m
        dp = [0] * (max_zero_count + 1)
        ```
    - `dp[0] = 0`，表示没有零，我们可以选择 0 个字符串。
    - `dp[j] = 0` 作为初始值，因为我们稍后将使用 `max` 来增加它们。

3. 根据一个示例，“按顺序”填入`dp`网格数据。

    ```
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
4. 根据`dp`网格数据，推导出“递推公式”。

    ```cpp
    dp[j] = max(dp[j], dp[j - zero_count] + 1)
    ```
5. 写出程序，并打印`dp`数组，不合预期就调整。

只考虑`0`数量限制的代码是：

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

#### 现在，你可以考虑另一个维度：`1`的数量限制。

它应该以与“0”类似的方式处理，只不过是在另一个维度上。请参阅下面的完整代码。

## 复杂度

- 时间复杂度: `O(N * M * Len)`.
- 空间复杂度: `O(N * M)`.

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

访问原文链接：[474. 一和零 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/474-ones-and-zeroes)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

