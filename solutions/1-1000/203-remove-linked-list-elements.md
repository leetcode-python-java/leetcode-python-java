# 203. Remove Linked List Elements - LeetCode Solution
LeetCode problem link: [203. Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements), [203. 移除链表元素](https://leetcode.cn/problems/remove-linked-list-elements)

[中文题解](#中文题解)

## LeetCode problem description
Given the `head` of a linked list and an integer `val`, remove all the nodes of the linked list that has `Node.val == val`, and return _the new head_.

### [Example 1]
![](../../images/examples/203_1.jpg)

**Input**: `head = [1,2,6,3,4,5,6], val = 6`

**Output**: `[1,2,3,4,5]`

### [Example 2]
**Input**: `head = [], val = 1`

**Output**: `[]`

### [Example 3]
**Input**: `head = [7,7,7,7], val = 7`

**Output**: `[]`

### [Constraints]
- The number of nodes in the list is in the range `[0, 10000]`.
- `1 <= Node.val <= 50`
- `0 <= val <= 50`

## Intuition behind the Solution
[中文题解](#中文题解)

Assume that the node to be deleted in the linked list is `d`, and the previous node of `d` is `p`, so `p.next` is `d`.

To delete `d`, just set `p.next = p.next.next`.

But there is no node before the `head` node, which means that the `head` node needs to be treated specially.

Is there a way to make the `head` node no longer special? In this way, there is no need to treat the `head` specially.

The way is to introduce a `dummy` node, `dummy.next = head`.

## Complexity
* Time: `O(n)`.
* Space: `O(1)`.

## Java
```java
// Solution is from Coding5DotCom
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
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
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

## 中文题解
假设链表中待删除的节点是`d`，`d`的前一个节点是`p`，所以`p.next`就是`d`。 删除`d`，只需要把`p.next = p.next.next`。

但`head`节点前面没有节点，这就意味着需要对`head`节点进行特殊处理。

是否有方法能够让`head`节点的不再特殊呢？这样就不需要特殊处理`head`了。

办法是引入`dummy`节点，`dummy.next = head`。
