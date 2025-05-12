# 1049. 最后一块石头的重量 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

访问原文链接：[1049. 最后一块石头的重量 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/1049-last-stone-weight-ii)，体验更佳！

力扣链接：[1049. 最后一块石头的重量 II](https://leetcode.cn/problems/last-stone-weight-ii), 难度等级：**中等**。

## LeetCode “1049. 最后一块石头的重量 II”问题描述

有一堆石头，用整数数组 `stones` 表示。其中 `stones[i]` 表示第 `i` 块石头的重量。

每一回合，从中选出**任意两块石头**，然后将它们一起粉碎。假设石头的重量分别为 `x` 和 `y`，且 `x <= y`。那么粉碎的可能结果如下：

- 如果 `x == y`，那么两块石头都会被完全粉碎；
- 如果 `x != y`，那么重量为 `x` 的石头将会完全粉碎，而重量为 `y` 的石头新重量为 `y-x`。

最后，**最多只会剩下一块** 石头。返回此石头 **最小的可能重量** 。如果没有石头剩下，就返回 `0`。

### [示例 1]

**输入**: `stones = [2,7,4,1,8,1]`

**输出**: `1`

**解释**: 

<p>组合 2 和 4，得到 2，所以数组转化为 [2,7,1,8,1]，<br>
组合 7 和 8，得到 1，所以数组转化为 [2,1,1,1]，<br>
组合 2 和 1，得到 1，所以数组转化为 [1,1,1]，<br>
组合 1 和 1，得到 0，所以数组转化为 [1]，这就是最优值。</p>


### [示例 2]

**输入**: `stones = [31,26,33,21,40]`

**输出**: `5`

### [约束]

1 <= stones.length <= 30
1 <= stones[i] <= 100

### [Hints]

<details>
  <summary>提示 1</summary>
  Think of the final answer as a sum of weights with + or - sign symbols in front of each weight. Actually, all sums with 1 of each sign symbol are possible.

  
</details>

<details>
  <summary>提示 2</summary>
  Use dynamic programming: for every possible sum with N stones, those sums +x or -x is possible with N+1 stones, where x is the value of the newest stone. (This overcounts sums that are all positive or all negative, but those don't matter.)

  
</details>

## 思路 1

- 这道题可以用蛮力法解决，就是找出数组所有的子集，看每个子集数组的和是否接近完整数组和的一半，找最接近的那个。但是当我们看到`stones.length <= 30`的时候，我们就知道这样的解法一定会超时。
- 所以我们需要换个思路，你之前的题目相当于求拆分后两个数组和的最小差值，如果找到一个子集数组，它的和最接近完整数组和的一半，那么它就是我们想要的子集数组。
- 那么这道题就变成了`0/1背包问题`。

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
    - `dp[j]`表示是否可以用前`i`个`stones`的`和`得到`j`。
    - `dp[j]`是一个布尔值。
2. 确定 `dp` 数组的初始值
    - 举个例子：

        ```
        stones = [2,7,4,1,8,1]，所以 '总和的一半' 是 11。
        背包的 `size` 就是 '11 + 1'，‘物品’ 是 'stones'。
        所以初始化后，'dp' 数组将是：
        #   0 1 2 3 4 5 6 7 8 9 10 11
        #   T F F F F F F F F F F  F  # dp
        # 2
        # 7
        # 4
        # 1
        # 8
        # 1
        ```
    - `dp[0]` 设为 `true`，表示不使用任何 `stones` 也可以得到一个空背包。另外，它作为起始值，后面的 `dp[j]` 将依赖于它。如果它是 `false`，则 `dp[j]` 的所有值都将为 `false`。
    - `dp[j] = false (j != 0)`，表示不使用 `stones` 就不可能得到 `j`。
3. 根据一个示例，“按顺序”填入`dp`网格数据。

    ```
    1. 使用第一块石头 '2'。
    #   0 1 2 3 4 5 6 7 8 9 10 11
    #   T F F F F F F F F F F  F
    # 2 T F T F F F F F F F F  F  # dp
    ```
    ```
    2. 使用第二颗石头“7”。
    #   0 1 2 3 4 5 6 7 8 9 10 11
    #   T F F F F F F F F F F  F
    # 2 T F T F F F F F F F F  F
    # 7 T F T F F F F T F T F  F
    ```
    ```
    3. 使用第三颗石头“4”。
    #   0 1 2 3 4 5 6 7 8 9 10 11
    #   T F F F F F F F F F F  F
    # 2 T F T F F F F F F F F  F
    # 7 T F T F F F F F T F F  F
    # 4 T F T F T F T T F T F  T # dp
    # ...
    ```
4. 根据`dp`网格数据，推导出“递推公式”。

    ```cpp
    dp[j] = dp[j] || dp[j - stones[i]]
    ```
5. 写出程序，并打印`dp`数组，不合预期就调整。

## 复杂度

- 时间复杂度: `O(n * sum/2)`.
- 空间复杂度: `O(sum/2)`.

## Python

```python
class Solution:
    def lastStoneWeightII(self, stones: List[int]) -> int:
        sum_ = sum(stones)

        dp = [False] * (sum_ // 2 + 1)
        dp[0] = True

        for stone in stones:
            # If not traversing in reverse order, the newly assigned value `dp[j]` will act as `dp[j - stone]` later,
            # then the subsequent `dp[j]` will be affected. But each `stone` can only be used once!
            for j in range(len(dp) - 1, 0, -1):
                if j < stone:
                    break
                dp[j] = dp[j] or dp[j - stone]

        for i in range(len(dp) - 1, -1, -1):
            if dp[i]:
                return sum_ - i * 2
```

## C#

```csharp
public class Solution {
    public int LastStoneWeightII(int[] stones) {
        var sum = stones.Sum();

        var dp = new bool[sum / 2 + 1];
        dp[0] = true;

        foreach (int stone in stones) {
            for (var j = dp.GetUpperBound(0); j >= stone; j--) {
                dp[j] = dp[j] || dp[j - stone];
            }
        }

        for (var j = dp.GetUpperBound(0); j >= 0; j--) {
            if (dp[j]) {
                return sum - j * 2;
            }
        }

        throw new ArithmeticException("lastStoneWeightII() has a logical error!");
    }
}
```

## C++

```cpp
class Solution {
public:
    int lastStoneWeightII(vector<int>& stones) {
        auto sum = reduce(stones.begin(), stones.end());

        auto dp = vector<bool>(sum / 2 + 1);
        dp[0] = true;

        for (auto stone : stones) {
            for (auto j = dp.size() - 1; j >= stone; j--) {
                dp[j] = dp[j] || dp[j - stone];
            }
        }

        for (auto i = dp.size() - 1; i >= 0; i--) {
            if (dp[i]) {
                return sum - i * 2;
            }
        }

        throw logic_error("lastStoneWeightII() has a logical error!");
    }
};
```

## Java

```java
class Solution {
    public int lastStoneWeightII(int[] stones) {
        var sum = IntStream.of(stones).sum();

        var dp = new boolean[sum / 2 + 1];
        dp[0] = true;

        for (var stone : stones) {
            for (var j = dp.length - 1; j >= stone; j--) {
                dp[j] = dp[j] || dp[j - stone];
            }
        }

        for (var j = dp.length - 1; j >= 0; j--) {
            if (dp[j]) {
                return sum - j * 2;
            }
        }

        throw new ArithmeticException("lastStoneWeightII() has a logical error!");
    }
}
```

## JavaScript

```javascript
var lastStoneWeightII = function (stones) {
  const sum = _.sum(stones)

  const dp = Array(Math.floor(sum / 2) + 1).fill(false)
  dp[0] = true

  for (const stone of stones) {
    for (let j = dp.length - 1; j >= stone; j--) {
      dp[j] = dp[j] || dp[j - stone]
    }
  }

  for (let j = dp.length - 1; j >= 0; j--) {
    if (dp[j]) {
      return sum - j * 2
    }
  }
};
```

## Go

```go
func lastStoneWeightII(stones []int) int {
    sum := 0
    for _, stone := range stones {
        sum += stone
    }

    dp := make([]bool, sum / 2 + 1)
    dp[0] = true

    for _, stone := range stones {
        for j := len(dp) - 1; j >= stone; j-- {
            dp[j] = dp[j] || dp[j - stone]
        }
    }

    for j := len(dp) - 1; j >= 0; j-- {
        if dp[j] {
            return sum - j * 2
        }
    }

    return -1 // This line should be unreachable. It represents function has a logical error.
}
```

## Ruby

```ruby
def last_stone_weight_ii(stones)
  sum = stones.sum

  dp = Array.new(sum / 2 + 1, false)
  dp[0] = true

  stones.each do |stone|
    (1...dp.size).reverse_each do |j|
      break if j < stone

      dp[j] = dp[j] || dp[j - stone]
    end
  end

  (0...dp.size).reverse_each do |j|
    return sum - j * 2 if dp[j]
  end
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

## 复杂度

- 时间复杂度: `O(n * sum/2)`.
- 空间复杂度: `O(n * sum/2)`.

## Python

```python
class Solution:
    def lastStoneWeightII(self, stones: List[int]) -> int:
        sum_ = sum(stones)

        dp = [False] * (sum_ // 2 + 1)
        dp[0] = True

        for stone in stones:
            dc = dp.copy()

            for j in range(stone, len(dp)):
                dp[j] = dc[j] or dc[j - stone]

        for i in range(len(dp) - 1, -1, -1):
            if dp[i]:
                return sum_ - i * 2
```

## C#

```csharp
public class Solution
{
    public int LastStoneWeightII(int[] stones)
    {
        int sum = stones.Sum();

        var dp = new bool[sum / 2 + 1];
        dp[0] = true;

        foreach (int stone in stones)
        {
            var dc = (bool[]) dp.Clone();

            for (var j = stone; j < dp.Length; j++)
            {
                dp[j] = dc[j] || dc[j - stone];
            }
        }

        for (var j = dp.GetUpperBound(0); j >= 0; j--)
        {
            if (dp[j])
            {
                return sum - j * 2;
            }
        }

        throw new ArithmeticException("lastStoneWeightII() has a logical error!");
    }
}
```

## C++

```cpp
class Solution {
public:
    int lastStoneWeightII(vector<int>& stones) {
        auto sum = reduce(stones.begin(), stones.end());

        auto dp = vector<bool>(sum / 2 + 1);
        dp[0] = true;

        for (auto stone : stones) {
            auto dc = dp;

            for (auto j = stone; j < dp.size(); j++) {
                dp[j] = dc[j] || dc[j - stone];
            }
        }

        for (auto i = dp.size() - 1; i >= 0; i--) {
            if (dp[i]) {
                return sum - i * 2;
            }
        }

        throw logic_error("lastStoneWeightII() has a logical error!");
    }
};
```

## Java

```java
class Solution {
    public int lastStoneWeightII(int[] stones) {
        var sum = IntStream.of(stones).sum();

        var dp = new boolean[sum / 2 + 1];
        dp[0] = true;

        for (var stone : stones) {
            var dc = dp.clone();

            for (var j = stone; j < dp.length; j++) {
                dp[j] = dc[j] || dc[j - stone];
            }
        }

        for (var j = dp.length - 1; j >= 0; j--) {
            if (dp[j]) {
                return sum - j * 2;
            }
        }

        throw new ArithmeticException("lastStoneWeightII() has a logical error!");
    }
}
```

## JavaScript

```javascript
var lastStoneWeightII = function (stones) {
  const sum = _.sum(stones)

  const dp = Array(Math.floor(sum / 2) + 1).fill(false)
  dp[0] = true

  for (const stone of stones) {
    const dc = [...dp]

    for (let j = stone; j < dp.length; j++) {
      dp[j] = dc[j] || dc[j - stone]
    }
  }

  for (let j = dp.length - 1; j >= 0; j--) {
    if (dp[j]) {
      return sum - j * 2
    }
  }
};
```

## Go

```go
func lastStoneWeightII(stones []int) int {
    sum := 0
    for _, stone := range stones {
        sum += stone
    }

    dp := make([]bool, sum / 2 + 1)
    dp[0] = true

    for _, stone := range stones {
        dc := slices.Clone(dp)

        for j := stone; j < len(dp); j++ {
            dp[j] = dc[j] || dc[j - stone]
        }
    }

    for j := len(dp) - 1; j >= 0; j-- {
        if dp[j] {
            return sum - j * 2
        }
    }

    return -1 // This line should be unreachable. It represents function has a logical error.
}
```

## Ruby

```ruby
def last_stone_weight_ii(stones)
  sum = stones.sum

  dp = Array.new(sum / 2 + 1, false)
  dp[0] = true

  stones.each do |stone|
    dc = dp.clone

    (stone...dp.size).each do |j|
      dp[j] = dc[j] || dc[j - stone]
    end
  end

  (0...dp.size).reverse_each do |j|
    return sum - j * 2 if dp[j]
  end
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.blog](https://leetcode.blog/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[1049. 最后一块石头的重量 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/1049-last-stone-weight-ii).

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

