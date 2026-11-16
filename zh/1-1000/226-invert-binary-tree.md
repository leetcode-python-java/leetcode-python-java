# 226. 翻转二叉树 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 coder.id 打造你的开发者个人IP →**](https://www.coder.id)

访问原文链接：[226. 翻转二叉树 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/226-invert-binary-tree)，体验更佳！

力扣链接：[226. 翻转二叉树](https://leetcode.cn/problems/invert-binary-tree), 难度等级：**简单**。

## LeetCode “226. 翻转二叉树”问题描述

给你一棵二叉树的根节点 `root` ，翻转这棵二叉树，并返回其根节点。

### [示例 1]

![](../../images/examples/226_1.jpg)

**输入**: `root = [4,2,7,1,3,6,9]`

**输出**: `[4,7,2,9,6,3,1]`

### [示例 2]

![](../../images/examples/226_2.jpg)

**输入**: `root = [2,1,3]`

**输出**: `[2,3,1]`

### [示例 3]

**输入**: `root = []`

**输出**: `[]`

### [约束]

- 树中节点数目范围在 `[0, 100]` 内
- `-100 <= Node.val <= 100`

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
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        node = root
        if node is None:
            return
        if node.left is None and node.right is None:
            return node
        
        # node.left, node.right = node.right, node.left # This is a quicker way in Python to swap.

        left = node.left
        node.left = node.right
        node.right = left

        self.invertTree(node.left)
        self.invertTree(node.right)

        return node
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

访问原文链接：[226. 翻转二叉树 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/226-invert-binary-tree)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

