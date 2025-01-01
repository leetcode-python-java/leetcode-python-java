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

## Steps to the Solution


## Complexity
* Time: `O()`.
* Space: `O()`.

## Java
```java
class LinkedNode {
    int val;
    LinkedNode next;

    LinkedNode(int val) {
        this.val = val;
    }
}

class MyLinkedList {
    private LinkedNode dummyHead = new LinkedNode(0);

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
        var node = new LinkedNode(val);
        node.next = dummyHead.next;
        dummyHead.next = node;
    }
    
    public void addAtTail(int val) {
        var node = dummyHead;

        while (node.next != null) {
            node = node.next;
        }

        node.next = new LinkedNode(val);
    }
    
    public void addAtIndex(int index, int val) {
        var node = dummyHead;
        var i = 0;

        while (node.next != null && i < index) {
            node = node.next;
            i += 1;
        }

        if (i == index) {
            var newNode = new LinkedNode(val);
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
class LinkedNode:
    def __init__(self, val=None):
        self.val = val
        self.next = None


class MyLinkedList:
    def __init__(self):
        self.dummy_head = LinkedNode()

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
        node = LinkedNode(val)
        node.next = self.dummy_head.next
        self.dummy_head.next = node

    def addAtTail(self, val: int) -> None:
        node = self.dummy_head

        while node.next:
            node = node.next

        node.next = LinkedNode(val)

    def addAtIndex(self, index: int, val: int) -> None:
        node = self.dummy_head
        i = 0

        while node.next and i < index:
            node = node.next
            i += 1

        if i == index:
            new_node = LinkedNode(val)
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

## 问题描述


### [Example 1]
![](../../images/examples/-)

**Input**: ``

**Output**: ``

## 中文题解

