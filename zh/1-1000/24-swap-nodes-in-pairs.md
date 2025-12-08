# 24. 两两交换链表中的节点 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **进阶你的开发者身份**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/你的名字` 或 `an.dev/你的名字`。
>
> [**立即前往 Show.dev 打造你的专属品牌 →**](https://www.show.dev)

---

访问原文链接：[24. 两两交换链表中的节点 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/24-swap-nodes-in-pairs)，体验更佳！

力扣链接：[24. 两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs), 难度等级：**中等**。

## LeetCode “24. 两两交换链表中的节点”问题描述

给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）。

### [示例 1]

![](../../images/examples/24_1.jpg)

**输入**: `head = [1,2,3,4]`

**输出**: `[2,1,4,3]`

### [示例 2]

**输入**: `head = []`

**输出**: `[]`

### [示例 3]

**输入**: `head = [1]`

**输出**: `[1]`

### [示例 4]

**输入**: `head = [1,2,3]`

**输出**: `[2,1,3]`

### [约束]

- 链表中节点的数目在范围 `[0, 100]` 内
- `0 <= Node.val <= 100`

## 思路

在做本题前，建议先完成简单题目[206. Reverse Linked List](206-reverse-linked-list.md)。

1. 解决这个问题，依然至少需要定义两个变量：`current`和`previous`。
2. 循环条件应是`while (current.next != null)`，而不应该是`while (current != null)`，因为需要操作`current.next.next`。

## 步骤

1. 遍历所有节点。

    ```java
    var previous = null;
    var current = head;
	
    while (current != null) {
        current = current.next;
    }
    ```

2. 因为每两个节点进行一次位置互换，所以需要改为一次走两步。

    ```java
    var previous = null;
    var current = head;
	
    while (current != null && current.next != null) { // 1
        var nextNext = current.next.next; // 2
        current = nextNext; // 3
    }
    ```

3. 交换 `current` 和 `current.next` 的位置。

	```java
	var previous = null;
	var current = head;
	
	while (current != null && current.next != null) {
	    var nextNext = current.next.next;
	
	    current.next.next = current; // 1
	    current.next = nextNext; // 2
	
	    current = nextNext;
	}
	```

4. 处理 `previous`。

	```java
	var previous = null;
	var current = head;
	
	while (current != null && current.next != null) {
	    var nextNext = current.next.next;
	
	    previous.next = current.next; // 1
	    current.next.next = current;
	    current.next = nextNext;
	
	    previous = current; // 2
	    current = nextNext;
	}
	```

5. 确定返回值。因为`head`节点在节点数量超过1时，会被交换到第二个节点的位置，为了统一方便处理，最好加入`dummy_head`节点。

	```java
	var dummyHead = new ListNode(); // 1
	dummyHead.next = head; // 2
	
	var previous = dummyHead; // 3
	var current = head;
	
	while (current != null && current.next != null) {
	    var nextNext = current.next.next;
	
	    previous.next = current.next;
	    current.next.next = current;
	    current.next = nextNext;
	
	    previous = current;
	    current = nextNext;
	}
	
	return dummyHead.next; // 4
	```

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

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
    public ListNode swapPairs(ListNode head) {
        var dummyHead = new ListNode(0, head);
        var previous = dummyHead;
        var current = head;

        while (current != null && current.next != null) {
            var nextNext = current.next.next;

            previous.next = current.next;
            current.next.next = current;
            current.next = nextNext;

            previous = current;
            current = nextNext;
        }

        return dummyHead.next;
    }
}
```

## Python

```python
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy_head = ListNode(next=head)
        previous = dummy_head
        current = head

        while current and current.next:
            next_next = current.next.next

            previous.next = current.next
            current.next.next = current
            current.next = next_next

            previous = current
            current = next_next

        return dummy_head.next
```

## C++

```cpp
/**
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
    ListNode* swapPairs(ListNode* head) {
        auto dummy_head = new ListNode(0, head);
        auto previous = dummy_head;
        auto current = head;

        while (current != nullptr && current->next != nullptr) {
            auto next_next = current->next->next;

            previous->next = current->next;
            current->next->next = current;
            current->next = next_next;

            previous = current;
            current = next_next;
        }

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
var swapPairs = function (head) {
  const dummyHead = new ListNode(0, head)

  let previous = dummyHead
  let current = head

  while (current != null && current.next != null) {
    const nextNext = current.next.next

    previous.next = current.next
    current.next.next = current
    current.next = nextNext

    previous = current
    current = nextNext
  }

  return dummyHead.next
};
```

## C#

```csharp
/**
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
    public ListNode SwapPairs(ListNode head)
    {
        var dummyHead = new ListNode(0, head);
        var previous = dummyHead;
        var current = head;

        while (current != null && current.next != null)
        {
            var nextNext = current.next.next;

            previous.next = current.next;
            current.next.next = current;
            current.next = nextNext;

            previous = current;
            current = nextNext;
        }

        return dummyHead.next;
    }
}
```

## Go

```go
/**
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func swapPairs(head *ListNode) *ListNode {
    dummyHead := &ListNode{0, head}

    previous := dummyHead
    current := head

    for current != nil && current.Next != nil {
        nextNext := current.Next.Next

        previous.Next = current.Next
        current.Next.Next = current
        current.Next = nextNext

        previous = current
        current = nextNext
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

def swap_pairs(head)
  dummy_head = ListNode.new
  dummy_head.next = head

  previous = dummy_head
  current = head

  while current && current.next
    next_next = current.next.next

    previous.next = current.next
    current.next.next = current
    current.next = next_next

    previous = current
    current = next_next
  end

  dummy_head.next
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **进阶你的开发者身份**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/你的名字` 或 `an.dev/你的名字`。
>
> [**立即前往 Show.dev 打造你的专属品牌 →**](https://www.show.dev)

---

访问原文链接：[24. 两两交换链表中的节点 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/24-swap-nodes-in-pairs)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

