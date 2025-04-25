# 203. 移除链表元素 - LeetCode Python/Java/C++ 题解

访问原文链接：[203. 移除链表元素 - LeetCode Python/Java/C++ 题解](https://leetcodepython.com/zh/leetcode/203-remove-linked-list-elements)，体验更佳！

力扣链接：[203. 移除链表元素](https://leetcode.cn/problems/remove-linked-list-elements), 难度等级：**简单**。

## LeetCode “203. 移除链表元素”问题描述

给你一个链表的头节点 `head` 和一个整数 `val` ，请你删除链表中所有满足 `Node.val == val` 的节点，并返回 **新的头节点** 。

### [示例 1]

![](../../images/examples/203_1.jpg)

**输入**: `head = [1,2,6,3,4,5,6], val = 6`

**输出**: `[1,2,3,4,5]`

### [示例 2]

**输入**: `head = [], val = 1`

**输出**: `[]`

### [示例 3]

**输入**: `head = [7,7,7,7], val = 7`

**输出**: `[]`

### [约束]

- 列表中的节点数目在范围 `[0, 10000]` 内
- `1 <= Node.val <= 50`
- `0 <= val <= 50`

## 思路

- 假设链表中待删除的节点是`d`，`d`的前一个节点是`p`，所以`p.next`就是`d`。 删除`d`，只需要把`p.next = p.next.next`。

- 因为用到了`p.next.next`，所以循环条件应为`while (p.next != null)`，而不是`while (p != null)`。

- 但`head`节点前面没有节点，这就意味着需要对`head`节点进行特殊处理。

	是否有方法能够让`head`节点的不再特殊呢？这样就不需要特殊处理`head`了。

	<details><summary>点击查看答案</summary><p>办法是引入`dummy`节点，`dummy.next = head`。</p></details>

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        var dummyHead = new ListNode();
        dummyHead.next = head;
        var node = dummyHead;

        while (node.next != null) {
            if (node.next.val == val) {
                node.next = node.next.next;
            } else {
                node = node.next;
            }
        }

        return dummyHead.next;
    }
}
```

## Python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        dummy_head = ListNode()
        dummy_head.next = head
        node = dummy_head

        while node.next:
            if node.next.val == val:
                node.next = node.next.next
            else:
                node = node.next

        return dummy_head.next
```

## C++

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        auto dummyHead = new ListNode();
        dummyHead->next = head;
        auto node = dummyHead;

        while (node->next != nullptr) {
            if (node->next->val == val) {
                auto next_node = node->next;
                node->next = node->next->next;
                delete next_node;
            } else {
                node = node->next;
            }
        }

        return dummyHead->next;
    }
};
```

## JavaScript

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
var removeElements = function (head, val) {
  const dummyHead = new ListNode()
  dummyHead.next = head
  let node = dummyHead

  while (node.next != null) {
    if (node.next.val == val) {
      node.next = node.next.next
    } else {
      node = node.next
    }
  }

  return dummyHead.next
};
```

## C#

```csharp
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public ListNode RemoveElements(ListNode head, int val) {
        var dummyHead = new ListNode();
        dummyHead.next = head;
        var node = dummyHead;

        while (node.next != null) {
            if (node.next.val == val) {
                node.next = node.next.next;
            } else {
                node = node.next;
            }
        }

        return dummyHead.next;
    }
}
```

## Go

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func removeElements(head *ListNode, val int) *ListNode {
    dummyHead := &ListNode{}
    dummyHead.Next = head
    node := dummyHead

    for node.Next != nil {
        if node.Next.Val == val {
            node.Next = node.Next.Next
        } else {
            node = node.Next
        }
    }

    return dummyHead.Next
}
```

## Ruby

```ruby
# Definition for singly-linked list.
# class ListNode
#     attr_accessor :val, :next
#     def initialize(val = 0, _next = nil)
#         @val = val
#         @next = _next
#     end
# end

def remove_elements(head, val)
  dummy_head = ListNode.new
  dummy_head.next = head
  node = dummy_head

  until node.next.nil?
    if node.next.val == val
      node.next = node.next.next
    else
      node = node.next
    end
  end

  dummy_head.next
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCodePython.com](https://leetcodepython.com/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[203. 移除链表元素 - LeetCode Python/Java/C++ 题解](https://leetcodepython.com/zh/leetcode/203-remove-linked-list-elements).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

