# 19. Remove Nth Node From End of List - LeetCode Solution
LeetCode problem link: [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list),
[19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list)

[中文题解](#中文题解)

## LeetCode problem description
Given the `head` of a linked list, remove the `n-th` node from the end of the list and return _its head_.

### [Example 1]
![](../../images/examples/19_1.jpg)

**Input**: `head = [1,2,3,4,5], n = 2`

**Output**: `[1,2,3,5]`

### [Example 2]
**Input**: `head = [1], n = 1`

**Output**: `[]`

### [Example 3]
**Input**: `head = [1,2], n = 1`

**Output**: `[1]`

### [Constraints]
- The number of nodes in the list is `sz`.
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

<details>
  <summary>Hint 1</summary>
  Maintain two pointers and update one with a delay of n steps.
</details>

## Intuition behind the Solution
[中文题解](#中文题解)

1. Deleting the `N-th` to last node in a linked list is equivalent to deleting the `node_count - N`-th node in the linked list.
2. First find out `node_count`.
3. When `index == node_count - N`, delete the node by `node.next = node.next.next`.
4. Since the deleted node may be `head`, a virtual node `dummy_node` is used to facilitate unified processing.

## Steps to the Solution
1. First find out `node_count`.
```ruby
node_count = 0
node = head

while node
  node_count += 1
  node = node.next
end
```

2. When `index == node_count - N`, delete the node by `node.next = node.next.next`.
```ruby
index = 0
node = head

while node
  if index == node_count - n
    node.next = node.next.next
    break
  end

  index += 1
  node = node.next
end
```

3. Since the deleted node may be `head`, a virtual node `dummy_node` is used to facilitate unified processing.
```ruby
dummy_head = ListNode.new # 1
dummy_head.next = head # 2
node = dummy_head # 3

# omitted code

return dummy_head.next
```

## Complexity
* Time: `O(n)`.
* Space: `O(1)`.

## Java
```java
/**
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        var nodeCount = 0;
        var node = head;

        while (node != null) {
            nodeCount++;
            node = node.next;
        }

        var index = 0;
        var dummyHead = new ListNode(0, head);
        node = dummyHead;

        while (node != null) {
            if (index == nodeCount - n) {
                node.next = node.next.next;
                break;
            }

            index++;
            node = node.next;
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
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        node_count = 0
        node = head

        while node:
            node_count += 1
            node = node.next

        index = 0
        dummy_head = ListNode(next=head)
        node = dummy_head

        while node:
            if index == node_count - n:
                node.next = node.next.next
                break

            index += 1
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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        auto node_count = 0;
        auto node = head;

        while (node != nullptr) {
            node_count += 1;
            node = node->next;
        }

        auto index = 0;
        auto dummy_head = new ListNode(0, head);
        node = dummy_head;

        for (auto i = 0; i < node_count - n; i++) {
            node = node->next;
        }

        auto target_node = node->next;
        node->next = node->next->next;
        delete target_node;

        auto result = dummy_head->next;
        delete dummy_head;
        return result;
    }
};
```

## JavaScript
```javascript
/**
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
var removeNthFromEnd = function (head, n) {
  let nodeCount = 0
  let node = head

  while (node != null) {
    nodeCount++
    node = node.next
  }

  let index = 0
  let dummyHead = new ListNode(0, head)
  node = dummyHead

  while (node != null) {
    if (index == nodeCount - n) {
        node.next = node.next.next
        break
    }

    index++
    node = node.next
  }

  return dummyHead.next
};
```

## C#
```c#
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
public class Solution
{
    public ListNode RemoveNthFromEnd(ListNode head, int n)
    {
        int nodeCount = 0;
        var node = head;

        while (node != null)
        {
            nodeCount++;
            node = node.next;
        }

        int index = 0;
        var dummyHead = new ListNode(0, head);
        node = dummyHead;

        while (node != null)
        {
            if (index == nodeCount - n)
            {
                node.next = node.next.next;
                break;
            }

            index++;
            node = node.next;
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
func removeNthFromEnd(head *ListNode, n int) *ListNode {
    nodeCount := 0
    node := head

    for node != nil {
        nodeCount++
        node = node.Next
    }

    index := 0
    dummyHead := &ListNode{0, head}
    node = dummyHead

    for node != nil {
        if index == nodeCount - n {
            node.Next = node.Next.Next
            break
        }

        index++
        node = node.Next
    }

    return dummyHead.Next
}
```

## Ruby
```ruby
# class ListNode
#     attr_accessor :val, :next
# 
#     def initialize(val = 0, _next = nil)
#         @val = val
#         @next = _next
#     end
# end

def remove_nth_from_end(head, n)
  node_count = 0
  node = head

  while node
    node_count += 1
    node = node.next
  end

  index = 0
  dummy_head = ListNode.new(0, head)
  node = dummy_head

  while node
    if index == node_count - n
      node.next = node.next.next
      break
    end

    index += 1
    node = node.next
  end

  dummy_head.next
end
```

## C
```c
// Welcome to create a PR to complete the code of this language, thanks!
```

## Kotlin
```kotlin
// Welcome to create a PR to complete the code of this language, thanks!
```

## Swift
```swift
// Welcome to create a PR to complete the code of this language, thanks!
```

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```

## 问题描述
给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

### [Example 1]
![](../../images/examples/19_1.jpg)

**输入**: `head = [1,2,3,4,5], n = 2`

**输出**: `[1,2,3,5]`

# 中文题解
## 思路
1. 删除链表的倒数第 `N` 个结点，等同于删除链表的第 `node_count - N` 个结点。
2. 先求出`node_count`。
3. 在 `index == node_count - N`时，进行删除节点操作：`node.next = node.next.next`。
4. 由于删除的节点可能是`head`，所以使用虚拟节点`dummy_node`，方便统一处理。

## 步骤
1. 求出`node_count`。
```ruby
node_count = 0
node = head

while node
  node_count += 1
  node = node.next
end
```

2. 在 `index == node_count - N`时，进行删除节点操作：`node.next = node.next.next`。
```ruby
index = 0
node = head

while node
  if index == node_count - n
    node.next = node.next.next
    break
  end

  index += 1
  node = node.next
end
```

3. 由于删除的节点可能是`head`，所以使用虚拟节点`dummy_node`，方便统一处理。
```ruby
dummy_head = ListNode.new # 1
dummy_head.next = head # 2
node = dummy_head # 3

# omitted code

return dummy_head.next
```
