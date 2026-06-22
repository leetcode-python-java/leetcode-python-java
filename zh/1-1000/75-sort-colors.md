# 75. 颜色分类 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[75. 颜色分类 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/75-sort-colors)，体验更佳！

力扣链接：[75. 颜色分类](https://leetcode.cn/problems/sort-colors), 难度等级：**中等**。

## LeetCode “75. 颜色分类”问题描述

给定一个包含红色、白色和蓝色、共 `n` 个元素的数组 `nums`，**原地**对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

我们使用整数 `0`、 `1` 和 `2` 分别表示红色、白色和蓝色。

必须在不使用库的内置排序函数的情况下解决这个问题。

### [示例 1]

**输入**: `nums = [2,0,2,1,1,0]`

**输出**: `[0,0,1,1,2,2]`

### [示例 2]

**输入**: `nums = [2,0,1]`

**输出**: `[0,1,2]`

### [约束]

- `n == nums.length`
- `1 <= n <= 300`
- `nums[i]` 为 `0`、`1` 或 `2`
- **进阶：**你能想出一个仅使用常数空间的一趟扫描算法吗？

### [Hints]

<details>
  <summary>提示 1</summary>
  A rather straight forward solution is a two-pass algorithm using counting sort.

  
</details>

<details>
  <summary>提示 2</summary>
  Iterate the array counting number of 0's, 1's, and 2's.

  
</details>

<details>
  <summary>提示 3</summary>
  Overwrite array with the total number of 0's, then 1's and followed by 2's.

  
</details>

## 思路

题目要求我们原地对只包含 `0`、`1`、`2` 的数组进行排序。进阶挑战是仅使用常数额外空间，在单次遍历（一趟扫描）中完成。
这正是由 Edsger W. Dijkstra 提出的著名的“荷兰国旗问题”（Dutch National Flag problem）。我们可以使用三个指针来解决它，将数组划分为三个主要区域：开头的 `0` 区域，结尾的 `2` 区域，以及当前正在处理的元素区域（这会自然而然地把 `1` 留在中间）。

## 步骤

1. 初始化三个指针：`low = 0`（0 的边界），`high = nums.length - 1`（2 的边界），以及 `i = 0`（当前正在遍历的元素索引）。
2. 当 `i <= high` 时，进行循环：
   - 如果 `nums[i] == 0`：交换 `nums[i]` 和 `nums[low]`。我们知道从 `low` 交换过来的元素必定是 `0` 或 `1`（因为 `i` 已经扫描过那里或者和 `low` 重合），所以可以安全地将 `low` 和 `i` 都加 1。
   - 如果 `nums[i] == 1`：元素已经处于中间的正确位置，只需将 `i` 加 1 即可。
   - 如果 `nums[i] == 2`：交换 `nums[i]` 和 `nums[high]`。我们将 `high` 减 1。但是，我们**不要**在这里将 `i` 加 1，因为从 `high` 换到 `i` 位置的新元素还没有被检查过（它可能是 `0`、`1` 或 `2`）。
3. 当 `i` 越过 `high` 时，数组就已经排序完成了。

## 复杂度

> - **时间复杂度**: `O(N)`，其中 `N` 是数组 `nums` 的长度。我们最多处理每个元素两次（被 `i` 遍历到，或者从 `high` 交换过来再被检查），这意味着我们只对数组进行了一趟扫描。
- **空间复杂度**: `O(1)`。排序完全是原地进行的，仅使用了三个整型变量作为指针，只需要常数级别的额外空间。

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Python

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        # low points to the next position for 0
        # high points to the next position for 2
        low, i, high = 0, 0, len(nums) - 1
        
        while i <= high:
            if nums[i] == 0:
                # Swap and advance both low and i
                nums[low], nums[i] = nums[i], nums[low]
                low += 1
                i += 1
            elif nums[i] == 2:
                # Swap and decrement high. Do NOT advance i yet
                # because the swapped element needs to be checked
                nums[high], nums[i] = nums[i], nums[high]
                high -= 1
            else:
                # nums[i] == 1, already in place
                i += 1
```

## Java

```java
class Solution {
    public void sortColors(int[] nums) {
        int low = 0;
        int i = 0;
        int high = nums.length - 1;
        
        while (i <= high) {
            if (nums[i] == 0) {
                swap(nums, low, i);
                low++;
                i++;
            } else if (nums[i] == 2) {
                swap(nums, i, high);
                high--;
                // Don't increment 'i' here, the new nums[i] needs to be evaluated
            } else {
                // nums[i] == 1
                i++;
            }
        }
    }
    
    private void swap(int[] nums, int a, int b) {
        int temp = nums[a];
        nums[a] = nums[b];
        nums[b] = temp;
    }
}
```

## JavaScript

```javascript
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var sortColors = function(nums) {
    let low = 0;
    let i = 0;
    let high = nums.length - 1;
    
    while (i <= high) {
        if (nums[i] === 0) {
            // Swap nums[low] and nums[i]
            [nums[low], nums[i]] = [nums[i], nums[low]];
            low++;
            i++;
        } else if (nums[i] === 2) {
            // Swap nums[i] and nums[high]
            [nums[high], nums[i]] = [nums[i], nums[high]];
            high--;
            // Do not increment i, evaluate the newly swapped element
        } else {
            // If it is 1, just move forward
            i++;
        }
    }
};
```

## Cpp

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int low = 0;
        int i = 0;
        int high = nums.size() - 1;
        
        while (i <= high) {
            if (nums[i] == 0) {
                swap(nums[low], nums[i]);
                low++;
                i++;
            } else if (nums[i] == 2) {
                swap(nums[i], nums[high]);
                high--;
                // Note: i is not incremented
            } else {
                // nums[i] == 1
                i++;
            }
        }
    }
};
```

## Csharp

```csharp
public class Solution {
    public void SortColors(int[] nums) {
        int low = 0;
        int i = 0;
        int high = nums.Length - 1;
        
        while (i <= high) {
            if (nums[i] == 0) {
                // Swap
                int temp = nums[low];
                nums[low] = nums[i];
                nums[i] = temp;
                
                low++;
                i++;
            } else if (nums[i] == 2) {
                // Swap
                int temp = nums[high];
                nums[high] = nums[i];
                nums[i] = temp;
                
                high--;
            } else {
                i++;
            }
        }
    }
}
```

## Go

```go
func sortColors(nums []int) {
    low := 0
    i := 0
    high := len(nums) - 1
    
    for i <= high {
        if nums[i] == 0 {
            nums[low], nums[i] = nums[i], nums[low]
            low++
            i++
        } else if nums[i] == 2 {
            nums[high], nums[i] = nums[i], nums[high]
            high--
        } else {
            // nums[i] == 1
            i++
        }
    }
}
```

## Ruby

```ruby
# @param {Integer[]} nums
# @return {Void} Do not return anything, modify nums in-place instead.
def sort_colors(nums)
    low = 0
    i = 0
    high = nums.length - 1
    
    while i <= high
        if nums[i] == 0
            nums[low], nums[i] = nums[i], nums[low]
            low += 1
            i += 1
        elsif nums[i] == 2
            nums[high], nums[i] = nums[i], nums[high]
            high -= 1
        else
            i += 1
        end
    end
end
```

## Rust

```rust
impl Solution {
    pub fn sort_colors(nums: &mut Vec<i32>) {
        let mut low = 0;
        let mut i = 0;
        let mut high = nums.len() as i32 - 1;
        
        while (i as i32) <= high {
            match nums[i] {
                0 => {
                    nums.swap(low, i);
                    low += 1;
                    i += 1;
                }
                2 => {
                    nums.swap(i, high as usize);
                    high -= 1;
                }
                _ => {
                    // It's 1
                    i += 1;
                }
            }
        }
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun sortColors(nums: IntArray): Unit {
        var low = 0
        var i = 0
        var high = nums.size - 1
        
        while (i <= high) {
            when (nums[i]) {
                0 -> {
                    val temp = nums[low]
                    nums[low] = nums[i]
                    nums[i] = temp
                    low++
                    i++
                }
                2 -> {
                    val temp = nums[high]
                    nums[high] = nums[i]
                    nums[i] = temp
                    high--
                }
                else -> {
                    i++
                }
            }
        }
    }
}
```

## Swift

```swift
class Solution {
    func sortColors(_ nums: inout [Int]) {
        var low = 0
        var i = 0
        var high = nums.count - 1
        
        while i <= high {
            if nums[i] == 0 {
                nums.swapAt(low, i)
                low += 1
                i += 1
            } else if nums[i] == 2 {
                nums.swapAt(i, high)
                high -= 1
            } else {
                i += 1
            }
        }
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

访问原文链接：[75. 颜色分类 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/75-sort-colors)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

