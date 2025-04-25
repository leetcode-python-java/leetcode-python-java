# 3494. 酿造药水需要的最少总时间 - LeetCode Python/Java/C++ 题解

访问原文链接：[3494. 酿造药水需要的最少总时间 - LeetCode Python/Java/C++ 题解](https://leetcodepython.com/zh/leetcode/3494-find-the-minimum-amount-of-time-to-brew-potions)，体验更佳！

力扣链接：[3494. 酿造药水需要的最少总时间](https://leetcode.cn/problems/find-the-minimum-amount-of-time-to-brew-potions), 难度等级：**中等**。

## LeetCode “3494. 酿造药水需要的最少总时间”问题描述

给你两个长度分别为 `n` 和 `m` 的整数数组 `skill` 和 `mana` 。

在一个实验室里，有 `n` 个巫师，他们必须按顺序酿造 `m` 个药水。每个药水的法力值为 `mana[j]`，并且每个药水 **必须** 依次通过 **所有** 巫师处理，才能完成酿造。第 `i` 个巫师在第 `j` 个药水上处理需要的时间为 *time<sub>ij</sub>* = `skill[i] * mana[j]`。

由于酿造过程非常精细，药水在当前巫师完成工作后 **必须** 立即传递给下一个巫师并开始处理。这意味着时间必须保持 **同步**，确保每个巫师在药水到达时 **马上** 开始工作。

返回酿造所有药水所需的 **最短** 总时间。

### [示例 1]

**输入**: `skill = [1,5,2,4], mana = [5,1,4,2]`

**输出**: `110`

**解释**: 

<table><thead>
<tr>
<th>药水编号</th>
<th>开始时间</th>
<th>巫师 0 完成时间</th>
<th>巫师 1 完成时间</th>
<th>巫师 2 完成时间</th>
<th>巫师 3 完成时间</th>
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

<p>举个例子，为什么巫师 0 不能在时间 <code>t = 52</code> 前开始处理第 1 个药水，假设巫师们在时间 <code>t = 50</code> 开始准备第 1 个药水。时间 <code>t = 58</code> 时，巫师 2 已经完成了第 1 个药水的处理，但巫师 3 直到时间 <code>t = 60</code> 仍在处理第 0 个药水，无法马上开始处理第 1个药水。</p>


### [示例 2]

**输入**: `skill = [1,1,1], mana = [1,1,1]`

**输出**: `5`

**解释**: 

<ol>
<li>第 0 个药水的准备从时间 <code>t = 0</code> 开始，并在时间 <code>t = 3</code> 完成。</li>
<li>第 1 个药水的准备从时间 <code>t = 1</code> 开始，并在时间 <code>t = 4</code> 完成。</li>
<li>第 2 个药水的准备从时间 <code>t = 2</code> 开始，并在时间 <code>t = 5</code> 完成。</li>
</ol>


### [示例 3]

**输入**: `skill = [1,2,3,4], mana = [1,2]`

**输出**: `21`

### [约束]

- `n == skill.length`
- `m == mana.length`
- `1 <= n, m <= 5000`
- `1 <= mana[i], skill[i] <= 5000`

### [Hints]

<details>
  <summary>提示 1</summary>
  Maintain each wizard's earliest free time (for the last potion) as `f[i]`.

  
</details>

<details>
  <summary>提示 2</summary>
  Let `x` be the current mana value. Starting from `now = f[0]`, update `now = max(now + skill[i - 1] * x, f[i])` for `i in [1..n]`. Then, the final `f[n - 1] = now + skill[n - 1] * x` for this potion.

  
</details>

<details>
  <summary>提示 3</summary>
  Update all other `f` values by `f[i] = f[i + 1] - skill[i + 1] * x` for `i in [0..n - 2]` (in reverse order).

  
</details>

## 思路

- 解决本题的第一步是确定用什么算法。因为每一瓶药水的制造都依赖上一瓶药水在某些巫师手中的完成情况，药水本身也需要一瓶一瓶地制造，所以应该使用什么算法呢？
    <details><summary>点击查看答案</summary><p>动态规划。</p></details>

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

1. 确定数组`dp`的每个值代表的含义。请思考下。
    mark-detail“行”代表“药水”，“列”代表“巫师”，这在题目中已经给出暗示了。<br>`dp[i][j]`含义是：第`j`个巫师完成第`i`瓶药水的时间。我故意没有加“最短”这个词，因为药水在制造过程中，离不了巫师的手！mark-detail
2.  `dp`数组值如何初始化？
    mark-detail把值全部设置为`0`就可以了。mark-detail
3. 根据一个示例，“按顺序”填入`dp`网格数据。如何填入数据？
    mark-detail“示例1”给出的那个表格的数据完全符合我们的需求，直接用它。mark-detail
4. 根据`dp`网格数据，推导出“递推公式”。“递推公式”是什么？
    mark-detail条件一：第`j - 1`个巫师完成他的第`i`瓶药水工作后，第`j`个巫师才可以开始他的第`i`瓶药水的工作。<br>条件二：第`j`个巫师完成他的第`i - 1`瓶药水的工作后，才可以开始他的第`i`瓶药水工作。<br>条件三：在第`j`个巫师完成他的第`i`瓶药水工作后，第`j + 1`个巫师必须立刻开始他的第`i`瓶药水工作，即药水不等人，第`j`个巫师**不能过早开始工作**。mark-detail
5. 写出程序，并打印`dp`数组，不合预期就调整。
    - 结果你发现某些数值比预期值小了。这时，就要根据那些“异常”的数值，思考是否存在逻辑漏洞了。漏洞在哪？
        mark-detail 逻辑漏洞就是：一些巫师依然过早地开始工作，导致药水在等人。mark-detail
    - 如何修复逻辑漏洞？
        mark-detail**从后往前**再处理一遍，因为最后一个巫师此时已经不存在过早开始工作的问题。由此可见遍历顺序的重要性。可能是从前向后，也可能是从后向前，还可能是都有。mark-detail

## 复杂度

- 时间复杂度: `O(M * N)`.
- 空间复杂度: `O(N)`.

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

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCodePython.com](https://leetcodepython.com/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[3494. 酿造药水需要的最少总时间 - LeetCode Python/Java/C++ 题解](https://leetcodepython.com/zh/leetcode/3494-find-the-minimum-amount-of-time-to-brew-potions).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

