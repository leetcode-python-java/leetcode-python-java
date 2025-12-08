# 349. 两个数组的交集 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

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

访问原文链接：[349. 两个数组的交集 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/349-intersection-of-two-arrays)，体验更佳！

力扣链接：[349. 两个数组的交集](https://leetcode.cn/problems/intersection-of-two-arrays), 难度等级：**简单**。

## LeetCode “349. 两个数组的交集”问题描述

给定两个数组 `nums1` 和 `nums2` ，返回 _它们的 **交集**_ 。输出结果中的每个元素一定是 **唯一** 的。我们可以 **不考虑输出结果的顺序**。

> 数组的交集: The intersection of two arrays is defined as the set of elements that are present in both arrays.

### [示例 1]

**输入**: `nums1 = [1,2,2,1], nums2 = [2,2]`

**输出**: `[2]`

### [示例 2]

**输入**: `nums1 = [4,9,5], nums2 = [9,4,9,8,4]`

**输出**: `[9,4]`

**解释**: `[4,9] 也是可通过的`

### [约束]

- `1 <= nums1.length, nums2.length <= 1000`
- `0 <= nums1[i], nums2[i] <= 1000`

## 思路

1. 把其中一个数组转为`set`，数据结构`set`的特点是元素不重复。
2. 遍历另一个数组时，如果发现当前元素已经存在于`set`中，则说明该元素属于交集，将该元素加入结果集中。
3. 结果集也采用`set`类型，因为需要去重。

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(N)`.

## Java

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        var results = new HashSet<Integer>();
        var num1Set = new HashSet<Integer>();

        for (var num : nums1) {
            num1Set.add(num);
        }

        for (var num : nums2) {
            if (num1Set.contains(num)) {
                results.add(num);
            }
        }

        return results.stream().mapToInt(num -> num).toArray();
    }
}
```

## Python

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        set_of_nums1 = set(nums1)
        results = set()

        for num in nums2:
            if num in set_of_nums1:
                results.add(num)

        return list(results)
```

## C++

```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> results;
        unordered_set<int> set_of_nums1(nums1.begin(), nums1.end());

        for (auto num : nums2) {
            if (set_of_nums1.contains(num)) {
                results.insert(num);
            }
        }

        return vector<int>(results.begin(), results.end());
    }
};
```

## JavaScript

```javascript
var intersection = function (nums1, nums2) {
  let results = new Set()
  let num1Set = new Set(nums1)

  for (const num of nums2) {
    if (num1Set.has(num)) {
      results.add(num)
    }
  }

  return Array.from(results)
};
```

## C#

```csharp
public class Solution
{
    public int[] Intersection(int[] nums1, int[] nums2)
    {
        var results = new HashSet<int>();
        var num1Set = new HashSet<int>();

        foreach (int num in nums1)
            num1Set.Add(num);

        foreach (int num in nums2)
        {
            if (num1Set.Contains(num))
            {
                results.Add(num);
            }
        }

        return results.ToArray();
    }
}
```

## Go

```go
func intersection(nums1 []int, nums2 []int) []int {
    results := map[int]bool{}
    num1Set := map[int]bool{}

    for _, num := range nums1 {
        num1Set[num] = true
    }

    for _, num := range nums2 {
        if _, ok := num1Set[num]; ok {
            results[num] = true
        }
    }

    return slices.Collect(maps.Keys(results))
}
```

## Ruby

```ruby
def intersection(nums1, nums2)
  nums1_set = Set.new(nums1)
  results = Set.new

  nums2.each do |num|
    if nums1_set.include?(num)
      results << num
    end
  end

  results.to_a
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

访问原文链接：[349. 两个数组的交集 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/349-intersection-of-two-arrays)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

