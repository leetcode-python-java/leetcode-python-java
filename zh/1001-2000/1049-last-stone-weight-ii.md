# 1049. 最后一块石头的重量 II - 力扣题解最佳实践

访问 原文链接：[1049. 最后一块石头的重量 II - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/1049-last-stone-weight-ii) 体验更佳！

GitHub 仓库: [fuck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

力扣链接：[1049. 最后一块石头的重量 II](https://leetcode.cn/problems/last-stone-weight-ii), 难度：**中等**。

## 力扣“1049. 最后一块石头的重量 II”问题描述

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
- 那么这道题就变成了`0/1背包问题`，它属于`动态规划`，`动态规划`是指当前题的答案可以从前面的同类题中推导出来，因此用`dp`数组来记录所有的答案。
- `0/1背包问题`的核心逻辑是使用二维`dp`数组或者一维`dp`**滚动数组**，先**遍历物品**，再**遍历背包大小**（`逆序`或者使用`dp.clone`），然后**引用当前'物品'大小对应的前一个值**。
- 使用二维`dp`数组需要记住的东西很多，面试的时候很难一次性写对，这里就不描述了。

## 步骤

### '0/1背包问题'中的常用步骤

这五个步骤是解决`动态规划`问题的模式。

1. 确定`dp[j]`的**含义**
    - 我们可以使用一维`dp`**滚动数组**。滚动数组意味着每次迭代时都会覆盖数组的值。
    - 首先，尝试使用问题的`return`值作为`dp[j]`的值来确定`dp[j]`的含义。如果不行，请尝试另一种方法。
    - 所以，`dp[j]`表示是否可以`sum`前`i`个`stones`得到`j`。
    - `dp[j]`是一个布尔值。
2. 确定 `dp` 数组的初始值
    - 举个例子：

        ```ruby
        stones = [2,7,4,1,8,1]，所以 '一半的总和' 是 11。
        背包的 `size` 是 '一半的总和'，`items` 是 'stones'。
        所以初始化后，'dp' 数组将是：
        # 0 1 2 3 4 5 6 7 8 9 10 11
        # T F F F F F F F F F F F F F # dp
        # 2
        # 7
        # 4
        # 1
        # 8
        # 1
        ```
    - 可以看到 `dp` 数组大小比背包大小大**一**。这样，背包大小和索引值就相等了，有助于理解。
    - `dp[0]` 设置为 `true`，表示不使用任何 `stones` 也可以得到一个空背包。另外，它作为起始值，后面的 `dp[j]` 将依赖于它。如果它是 `false`，则 `dp[j]` 的所有值都将为 `false`。
    - `dp[j] = false (j != 0)`，表示不使用 `stones` 就不可能得到 `j`。
3. 确定 `dp` 数组的递归公式
    - 尝试完成网格。在此过程中，您将获得推导公式的灵感。

        ```ruby
        1. 使用第一块石头 '2'。
        # 0 1 2 3 4 5 6 7 8 9 10 11
        # T F F F F F F F F F F F F
        # 2 T F T F F F F F F F F F # dp
        ```
        ```ruby
        2. 使用第二颗石头“7”。
        # 0 1 2 3 4 5 6 7 8 9 10 11
        # T F F F F F F F F F F F
        # 2 T F T F F F F F F F F
        # 7 T F T F F F F T F T F F
        ```
        ```ruby
        3. 使用第三颗石头“4”。
        # 0 1 2 3 4 5 6 7 8 9 10 11
        # T F F F F F F F F F F F F
        # 2 T F T F F F F F F F F F
        # 7 T F T F F F F F T F T F F
        # 4 T F T F T F T F T F T F T # dp
        # ...
        # 您不需要完成网格，只要您有足够的信息来推导出公式。
        ```
    - 在分析示例 `dp` 网格后，我们可以推导出 `递归公式`：

        ```cpp
        dp[j] = dp[j] || dp[j - stones[i]]
        ```
4. 确定 `dp` 数组的遍历顺序
    - `dp[j]` 依赖于 `dp[j]` 和 `dp[j - stones[i]]`，所以我们应该 **以相反的顺序** 遍历 `dp` 数组。
    - 请思考我们是否可以 **不以相反的顺序** 遍历 `dp` 数组？在 `Python` 解决方案的代码注释中，我将回答这个问题。
5. 检查 `dp` 数组的值
    - 打印 `dp` 以查看它是否符合预期。

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

亲爱的力扣人，为了您更好的刷题体验，请访问 [leetcoder.net](https://leetcoder.net)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[1049. 最后一块石头的重量 II - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/1049-last-stone-weight-ii).

GitHub 仓库: [fuck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).
