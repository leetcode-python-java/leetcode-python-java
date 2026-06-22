# 416. 分割等和子集 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[416. 分割等和子集 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/416-partition-equal-subset-sum)，体验更佳！

力扣链接：[416. 分割等和子集](https://leetcode.cn/problems/partition-equal-subset-sum), 难度等级：**中等**。

## LeetCode “416. 分割等和子集”问题描述

给你一个 **只包含正整数** 的 **非空** 数组 `nums` 。请你判断是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

### [示例 1]

**输入**: `nums = [1,5,11,5]`

**输出**: `true`

**解释**: `数组可以分割成 [1, 5, 5] 和 [11] 。`

### [示例 2]

**输入**: `nums = [1,2,3,5]`

**输出**: `false`

**解释**: `数组不能分割成两个元素和相等的子集。`

### [约束]

- `1 <= nums.length <= 200`
- `1 <= nums[i] <= 100`

## 思路 1

- 第一次看到这道题，我们可能想循环遍历数组的所有子集，如果有一个子集的和等于`和的一半`，就返回`true`。这可以用`回溯算法`来实现，但是看到`nums.length <= 200`这个约束，我们估计程序会超时。
- 本题可用`0/1背包问题`算法来解。

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
    - `dp[j]`表示是否前`i`个`nums`的`和`是否等于`j`。
    - `dp[j]`是一个布尔值。
2. 确定 `dp` 数组的初始值
    - 举个例子：

        ```
        nums = [1,5,11,5]，所以 '和的一半' 是 11。
        背包的 `size` 是 '11 + 1'，`物品` 是 `nums`。
        所以初始化后，'dp' 数组将是：
        #    0 1 2 3 4 5 6 7 8 9 10 11
        #    T F F F F F F F F F F  F # dp
        # 1
        # 5
        # 11
        # 5
        ```
    - `dp[0]` 设置为 `true`，表示不放任何物品即可得到空背包，另外，它作为起始值，后面的 `dp[j]` 将依赖它。如果为 `false`，则 `dp[j]` 的所有值都将为 `false`。
    - `dp[j] = false (j != 0)`，表示0个 `nums`的和不可能等于 `j`。

3. 根据一个示例，“按顺序”填入`dp`网格数据。

    ```
    1. 使用第一个数字 '1'。
    #    0 1 2 3 4 5 6 7 8 9 10 11
    #    T F F F F F F F F F F  F
    # 1  T T F F F F F F F F F  F # dp
    ```

    ```
    2. 使用第二个数字 '5'。
    #    0 1 2 3 4 5 6 7 8 9 10 11
    #    T F F F F F F F F F F  F
    # 1  T T F F F F F F F F F  F
    # 5  T T F F F T T F F F F  F
    ```

    ```
    3. 使用第三个数字 '11'。
    #    0 1 2 3 4 5 6 7 8 9 10 11
    #    T F F F F F F F F F F  F
    # 1  T T F F F F F F F F F  F
    # 5  T T F F F T T F F F F  F
    # 11 T T F F F T T F F F F  T
    ```

    ```
    3. 使用最后一个数字“5”。
    #    0 1 2 3 4 5 6 7 8 9 10 11
    #    T F F F F F F F F F F  F
    # 1  T T F F F F F F F F F  F
    # 5  T T F F F T T F F F F  F
    # 11 T T F F F T T F F F F  T
    # 5  T T F F F T T F F F T  T # dp
    ```
4. 根据`dp`网格数据，推导出“递推公式”。

    ```cpp
    dp[j] = dp[j] || dp[j - nums[i]]
    ```
5. 写出程序，并打印`dp`数组，不合预期就调整。

## 复杂度

- 时间复杂度: `O(n * sum/2)`.
- 空间复杂度: `O(sum/2)`.

## Python

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        sum_ = sum(nums)

        if sum_ % 2 == 1:
            return False

        dp = [False] * ((sum_ // 2) + 1)
        dp[0] = True

        for num in nums:
            # If not traversing in reverse order, the newly assigned value `dp[j]` will act as `dp[j - num]` later,
            # then the subsequent `dp[j]` will be affected. But each `num` can only be used once!
            j = len(dp) - 1
            while j >= num:
                dp[j] = dp[j] or dp[j - num]
                j -= 1

        return dp[-1]
```

## C#

```csharp
public class Solution
{
    public bool CanPartition(int[] nums)
    {
        int sum = nums.Sum();

        if (sum % 2 == 1)
            return false;

        var dp = new bool[sum / 2 + 1];
        dp[0] = true;

        foreach (var num in nums)
        {
            for (var j = dp.GetUpperBound(0); j >= num; j--)
            {
                dp[j] = dp[j] || dp[j - num];
            }
        }

        return dp.Last();
    }
}
```

## C++

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        auto sum = reduce(nums.begin(), nums.end());

        if (sum % 2 == 1) {
            return false;
        }

        auto dp = vector<bool>(sum / 2 + 1);
        dp[0] = true;

        for (auto num : nums) {
            for (auto j = dp.size() - 1; j >= num; j--) {
                dp[j] = dp[j] || dp[j - num];
            }
        }

        return dp.back();
    }
};
```

## Java

```java
class Solution {
    public boolean canPartition(int[] nums) {
        var sum = IntStream.of(nums).sum();
        
        if (sum % 2 == 1) {
            return false;
        }

        var dp = new boolean[sum / 2 + 1];
        dp[0] = true;

        for (var num : nums) {
            for (var j = dp.length - 1; j >= num; j--) {
                dp[j] = dp[j] || dp[j - num];
            }
        }

        return dp[dp.length - 1];
    }
}
```

## JavaScript

```javascript
var canPartition = function (nums) {
  const sum = _.sum(nums)

  if (sum % 2 == 1) {
    return false
  }

  const dp = Array(sum / 2 + 1).fill(false)
  dp[0] = true

  for (const num of nums) {
    for (let j = dp.length - 1; j >= num; j--) {
      dp[j] = dp[j] || dp[j - num]
    }
  }

  return dp.at(-1)
};
```

## Go

```go
func canPartition(nums []int) bool {
    sum := 0
    for _, num := range nums {
        sum += num
    }

    if sum % 2 == 1 {
        return false
    }

    dp := make([]bool, sum / 2 + 1)
    dp[0] = true

    for _, num := range nums {
        for j := len(dp) - 1; j >= num; j-- {
            dp[j] = dp[j] || dp[j - num]
        }
    }

    return dp[len(dp) - 1]
}
```

## Ruby

```ruby
def can_partition(nums)
  sum = nums.sum

  return false if sum % 2 == 1

  dp = Array.new(sum / 2 + 1, false)
  dp[0] = true

  nums.each do |num|
    (num...dp.size).reverse_each do |j|
      dp[j] = dp[j] || dp[j - num]
    end
  end

  dp[-1]
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## 思路 2

在*方案 1*中，遍历顺序是 **从右到左**，这真的很重要。

面试的时候，你需要记住它。有什么办法可以不用担心遍历顺序？

<details><summary>点击查看答案</summary><p> 只要把原`dp`复制一份，并引用复制品的值，就不用担心原`dp`值被修改了。</p></details>

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

## 复杂度

- 时间复杂度: `O(n * sum/2)`.
- 空间复杂度: `O(n * sum/2)`.

## Python

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        sum_ = sum(nums)

        if sum_ % 2 == 1:
            return False

        dp = [False] * ((sum_ // 2) + 1)
        dp[0] = True

        for num in nums:
            # Make a copy of the 'dp' that has not been modified to eliminate distractions.
            dc = dp.copy()

            for j in range(num, len(dp)): # any order is fine
                dp[j] = dc[j] or dc[j - num] # Use 'dc' instead of 'dp' because 'dp' will be modified.

        return dp[-1]
```

## C#

```csharp
public class Solution
{
    public bool CanPartition(int[] nums)
    {
        int sum = nums.Sum();

        if (sum % 2 == 1)
            return false;

        var dp = new bool[sum / 2 + 1];
        dp[0] = true;

        foreach (var num in nums)
        {
            var dc = (bool[])dp.Clone();

            for (var j = num; j < dp.Length; j++)
            {
                dp[j] = dc[j] || dc[j - num];
            }
        }

        return dp.Last();
    }
}
```

## C++

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        auto sum = reduce(nums.begin(), nums.end());

        if (sum % 2 == 1) {
            return false;
        }

        auto dp = vector<bool>(sum / 2 + 1);
        dp[0] = true;

        for (auto num : nums) {
            auto dc = dp;

            for (auto j = num; j < dp.size(); j++) {
                dp[j] = dc[j] || dc[j - num];
            }
        }

        return dp.back();
    }
};
```

## Java

```java
class Solution {
    public boolean canPartition(int[] nums) {
        var sum = IntStream.of(nums).sum();
        
        if (sum % 2 == 1) {
            return false;
        }

        var dp = new boolean[sum / 2 + 1];
        dp[0] = true;

        for (var num : nums) {
            var dc = dp.clone();

            for (var j = num; j < dp.length; j++) {
                dp[j] = dc[j] || dc[j - num];
            }
        }

        return dp[dp.length - 1];
    }
}
```

## JavaScript

```javascript
var canPartition = function (nums) {
  const sum = _.sum(nums)

  if (sum % 2 == 1) {
    return false
  }

  const dp = Array(sum / 2 + 1).fill(false)
  dp[0] = true

  for (const num of nums) {
    const dc = [...dp]

    for (let j = num; j < dp.length; j++) {
      dp[j] = dc[j] || dc[j - num]
    }
  }

  return dp.at(-1)
};
```

## Go

```go
func canPartition(nums []int) bool {
    sum := 0
    for _, num := range nums {
        sum += num
    }

    if sum % 2 == 1 {
        return false
    }

    dp := make([]bool, sum / 2 + 1)
    dp[0] = true

    for _, num := range nums {
        dc := slices.Clone(dp)

        for j := num; j < len(dp); j++ {
            dp[j] = dc[j] || dc[j - num]
        }
    }

    return dp[len(dp) - 1]
}
```

## Ruby

```ruby
def can_partition(nums)
  sum = nums.sum

  return false if sum % 2 == 1

  dp = Array.new(sum / 2 + 1, false)
  dp[0] = true

  nums.each do |num|
    dc = dp.clone

    (num...dp.size).each do |j|
      dp[j] = dc[j] || dc[j - num]
    end
  end

  dp[-1]
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

访问原文链接：[416. 分割等和子集 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/416-partition-equal-subset-sum)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

