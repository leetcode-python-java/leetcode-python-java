# 19. Remove Nth Node From End of List - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

Visit original link: [19. Remove Nth Node From End of List - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/19-remove-nth-node-from-end-of-list) for a better experience!

LeetCode link: [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list), difficulty: **Medium**.

## LeetCode description of "19. Remove Nth Node From End of List"

Given the `head` of a linked list, remove the *n<sup>th</sup>* node from the end of the list and return *its head*.

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

### [Hints]

<details>
  <summary>Hint 1</summary>
  Maintain two pointers and update one with a delay of n steps.

  
</details>

## Intuition

1. Deleting the *n<sup>th</sup>* to last node in the linked list is equivalent to deleting the (node_count - n)<sup>th</sup> node in the linked list.
2. First find out `node_count`.
3. When `index == node_count - n`, delete the node by `node.next = node.next.next`.
4. Since the deleted node may be `head`, a virtual node `dummy_node` is used to facilitate unified processing.

## Step by Step Solutions

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

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

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

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCode.blog](https://leetcode.blog): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [19. Remove Nth Node From End of List - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/19-remove-nth-node-from-end-of-list).

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

