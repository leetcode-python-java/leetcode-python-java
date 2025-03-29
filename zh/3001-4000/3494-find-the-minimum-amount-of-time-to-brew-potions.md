Visit 原文链接：[leetcoder.net - 力扣题解最佳实践 - 力扣人](https://leetcoder.net/zh/leetcode/3494-find-the-minimum-amount-of-time-to-brew-potions) for a better experience!

GitHub repo: [fuck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

# 3494. 酿造药水需要的最少总时间 - 力扣题解最佳实践 - 力扣人

力扣链接：[3494. 酿造药水需要的最少总时间](https://leetcode.cn/problems/find-the-minimum-amount-of-time-to-brew-potions), 难度：**中等**。

## 力扣“3494. 酿造药水需要的最少总时间”问题描述

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

- 该算法的核心是要确定**递推公式**，但*第一步*不是做这件事情，是做什么呢？
    <details><summary>点击查看答案</summary><p>是确定数组中每一个值代表的含义。</p></details>

- 动态规划可以用*二维数组*或*滚动数组*实现。在讲解时，用*二维数组*比较清晰；在实现时，用*滚动数组*比较简明。所以接下来，我要用*二维数组*来讲解本题。

- “动态规划”分为五步。请严格按这五步操作。
    1. 确定每一个值代表什么含义。
    2. 初始化数组值。
    3. 填入一些数据。
    4. 根据填入的数据，推导出“递推公式”。
    5. 写出程序，并打印数组，看是否合乎预期。不合乎预期就继续调整程序。

## 步骤

- 那么二维数组中每一个值究竟代表什么含义？首先是每一行，然后是行中的某列的值。
    mark-detail行是代表药水，列代表巫师，这在题目中已经给出暗示了。<br>列的值`dp[i][j]`的含义，需要根据题目的问题描述得出，如果不适合，再调整。所以含义是：第`j`个巫师完成第`i`瓶药水的时间。我故意没有加“最短”这个词，因为药水在制造过程中，离不了巫师的手！mark-detail

- 如何初始组值？
    mark-detail把值全部设置为`0`就可以了。mark-detail

- 如何填入数据？
    mark-detail“示例1”给出的那个表格的数据完全符合我们的需求，直接用它。mark-detail

- 如何根据填入的数据，推导出“递推公式”？
    mark-detail条件一：第`j - 1`个巫师完成他的第`i`瓶药水工作后，第`j`个巫师才可以开始他的第`i`瓶药水的工作。<br>条件二：第`j`个巫师完成他的第`i - 1`瓶药水的工作后，才可以开始他的第`i`瓶药水工作。<br>条件三：在第`j`个巫师完成他的第`i`瓶药水工作后，第`j + 1`个巫师必须立刻开始他的第`i`瓶药水工作，即药水不等人，第`j`个巫师**不能过早开始工作**。mark-detail   

- 根据以上的三个条件，请写出代码，并打印数组，看是否合乎预期。
- 结果你发现某些数值比预期值小了。这时，就要根据那些“异常”的数值，思考是否存在逻辑漏洞了。漏洞在哪？
    mark-detail逻辑漏洞就是：一些巫师依然过早地开始工作，导致药水在等人。mark-detail

- 如何修复逻辑漏洞？
    mark-detail**从后往前**再处理一遍，因为最后一个巫师此时已经不存在过早开始工作的问题。mark-detail

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

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [leetcoder.net](https://leetcoder.net): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

原文链接：[leetcoder.net - 力扣题解最佳实践 - 力扣人](https://leetcoder.net/zh/leetcode/3494-find-the-minimum-amount-of-time-to-brew-potions).

GitHub repo: [fuck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).
