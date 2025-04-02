# 206. 反转链表 - 力扣题解最佳实践

访问原文链接：[206. 反转链表 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/206-reverse-linked-list)，体验更佳！

力扣链接：[206. 反转链表](https://leetcode.cn/problems/reverse-linked-list), 难度：**简单**。

## 力扣“206. 反转链表”问题描述

给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

### [示例 1]

![](../../images/examples/206_1.jpg)

**输入**: `head = [1,2,3,4,5]`

**输出**: `[5,4,3,2,1]`

### [示例 2]

![](../../images/examples/206_2.jpg)

**输入**: `[1,2]`

**输出**: `[2,1]`

### [示例 3]

**输入**: `[]`

**输出**: `[]`

### [约束]

- 链表中节点的数目范围是 `[0, 5000]`
- `-5000 <= Node.val <= 5000`

## 思路

1. 解决这个问题，只需要定义**两**个变量：`current`和`previous`。

	<details><summary>点击查看答案</summary><p>`current.next = previous` 就是反转了。</p></details>

2. 循环条件是`while (current != null)`，还是`while (current.next != null)`？

	<details><summary>点击查看答案</summary><p>是 `while (current != null)`，因为需要操作的是 `current.next = previous`。</p></details>

## 步骤

1. 遍历所有节点。

	```javascript
	previous = null
	current = head
	
	while (current != null) {
	    current = current.next
	}
	```

2. 加入`current.next = previous`。

	```javascript
	previous = null
	current = head
	
	while (current != null) {
	    tempNext = current.next
	    current.next = previous
	    current = tempNext
	}
	```

3. `previous`目前始终是`null`，需要让它变化起来：`previous = current`。

	```javascript
	previous = null
	current = head
	
	while (current != null) {
	    tempNext = current.next
	    current.next = previous
	    previous = current
	    current = tempNext
	}
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
    public ListNode reverseList(ListNode head) {
        ListNode previous = null;
        var current = head;

        while (current != null) {
            var tempNext = current.next;
            current.next = previous;
            previous = current;
            current = tempNext;
        }

        return previous;
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
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        previous = None
        current = head

        while current:
            temp_next = current.next
            current.next = previous
            previous = current
            current = temp_next

        return previous
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
    ListNode* reverseList(ListNode* head) {
        ListNode* previous = nullptr;
        ListNode* current = head;

        while (current) {
            auto temp_next = current->next;
            current->next = previous;
            previous = current;
            current = temp_next;
        }

        return previous;
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
var reverseList = function (head) {
  let previous = null
  let current = head

  while (current != null) {
    const tempNext = current.next
    current.next = previous
    previous = current
    current = tempNext
  }

  return previous
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
    public ListNode ReverseList(ListNode head)
    {
        ListNode previous = null;
        ListNode current = head;

        while (current != null)
        {
            var tempNext = current.next;
            current.next = previous;
            previous = current;
            current = tempNext;
        }

        return previous;
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
func reverseList(head *ListNode) *ListNode {
    var previous *ListNode
    current := head

    for current != nil {
        tempNext := current.Next
        current.Next = previous
        previous = current
        current = tempNext
    }

    return previous
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

def reverse_list(head)
  previous = nil
  current = head

  while current
    temp_next = current.next
    current.next = previous
    previous = current
    current = temp_next
  end

  previous
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [leetcoder.net](https://leetcoder.net/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[206. 反转链表 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/206-reverse-linked-list).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

