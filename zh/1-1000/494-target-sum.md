# 494. 目标和 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[494. 目标和 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/494-target-sum)，体验更佳！

力扣链接：[494. 目标和](https://leetcode.cn/problems/target-sum), 难度等级：**中等**。

## LeetCode “494. 目标和”问题描述

给你一个非负整数数组 `nums` 和一个整数 `target` 。

向数组中的每个整数前添加 `'+'` 或 `'-'` ，然后串联起所有整数，可以构造一个 **表达式** ：

- 例如，`nums = [2, 1]` ，可以在 `2` 之前添加 `'+'` ，在 `1` 之前添加 `'-'` ，然后串联起来得到表达式 `"+2-1"` 。

返回可以通过上述方法构造的、运算结果等于 `target` 的不同 **表达式** 的数目。

### [示例 1]

**输入**: `nums = [1,1,1,1,1], target = 3`

**输出**: `5`

**解释**: 

<p>-1 + 1 + 1 + 1 + 1 = 3<br>
+1 - 1 + 1 + 1 + 1 = 3<br>
+1 + 1 - 1 + 1 + 1 = 3<br>
+1 + 1 + 1 - 1 + 1 = 3<br>
+1 + 1 + 1 + 1 - 1 = 3</p>


### [示例 2]

**输入**: `nums = [1], target = 1`

**输出**: `1`

### [约束]

- `1 <= nums.length <= 20`
- `0 <= nums[i] <= 1000`
- `0 <= sum(nums[i]) <= 1000`
- `-1000 <= target <= 1000`

## 思路

如果你以前没有解决过类似的问题，那么这个问题相当难。所以在开始做这道题之前，建议你先做另一道与这道题类似的相对简单的题目[416. 分割相等子集和](416-partition-equal-subset-sum.md)。

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

1. 确定`dp[j]`的**含义**
    - `dp[j]`表示通过使用**前**个`i`个数字，您可以构建的不同**表达式**的数量，其计算结果为`j`。
    - `dp[j]`是一个**整数**。
2. 确定`dp`数组的初始值
    - 使用一个例子。我们没有使用`示例1：输入：nums = [1,1,1,1,1], target = 3`，因为它太特殊，不是推导公式的好例子。
    - 我编了一个例子：`nums = [1,2,1,2], target = 4`。
    - 首先，确定背包的`size`。
        - `target`值可能很小，比如`0`，所以光靠它不能确定背包的`size`。
        - 还应该考虑`nums`的总和，以完全覆盖所有背包尺寸。
        - `target`可以是负数，但考虑到`+`和`-`是任意添加到`num`的，`dp[j]`应该围绕`0`对称。所以负数 `target` 的结果 `dp[target]` 等于 `dp[abs(target)]`。
        - 所以背包的 `size` 可以是 `max(sum(nums), target) + 1`。
    - 然后，确定什么是`物品`。`物品`在本题中 就是 `nums`。

        ```
        所以初始化后，`dp` 数组将是：
        #   0 1 2 3 4 5 6
        #   1 0 0 0 0 0 0 # dp
        # 1
        # 2
        # 1
        # 2
        ```
    - `dp[0]` 设置为 `1`，表示不使用任何 `nums` 就可以实现空背包。另外，它作为起始值，后面的`dp[j]`都会依赖它，如果为`0`，则`dp[j]`的所有值都为`0`。
    - `dp[j] = 0 (j != 0)`，说明没有`nums`是不可能得到`j`的。
3. 根据一个示例，“按顺序”填入`dp`网格数据。

    ```
    1. 使用第一个数字'1'。
    #   0 1 2 3 4 5 6
    #   1 0 0 0 0 0 0
    # 1 0 1 0 0 0 0 0 # dp
    # 2
    # 1
    # 2
    ```
    ```
    2. 使用第二个数字'2'。
    #   0 1 2 3 4 5 6
    #   1 0 0 0 0 0 0
    # 1 0 1 0 0 0 0 0
    # 2 0 1 0 1 0 0 0
    # 1
    # 2
    ```
    ```
    3. 使用第三个数字'1'。
    #   0 1 2 3 4 5 6
    #   1 0 0 0 0 0 0
    # 1 0 1 0 0 0 0 0
    # 2 0 1 0 1 0 0 0
    # 1 2 0 2 0 1 0 0
    # 2
    ```
    ```
    4. 使用第四个数字'2'。
    #   0 1 2 3 4 5 6
    #   1 0 0 0 0 0 0
    # 1 0 1 0 0 0 0 0
    # 2 0 1 0 1 0 0 0
    # 1 2 0 2 0 1 0 0
    # 2 4 0 3 0 2 0 1 # dp
    ```
4. 根据`dp`网格数据，推导出“递推公式”。

    ```java
    dp[j] = dp[abs(j - nums[i])] + dp[j + nums[i]]
    ```
    - 如果 `j < nums[i]`，`dp[j - nums[i]]` 将引发 `数组索引超出范围` 异常。因此我们使用等于它的 `dp[abs(j - num)]`，因为 `dp[j]` 是围绕 `0` 对称的，比如 `dp[-j]` 等于 `dp[j]`（`-j` 是虚数索引）。
    - 当 `j + nums[i] >= dp.length`时，`dp[j + nums[i]]` 必须为 `0`，防止产生干扰。
5. 写出程序，并打印`dp`数组，不合预期就调整。

## 复杂度

- 时间复杂度: `O(n * sum)`.
- 空间复杂度: `O(n * sum)`.

## C#

```csharp
public class Solution
{
    public int FindTargetSumWays(int[] nums, int target)
    {
        target = Math.Abs(target);

        var dp = new int[Math.Max(nums.Sum(), target) + 1];
        dp[0] = 1;

        foreach (var num in nums)
        {
            var dc = (int[])dp.Clone();

            for (var j = 0; j < dp.Length; j++)
            {
                dp[j] = dc[Math.Abs(j - num)] + (j + num < dp.Length ? dc[j + num] : 0);
            }
        }

        return dp[target];
    }
}
```

## Python

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        target = abs(target)

        dp = [0] * (max(sum(nums), target) + 1)
        dp[0] = 1

        for num in nums:
            dc = dp.copy()

            for j in range(len(dp)):
                dp[j] = dc[abs(j - num)] + (dc[j + num] if j + num < len(dp) else 0)

        return dp[target]
```

## C++

```cpp
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int target) {
        auto sum = reduce(nums.begin(), nums.end());
        target = abs(target);

        auto dp = vector<int>(max(sum, target) + 1);
        dp[0] = 1;

        for (auto num : nums) {
            auto dc = dp;

            for (auto j = 0; j < dp.size(); j++) {
                dp[j] = dc[abs(j - num)] + (j + num < dp.size() ? dc[j + num] : 0);
            }
        }

        return dp[target];
    }
};
```

## Java

```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        var sum = IntStream.of(nums).sum();
        target = Math.abs(target);

        var dp = new int[Math.max(sum, target) + 1];
        dp[0] = 1;

        for (var num : nums) {
            var dc = dp.clone();

            for (var j = 0; j < dp.length; j++) {
                dp[j] = dc[Math.abs(j - num)] + (j + num < dp.length ? dc[j + num] : 0);
            }
        }

        return dp[target];
    }
}
```

## JavaScript

```javascript
var findTargetSumWays = function (nums, target) {
   target = Math.abs(target)

   const dp = Array(Math.max(_.sum(nums), target) + 1).fill(0)
   dp[0] = 1

   for (const num of nums) {
      const dc = [...dp]

      for (let j = 0; j < dp.length; j++) {
         dp[j] = dc[Math.abs(j - num)] + (j + num < dp.length ? dc[j + num] : 0)
      }
   }

   return dp[target]
};
```

## Go

```go
func findTargetSumWays(nums []int, target int) int {
    sum := 0
    for _, num := range nums {
        sum += num
    }
    target = int(math.Abs(float64(target)))

    dp := make([]int, max(sum, target) + 1)
    dp[0] = 1

    for _, num := range nums {
        dc := slices.Clone(dp)

        for j := 0; j < len(dp); j++ {
            addition := 0
            if j + num < len(dp) {
                addition = dc[j + num]
            }
            dp[j] = dc[int(math.Abs(float64((j - num))))] + addition
        }
    }

    return dp[target]
}
```

## Ruby

```ruby
def find_target_sum_ways(nums, target)
  target = target.abs

  dp = Array.new([ nums.sum, target ].max + 1, 0)
  dp[0] = 1

  nums.each do |num|
    dc = dp.clone

    dp.each_with_index do |_, j|
      dp[j] = dc[(j - num).abs] + (j + num < dp.size ? dc[j + num] : 0)
    end
  end

  dp[target]
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

访问原文链接：[494. 目标和 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/494-target-sum)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

