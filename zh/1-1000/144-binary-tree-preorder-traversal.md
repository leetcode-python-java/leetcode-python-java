# 144. 二叉树的前序遍历 - 力扣题解最佳实践
力扣链接：[144. 二叉树的前序遍历](https://leetcode.cn/problems/binary-tree-preorder-traversal) ，难度：**容易**。

## 力扣“144. 二叉树的前序遍历”问题描述
给你二叉树的根节点 `root` ，返回它节点值的 **前序** 遍历。

### [示例 1]

**输入**: `root = [1,null,2,3]`

**输出**: `[1,2,3]`

**解释**:

![](../../images/examples/144_1.png)

### [示例 2]

**输入**: `root = [1,2,3,4,5,null,8,null,null,6,7,9]`

**输出**: `[1,2,4,5,6,7,3,8,9]`

**解释**:

![](../../images/examples/144_2.png)

### [示例 3]

**输入**: `root = []`

**输出**: `[]`

### [示例 4]

**输入**: `root = [1]`

**输出**: `[1]`

### [约束]
- 树中节点数目在范围 `[0, 100]` 内
- `-100 <= Node.val <= 100`

## 思路
以后会被添加。

## 步骤
以后会被添加。

## 复杂度
* 时间：`O(N)`。
* 空间：`O(N)`。

## 进阶
递归算法很简单，你可以通过迭代算法完成吗？

## 进阶思路
以后会被添加。

## Python
### Solution 1: Recursion
```python
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        self.values = []

        self.traverse(root)

        return self.values

    def traverse(self, node):
        if node is None:
            return

        self.values.append(node.val)

        self.traverse(node.left)

        self.traverse(node.right)
```

### Solution 2: Iteration
```python
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        values = []
        stack = []

        if root:
            stack.append(root)

        while stack:
            node = stack.pop()
            values.append(node.val)

            if node.right:
                stack.append(node.right)

            if node.left:
                stack.append(node.left)

        return values
```

## JavaScript
```javascript
// Welcome to create a PR to complete the code of this language, thanks!
```

## Java
```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## C#
```c#
// Welcome to create a PR to complete the code of this language, thanks!
```

## Go
```go
// Welcome to create a PR to complete the code of this language, thanks!
```

## Ruby
```ruby
# Welcome to create a PR to complete the code of this language, thanks!
```

## C, Kotlin, Swift, Rust or other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
