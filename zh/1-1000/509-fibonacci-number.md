# 509. 斐波那契数 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[509. 斐波那契数 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/509-fibonacci-number)，体验更佳！

力扣链接：[509. 斐波那契数](https://leetcode.cn/problems/fibonacci-number), 难度等级：**简单**。

## LeetCode “509. 斐波那契数”问题描述

**斐波那契数** （通常用 `F(n)` 表示）形成的序列称为 **斐波那契数列** 。该数列由 `0` 和 `1` 开始，后面的每一项数字都是前面两项数字的和。也就是：

> F(0) = 0，F(1) = 1
> F(n) = F(n - 1) + F(n - 2)，其中 n > 1

给定 `n` ，请计算 `F(n)` 。

### [示例 1]

**输入**: `n = 2`

**输出**: `1`

**解释**: `F(2) = F(1) + F(0) = 1 + 0 = 1`

### [示例 2]

**输入**: `n = 3`

**输出**: `2`

**解释**: `F(3) = F(2) + F(1) = 1 + 1 = 2`

### [示例 3]

**输入**: `n = 4`

**输出**: `3`

**解释**: `F(4) = F(3) + F(2) = 2 + 1 = 3`

### [约束]

0 <= n <= 30

## 思路 1



## “递归”的模式

递归（Recursion）是计算机科学和数学中的一个重要概念，指的是 一个函数在其定义中 **直接或间接调用自身** 的方法。

### 递归的核心思想

- **自我调用**：函数在执行过程中调用自身。
- **基线情况**：相当于终止条件。到达基线情况后，就可以返回结果了，不需要再递归调用，防止无限循环。
- **递归步骤**：问题逐步向“基线情况”靠近的步骤。

## 复杂度

> 如果不加用于缓存已知结果的Map，时间复杂度将上升为O( 2^N )

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(N)`.

## C#

```csharp
public class Solution {
    IDictionary<int, int> numToFibNum = new Dictionary<int, int>();

    public int Fib(int n) {
        if (n <= 1) {
            return n;
        }

        if (numToFibNum.ContainsKey(n)) {
            return numToFibNum[n];
        }

        numToFibNum[n] = Fib(n - 1) + Fib(n - 2);

        return numToFibNum[n];
    }
}
```

## Python

```python
class Solution:
    @cache
    def fib(self, n: int) -> int:
        if n <= 1:
            return n

        return self.fib(n - 1) + self.fib(n - 2)
```

## C++

```cpp
class Solution {
public:
    int fib(int n) {
        if (n <= 1) {
            return n;
        }

        if (num_to_fib_num_.contains(n)) {
            return num_to_fib_num_[n];
        }

        num_to_fib_num_[n] = fib(n - 1) + fib(n - 2);

        return num_to_fib_num_[n];
    }

private:
    unordered_map<int, int> num_to_fib_num_;
};
```

## Java

```java
class Solution {
    var numToFibNum = new HashMap<Integer, Integer>();

    public int fib(int n) {
        if (n <= 1) {
            return n;
        }

        if (numToFibNum.containsKey(n)) {
            return numToFibNum.get(n);
        }

        numToFibNum.put(n, fib(n - 1) + fib(n - 2));

        return numToFibNum.get(n);
    }
}
```

## JavaScript

```javascript
const numToFibNum = new Map()

var fib = function (n) {
    if (n <= 1) {
        return n
    }

    if (numToFibNum.has(n)) {
        return numToFibNum.get(n)
    }

    numToFibNum.set(n, fib(n - 1) + fib(n - 2))

    return numToFibNum.get(n)
};
```

## Go

```go
func fib(m int) int {
    numToFibNum := map[int]int{}

    var fibonacci func (int) int

    fibonacci = func (n int) int {
        if n <= 1 {
            return n
        }

        if result, ok := numToFibNum[n]; ok {
            return result
        }

        numToFibNum[n] = fibonacci(n - 1) + fibonacci(n - 2)
        return numToFibNum[n]
    }

    return fibonacci(m)
}
```

## Ruby

```ruby
def fib(n)
  return n if n <= 1

  @cache = {} if @cache.nil?

  return @cache[n] if @cache.key?(n)

  @cache[n] = fib(n - 1) + fib(n - 2)

  @cache[n]
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## 思路 2



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

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(N)`.

## C#

```csharp
public class Solution
{
    public int Fib(int n)
    {
        if (n <= 1)
            return n;

        var dp = new int[n + 1];
        dp[1] = 1;

        for (var i = 2; i < dp.Length; i++)
        {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }
}
```

## Python

```python
class Solution:
    def fib(self, n: int) -> int:
        if n == 0:
            return 0

        dp = [0] * (n + 1)
        dp[1] = 1

        for i in range(2, len(dp)):
            dp[i] = dp[i - 1] + dp[i - 2]

        return dp[-1]
```

## C++

```cpp
class Solution {
public:
    int fib(int n) {
        if (n <= 1) {
            return n;
        }

        auto dp = vector<int>(n + 1);
        dp[1] = 1;

        for (auto i = 2; i < dp.size(); i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }
};
```

## Java

```java
class Solution {
    public int fib(int n) {
        if (n <= 1) {
            return n;
        }

        var dp = new int[n + 1];
        dp[1] = 1;

        for (var i = 2; i < dp.length; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }
}
```

## JavaScript

```javascript
var fib = function (n) {
    if (n <= 1) {
        return n
    }

    const dp = Array(n + 1).fill(0)
    dp[1] = 1

    for (let i = 2; i < dp.length; i++) {
        dp[i] = dp[i - 1] + dp[i - 2]
    }

    return dp[n]
};
```

## Go

```go
func fib(n int) int {
    if n == 0 {
        return 0
    }

    dp := make([]int, n + 1)
    dp[1] = 1

    for i := 2; i <= n; i++ {
        dp[i] = dp[i - 2] + dp[i - 1]
    }

    return dp[n]
}
```

## Ruby

```ruby
def fib(n)
  return 0 if n == 0

  dp = Array.new(n + 1, 0)
  dp[1] = 1

  (2...dp.size).each do |i|
    dp[i] = dp[i - 1] + dp[i - 2]
  end

  dp[-1]
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## 思路 3



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

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## C#

```csharp
public class Solution
{
    public int Fib(int n)
    {
        if (n <= 1)
            return n;

        int[] dp = [0, 1];

        for (var i = 2; i <= n; i++)
        {
            var dc = (int[])dp.Clone();

            dp[0] = dc[1];
            dp[1] = dc[0] + dc[1];
        }

        return dp[1];
    }
}
```

## Python

```python
class Solution:
    def fib(self, n: int) -> int:
        if n == 0:
            return 0

        dp = [0, 1]

        for i in range(2, n + 1):
            dc = dp.copy()

            dp[0] = dc[1]
            dp[1] = dc[0] + dc[1]

        return dp[1]
```

## C++

```cpp
class Solution {
public:
    int fib(int n) {
        if (n <= 1) {
            return n;
        }

        vector dp = {0, 1};

        for (auto i = 2; i <= n; i++) {
            auto dc = dp;

            dp[0] = dc[1];
            dp[1] = dc[0] + dc[1];
        }

        return dp[1];
    }
};
```

## Java

```java
class Solution {
    public int fib(int n) {
        if (n <= 1) {
            return n;
        }

        int[] dp = {0, 1};

        for (var i = 2; i <= n; i++) {
            var dc = dp.clone();

            dp[0] = dc[1];
            dp[1] = dc[0] + dc[1];
        }

        return dp[1];
    }
}
```

## JavaScript

```javascript
var fib = function (n) {
    if (n <= 1) {
        return n
    }

    const dp = [0, 1]

    for (let i = 2; i <= n; i++) {
        const dc = [...dp]

        dp[0] = dc[1]
        dp[1] = dc[0] + dc[1]
    }

    return dp[1]
};
```

## Go

```go
func fib(n int) int {
    if n == 0 {
        return 0
    }

    dp := []int{0, 1}

    for i := 2; i <= n; i++ {
        dc := slices.Clone(dp)

        dp[0] = dc[1]
        dp[1] = dc[0] + dc[1]
    }

    return dp[1]
}
```

## Ruby

```ruby
def fib(n)
  return 0 if n == 0

  dp = [0, 1]

  (2..n).each do |i|
    dc = dp.clone

    dp[0] = dc[1]
    dp[1] = dc[0] + dc[1]
  end

  dp[1]
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

访问原文链接：[509. 斐波那契数 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/509-fibonacci-number)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

