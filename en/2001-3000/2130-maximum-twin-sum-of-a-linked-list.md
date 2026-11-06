# 2130. Maximum Twin Sum of a Linked List - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at coder.id →**](https://www.coder.id)

Visit original link: [2130. Maximum Twin Sum of a Linked List - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/2130-maximum-twin-sum-of-a-linked-list) for a better experience!

LeetCode link: [2130. Maximum Twin Sum of a Linked List](https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list), difficulty: **Medium**.

## LeetCode description of "2130. Maximum Twin Sum of a Linked List"

In a linked list of size `n`, where `n` is **even**, the `i^{th}` node (**0-indexed**) of the linked list is known as the **twin** of the `(n-1-i)^{th}` node, if `0 <= i <= (n / 2) - 1`.

- For example, if `n = 4`, then node `0` is the twin of node `3`, and node `1` is the twin of node `2`. These are the only nodes with twins for `n = 4`.

The **twin sum** is defined as the sum of a node and its twin.

Given the `head` of a linked list with even length, return *the **maximum twin sum** of the linked list*.

### [Example 1]

**Input**: `head = [5,4,2,1]`

**Output**: `6`

**Explanation**: 

<p>Nodes 0 and 1 are the twins of nodes 3 and 2, respectively. All have twin sum = 6.<br>
There are no other nodes with twins in the linked list.<br>
Thus, the maximum twin sum of the linked list is 6.</p>


### [Example 2]

**Input**: `head = [4,2,2,3]`

**Output**: `7`

**Explanation**: 

<p>The nodes with twins present in this linked list are:<br>
- Node 0 is the twin of node 3 having a twin sum of 4 + 3 = 7.<br>
- Node 1 is the twin of node 2 having a twin sum of 2 + 2 = 4.<br>
Thus, the maximum twin sum of the linked list is max(7, 4) = 7.</p>


### [Example 3]

**Input**: `head = [1,100000]`

**Output**: `100001`

**Explanation**: 

<p>There is only one node with a twin in the linked list having twin sum of 1 + 100000 = 100001.</p>


### [Constraints]

- The number of nodes in the list is an **even** integer in the range `[2, 10^5]`.
- `1 <= Node.val <= 10^5`

### [Hints]

<details>
  <summary>Hint 1</summary>
  How can "reversing" a part of the linked list help find the answer?

  
</details>

<details>
  <summary>Hint 2</summary>
  We know that the twin of the i-th node is the (n-1-i)-th node. If we reverse the second half of the linked list, the twin of the i-th node will be the i-th node in the reversed second half.

  
</details>

<details>
  <summary>Hint 3</summary>
  How can two pointers be used to find every twin sum optimally?

  
</details>

<details>
  <summary>Hint 4</summary>
  Use two different pointers pointing to the first nodes of the two halves of the linked list. The second pointer will point to the first node of the reversed half, which is the (n-1-i)th node in the original linked list. By moving both pointers forward at the same time, we find all twin sums.

  
</details>

## Intuition

The problem asks us to find the maximum sum of twin nodes in a linked list. The twin of the `i`-th node is the `(n - 1 - i)`-th node. 

In a standard array, we could easily compute the sum using two pointers starting from both ends (`arr[i] + arr[n - 1 - i]`). However, linked lists do not support random access, nor do they allow traversing backward.

To solve this efficiently without using extra space (like storing values in an array or stack), we can use the **Fast and Slow Pointers** technique combined with **Linked List Reversal**:
1. By using a slow pointer and a fast pointer, we can locate the exact middle of the linked list. Since the list has an even number of nodes, the slow pointer will naturally land on the start of the second half.
2. By reversing the second half of the linked list in place, the `(n - 1 - i)`-th node will line up perfectly with the `i`-th node when we iterate from the start of the first half and the start of the reversed second half.
3. We then simply traverse both halves simultaneously, computing the sum for each twin pair and keeping track of the maximum sum observed.

## Step-by-Step Solution

1. **Find the Middle:** Initialize two pointers, `slow` and `fast`, both starting at the `head`. Move `slow` one step at a time and `fast` two steps at a time. When `fast` reaches the end of the list, `slow` will be exactly at the beginning of the second half.
2. **Reverse the Second Half:** Starting from the `slow` pointer, reverse the remaining nodes. Use three pointers (`prev`, `curr`, `nextNode`) to perform the reversal. After this loop, `prev` will be the head of the reversed second half.
3. **Calculate Twin Sums:** Initialize a pointer `firstHalf` at the original `head`, and a pointer `secondHalf` at `prev` (the head of the reversed second half).
4. Iterate while `secondHalf` is not null:
   - Compute `currentSum = firstHalf.val + secondHalf.val`.
   - Update `maxSum = max(maxSum, currentSum)`.
   - Move both `firstHalf` and `secondHalf` one step forward.
5. Return the `maxSum`.

## Complexity

> - **Time Complexity:** `O(n)`. We make one pass to find the middle `O(n/2)`, one pass to reverse the second half `O(n/2)`, and one pass to compute the sums `O(n/2)`. Overall time complexity is linear `O(n)`.
- **Space Complexity:** `O(1)`. We only use a few extra pointers (`slow`, `fast`, `prev`, `curr`, etc.) for our operations, making the algorithm run in strictly constant extra space.

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
    def pairSum(self, head: Optional[ListNode]) -> int:
        # Step 1: Find the middle of the linked list using slow and fast pointers.
        slow = head
        fast = head
        while fast and fast.next:
            slow = slow.next          # moves 1 step
            fast = fast.next.next     # moves 2 steps
            
        # Step 2: Reverse the second half of the linked list.
        # slow is currently at the beginning of the second half.
        prev = None
        curr = slow
        while curr:
            next_node = curr.next     # temporarily store the next node
            curr.next = prev          # reverse the link
            prev = curr               # move prev forward
            curr = next_node          # move curr forward
            
        # Step 3: Iterate through both halves and calculate the twin sums.
        max_twin_sum = 0
        first_half = head
        second_half = prev            # prev is now the head of the reversed second half
        
        while second_half:
            # The twin sum is the sum of the corresponding nodes from both halves
            current_sum = first_half.val + second_half.val
            max_twin_sum = max(max_twin_sum, current_sum)
            
            # Move both pointers forward
            first_half = first_half.next
            second_half = second_half.next
            
        return max_twin_sum
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
    public int pairSum(ListNode head) {
        // 1. Find the middle of the linked list
        ListNode slow = head;
        ListNode fast = head;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        // 2. Reverse the second half of the list
        // slow is pointing to the start of the second half
        ListNode prev = null;
        ListNode curr = slow;
        
        while (curr != null) {
            ListNode nextNode = curr.next; // store the next node
            curr.next = prev;              // reverse the link
            prev = curr;                   // move prev to current node
            curr = nextNode;               // advance curr
        }
        
        // 3. Compute maximum twin sum
        // prev now points to the head of the reversed second half
        ListNode firstHalf = head;
        ListNode secondHalf = prev;
        int maxTwinSum = 0;
        
        while (secondHalf != null) {
            // calculate the twin sum for the current pair
            int currentSum = firstHalf.val + secondHalf.val;
            maxTwinSum = Math.max(maxTwinSum, currentSum);
            
            // advance both pointers
            firstHalf = firstHalf.next;
            secondHalf = secondHalf.next;
        }
        
        return maxTwinSum;
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
 * @return {number}
 */
var pairSum = function(head) {
    // Step 1: Use fast and slow pointers to find the midpoint
    let slow = head;
    let fast = head;
    
    while (fast !== null && fast.next !== null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    
    // Step 2: Reverse the second half of the linked list
    // Starting from 'slow', we flip the direction of the next pointers
    let prev = null;
    let curr = slow;
    
    while (curr !== null) {
        let nextNode = curr.next;
        curr.next = prev;
        prev = curr;
        curr = nextNode;
    }
    
    // Step 3: Find the maximum twin sum
    // 'prev' is the head of the reversed second half
    let firstHalf = head;
    let secondHalf = prev;
    let maxTwinSum = 0;
    
    while (secondHalf !== null) {
        let currentSum = firstHalf.val + secondHalf.val;
        maxTwinSum = Math.max(maxTwinSum, currentSum);
        
        firstHalf = firstHalf.next;
        secondHalf = secondHalf.next;
    }
    
    return maxTwinSum;
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
    int pairSum(ListNode* head) {
        // Step 1: Find the middle using fast and slow pointers
        ListNode* slow = head;
        ListNode* fast = head;
        
        while (fast != nullptr && fast->next != nullptr) {
            slow = slow->next;
            fast = fast->next->next;
        }
        
        // Step 2: Reverse the second half
        ListNode* prev = nullptr;
        ListNode* curr = slow;
        
        while (curr != nullptr) {
            ListNode* nextNode = curr->next;
            curr->next = prev;
            prev = curr;
            curr = nextNode;
        }
        
        // Step 3: Calculate twin sums and find the maximum
        ListNode* firstHalf = head;
        ListNode* secondHalf = prev;
        int maxTwinSum = 0;
        
        while (secondHalf != nullptr) {
            int currentSum = firstHalf->val + secondHalf->val;
            maxTwinSum = max(maxTwinSum, currentSum);
            
            firstHalf = firstHalf->next;
            secondHalf = secondHalf->next;
        }
        
        return maxTwinSum;
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
    public int PairSum(ListNode head) {
        // 1. Get to the middle of the linked list
        ListNode slow = head;
        ListNode fast = head;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        // 2. Reverse the second half
        ListNode prev = null;
        ListNode curr = slow;
        
        while (curr != null) {
            ListNode nextNode = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextNode;
        }
        
        // 3. Evaluate max twin sum
        ListNode firstHalf = head;
        ListNode secondHalf = prev;
        int maxTwinSum = 0;
        
        while (secondHalf != null) {
            int currentSum = firstHalf.val + secondHalf.val;
            maxTwinSum = Math.Max(maxTwinSum, currentSum);
            
            firstHalf = firstHalf.next;
            secondHalf = secondHalf.next;
        }
        
        return maxTwinSum;
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
func pairSum(head *ListNode) int {
    // Phase 1: Locate the midpoint
    slow, fast := head, head
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
    }
    
    // Phase 2: Reverse the list from the midpoint onwards
    var prev *ListNode
    curr := slow
    for curr != nil {
        nextNode := curr.Next
        curr.Next = prev
        prev = curr
        curr = nextNode
    }
    
    // Phase 3: Traverse the original first half and the reversed second half
    firstHalf := head
    secondHalf := prev
    maxTwinSum := 0
    
    for secondHalf != nil {
        currentSum := firstHalf.Val + secondHalf.Val
        if currentSum > maxTwinSum {
            maxTwinSum = currentSum
        }
        
        firstHalf = firstHalf.Next
        secondHalf = secondHalf.Next
    }
    
    return maxTwinSum
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
# @return {Integer}
def pair_sum(head)
    # 1. Use fast and slow pointers to locate the middle of the list
    slow = head
    fast = head
    
    while fast && fast.next
        slow = slow.next
        fast = fast.next.next
    end
    
    # 2. Reverse the second half (starting from slow)
    prev = nil
    curr = slow
    
    while curr
        next_node = curr.next
        curr.next = prev
        prev = curr
        curr = next_node
    end
    
    # 3. Find the maximum twin sum
    max_twin_sum = 0
    first_half = head
    second_half = prev
    
    while second_half
        current_sum = first_half.val + second_half.val
        max_twin_sum = current_sum if current_sum > max_twin_sum
        
        first_half = first_half.next
        second_half = second_half.next
    end
    
    max_twin_sum
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
    pub fn pair_sum(head: Option<Box<ListNode>>) -> i32 {
        // Due to ownership and borrowing rules in Rust, 
        // linked lists are often easier to process by extracting values to a Vec.
        // This converts the O(1) space to O(N), but simplifies the implementation.
        // It remains O(N) time complexity.
        
        let mut values = Vec::new();
        let mut curr = head;
        
        // Extract all node values
        while let Some(node) = curr {
            values.push(node.val);
            curr = node.next;
        }
        
        let mut max_twin_sum = 0;
        let n = values.len();
        
        // Calculate the sum of the twins
        for i in 0..(n / 2) {
            let twin_sum = values[i] + values[n - 1 - i];
            if twin_sum > max_twin_sum {
                max_twin_sum = twin_sum;
            }
        }
        
        max_twin_sum
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
    fun pairSum(head: ListNode?): Int {
        // Step 1: Find the middle
        var slow: ListNode? = head
        var fast: ListNode? = head
        
        while (fast != null && fast.next != null) {
            slow = slow?.next
            fast = fast.next?.next
        }
        
        // Step 2: Reverse the second half of the list
        var prev: ListNode? = null
        var curr: ListNode? = slow
        
        while (curr != null) {
            val nextNode = curr.next
            curr.next = prev
            prev = curr
            curr = nextNode
        }
        
        // Step 3: Compute maximum twin sum
        var firstHalf: ListNode? = head
        var secondHalf: ListNode? = prev
        var maxTwinSum = 0
        
        while (secondHalf != null) {
            // Because constraints guarantee values exist, we can use !! safely
            val currentSum = firstHalf!!.`val` + secondHalf.`val`
            if (currentSum > maxTwinSum) {
                maxTwinSum = currentSum
            }
            
            firstHalf = firstHalf.next
            secondHalf = secondHalf.next
        }
        
        return maxTwinSum
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
    func pairSum(_ head: ListNode?) -> Int {
        // Find the middle using fast and slow pointers
        var slow = head
        var fast = head
        
        while fast != nil && fast?.next != nil {
            slow = slow?.next
            fast = fast?.next?.next
        }
        
        // Reverse the second half
        var prev: ListNode? = nil
        var curr = slow
        
        while curr != nil {
            let nextNode = curr?.next
            curr?.next = prev
            prev = curr
            curr = nextNode
        }
        
        // Find the max twin sum
        var firstHalf = head
        var secondHalf = prev
        var maxTwinSum = 0
        
        while secondHalf != nil {
            // Safely unwrap as we know the structure guarantees parallel nodes
            let currentSum = (firstHalf?.val ?? 0) + (secondHalf?.val ?? 0)
            maxTwinSum = max(maxTwinSum, currentSum)
            
            firstHalf = firstHalf?.next
            secondHalf = secondHalf?.next
        }
        
        return maxTwinSum
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

Visit original link: [2130. Maximum Twin Sum of a Linked List - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/2130-maximum-twin-sum-of-a-linked-list) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

