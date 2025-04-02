# 416. 分割等和子集 - 力扣题解最佳实践

访问原文链接：[416. 分割等和子集 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/416-partition-equal-subset-sum)，体验更佳！

力扣链接：[416. 分割等和子集](https://leetcode.cn/problems/partition-equal-subset-sum), 难度：**中等**。

## 力扣“416. 分割等和子集”问题描述

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

亲爱的力扣人，为了您更好的刷题体验，请访问 [leetcoder.net](https://leetcoder.net/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[416. 分割等和子集 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/416-partition-equal-subset-sum).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

