# 3478. 选出和最大的 K 个元素 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

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

访问原文链接：[3478. 选出和最大的 K 个元素 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/3478-choose-k-elements-with-maximum-sum)，体验更佳！

力扣链接：[3478. 选出和最大的 K 个元素](https://leetcode.cn/problems/choose-k-elements-with-maximum-sum), 难度等级：**中等**。

## LeetCode “3478. 选出和最大的 K 个元素”问题描述

给你两个整数数组，`nums1` 和 `nums2`，长度均为 `n`，以及一个正整数 `k` 。

对从 `0` 到 `n - 1` 每个下标 `i` ，执行下述操作：

- 找出所有满足 `nums1[j]` 小于 `nums1[i]` 的下标 `j` 。
- 从这些下标对应的 `nums2[j]` 中选出 至多 `k` 个，并 最大化 这些值的总和作为结果。

返回一个长度为 `n` 的数组 `answer` ，其中 `answer[i]` 表示对应下标 `i` 的结果。


### [示例 1]

**输入**: `nums1 = [4,2,1,5,3], nums2 = [10,20,30,40,50], k = 2`

**输出**: `[80,30,0,80,50]`

**解释**: 

<ul>
<li>对于 <code>i = 0</code> ：满足 <code>nums1[j] &lt; nums1[0]</code> 的下标为 <code>[1, 2, 4]</code> ，选出其中值最大的两个，结果为 <code>50 + 30 = 80</code> 。</li>
<li>对于 <code>i = 1</code> ：满足 <code>nums1[j] &lt; nums1[1]</code> 的下标为 <code>[2]</code> ，只能选择这个值，结果为 <code>30</code> 。</li>
<li>对于 <code>i = 2</code> ：不存在满足 <code>nums1[j] &lt; nums1[2]</code> 的下标，结果为 <code>0</code> 。</li>
<li>对于 <code>i = 3</code> ：满足 <code>nums1[j] &lt; nums1[3]</code> 的下标为 <code>[0, 1, 2, 4]</code> ，选出其中值最大的两个，结果为 <code>50 + 30 = 80</code> 。</li>
<li>对于 <code>i = 4</code> ：满足 <code>nums1[j] &lt; nums1[4]</code> 的下标为 <code>[1, 2]</code> ，选出其中值最大的两个，结果为 <code>30 + 20 = 50</code> 。</li>
</ul>


### [示例 2]

**输入**: `nums1 = [2,2,2,2], nums2 = [3,1,2,3], k = 1`

**输出**: `[0,0,0,0]`

**解释**: 

<p>由于 <code>nums1</code> 中的所有元素相等，不存在满足条件 <code>nums1[j] &lt; nums1[i]</code>，所有位置的结果都是 <code>0</code> 。</p>


### [约束]

- `n == nums1.length == nums2.length`
- `1 <= n <= 10^5`
- `1 <= nums1[i], nums2[i] <= 10^6`
- `1 <= k <= n`

### [Hints]

<details>
  <summary>提示 1</summary>
  Sort `nums1` and its corresponding `nums2` values together based on `nums1`.

  
</details>

<details>
  <summary>提示 2</summary>
  Use a max heap to track the top `k` values of `nums2` as you process each element in the sorted order.

  
</details>

## 思路

- 要求1：找出所有满足 `nums1[j]` 小于 `nums1[i]` 的下标 `j` 。
    看到这个，大家一定会想到把 `nums1` 按从小到大排序，这样，前面的小于等于后面的，但一排序下标就**乱**了。如果对这个问题没有好办法解决，整个题目就做不出来。先请思考下。

    <details><summary>点击查看答案</summary><p>在排序时带上索引下标，即排序的对象是元组`(num, index)`的数组。这个技术**一定要掌握**，许多题目都会用到。</p></details>

    解决了上面的问题，下标就都有了，我们再看：

- 要求2：从这些下标对应的 `nums2[j]` 中选出 至多 `k` 个，并 **最大化** 这些值的总和作为结果。

    看到这个，你想到用什么好方法了吗？

    <details><summary>点击查看答案</summary><p>堆排序，维护一个大小为 `k` 的大根堆。这也是经常考察的知识点，**一定要掌握**哦。</p></details>

    看到这，请你先按上文提示把代码实现一下。

- 最后，发现还要对连续出现的重复的 `num` 进行特别处理，即相同的 `num` 对应的 `answer` 中的值应该是一样的。处理方法有多种，怎么处理最简单呢？

    <details><summary>点击查看答案</summary><p> 用一个 `Map`， `key`为 `num`, 相同的 `key` 直接使用 `key` 对应的`值`。</p></details>

## 复杂度

- 时间复杂度: `O(N * logN)`.
- 空间复杂度: `O(N)`.

## Python

```python
class Solution:
    def findMaxSum(self, nums1: List[int], nums2: List[int], k: int) -> List[int]:
        num_index_list = [(num, index) for index, num in enumerate(nums1)] # key 1
        num_index_list.sort()

        answer = [None] * len(nums1)
        k_max_nums = []
        sum_ = 0
        num_to_sum = defaultdict(int) # key 2

        for i, num_index in enumerate(num_index_list):
            num, index = num_index

            if num in num_to_sum:
                answer[index] = num_to_sum[num]
            else:
                answer[index] = sum_
                num_to_sum[num] = sum_

            heapq.heappush(k_max_nums, nums2[index])
            sum_ += nums2[index]

            if len(k_max_nums) > k:
                num = heapq.heappop(k_max_nums) # key 3
                sum_ -= num

        return answer
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

访问原文链接：[3478. 选出和最大的 K 个元素 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/3478-choose-k-elements-with-maximum-sum)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

