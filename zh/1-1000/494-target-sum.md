# 494. 目标和 - 力扣题解最佳实践

访问原文链接：[494. 目标和 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/494-target-sum)，体验更佳！

力扣链接：[494. 目标和](https://leetcode.cn/problems/target-sum), 难度：**中等**。

## 力扣“494. 目标和”问题描述

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

亲爱的力扣人，为了您更好的刷题体验，请访问 [leetcoder.net](https://leetcoder.net/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[494. 目标和 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/494-target-sum).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

