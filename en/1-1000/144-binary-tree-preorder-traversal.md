# 144. Binary Tree Preorder Traversal - Best Practices of LeetCode Solutions
LeetCode link: [144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal), difficulty: **Easy**.

## LeetCode description of "144. Binary Tree Preorder Traversal"
Given the `root` of a binary tree, return _the preorder traversal of its nodes' values_.

### [Example 1]

**Input**: `root = [1,null,2,3]`

**Output**: `[1,2,3]`

**Explanation**:

![](../../images/examples/144_1.png)

### [Example 2]

**Input**: `root = [1,2,3,4,5,null,8,null,null,6,7,9]`

**Output**: `[1,2,4,5,6,7,3,8,9]`

**Explanation**:

![](../../images/examples/144_2.png)

### [Example 3]

**Input**: `root = []`

**Output**: `[]`

### [Example 4]

**Input**: `root = [1]`

**Output**: `[1]`

### [Constraints]
- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

## Intuition
Will be added later.

## Steps
Will be added later.

## Complexity
Recursive solution and iterative solution are equal in complexity.

* Time: `O(N)`.
* Space: `O(N)`.

## Follow-up
Recursive solution is trivial, could you do it iteratively?

## Follow-up intuition
Will be added later.

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
