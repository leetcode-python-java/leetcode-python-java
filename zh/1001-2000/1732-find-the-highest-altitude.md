# 1732. 找到最高海拔 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[1732. 找到最高海拔 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/1732-find-the-highest-altitude)，体验更佳！

力扣链接：[1732. 找到最高海拔](https://leetcode.cn/problems/find-the-highest-altitude), 难度等级：**简单**。

## LeetCode “1732. 找到最高海拔”问题描述

有一个自行车手打算进行一场公路骑行，这条路线总共由 `n + 1` 个不同海拔的点组成。自行车手从海拔为 `0` 的点 `0` 开始骑行。

给你一个长度为 `n` 的整数数组 `gain` ，其中 `gain[i]` 是点 `i` 和点 `i + 1` 的 **净海拔高度差**（`0 <= i < n`）。请你返回 **最高点的海拔**。

### [示例 1]

**输入**: `gain = [-5,1,5,0,-7]`

**输出**: `1`

**解释**: `海拔高度依次为 [0,-5,-4,1,1,-6] 。最高海拔为 1 。`

### [示例 2]

**输入**: `gain = [-4,-3,-2,-1,4,3,2]`

**输出**: `0`

**解释**: 

<p>海拔高度依次为 [0,-4,-7,-9,-10,-6,-3,-1] 。最高海拔为 0 。</p>


### [约束]

- `n == gain.length`
- `1 <= n <= 100`
- `-100 <= gain[i] <= 100`

### [Hints]

<details>
  <summary>提示 1</summary>
  Let's note that the altitude of an element is the sum of gains of all the elements behind it

  
</details>

<details>
  <summary>提示 2</summary>
  Getting the altitudes can be done by getting the prefix sum array of the given array

  
</details>

## 思路

题目要求找到公路骑行过程中达到的最高海拔。自行车手从海拔 `0` 开始。`gain` 数组表示连续两点之间的海拔变化。

这意味着在任意点 `i` 的海拔是直到点 `i-1` 的所有海拔变化的总和（即前缀和）。我们可以维护一个累加的当前海拔高度，并不断更新遇到的最高海拔。

## 步骤

1. 初始化两个变量：`current_altitude`（当前海拔）设为 `0`，`max_altitude`（最高海拔）设为 `0`。
2. 遍历 `gain` 数组中的每一个海拔变化值 `g`。
3. 将 `g` 加到 `current_altitude` 上，得到下一个点的实际海拔。
4. 比较 `max_altitude` 和 `current_altitude`，将两者中的较大值赋给 `max_altitude`。
5. 遍历结束后，返回 `max_altitude` 即可。

## 复杂度

> - **时间复杂度**: `O(N)`，其中 `N` 是数组 `gain` 的长度。我们只需要对数组进行一次遍历。
- **空间复杂度**: `O(1)`。我们仅仅使用了几个整型变量来存储当前海拔和最高海拔，因此需要的额外空间是常数级别的。

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Python

```python
class Solution:
    def largestAltitude(self, gain: List[int]) -> int:
        current_altitude = 0
        max_altitude = 0
        
        for g in gain:
            current_altitude += g
            if current_altitude > max_altitude:
                max_altitude = current_altitude
                
        return max_altitude
```

## Java

```java
class Solution {
    public int largestAltitude(int[] gain) {
        int currentAltitude = 0;
        int maxAltitude = 0;
        
        for (int g : gain) {
            currentAltitude += g;
            if (currentAltitude > maxAltitude) {
                maxAltitude = currentAltitude;
            }
        }
        
        return maxAltitude;
    }
}
```

## JavaScript

```javascript
/**
 * @param {number[]} gain
 * @return {number}
 */
var largestAltitude = function(gain) {
    let currentAltitude = 0;
    let maxAltitude = 0;
    
    for (const g of gain) {
        currentAltitude += g;
        if (currentAltitude > maxAltitude) {
            maxAltitude = currentAltitude;
        }
    }
    
    return maxAltitude;
};
```

## Cpp

```cpp
class Solution {
public:
    int largestAltitude(vector<int>& gain) {
        int currentAltitude = 0;
        int maxAltitude = 0;
        
        for (int g : gain) {
            currentAltitude += g;
            if (currentAltitude > maxAltitude) {
                maxAltitude = currentAltitude;
            }
        }
        
        return maxAltitude;
    }
};
```

## Csharp

```csharp
public class Solution {
    public int LargestAltitude(int[] gain) {
        int currentAltitude = 0;
        int maxAltitude = 0;
        
        foreach (int g in gain) {
            currentAltitude += g;
            if (currentAltitude > maxAltitude) {
                maxAltitude = currentAltitude;
            }
        }
        
        return maxAltitude;
    }
}
```

## Go

```go
func largestAltitude(gain []int) int {
    currentAltitude := 0
    maxAltitude := 0
    
    for _, g := range gain {
        currentAltitude += g
        if currentAltitude > maxAltitude {
            maxAltitude = currentAltitude
        }
    }
    
    return maxAltitude
}
```

## Ruby

```ruby
# @param {Integer[]} gain
# @return {Integer}
def largest_altitude(gain)
    current_altitude = 0
    max_altitude = 0
    
    gain.each do |g|
        current_altitude += g
        max_altitude = current_altitude if current_altitude > max_altitude
    end
    
    max_altitude
end
```

## Rust

```rust
impl Solution {
    pub fn largest_altitude(gain: Vec<i32>) -> i32 {
        let mut current_altitude = 0;
        let mut max_altitude = 0;
        
        for g in gain {
            current_altitude += g;
            if current_altitude > max_altitude {
                max_altitude = current_altitude;
            }
        }
        
        max_altitude
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun largestAltitude(gain: IntArray): Int {
        var currentAltitude = 0
        var maxAltitude = 0
        
        for (g in gain) {
            currentAltitude += g
            if (currentAltitude > maxAltitude) {
                maxAltitude = currentAltitude
            }
        }
        
        return maxAltitude
    }
}
```

## Swift

```swift
class Solution {
    func largestAltitude(_ gain: [Int]) -> Int {
        var currentAltitude = 0
        var maxAltitude = 0
        
        for g in gain {
            currentAltitude += g
            if currentAltitude > maxAltitude {
                maxAltitude = currentAltitude
            }
        }
        
        return maxAltitude
    }
}
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

访问原文链接：[1732. 找到最高海拔 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/1732-find-the-highest-altitude)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

