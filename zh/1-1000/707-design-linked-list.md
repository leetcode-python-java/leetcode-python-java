原文链接：[leetcoder.net - 力扣题解最佳实践 - 力扣人](https://leetcoder.net/zh/leetcode/707-design-linked-list)

# 707. 设计链表 - 力扣题解最佳实践 - 力扣人

力扣链接：[707. 设计链表](https://leetcode.cn/problems/design-linked-list), 难度：**中等**。

## 力扣“707. 设计链表”问题描述

你可以选择使用单链表或者双链表，设计并实现自己的链表。

单链表中的节点应该具备两个属性：`val` 和 `next` 。`val` 是当前节点的值，`next` 是指向下一个节点的指针/引用。

如果是双向链表，则还需要属性 `prev` 以指示链表中的上一个节点。假设链表中的所有节点下标从 0 开始。

实现 `MyLinkedList` 类：

- `MyLinkedList()` 初始化 `MyLinkedList` 对象。
- `int get(int index)` 获取链表中下标为 `index` 的节点的值。如果下标无效，则返回 `-1` 。
- `void addAtHead(int val)` 将一个值为 `val` 的节点插入到链表中第一个元素之前。在插入完成后，新节点会成为链表的第一个节点。
- `void addAtTail(int val)` 将一个值为 `val` 的节点追加到链表中作为链表的最后一个元素。
- `void addAtIndex(int index, int val)` 将一个值为 `val` 的节点插入到链表中下标为 `index` 的节点之前。如果 `index` 等于链表的长度，那么该节点会被追加到链表的末尾。如果 index 比长度更大，该节点将 不会插入 到链表中。
- `void deleteAtIndex(int index)` 如果下标有效，则删除链表中下标为 `index` 的节点。

### [示例 1]

**输入**: `["MyLinkedList", "addAtHead", "addAtTail", "addAtIndex", "get", "deleteAtIndex", "get"] [[], [1], [3], [1, 2], [1], [1], [1]]`

**输出**: `[null, null, null, null, 2, null, 3]`

**解释**: 

MyLinkedList myLinkedList = new MyLinkedList();
myLinkedList.addAtHead(1);
myLinkedList.addAtTail(3);
myLinkedList.addAtIndex(1, 2);    // 链表变为 1->2->3
myLinkedList.get(1);              // 返回 2
myLinkedList.deleteAtIndex(1);    // 现在，链表变为 1->3
myLinkedList.get(1);              // 返回 3

### [约束]

- `0 <= index, val <= 1000`
- 请不要使用内置的 LinkedList 库。
- 调用 `get`、`addAtHead`、`addAtTail`、`addAtIndex` 和 `deleteAtIndex` 的次数不超过 `2000` 。

## 思路

在做本题前，建议先完成较简单的相关题目 [19. 删除链表的倒数第 N 个结点](19-remove-nth-node-from-end-of-list.md)。

本题可以全面考察候选人对链表的掌握程度，以下几点需要重视：

1. 最好使用一个`dummyHead`节点做为链表入口。
2. 最好使用一个新的`ListNode`类，这样，`dummyHead`就不用和`val`、`next`混在一起。
3. 先实现容易的方法，顺序为`addAtHead`, `addAtTail`, `addAtIndex`, `deleteAtIndex`, `get`。

## 复杂度

- 时间复杂度: `O(N * N)`.
- 空间复杂度: `O(N)`.

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

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

