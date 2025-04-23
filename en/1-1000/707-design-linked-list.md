# 707. Design Linked List - LeetCode solutions in Python/Java/C++ and more

Visit original link: [707. Design Linked List - LeetCode solutions in Python/Java/C++ and more](https://leetcodepython.com/en/leetcode/707-design-linked-list) for a better experience!

LeetCode link: [707. Design Linked List](https://leetcode.com/problems/design-linked-list), difficulty: **Medium**.

## LeetCode description of "707. Design Linked List"

Design your implementation of the linked list. You can choose to use a singly or doubly linked list.

A node in a singly linked list should have two attributes: `val` and `next`. `val` is the value of the current node, and `next` is a pointer/reference to the next node.

If you want to use the doubly linked list, you will need one more attribute `prev` to indicate the previous node in the linked list. Assume all nodes in the linked list are **0-indexed**.


Implement the `MyLinkedList` class:

- `MyLinkedList()` Initializes the `MyLinkedList` object.
- `int get(int index)` Get the value of the *index<sup>th</sup>* node in the linked list. If the index is invalid, return `-1`.
- `void addAtHead(int val)` Add a node of value `val` before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
- `void addAtTail(int val)` Append a node of value `val` as the last element of the linked list.
- `void addAtIndex(int index, int val)` Add a node of value `val` before the *index<sup>th</sup>* node in the linked list. If `index` equals the length of the linked list, the node will be appended to the end of the linked list. If `index` is greater than the length, the node will **not be inserted**.
- `void deleteAtIndex(int index)` Delete the *index<sup>th</sup>* node in the linked list, if the index is valid.

### [Example 1]

**Input**: `["MyLinkedList", "addAtHead", "addAtTail", "addAtIndex", "get", "deleteAtIndex", "get"] [[], [1], [3], [1, 2], [1], [1], [1]]`

**Output**: `[null, null, null, null, 2, null, 3]`

**Explanation**: 

<p>MyLinkedList myLinkedList = new MyLinkedList();<br>
myLinkedList.addAtHead(1);<br>
myLinkedList.addAtTail(3);<br>
myLinkedList.addAtIndex(1, 2);    // linked list becomes 1-&gt;2-&gt;3<br>
myLinkedList.get(1);              // return 2<br>
myLinkedList.deleteAtIndex(1);    // now the linked list is 1-&gt;3<br>
myLinkedList.get(1);              // return 3</p>


### [Constraints]

- `0 <= index, val <= 1000`
- Please do not use the built-in LinkedList library.
- At most `2000` calls will be made to `get`, `addAtHead`, `addAtTail`, `addAtIndex` and `deleteAtIndex`.

## Intuition

Before solving this problem, it is recommended to solve the simple problem [19. Remove Nth Node From End of List](19-remove-nth-node-from-end-of-list.md) first.

This question can comprehensively test the candidate's mastery of linked lists. The following points need to be paid attention to:

1. It is best to use a `dummyHead` node as the entry of the linked list.
2. It is best to use a new `ListNode` class, so that `dummyHead` does not need to be mixed with `val` and `next`.
3. Implement the easy methods first, in the order of `addAtHead`, `addAtTail`, `addAtIndex`, `deleteAtIndex`, `get`.

## Complexity

- Time complexity: `O(N * N)`.
- Space complexity: `O(N)`.

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

```csharp
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
// ListNode represents a node in the singly-linked list
// type ListNode struct {
//     Val  int
//     Next *ListNode
// }

// MyLinkedList implements linked list operations using a dummy head node
type MyLinkedList struct {
    dummyHead *ListNode
}

// Constructor initializes a new linked list
func Constructor() MyLinkedList {
    return MyLinkedList{
        dummyHead: &ListNode{}, // Initialize dummy head with zero value
    }
}

// Get retrieves the value at specified index, returns -1 for invalid indices
func (ll *MyLinkedList) Get(index int) int {
    current := ll.dummyHead.Next
    count := 0
    
    // Traverse until reaching desired index or end of list
    for current != nil && count < index {
        current = current.Next
        count++
    }
    
    // Validate index and return value if found
    if current != nil && count == index {
        return current.Val
    }
    return -1
}

// AddAtHead inserts new node at beginning of the list
func (ll *MyLinkedList) AddAtHead(val int) {
    newNode := &ListNode{Val: val}
    newNode.Next = ll.dummyHead.Next
    ll.dummyHead.Next = newNode
}

// AddAtTail appends new node at end of the list
func (ll *MyLinkedList) AddAtTail(val int) {
    current := ll.dummyHead
    // Traverse to last node
    for current.Next != nil {
        current = current.Next
    }
    current.Next = &ListNode{Val: val}
}

// AddAtIndex inserts node at specified position if valid
func (ll *MyLinkedList) AddAtIndex(index int, val int) {
    prev := ll.dummyHead
    count := 0
    
    // Find insertion point
    for prev.Next != nil && count < index {
        prev = prev.Next
        count++
    }
    
    // Only insert if index matches traversal count
    if count == index {
        newNode := &ListNode{Val: val}
        newNode.Next = prev.Next
        prev.Next = newNode
    }
}

// DeleteAtIndex removes node at specified position if valid
func (ll *MyLinkedList) DeleteAtIndex(index int) {
    prev := ll.dummyHead
    count := 0
    
    // Find node preceding the deletion target
    for prev.Next != nil && count < index {
        prev = prev.Next
        count++
    }
    
    // Perform deletion if index is valid and node exists
    if prev.Next != nil && count == index {
        prev.Next = prev.Next.Next
    }
}
```

## C++

```cpp
class MyLinkedList {
private:
    struct ListNode {
        int val;
        ListNode* next;
        ListNode(int x) : val(x), next(nullptr) {}
    };
    
    ListNode* dummy_head_;
    
public:
    MyLinkedList() {
        dummy_head_ = new ListNode(0);
    }
    
    int get(int index) {
        auto node = dummy_head_->next;
        auto i = 0;
        
        while (node && i < index) {
            node = node->next;
            i++;
        }
        
        return (i == index && node) ? node->val : -1;
    }
    
    void addAtHead(int val) {
        auto node = new ListNode(val);
        node->next = dummy_head_->next;
        dummy_head_->next = node;
    }
    
    void addAtTail(int val) {
        auto node = dummy_head_;
        while (node->next) {
            node = node->next;
        }
        node->next = new ListNode(val);
    }
    
    void addAtIndex(int index, int val) {
        auto node = dummy_head_;
        auto i = 0;
        
        while (node->next && i < index) {
            node = node->next;
            i++;
        }
        
        if (i == index) {
            auto new_node = new ListNode(val);
            new_node->next = node->next;
            node->next = new_node;
        }
    }
    
    void deleteAtIndex(int index) {
        auto node = dummy_head_;
        auto i = 0;
        
        while (node->next && i < index) {
            node = node->next;
            i++;
        }
        
        if (i == index && node->next) {
            auto to_delete = node->next;
            node->next = node->next->next;
            delete to_delete;
        }
    }
};

```

## Ruby

```ruby
# ListNode class with val and next_node (since 'next' is reserved in some languages)
class ListNode
  attr_accessor :val, :next_node

  def initialize(val = nil)
    @val = val
    @next_node = nil
  end
end

# MyLinkedList implementation with dummy head
class MyLinkedList
  def initialize
    @dummy_head = ListNode.new  # Dummy head node
  end

  # Get value at index, return -1 if invalid
  def get(index)
    current = @dummy_head.next_node
    count = 0
    
    while current && count < index
      current = current.next_node
      count += 1
    end
    
    current && count == index ? current.val : -1
  end

  # Add node at head
  def add_at_head(val)
    new_node = ListNode.new(val)
    new_node.next_node = @dummy_head.next_node
    @dummy_head.next_node = new_node
  end

  # Add node at tail
  def add_at_tail(val)
    current = @dummy_head
    
    while current.next_node
      current = current.next_node
    end
    
    current.next_node = ListNode.new(val)
  end

  # Add node at index if valid
  def add_at_index(index, val)
    prev = @dummy_head
    count = 0
    
    while prev.next_node && count < index
      prev = prev.next_node
      count += 1
    end
    
    if count == index
      new_node = ListNode.new(val)
      new_node.next_node = prev.next_node
      prev.next_node = new_node
    end
  end

  # Delete node at index if valid
  def delete_at_index(index)
    prev = @dummy_head
    count = 0
    
    while prev.next_node && count < index
      prev = prev.next_node
      count += 1
    end
    
    if prev.next_node && count == index
      prev.next_node = prev.next_node.next_node
    end
  end
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCodePython.com](https://leetcodepython.com): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [707. Design Linked List - LeetCode solutions in Python/Java/C++ and more](https://leetcodepython.com/en/leetcode/707-design-linked-list).

GitHub repository: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

