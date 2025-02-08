# 337. House Robber III
LeetCode link: [337. House Robber III](https://leetcode.com/problems/house-robber-iii/)

## LeetCode problem description
The thief has found himself a new place for his thievery again. There is only one entrance to this area, called `root`.

Besides the `root`, each house has one and only one parent house. After a tour, the smart thief realized that all houses in this place form a binary tree. **It will automatically contact the police if two directly-linked houses were broken into on the same night**.

Given the `root` of the binary tree, return the **maximum amount of money** the thief can rob **without alerting the police**.
```
------------------------------------------------------------------------
[Example 1]

Input: root = [3,2,3,null,3,null,1]
Output: 7
Explanation: Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
------------------------------------------------------------------------
[Example 2]

Input: root = [3,4,5,1,3,null,1]
Output: 9
Explanation: Maximum amount of money the thief can rob = 4 + 5 = 9.
------------------------------------------------------------------------
[Constraints]

The number of nodes in the tree is in the range [1, 10000].
0 <= Node.val <= 10000
------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Dynamic programming**.

Detailed solutions will be given later, and now only the best practices in 3-7 languages are given.

### Complexity
* Time: `O(n)`.
* Space: `O(n)`.

## Python
### Solution 1: Easier to understand
```python
class Solution:
    def __init__(self):
        self.node_to_money = defaultdict(int)

    # Uncomment the next line, you can solve it without using `self.node_to_money` dict.
    # @cache
    def rob(self, node: Optional[TreeNode]) -> int:
        if node is None:
            return 0

        if node in self.node_to_money:
            return self.node_to_money[node]

        money_exclude_node = self.rob(node.left) + self.rob(node.right)

        money_include_node = node.val
        if node.left:
            money_include_node += self.rob(node.left.left) + self.rob(node.left.right)
        if node.right:
            money_include_node += self.rob(node.right.left) + self.rob(node.right.right)

        self.node_to_money[node] = max(money_exclude_node, money_include_node)

        return self.node_to_money[node]
```

### Solution 2: Most concise
```python
class Solution:
    def rob(self, root: Optional[TreeNode]) -> int:
        return max(self.rob_tree(root))

    def rob_tree(self, node):
        if node is None:
            return 0, 0

        left_pair = self.rob_tree(node.left)
        right_pair = self.rob_tree(node.right)

        return max(left_pair) + max(right_pair), node.val + left_pair[0] + right_pair[0]
```

### Solution 3:
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def rob(self, root: Optional[TreeNode]) -> int:
        return self.robbing(root)[0]

    def robbing(self, node):
        if not node:
            return 0, 0

        left = self.robbing(node.left)

        right = self.robbing(node.right)

        return max(node.val + left[1] + right[1], left[0] + right[0]), left[0] + right[0]
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## Java
```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## C#
```c#
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
### Solution 1: Easier to understand
```javascript
const nodeToMoney = new Map()

var rob = function (root) {
  nodeToMoney.clear()

  return robTree(root)
};


function robTree(node) {
  if (node == null) {
    return 0
  }

  if (nodeToMoney.has(node)) {
    return nodeToMoney.get(node)
  }

  const moneyExcludeNode = robTree(node.left) + robTree(node.right)

  let moneyIncludeNode = node.val
  if (node.left) {
    moneyIncludeNode += robTree(node.left.left) + robTree(node.left.right)
  }
  if (node.right) {
    moneyIncludeNode += robTree(node.right.left) + robTree(node.right.right)
  }

  nodeToMoney.set(node, Math.max(moneyExcludeNode, moneyIncludeNode))

  return nodeToMoney.get(node)
}
```

### Solution 2: Most concise
```javascript
var rob = function (root) {
  return Math.max(...robTree(root))
};

function robTree(node) {
  if (node == null) {
    return [0, 0]
  }

  const leftPair = robTree(node.left)
  const rightPair = robTree(node.right)

  return [
    Math.max(...leftPair) + Math.max(...rightPair),
    node.val + leftPair[0] + rightPair[0]
  ]
}
```

## Go
### Solution 1: Easier to understand
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func rob(root *TreeNode) int {
    nodeToMoney := map[*TreeNode]int{}

    var robTree func (*TreeNode) int

    robTree = func (node *TreeNode) int {
        if node == nil {
            return 0
        }

        if money, ok := nodeToMoney[node]; ok {
            return money
        }

        moneyExcludeNode := robTree(node.Left) + robTree(node.Right)

        moneyIncludeNode := node.Val
        if node.Left != nil {
            moneyIncludeNode += robTree(node.Left.Left) + robTree(node.Left.Right)
        }
        if node.Right != nil {
            moneyIncludeNode += robTree(node.Right.Left) + robTree(node.Right.Right)
        }

        nodeToMoney[node] = max(moneyExcludeNode, moneyIncludeNode)

        return nodeToMoney[node]
    }

    return robTree(root)
}
```

### Solution 2: Most concise
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func rob(root *TreeNode) int {
    return slices.Max(robTree(root))
}

func robTree(node *TreeNode) []int {
    if node == nil {
        return []int{0, 0}
    }

    leftPair := robTree(node.Left)
    rightPair := robTree(node.Right)

    return []int{
        slices.Max(leftPair) + slices.Max(rightPair),
        node.Val + leftPair[0] + rightPair[0],
    }
}
```

## Ruby
```ruby
# Welcome to create a PR to complete the code of this language, thanks!
```

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
