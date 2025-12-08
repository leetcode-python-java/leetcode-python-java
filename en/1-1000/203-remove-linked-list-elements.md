# 203. Remove Linked List Elements - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
> We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [203. Remove Linked List Elements - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/203-remove-linked-list-elements) for a better experience!

LeetCode link: [203. Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements), difficulty: **Easy**.

## LeetCode description of "203. Remove Linked List Elements"

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

## Intuition

- Assume that the node to be deleted in the linked list is `d`, and the previous node of `d` is `p`, so `p.next` is `d`.

	To delete `d`, just set `p.next = p.next.next`.

- Because `p.next.next` is used, the loop condition should be `while (p.next != null)` instead of `while (p != null)`.

- But there is no node before the `head` node, which means that the `head` node needs to be treated specially.

	Is there a way to make the `head` node no longer special? In this way, there is no need to treat the `head` specially.

	<details><summary>Click to view the answer</summary><p>The way is to introduce a `dummy` node, `dummy.next = head`.</p></details>

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

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

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
> We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [203. Remove Linked List Elements - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/203-remove-linked-list-elements) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

