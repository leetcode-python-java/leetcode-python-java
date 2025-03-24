Original link: [leetcoder.net - LeetCoder: Fucking Good LeetCode Solutions](https://leetcoder.net/en/leetcode/206-reverse-linked-list)

# 206. Reverse Linked List - LeetCoder: Fucking Good LeetCode Solutions

LeetCode link: [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list), Difficulty: **Easy**.

## LeetCode description of "206. Reverse Linked List"

Given the `head` of a singly linked list, reverse the list, and return _the reversed list_.

### [Example 1]

![](../../images/examples/206_1.jpg)

**Input**: `head = [1,2,3,4,5]`

**Output**: `[5,4,3,2,1]`

### [Example 2]

![](../../images/examples/206_2.jpg)

**Input**: `[1,2]`

**Output**: `[2,1]`

### [Example 3]

**Input**: `[]`

**Output**: `[]`

### [Constraints]

- The number of nodes in the list is the range `[0, 5000]`.
- `-5000 <= Node.val <= 5000`

## Intuition

1. To solve this problem, we only need to define **two** variables: `current` and `previous`. How do we inverse two node?

    <details><summary>Click to view the answer</summary><p>`current.next = previous` is the inversion.</p></details>

2. Which should be the loop condition? `while (current != null)` or `while (current.next != null)`?

	<details><summary>Click to view the answer</summary><p>It is `while (current != null)`, because the operation to be performed is `current.next = previous`.</p></details>

## Steps

1. Traverse all nodes.

	```javascript
	previous = null
	current = head
	
	while (current != null) {
	    current = current.next
	}
	```

2. Add `current.next = previous`.

	```javascript
	previous = null
	current = head
	
	while (current != null) {
	    tempNext = current.next
	    current.next = previous
	    current = tempNext
	}
	```

3. Currently `previous` is always `null`, we need to change it: `previous = current`.

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

