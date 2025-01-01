# 206. Reverse Linked List - LeetCode Solution
LeetCode problem link: [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list),
[206. 反转链表](https://leetcode.cn/problems/reverse-linked-list)

[中文题解](#中文题解)

## LeetCode problem description
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

## Intuition behind the Solution
[中文题解](#中文题解)

1. To solve this problem, we only need to define **two** variables: `current` and `previous`.
2. `current.next = previous` is the inversion.
3. The loop condition should be `while current != null` instead of `while current.next != null`, because the operation to be performed is `current.next = previous`.

## Steps to the Solution
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

3. `previous` is always `null`, we need to change it: `previous = current`.
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
* Time: `O(n)`.
* Space: `O(1)`.

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
```c#
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
给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

**输入**: `head = [1,2,3,4,5]`

**输出**: `[5,4,3,2,1]`

## 中文题解
### 思路
1. 解决这个问题，只需要定义**两**个变量：`current`和`previous`。
2. `current.next = previous`就是反转了。
3. 循环条件应是`while current != null`，而不应该是`while current.next != null`，因为需要操作的是`current.next = previous`.

### 步骤
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
