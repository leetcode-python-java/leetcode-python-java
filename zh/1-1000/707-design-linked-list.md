# 707. 设计链表 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 Show.dev 打造你的个人品牌 →**](https://www.show.dev)

---

访问原文链接：[707. 设计链表 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/707-design-linked-list)，体验更佳！

力扣链接：[707. 设计链表](https://leetcode.cn/problems/design-linked-list), 难度等级：**中等**。

## LeetCode “707. 设计链表”问题描述

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

<p>MyLinkedList myLinkedList = new MyLinkedList();<br>
myLinkedList.addAtHead(1);<br>
myLinkedList.addAtTail(3);<br>
myLinkedList.addAtIndex(1, 2);    // 链表变为 1-&gt;2-&gt;3<br>
myLinkedList.get(1);              // 返回 2<br>
myLinkedList.deleteAtIndex(1);    // 现在，链表变为 1-&gt;3<br>
myLinkedList.get(1);              // 返回 3</p>


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

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 Show.dev 打造你的个人品牌 →**](https://www.show.dev)

---

访问原文链接：[707. 设计链表 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/707-design-linked-list)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

