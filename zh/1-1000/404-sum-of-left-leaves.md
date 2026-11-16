# 404. 左叶子之和 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 coder.id 打造你的开发者个人IP →**](https://www.coder.id)

访问原文链接：[404. 左叶子之和 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/404-sum-of-left-leaves)，体验更佳！

力扣链接：[404. 左叶子之和](https://leetcode.cn/problems/sum-of-left-leaves), 难度等级：**简单**。

## LeetCode “404. 左叶子之和”问题描述

给定二叉树的根节点 `root` ，返回所有左叶子之和。

### [示例 1]

![](../../images/examples/404_1.jpg)

**输入**: `root = [3,9,20,null,null,15,7]`

**输出**: `24`

**解释**: `在这个二叉树中，有两个左叶子，分别是 9 和 15，所以返回 24`

### [示例 2]

**输入**: `root = [1]`

**输出**: `0`

### [约束]

- 节点数在 `[1, 1000]` 范围内
- `-1000 <= Node.val <= 1000`

## 思路



## 复杂度

- 时间复杂度: `O(n)`.
- 空间复杂度: `O(n)`.

## Python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
        self.result = 0
        self.traverse(root, False)
        return self.result

    def traverse(self, node, is_left):
        if node is None:
            return
        
        if is_left_leaf(node, is_left):
            self.result += node.val
            return
        
        self.traverse(node.left, True)
        self.traverse(node.right, False)
        

def is_left_leaf(node, is_left):
    return is_left and node.left is None and node.right is None
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**coder.id**](https://www.coder.id) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.coder.id`，极具职业含金量的专属域名。

>
> [**立即前往 coder.id 打造你的个人品牌 →**](https://www.coder.id)

---

访问原文链接：[404. 左叶子之和 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/404-sum-of-left-leaves)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

