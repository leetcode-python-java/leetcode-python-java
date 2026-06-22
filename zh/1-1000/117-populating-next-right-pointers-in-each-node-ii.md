# 117. 填充每个节点的下一个右侧节点指针 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[117. 填充每个节点的下一个右侧节点指针 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/117-populating-next-right-pointers-in-each-node-ii)，体验更佳！

力扣链接：[117. 填充每个节点的下一个右侧节点指针 II](https://leetcode.cn/problems/populating-next-right-pointers-in-each-node-ii), 难度等级：**中等**。

## LeetCode “117. 填充每个节点的下一个右侧节点指针 II”问题描述

给定一个二叉树：

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 `NULL` 。

初始状态下，所有 next 指针都被设置为 `NULL` 。

### [示例 1]

![](../../images/examples/117_1.png)

**输入**: `root = [1,2,3,4,5,null,7]`

**输出**: `[1,#,2,3,#,4,5,7,#]`

**解释**: 

<p>给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点，如图 B 所示。序列化输出按层序遍历顺序（由 next 指针连接），&#39;#&#39; 表示每层的末尾。</p>


### [示例 2]

**输入**: `root = []`

**输出**: `[]`

### [约束]

* 树中的节点数在范围 `[0, 6000]` 内
* `-100 <= Node.val <= 100`

## 思路

我们需要连接同一层的节点。使用队列的标准广度优先搜索（BFS）需要 O(N) 的空间。然而，题目要求 O(1) 的额外空间。注意到一旦某一层的 `next` 指针被完全连接，它就形成了一个链表。我们可以将当前层作为链表进行遍历，找到所有子节点并将它们连接起来，形成下一层的链表。通过为下一层使用一个哑节点（dummy node），我们可以很容易地跟踪下一层的起始位置。

## 步骤

1. 初始化一个指针 `head` 指向树的 `root`。这代表当前层的起始节点。
2. 当 `head` 不为空时进行循环：
   - 创建一个 `dummy` 节点，作为下一层链表的头节点。
   - 使用一个 `tail` 指针（初始指向 `dummy`）来追加子节点。
   - 使用 `next` 指针遍历当前层：
     - 如果 `head.left` 存在，将其追加到 `tail.next`，并将 `tail` 向前移动。
     - 如果 `head.right` 存在，将其追加到 `tail.next`，并将 `tail` 向前移动。
     - 将 `head` 移动到当前层的 `next` 节点。
   - 将 `head` 移动到 `dummy.next`，即新构建的下一层的起始位置。
3. 返回原始的 `root`。

## 复杂度

> - **时间复杂度**: `O(N)`。我们精确地访问了二叉树中的每个节点一次。
- **空间复杂度**: `O(1)`。我们在层序遍历中只使用了几个额外的指针（`head`、`dummy`、`tail`），避免了使用队列带来的 `O(N)` 空间开销。由于这是迭代方法，因此也没有使用隐式栈空间。

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Python

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val: int = 0, left: 'Node' = None, right: 'Node' = None, next: 'Node' = None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""

class Solution:
    def connect(self, root: 'Node') -> 'Node':
        # Start with the root node as the head of the current level
        head = root
        
        while head:
            # Create a dummy node to act as the head of the next level's linked list
            dummy = Node(0)
            # Tail pointer to append children to the next level
            tail = dummy
            
            # Traverse the current level
            while head:
                # If there is a left child, append it to the next level's list
                if head.left:
                    tail.next = head.left
                    tail = tail.next
                
                # If there is a right child, append it to the next level's list
                if head.right:
                    tail.next = head.right
                    tail = tail.next
                
                # Move to the next node in the current level
                head = head.next
            
            # Move down to the next level
            head = dummy.next
            
        return root
```

## Java

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node next;

    public Node() {}
    
    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _left, Node _right, Node _next) {
        val = _val;
        left = _left;
        right = _right;
        next = _next;
    }
};
*/

class Solution {
    public Node connect(Node root) {
        // Start with the root node as the head of the current level
        Node head = root;
        
        while (head != null) {
            // Dummy node to track the start of the next level
            Node dummy = new Node(0);
            // Tail pointer to append nodes to the next level
            Node tail = dummy;
            
            // Traverse the current level
            while (head != null) {
                // If the left child exists, link it
                if (head.left != null) {
                    tail.next = head.left;
                    tail = tail.next;
                }
                
                // If the right child exists, link it
                if (head.right != null) {
                    tail.next = head.right;
                    tail = tail.next;
                }
                
                // Move to the next node in the current level
                head = head.next;
            }
            
            // Move to the next level (the first node after dummy)
            head = dummy.next;
        }
        
        return root;
    }
}
```

## JavaScript

```javascript
/**
 * // Definition for a _Node.
 * function _Node(val, left, right, next) {
 *    this.val = val === undefined ? null : val;
 *    this.left = left === undefined ? null : left;
 *    this.right = right === undefined ? null : right;
 *    this.next = next === undefined ? null : next;
 * };
 */

/**
 * @param {_Node} root
 * @return {_Node}
 */
var connect = function(root) {
    // Start with the root node as the head of the current level
    let head = root;
    
    while (head !== null) {
        // Dummy node to track the start of the next level
        let dummy = new _Node(0);
        // Tail pointer to append nodes to the next level
        let tail = dummy;
        
        // Traverse the current level
        while (head !== null) {
            // If the left child exists, link it
            if (head.left !== null) {
                tail.next = head.left;
                tail = tail.next;
            }
            
            // If the right child exists, link it
            if (head.right !== null) {
                tail.next = head.right;
                tail = tail.next;
            }
            
            // Move to the next node in the current level
            head = head.next;
        }
        
        // Move to the next level (the first node after dummy)
        head = dummy.next;
    }
    
    return root;
};
```

## Cpp

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/

class Solution {
public:
    Node* connect(Node* root) {
        // Start with the root node as the head of the current level
        Node* head = root;
        
        while (head != nullptr) {
            // Dummy node to track the start of the next level
            Node* dummy = new Node(0);
            // Tail pointer to append nodes to the next level
            Node* tail = dummy;
            
            // Traverse the current level
            while (head != nullptr) {
                // If the left child exists, link it
                if (head->left != nullptr) {
                    tail->next = head->left;
                    tail = tail->next;
                }
                
                // If the right child exists, link it
                if (head->right != nullptr) {
                    tail->next = head->right;
                    tail = tail->next;
                }
                
                // Move to the next node in the current level
                head = head->next;
            }
            
            // Move to the next level (the first node after dummy)
            head = dummy->next;
            // Prevent memory leak
            delete dummy;
        }
        
        return root;
    }
};
```

## Csharp

```csharp
/*
// Definition for a Node.
public class Node {
    public int val;
    public Node left;
    public Node right;
    public Node next;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _left, Node _right, Node _next) {
        val = _val;
        left = _left;
        right = _right;
        next = _next;
    }
}
*/

public class Solution {
    public Node Connect(Node root) {
        // Start with the root node as the head of the current level
        Node head = root;
        
        while (head != null) {
            // Dummy node to track the start of the next level
            Node dummy = new Node();
            // Tail pointer to append nodes to the next level
            Node tail = dummy;
            
            // Traverse the current level
            while (head != null) {
                // If the left child exists, link it
                if (head.left != null) {
                    tail.next = head.left;
                    tail = tail.next;
                }
                
                // If the right child exists, link it
                if (head.right != null) {
                    tail.next = head.right;
                    tail = tail.next;
                }
                
                // Move to the next node in the current level
                head = head.next;
            }
            
            // Move to the next level (the first node after dummy)
            head = dummy.next;
        }
        
        return root;
    }
}
```

## Go

```go
/**
 * Definition for a Node.
 * type Node struct {
 *     Val int
 *     Left *Node
 *     Right *Node
 *     Next *Node
 * }
 */

func connect(root *Node) *Node {
    // Start with the root node as the head of the current level
    head := root
    
    for head != nil {
        // Dummy node to track the start of the next level
        dummy := &Node{}
        // Tail pointer to append nodes to the next level
        tail := dummy
        
        // Traverse the current level
        for head != nil {
            // If the left child exists, link it
            if head.Left != nil {
                tail.Next = head.Left
                tail = tail.Next
            }
            
            // If the right child exists, link it
            if head.Right != nil {
                tail.Next = head.Right
                tail = tail.Next
            }
            
            // Move to the next node in the current level
            head = head.Next
        }
        
        // Move to the next level (the first node after dummy)
        head = dummy.Next
    }
    
    return root
}
```

## Ruby

```ruby
# Definition for Node.
# class Node
#     attr_accessor :val, :left, :right, :next
#     def initialize(val)
#         @val = val
#         @left, @right, @next = nil, nil, nil
#     end
# end

# @param {Node} root
# @return {Node}
def connect(root)
    # Start with the root node as the head of the current level
    head = root
    
    while head
        # Dummy node to track the start of the next level
        dummy = Node.new(0)
        # Tail pointer to append nodes to the next level
        tail = dummy
        
        # Traverse the current level
        while head
            # If the left child exists, link it
            if head.left
                tail.next = head.left
                tail = tail.next
            end
            
            # If the right child exists, link it
            if head.right
                tail.next = head.right
                tail = tail.next
            end
            
            # Move to the next node in the current level
            head = head.next
        end
        
        # Move to the next level (the first node after dummy)
        head = dummy.next
    end
    
    root
end
```

## Rust

```rust
// Note: LeetCode does not officially support Rust for TreeLinkNode problems with mutable 'next' pointers easily.
// This is a conceptual implementation using typical interior mutability patterns in Rust.
use std::rc::Rc;
use std::cell::RefCell;

// Definition for a Node.
#[derive(Debug, PartialEq, Eq)]
pub struct Node {
    pub val: i32,
    pub left: Option<Rc<RefCell<Node>>>,
    pub right: Option<Rc<RefCell<Node>>>,
    pub next: Option<Rc<RefCell<Node>>>,
}

impl Node {
    #[inline]
    pub fn new(val: i32) -> Self {
        Node {
            val,
            left: None,
            right: None,
            next: None,
        }
    }
}

pub struct Solution;

impl Solution {
    pub fn connect(root: Option<Rc<RefCell<Node>>>) -> Option<Rc<RefCell<Node>>> {
        if root.is_none() {
            return None;
        }

        // Start with the root node as the head of the current level
        let mut head = root.clone();

        while let Some(current_head) = head {
            // Dummy node to track the start of the next level
            let dummy = Rc::new(RefCell::new(Node::new(0)));
            let mut tail = dummy.clone();
            
            let mut current = Some(current_head);

            // Traverse the current level
            while let Some(node_rc) = current {
                let node = node_rc.borrow();

                // If the left child exists, link it
                if let Some(left) = node.left.clone() {
                    tail.borrow_mut().next = Some(left.clone());
                    tail = left;
                }

                // If the right child exists, link it
                if let Some(right) = node.right.clone() {
                    tail.borrow_mut().next = Some(right.clone());
                    tail = right;
                }

                // Move to the next node in the current level
                current = node.next.clone();
            }

            // Move to the next level (the first node after dummy)
            head = dummy.borrow().next.clone();
        }

        root
    }
}
```

## Kotlin

```kotlin
/**
 * Definition for a Node.
 * class Node(var `val`: Int) {
 *     var left: Node? = null
 *     var right: Node? = null
 *     var next: Node? = null
 * }
 */

class Solution {
    fun connect(root: Node?): Node? {
        // Start with the root node as the head of the current level
        var head = root
        
        while (head != null) {
            // Dummy node to track the start of the next level
            val dummy = Node(0)
            // Tail pointer to append nodes to the next level
            var tail: Node? = dummy
            
            // Traverse the current level
            while (head != null) {
                // If the left child exists, link it
                if (head.left != null) {
                    tail?.next = head.left
                    tail = tail?.next
                }
                
                // If the right child exists, link it
                if (head.right != null) {
                    tail?.next = head.right
                    tail = tail?.next
                }
                
                // Move to the next node in the current level
                head = head.next
            }
            
            // Move to the next level (the first node after dummy)
            head = dummy.next
        }
        
        return root
    }
}
```

## Swift

```swift
/**
 * Definition for a Node.
 * public class Node {
 *     public var val: Int
 *     public var left: Node?
 *     public var right: Node?
 *     public var next: Node?
 *     public init(_ val: Int) {
 *         self.val = val
 *         self.left = nil
 *         self.right = nil
 *         self.next = nil
 *     }
 * }
 */

class Solution {
    func connect(_ root: Node?) -> Node? {
        // Start with the root node as the head of the current level
        var head = root
        
        while head != nil {
            // Dummy node to track the start of the next level
            let dummy = Node(0)
            // Tail pointer to append nodes to the next level
            var tail: Node? = dummy
            
            // Traverse the current level
            while head != nil {
                // If the left child exists, link it
                if let left = head?.left {
                    tail?.next = left
                    tail = tail?.next
                }
                
                // If the right child exists, link it
                if let right = head?.right {
                    tail?.next = right
                    tail = tail?.next
                }
                
                // Move to the next node in the current level
                head = head?.next
            }
            
            // Move to the next level (the first node after dummy)
            head = dummy.next
        }
        
        return root
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

访问原文链接：[117. 填充每个节点的下一个右侧节点指针 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/117-populating-next-right-pointers-in-each-node-ii)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

