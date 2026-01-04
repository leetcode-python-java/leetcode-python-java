# 605. 种花问题 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

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

访问原文链接：[605. 种花问题 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/605-can-place-flowers)，体验更佳！

力扣链接：[605. 种花问题](https://leetcode.cn/problems/can-place-flowers), 难度等级：**简单**。

## LeetCode “605. 种花问题”问题描述

假设有一个很长的花坛，一部分地块种植了花，另一部分却没有。可是，花**不能种植在相邻**的地块上，它们会争夺水源，两者都会死去。

给你一个整数数组 `flowerbed` 表示花坛，由若干 `0` 和 `1` 组成，其中 `0` 表示没种植花，`1` 表示种植了花。另有一个数 `n` ，能否在不打破种植规则的情况下种入 `n` 朵花？能则返回 `true` ，不能则返回 `false` 。

### [示例 1]

**输入**: `flowerbed = [1,0,0,0,1], n = 1`

**输出**: `true`

### [示例 2]

**输入**: `flowerbed = [1,0,0,0,1], n = 2`

**输出**: `false`

### [约束]

- `1 <= flowerbed.length <= 2 * 10^4`
- `flowerbed[i]` 为 `0` 或 `1`
- `flowerbed` 中不存在相邻的两朵花
- `0 <= n <= flowerbed.length`

## 思路

检查每个空地块（`0`），若其左右均为空（或边界），则可种花（置`1`），并计数。若最终计数≥`n`，返回`true`，否则`false`。

## “贪心算法”的模式

“贪心算法”是在每一步中都采取当前状态下最优的决策，从而希望导致“全局最优”的算法策略。即“局部最优”能导致“全局最优”。

## 步骤

1. 初始化计数器`count = 0`。
2. 遍历花坛每个地块：
    - 若当前为`1`，跳过。
    - 若当前为`0`且左右均为`0`（或边界），则种花（置`1`），`count += 1`。
3. 返回`count >= n`。

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Python

```python
class Solution:
    def canPlaceFlowers(self, flowerbed: List[int], n: int) -> bool:
        count = 0

        for i in range(len(flowerbed)):
            if flowerbed[i] == 1:
                continue

            if (i == 0 or flowerbed[i - 1] == 0) and \
               (i == len(flowerbed) - 1 or flowerbed[i + 1] == 0):
                flowerbed[i] = 1
                count += 1

        return count >= n
```

## Java

```java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int count = 0;

        for (int i = 0; i < flowerbed.length; i++) {
            if (flowerbed[i] == 1) {
                continue;
            }

            if ((i == 0 || flowerbed[i - 1] == 0) && 
                (i == flowerbed.length - 1 || flowerbed[i + 1] == 0)) {
                flowerbed[i] = 1;
                count++;
            }
        }

        return count >= n;
    }
}
```

## C++

```cpp
class Solution {
public:
    bool canPlaceFlowers(vector<int>& flowerbed, int n) {
        int count = 0;

        for (int i = 0; i < flowerbed.size(); i++) {
            if (flowerbed[i] == 1) {
                continue;
            }

            if ((i == 0 || flowerbed[i - 1] == 0) && 
                (i == flowerbed.size() - 1 || flowerbed[i + 1] == 0)) {
                flowerbed[i] = 1;
                count++;
            }
        }

        return count >= n;
    }
};
```

## JavaScript

```javascript
var canPlaceFlowers = function(flowerbed, n) {
  let count = 0;

  for (let i = 0; i < flowerbed.length; i++) {
    if (flowerbed[i] === 1) {
      continue;
    }

    if ((i === 0 || flowerbed[i - 1] === 0) && 
      (i === flowerbed.length - 1 || flowerbed[i + 1] === 0)) {
      flowerbed[i] = 1;
      count++;
    }
  }

  return count >= n;  
};

```

## Go

```go
func canPlaceFlowers(flowerbed []int, n int) bool {
    count := 0

    for i := 0; i < len(flowerbed); i++ {
        if flowerbed[i] == 1 {
            continue
        }

        if (i == 0 || flowerbed[i - 1] == 0) && 
           (i == len(flowerbed) - 1 || flowerbed[i + 1] == 0) {
            flowerbed[i] = 1
            count++
        }
    }

    return count >= n
}

```

## C#

```csharp
public class Solution
{
    public bool CanPlaceFlowers(int[] flowerbed, int n)
    {
        int count = 0;

        for (int i = 0; i < flowerbed.Length; i++)
        {
            if (flowerbed[i] == 1)
            {
                continue;
            }

            if ((i == 0 || flowerbed[i - 1] == 0) && 
                (i == flowerbed.Length - 1 || flowerbed[i + 1] == 0))
                {
                flowerbed[i] = 1;
                count++;
            }
        }

        return count >= n;
    }
}
```

## Ruby

```ruby
def can_place_flowers(flowerbed, n)
  count = 0

  flowerbed.each_with_index do |plot, i|
    next if plot == 1

    if (i == 0 || flowerbed[i - 1] == 0) && 
       (i == flowerbed.length - 1 || flowerbed[i + 1] == 0)
      flowerbed[i] = 1
      count += 1
    end
  end

  count >= n
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

访问原文链接：[605. 种花问题 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/605-can-place-flowers)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

