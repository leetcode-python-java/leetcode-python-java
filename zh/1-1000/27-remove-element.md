# 27. 移除元素 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 Show.dev 打造你的个人品牌 →**](https://www.show.dev)

---

访问原文链接：[27. 移除元素 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/27-remove-element)，体验更佳！

力扣链接：[27. 移除元素](https://leetcode.cn/problems/remove-element), 难度等级：**简单**。

## LeetCode “27. 移除元素”问题描述

给你一个数组 `nums` 和一个值 `val`，你需要 [原地](https://en.wikipedia.org/wiki/In-place_algorithm) 移除所有数值等于 `val` 的元素。元素的顺序可能发生改变。然后返回 `nums` 中与 `val` 不同的元素的数量。

假设 `nums` 中不等于 `val` 的元素数量为 `k`，要通过此题，您需要执行以下操作：

- 更改 `nums` 数组，使 `nums` 的前 `k` 个元素包含不等于 `val` 的元素。`nums` 的其余元素和 `nums` 的大小并不重要。
- 返回 `k`。

### [示例 1]

**输入**: `nums = [3,2,2,3], val = 3`

**输出**: `2, nums = [2,2,_,_]`

**解释**: 

<p>你的函数函数应该返回 k = 2, 并且 nums 中的前两个元素均为 2。<br>
你在返回的 k 个元素之外留下了什么并不重要（因此它们并不计入评测）。</p>


### [示例 2]

**输入**: `nums = [0,1,2,2,3,0,4,2], val = 2`

**输出**: `5, nums = [0,1,4,0,3,_,_,_]`

**解释**: 

<p>你的函数应该返回 k = 5，并且 nums 中的前五个元素为 0,0,1,3,4。<br>
注意这五个元素可以任意顺序返回。<br>
你在返回的 k 个元素之外留下了什么并不重要（因此它们并不计入评测）。</p>


### [约束]

- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`

### [Hints]

<details>
  <summary>提示 1</summary>
  The problem statement clearly asks us to modify the array in-place and it also says that the element beyond the new length of the array can be anything. Given an element, we need to remove all the occurrences of it from the array. We don't technically need to **remove** that element per-say, right?

  
</details>

<details>
  <summary>提示 2</summary>
  We can move all the occurrences of this element to the end of the array. Use two pointers!

  ![](../../images/hints/27_2.png)
</details>

<details>
  <summary>提示 3</summary>
  Yet another direction of thought is to consider the elements to be removed as non-existent. In a single pass, if we keep copying the visible elements in-place, that should also solve this problem for us.

  
</details>

## 思路 1

- `双指针`，一左一右，左侧的指向数组头部，右侧的指向数组尾部。
- 如果发现左侧指针对应的数值等于*val*，并且右侧指针对应的数值不等于*val*，就进行值交换。
- 这种手段容易想到，但代码量比起`快慢指针`要多。

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Java

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        var left = 0;
        var right = nums.length - 1;

        while (left <= right) {
            if (nums[left] != val) {
                left += 1;
                continue;
            }

            if (nums[right] == val) {
                right -= 1;
                continue;
            }

            nums[left] = nums[right];
            left += 1;
            right -= 1;
        }

        return left;
    }
}
```

## Python

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        left = 0
        right = len(nums) - 1

        while left <= right:
            if nums[left] != val:
                left += 1
                continue

            if nums[right] == val:
                right -= 1
                continue

            nums[left] = nums[right]
            left += 1
            right -= 1

        return left
```

## C++

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int left = 0;
        int right = nums.size() - 1;

        while (left <= right) {
            if (nums[left] != val) {
                left += 1;
                continue;
            }

            if (nums[right] == val) {
                right -= 1;
                continue;
            }

            nums[left] = nums[right];
            left += 1;
            right -= 1;
        }

        return left;
    }
};
```

## JavaScript

```javascript
var removeElement = function (nums, val) {
  let left = 0
  let right = nums.length - 1

  while (left <= right) {
    if (nums[left] != val) {
      left += 1
      continue
    }

    if (nums[right] == val) {
      right -= 1
      continue
    }

    nums[left] = nums[right]
    left += 1
    right -= 1
  }

  return left
};
```

## C#

```csharp
public class Solution
{
    public int RemoveElement(int[] nums, int val)
    {
        int left = 0;
        int right = nums.Length - 1;

        while (left <= right)
        {
            if (nums[left] != val)
            {
                left += 1;
                continue;
            }

            if (nums[right] == val)
            {
                right -= 1;
                continue;
            }

            nums[left] = nums[right];
            left += 1;
            right -= 1;
        }

        return left;
    }
}
```

## Go

```go
func removeElement(nums []int, val int) int {
    left := 0
    right := len(nums) - 1

    for left <= right {
        if nums[left] != val {
            left += 1
            continue
        }

        if nums[right] == val {
            right -= 1
            continue
        }

        nums[left] = nums[right]
        left++
        right--
    }

    return left
}
```

## Ruby

```ruby
def remove_element(nums, val)
  left = 0
  right = nums.size - 1

  while left <= right
    if nums[left] != val
      left += 1
      next
    end

    if (nums[right] == val)
      right -= 1
      next
    end

    nums[left] = nums[right]
    left += 1
    right -= 1
  end

  left
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## 思路 2

- `快慢指针方法`，指两个指针起初都指向数组头部，后来一个指针走得更快些。
- 对于本题，什么情况下需要让快指针走快？就是快指针对应的值等于*val*时。而慢指针要保证走过的每个值都不等于*val*。
- 值的交换就发生在快指针对应的值不等于*val*，慢指针对应的值等于*val*的时候。
- 这种手段不容易想到，但比`左右双指针技术`更简洁。

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Java

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        var slowIndex = 0;

        for (var num : nums) { // This line is the most important. You'd better memorize it.
            if (num != val) {
                nums[slowIndex] = num;
                slowIndex += 1;
            }
        }

        return slowIndex;
    }
}
```

## Python

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        slow_index = 0

        for num in nums: # This line is the most important. You'd better memorize it.
            if num != val:
                nums[slow_index] = num
                slow_index += 1

        return slow_index
```

## C++

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        auto slow_index = 0;

        for (auto num : nums) { // This line is the most important. You'd better memorize it.
            if (num != val) {
                nums[slow_index] = num;
                slow_index += 1;
            }
        }

        return slow_index;
    }
};
```

## JavaScript

```javascript
var removeElement = function (nums, val) {
  let slowIndex = 0

  nums.forEach((num) => { // This line is the most important. You'd better memorize it.
    if (num != val) {
      nums[slowIndex] = num
      slowIndex += 1
    }
  })

  return slowIndex
};
```

## C#

```csharp
public class Solution
{
    public int RemoveElement(int[] nums, int val)
    {
        int slowIndex = 0;

        foreach (int num in nums) // This line is the most important. You'd better memorize it.
        {
            if (num != val)
            {
                nums[slowIndex] = num;
                slowIndex += 1;
            }
        }

        return slowIndex;
    }
}
```

## Go

```go
func removeElement(nums []int, val int) int {
    slowIndex := 0

    for _, num := range nums { // This line is the most important. You'd better memorize it.
        if num != val {
            nums[slowIndex] = num
            slowIndex += 1
        }
    }

    return slowIndex
}
```

## Ruby

```ruby
def remove_element(nums, val)
  slow_index = 0

  nums.each do |num| # This line is the most important. You'd better memorize it.
    if num != val
      nums[slow_index] = num
      slow_index += 1
    end
  end

  slow_index
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 Show.dev 打造你的个人品牌 →**](https://www.show.dev)

---

访问原文链接：[27. 移除元素 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/27-remove-element)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

