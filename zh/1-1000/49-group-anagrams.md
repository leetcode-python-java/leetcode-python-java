# 49. 字母异位词分组 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**leader.me**](https://www.leader.me) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[49. 字母异位词分组 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/49-group-anagrams)，体验更佳！

力扣链接：[49. 字母异位词分组](https://leetcode.cn/problems/group-anagrams), 难度等级：**中等**。

## LeetCode “49. 字母异位词分组”问题描述

给你一个字符串数组，请你将 **字母异位词** 组合在一起。可以按任意顺序返回结果列表。

> **字母异位词** 是由重新排列源单词的所有字母得到的一个新单词。

### [示例 1]

**输入**: `strs = ["eat", "tea", "tan", "ate", "nat", "bat"]`

**输出**: `[["bat"],["nat","tan"],["ate","eat","tea"]]`

### [示例 2]

**输入**: `strs = [""]`

**输出**: `[[""]]`

### [示例 3]

**输入**: `strs = ["a"]`

**输出**: `[["a"]]`

### [约束]

- `1 <= strs.length <= 10^4`
- `0 <= strs[i].length <= 100`
- `strs[i]` 仅包含小写字母

## 思路

- 两个字符串，`bat`和`atb`，用什么方法能最快地知道他们是字母异位词呢？

    <details><summary>点击查看答案</summary><p>将每个字符串都按字母表顺序排序，然后比较排过序的两个字符串。相等，就是。</p></details>

- 但是排序后，原字符串没有被考虑进来，而结果求的是原字符串的分组。如何解决？

    <details><summary>点击查看答案</summary><p>用元组，即把按字母表顺序排序后的字符串和原字符串放在一个元组里，像这样：`("abt", "bat")`。</p></details>

- 剩下要做的，就是对这个元组数组进行分组了。如何分组最简单？

    <details><summary>点击查看答案</summary><p>用`Map`，`key`是按字母表顺序排过序的字符串，`value`是原字符串的数组。</p></details>

## 复杂度

> M = string.length

- 时间复杂度: `O(N * M * logM)`.
- 空间复杂度: `O(N)`.

## Python

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        pairs = [(''.join(sorted(string)), string) for string in strs]

        ordered_to_original = defaultdict(list)

        for ordered, original in pairs:
            ordered_to_original[ordered].append(original)

        return list(ordered_to_original.values())
```

## Ruby

```ruby
# @param {String[]} strs
# @return {String[][]}
def group_anagrams(strs)
  result = Hash.new([])
  strs.each do |str|
    result[str.chars.sort.join] += [str]
  end
  result.values
end

# Or solution 2: More concise way

# @param {String[]} strs
# @return {String[][]}
def group_anagrams(strs)
  strs.group_by { |string| string.chars.sort }.values
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
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[49. 字母异位词分组 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/49-group-anagrams)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

