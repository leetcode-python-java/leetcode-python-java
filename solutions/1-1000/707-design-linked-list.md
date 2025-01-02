# 707. Design Linked List - LeetCode Solution
LeetCode problem link: [707. Design Linked List](https://leetcode.com/problems/design-linked-list),
[707. 设计链表](https://leetcode.cn/problems/design-linked-list)

[中文题解](#中文题解)

## LeetCode problem description
Design your implementation of the linked list. You can choose to use a singly or doubly linked list.

A node in a singly linked list should have two attributes: `val` and `next`. `val` is the value of the current node, and `next` is a pointer/reference to the next node.

If you want to use the doubly linked list, you will need one more attribute `prev` to indicate the previous node in the linked list. Assume all nodes in the linked list are **0-indexed**.


Implement the `MyLinkedList` class:

* `MyLinkedList()` Initializes the `MyLinkedList` object.
* `int get(int index)` Get the value of the `index-th` node in the linked list. If the index is invalid, return `-1`.
* `void addAtHead(int val)` Add a node of value `val` before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
* `void addAtTail(int val)` Append a node of value `val` as the last element of the linked list.
* `void addAtIndex(int index, int val)` Add a node of value `val` before the `index-th` node in the linked list. If `index` equals the length of the linked list, the node will be appended to the end of the linked list. If `index` is greater than the length, the node will **not be inserted**.
* `void deleteAtIndex(int index)` Delete the `index-th` node in the linked list, if the index is valid.

### [Example 1]
**Input**
```ruby
["MyLinkedList", "addAtHead", "addAtTail", "addAtIndex", "get", "deleteAtIndex", "get"]
[[], [1], [3], [1, 2], [1], [1], [1]]
```

**Output**
```ruby
[null, null, null, null, 2, null, 3]
```

**Explanation**
```java
MyLinkedList myLinkedList = new MyLinkedList();
myLinkedList.addAtHead(1);
myLinkedList.addAtTail(3);
myLinkedList.addAtIndex(1, 2);    // linked list becomes 1->2->3
myLinkedList.get(1);              // return 2
myLinkedList.deleteAtIndex(1);    // now the linked list is 1->3
myLinkedList.get(1);              // return 3
```

### [Constraints]
- `0 <= index, val <= 1000`
- Please do not use the built-in LinkedList library.
- At most `2000` calls will be made to `get`, `addAtHead`, `addAtTail`, `addAtIndex` and `deleteAtIndex`.

## Intuition behind the Solution
Before solving this problem, it is recommended to solve the simple problem [19. Remove Nth Node From End of List](./19-remove-nth-node-from-end-of-list.md) first.

This question can comprehensively test the candidate's mastery of linked lists. The following points need to be paid attention to:

1. It is best to use a `dummyHead` node as the entry of the linked list.
2. It is best to use a new `ListNode` class, so that `dummyHead` does not need to be mixed with `val` and `next`.
3. Implement the easy methods first, in the order of `addAtHead`, `addAtTail`, `addAtIndex`, `deleteAtIndex`, `get`.

## Complexity
* Time: `O(n * n)`.
* Space: `O(n)`.

## Java
```java
class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
    }
}

class MyLinkedList {
    private ListNode dummyHead = new ListNode(0);

    public MyLinkedList() {}

    public int get(int index) {
        var node = dummyHead.next;
        var i = 0;

        while (node != null && i < index) {
            node = node.next;
            i += 1;
        }

        if (i == index && node != null) {
            return node.val;
        }

        return -1;
    }
    
    public void addAtHead(int val) {
        var node = new ListNode(val);
        node.next = dummyHead.next;
        dummyHead.next = node;
    }
    
    public void addAtTail(int val) {
        var node = dummyHead;

        while (node.next != null) {
            node = node.next;
        }

        node.next = new ListNode(val);
    }
    
    public void addAtIndex(int index, int val) {
        var node = dummyHead;
        var i = 0;

        while (node.next != null && i < index) {
            node = node.next;
            i += 1;
        }

        if (i == index) {
            var newNode = new ListNode(val);
            newNode.next = node.next;
            node.next = newNode;
        }
    }
    
    public void deleteAtIndex(int index) {
        var node = dummyHead;
        var i = 0;

        while (node.next != null && i < index) {
            node = node.next;
            i += 1;
        }

        if (i == index && node.next != null) {
            node.next = node.next.next;
        }
    }
}
```

## Python
```python
class ListNode:
    def __init__(self, val=None):
        self.val = val
        self.next = None


class MyLinkedList:
    def __init__(self):
        self.dummy_head = ListNode()

    def get(self, index: int) -> int:
        node = self.dummy_head.next
        i = 0

        while node and i < index:
            node = node.next
            i += 1

        if i == index and node:
            return node.val

        return -1

    def addAtHead(self, val: int) -> None:
        node = ListNode(val)
        node.next = self.dummy_head.next
        self.dummy_head.next = node

    def addAtTail(self, val: int) -> None:
        node = self.dummy_head

        while node.next:
            node = node.next

        node.next = ListNode(val)

    def addAtIndex(self, index: int, val: int) -> None:
        node = self.dummy_head
        i = 0

        while node.next and i < index:
            node = node.next
            i += 1

        if i == index:
            new_node = ListNode(val)
            new_node.next = node.next
            node.next = new_node
        
    def deleteAtIndex(self, index: int) -> None:
        node = self.dummy_head
        i = 0

        while node.next and i < index:
            node = node.next
            i += 1

        if i == index and node.next:
            node.next = node.next.next
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
class ListNode {
  constructor(val) {
    this.val = val
    this.next = null
  }
}

var MyLinkedList = function () {
  this.dummyHead = new ListNode(0)
};

MyLinkedList.prototype.get = function (index) {
  let node = this.dummyHead.next
  let i = 0

  while (node != null && i < index) {
    node = node.next
    i += 1
  }

  if (i == index && node != null) {
    return node.val
  }

  return -1
};

MyLinkedList.prototype.addAtHead = function (val) {
  const node = new ListNode(val)
  node.next = this.dummyHead.next
  this.dummyHead.next = node
};

MyLinkedList.prototype.addAtTail = function (val) {
  let node = this.dummyHead

  while (node.next != null) {
    node = node.next
  }

  node.next = new ListNode(val)
};

MyLinkedList.prototype.addAtIndex = function (index, val) {
  let node = this.dummyHead
  let i = 0

  while (node.next != null && i < index) {
    node = node.next
    i += 1
  }

  if (i == index) {
    const newNode = new ListNode(val);
    newNode.next = node.next;
    node.next = newNode;
  }
};

MyLinkedList.prototype.deleteAtIndex = function (index) {
  let node = this.dummyHead
  let i = 0

  while (node.next != null && i < index) {
    node = node.next
    i += 1
  }

  if (i == index && node.next != null) {
    node.next = node.next.next
  }
};
```

## C#
```c#
public class ListNode
{
    public int val;
    public ListNode next;

    public ListNode(int val)
    {
        this.val = val;
    }
}

public class MyLinkedList
{
    ListNode dummyHead = new ListNode(0);

    public MyLinkedList() {}
    
    public int Get(int index)
    {
        var node = dummyHead.next;
        int i = 0;

        while (node != null && i < index)
        {
            node = node.next;
            i += 1;
        }

        if (i == index && node != null)
            return node.val;

        return -1;
    }
    
    public void AddAtHead(int val)
    {
        var node = new ListNode(val);
        node.next = dummyHead.next;
        dummyHead.next = node;
    }
    
    public void AddAtTail(int val)
    {
        var node = dummyHead;

        while (node.next != null)
            node = node.next;

        node.next = new ListNode(val);
    }
    
    public void AddAtIndex(int index, int val)
    {
        var node = dummyHead;
        int i = 0;

        while (node.next != null && i < index)
        {
            node = node.next;
            i += 1;
        }

        if (i == index) {
            var newNode = new ListNode(val);
            newNode.next = node.next;
            node.next = newNode;
        }
    }
    
    public void DeleteAtIndex(int index) 
    {
        var node = dummyHead;
        int i = 0;

        while (node.next != null && i < index)
        {
            node = node.next;
            i += 1;
        }

        if (i == index && node.next != null)
            node.next = node.next.next;
    }
}
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
在做本题前，建议先完成较简单的相关题目 [19. 删除链表的倒数第 N 个结点](./19-remove-nth-node-from-end-of-list.md)。

本题可以全面考察候选人对链表的掌握程度，以下几点需要重视：

1. 最好使用一个`dummyHead`节点做为链表入口。
2. 最好使用一个新的`ListNode`类，这样，`dummyHead`就不用和`val`、`next`混在一起。
3. 先实现容易的方法，顺序为`addAtHead`, `addAtTail`, `addAtIndex`, `deleteAtIndex`, `get`。
