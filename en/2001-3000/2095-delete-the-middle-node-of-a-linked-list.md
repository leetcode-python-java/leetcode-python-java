# 2095. Delete the Middle Node of a Linked List - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at coder.id →**](https://www.coder.id)

Visit original link: [2095. Delete the Middle Node of a Linked List - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/2095-delete-the-middle-node-of-a-linked-list) for a better experience!

LeetCode link: [2095. Delete the Middle Node of a Linked List](https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list), difficulty: **Medium**.

## LeetCode description of "2095. Delete the Middle Node of a Linked List"

You are given the `head` of a linked list. **Delete** the **middle node**, and return *the* `head` *of the modified linked list*.

The **middle node** of a linked list of size `n` is the `⌊n / 2⌋^{th}` node from the **start** using **0-based indexing**, where `⌊x⌋` denotes the largest integer less than or equal to `x`.

- For `n` = `1`, `2`, `3`, `4`, and `5`, the middle nodes are `0`, `1`, `1`, `2`, and `2`, respectively.

### [Example 1]

**Input**: `head = [1,3,4,7,1,2,6]`

**Output**: `[1,3,4,1,2,6]`

**Explanation**: 

<p>The above figure represents the given linked list. The indices of the nodes are written below.<br>
Since n = 7, node 3 with value 7 is the middle node, which is marked in red.<br>
We return the new list after removing this node.</p>


### [Example 2]

**Input**: `head = [1,2,3,4]`

**Output**: `[1,2,4]`

**Explanation**: 

<p>The above figure represents the given linked list.<br>
For n = 4, node 2 with value 3 is the middle node, which is marked in red.</p>


### [Example 3]

**Input**: `head = [2,1]`

**Output**: `[2]`

**Explanation**: 

<p>The above figure represents the given linked list.<br>
For n = 2, node 1 with value 1 is the middle node, which is marked in red.<br>
Node 0 with value 2 is the only node remaining after removing node 1.</p>


### [Example 4]

**Input**: `head = [1,3,4,7,1,2,6]`

**Output**: `[1,3,4,1,2,6]`

**Explanation**: 

<p>The above figure represents the given linked list. The indices of the nodes are written below.<br>
Since n = 7, node 3 with value 7 is the middle node, which is marked in red.<br>
We return the new list after removing this node.</p>


### [Example 5]

**Input**: `head = [1,2,3,4]`

**Output**: `[1,2,4]`

**Explanation**: 

<p>The above figure represents the given linked list.<br>
For n = 4, node 2 with value 3 is the middle node, which is marked in red.</p>


### [Example 6]

**Input**: `head = [2,1]`

**Output**: `[2]`

**Explanation**: 

<p>The above figure represents the given linked list.<br>
For n = 2, node 1 with value 1 is the middle node, which is marked in red.<br>
Node 0 with value 2 is the only node remaining after removing node 1.</p>


### [Example 7]

**Input**: `head = [1,3,4,7,1,2,6]`

**Output**: `[1,3,4,1,2,6]`

**Explanation**: 

<p>The above figure represents the given linked list. The indices of the nodes are written below.<br>
Since n = 7, node 3 with value 7 is the middle node, which is marked in red.<br>
We return the new list after removing this node.</p>


### [Example 8]

**Input**: `head = [1,2,3,4]`

**Output**: `[1,2,4]`

**Explanation**: 

<p>The above figure represents the given linked list.<br>
For n = 4, node 2 with value 3 is the middle node, which is marked in red.</p>


### [Example 9]

**Input**: `head = [2,1]`

**Output**: `[2]`

**Explanation**: 

<p>The above figure represents the given linked list.<br>
For n = 2, node 1 with value 1 is the middle node, which is marked in red.<br>
Node 0 with value 2 is the only node remaining after removing node 1.</p>


### [Constraints]

- The number of nodes in the list is in the range `[1, 10^5]`.
- `1 <= Node.val <= 10^5`

### [Hints]

<details>
  <summary>Hint 1</summary>
  If a point with a speed s moves n units in a given time, a point with speed 2 * s will move 2 * n units at the same time. Can you use this to find the middle node of a linked list?

  
</details>

<details>
  <summary>Hint 2</summary>
  If you are given the middle node, the node before it, and the node after it, how can you modify the linked list?

  
</details>

<details>
  <summary>Hint 3</summary>
  If a point with a speed s moves n units in a given time, a point with speed 2 * s will move 2 * n units at the same time. Can you use this to find the middle node of a linked list?

  
</details>

<details>
  <summary>Hint 4</summary>
  If you are given the middle node, the node before it, and the node after it, how can you modify the linked list?

  
</details>

<details>
  <summary>Hint 5</summary>
  If a point with a speed s moves n units in a given time, a point with speed 2 * s will move 2 * n units at the same time. Can you use this to find the middle node of a linked list?

  
</details>

<details>
  <summary>Hint 6</summary>
  If you are given the middle node, the node before it, and the node after it, how can you modify the linked list?

  
</details>

## Intuition

To delete the middle node of a linked list in a single pass, we can use the classic **Fast and Slow Pointers** approach (also known as the Tortoise and Hare algorithm).

When we have two pointers traversing a list:
- The **slow** pointer moves one step at a time.
- The **fast** pointer moves two steps at a time.

Because the fast pointer moves exactly twice as fast as the slow pointer, by the time the fast pointer reaches the end of the list, the slow pointer will be exactly at the middle node!

However, to *delete* a node in a singly linked list, we actually need to modify the `next` pointer of the node *preceding* the one we want to delete. Thus, we have two options:
1. Keep track of a `previous` pointer that follows the slow pointer.
2. Initialize the pointers cleverly: we can start a `dummy` node pointing to `head`, and let the slow pointer start at `dummy` while the fast pointer starts at `head`. By the time `fast` reaches the end, `slow` will point to the node **right before** the middle node.

The dummy node approach is extremely clean and effortlessly handles edge cases (such as a list with only 1 element).

## Step-by-Step Solution

1. **Handle edge case:** If the linked list has only one node (`head.next == null`), return `null` because the middle node is the only node, and deleting it leaves an empty list. (Or we can handle this using a dummy node universally).
2. **Initialize dummy node:** Create a `dummy` node where `dummy.next = head`.
3. **Initialize pointers:** Set `slow = dummy` and `fast = head`.
4. **Traverse the list:** Loop as long as `fast != null` and `fast.next != null`.
   - Move `slow` one step: `slow = slow.next`.
   - Move `fast` two steps: `fast = fast.next.next`.
5. **Delete the middle node:** Once the loop ends, `slow` is pointing to the node exactly before the middle node. Simply bypass the middle node by doing `slow.next = slow.next.next`.
6. **Return the result:** Return `dummy.next` (which is the new head of the list).

## Complexity

> - **Time Complexity:** `O(N)`
  We traverse the linked list using the fast pointer. The fast pointer takes `N / 2` steps to reach the end. Since each step is a constant time operation, the overall time complexity is linear.
- **Space Complexity:** `O(1)`
  We only use three extra pointers (`dummy`, `slow`, `fast`), regardless of the size of the linked list. Therefore, the space complexity is strictly constant.

- Time complexity: ``.
- Space complexity: ``.

## Python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteMiddle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # Edge case: if there is only 1 node, deleting it returns None.
        # The dummy node approach handles this automatically, 
        # but returning directly is also fine.
        
        # Create a dummy node that points to the head.
        # This helps us stop the slow pointer EXACTLY one node before the middle.
        dummy = ListNode(0, head)
        
        # Initialize slow pointer at dummy, and fast pointer at head.
        slow = dummy
        fast = head
        
        # Traverse the list. Fast moves 2 steps, slow moves 1 step.
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            
        # At this point, fast has reached the end.
        # slow is pointing to the node preceding the middle node.
        # Bypass the middle node to delete it.
        slow.next = slow.next.next
        
        # Return the new head
        return dummy.next
```

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
    public ListNode deleteMiddle(ListNode head) {
        // Create a dummy node that points to the head.
        // This is crucial to make the slow pointer stop right before the middle node.
        ListNode dummy = new ListNode(0, head);
        
        // slow starts at dummy, fast starts at head.
        ListNode slow = dummy;
        ListNode fast = head;
        
        // Loop until fast reaches the end of the list.
        while (fast != null && fast.next != null) {
            // slow moves 1 step
            slow = slow.next;
            // fast moves 2 steps
            fast = fast.next.next;
        }
        
        // slow is now pointing to the node just before the middle node.
        // We delete the middle node by skipping it.
        slow.next = slow.next.next;
        
        // Return the modified list starting from dummy.next
        return dummy.next;
    }
}
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
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var deleteMiddle = function(head) {
    // We use a dummy node to easily handle the case where we need to delete the first node 
    // or when we need to stop the slow pointer one step before the middle node.
    let dummy = new ListNode(0, head);
    
    // Slow pointer starts at dummy, fast pointer starts at head
    let slow = dummy;
    let fast = head;
    
    // Fast pointer moves twice as fast as the slow pointer
    while (fast !== null && fast.next !== null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    
    // Once fast reaches the end, slow is exactly at the node BEFORE the middle.
    // Skip the middle node to delete it.
    slow.next = slow.next.next;
    
    // Return the new head
    return dummy.next;
};
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
    ListNode* deleteMiddle(ListNode* head) {
        // If there is only one node, deleting it results in an empty list.
        if (!head || !head->next) {
            return nullptr;
        }
        
        // Slow pointer starts at head, fast pointer starts two steps ahead.
        // This is an alternative to using a dummy node.
        // By giving fast a head start, slow will stop one node before the middle.
        ListNode* slow = head;
        ListNode* fast = head->next->next;
        
        // Traverse the list
        while (fast != nullptr && fast->next != nullptr) {
            slow = slow->next;          // Move slow by 1
            fast = fast->next->next;    // Move fast by 2
        }
        
        // Delete the middle node. 
        // In C++, it is good practice to free the memory of the deleted node.
        ListNode* toDelete = slow->next;
        slow->next = slow->next->next;
        delete toDelete;
        
        return head;
    }
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
    public ListNode DeleteMiddle(ListNode head) {
        // Dummy node helps to stop slow pointer just before the middle node
        ListNode dummy = new ListNode(0, head);
        
        ListNode slow = dummy;
        ListNode fast = head;
        
        // Traverse the linked list
        while (fast != null && fast.next != null) {
            slow = slow.next;        // 1 step
            fast = fast.next.next;   // 2 steps
        }
        
        // Bypass the middle node to remove it from the list
        slow.next = slow.next.next;
        
        return dummy.next;
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
func deleteMiddle(head *ListNode) *ListNode {
    // Create a dummy node pointing to head
    // This allows the slow pointer to easily stop before the middle node
    dummy := &ListNode{Val: 0, Next: head}
    
    slow := dummy
    fast := head
    
    // Fast pointer moves 2 steps, slow moves 1 step
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
    }
    
    // Skip the middle node
    slow.Next = slow.Next.Next
    
    return dummy.Next
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
# @param {ListNode} head
# @return {ListNode}
def delete_middle(head)
    # A dummy node helps handle the edge case where the list has only 1 node
    dummy = ListNode.new(0, head)
    
    slow = dummy
    fast = head
    
    # Traverse with fast pointer moving twice as fast
    while fast && fast.next
        slow = slow.next
        fast = fast.next.next
    end
    
    # slow is now exactly before the middle node, bypass it
    slow.next = slow.next.next
    
    dummy.next
end
```

## Rust

```rust
// Definition for singly-linked list.
// #[derive(PartialEq, Eq, Clone, Debug)]
// pub struct ListNode {
//   pub val: i32,
//   pub next: Option<Box<ListNode>>
// }
// 
// impl ListNode {
//   #[inline]
//   fn new(val: i32) -> Self {
//     ListNode {
//       next: None,
//       val
//     }
//   }
// }
impl Solution {
    pub fn delete_middle(mut head: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
        // Count total number of nodes first
        let mut count = 0;
        let mut curr = &head;
        while let Some(node) = curr {
            count += 1;
            curr = &node.next;
        }
        
        // If there is only one node, return None
        if count <= 1 {
            return None;
        }
        
        // Find the index of the node right BEFORE the middle node
        let mid = count / 2;
        
        // Traverse to the node just before the middle
        let mut curr = &mut head;
        for _ in 0..mid - 1 {
            if let Some(node) = curr {
                curr = &mut node.next;
            }
        }
        
        // Take the node before middle, and skip the middle node
        if let Some(node) = curr {
            let next_node = node.next.take();
            if let Some(middle) = next_node {
                node.next = middle.next;
            }
        }
        
        head
    }
}
```

## Kotlin

```kotlin
/**
 * Example:
 * var li = ListNode(5)
 * var v = li.`val`
 * Definition for singly-linked list.
 * class ListNode(var `val`: Int) {
 *     var next: ListNode? = null
 * }
 */
class Solution {
    fun deleteMiddle(head: ListNode?): ListNode? {
        // Create a dummy node pointing to head
        val dummy = ListNode(0)
        dummy.next = head
        
        var slow: ListNode? = dummy
        var fast: ListNode? = head
        
        // Fast moves 2 steps, slow moves 1 step
        while (fast != null && fast.next != null) {
            slow = slow?.next
            fast = fast.next?.next
        }
        
        // Delete the middle node by skipping it
        slow?.next = slow?.next?.next
        
        // Return the modified list head
        return dummy.next
    }
}
```

## Swift

```swift
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public var val: Int
 *     public var next: ListNode?
 *     public init() { self.val = 0; self.next = nil; }
 *     public init(_ val: Int) { self.val = val; self.next = nil; }
 *     public init(_ val: Int, _ next: ListNode?) { self.val = val; self.next = next; }
 * }
 */
class Solution {
    func deleteMiddle(_ head: ListNode?) -> ListNode? {
        // Dummy node to handle the case where list has 1 node
        let dummy = ListNode(0, head)
        
        var slow: ListNode? = dummy
        var fast: ListNode? = head
        
        // Traverse: fast moves 2 steps, slow moves 1 step
        while fast != nil && fast?.next != nil {
            slow = slow?.next
            fast = fast?.next?.next
        }
        
        // Remove the middle node
        slow?.next = slow?.next?.next
        
        return dummy.next
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**coder.id**](https://www.coder.id) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.coder.id`.
>
> [**Build Your Programmer Brand at coder.id →**](https://www.coder.id)

---

Visit original link: [2095. Delete the Middle Node of a Linked List - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/2095-delete-the-middle-node-of-a-linked-list) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

