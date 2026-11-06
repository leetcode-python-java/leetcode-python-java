# 2130. 链表最大孪生和 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 coder.id 打造你的开发者个人IP →**](https://www.coder.id)

访问原文链接：[2130. 链表最大孪生和 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/2130-maximum-twin-sum-of-a-linked-list)，体验更佳！

力扣链接：[2130. 链表最大孪生和](https://leetcode.cn/problems/maximum-twin-sum-of-a-linked-list), 难度等级：**中等**。

## LeetCode “2130. 链表最大孪生和”问题描述

在一个大小为 `n` 且 `n` 为 **偶数** 的链表中，对于 `0 <= i <= (n / 2) - 1` 的 `i` ，第 `i` 个节点（下标从 **0** 开始）的孪生节点为第 `(n-1-i)` 个节点 。

- 比方说，如果 `n = 4` ，那么节点 `0` 是节点 `3` 的孪生节点，节点 `1` 是节点 `2` 的孪生节点。这是长度为 `n = 4` 的链表中所有的孪生节点。

**孪生和** 定义为一个节点和它孪生节点两者值之和。

给你一个长度为偶数的链表的头节点 `head` ，请你返回链表的 **最大孪生和** 。

### [示例 1]

**输入**: `head = [5,4,2,1]`

**输出**: `6`

**解释**: 

<p>节点 0 和节点 1 分别是节点 3 和 2 的孪生节点。孪生和都为 6 。<br>
链表中没有其他孪生节点。<br>
所以，链表的最大孪生和是 6 。</p>


### [示例 2]

**输入**: `head = [4,2,2,3]`

**输出**: `7`

**解释**: 

<p>链表中的孪生节点为：<br>
- 节点 0 是节点 3 的孪生节点，孪生和为 4 + 3 = 7 。<br>
- 节点 1 是节点 2 的孪生节点，孪生和为 2 + 2 = 4 。<br>
所以，最大孪生和为 max(7, 4) = 7 。</p>


### [示例 3]

**输入**: `head = [1,100000]`

**输出**: `100001`

**解释**: `链表中只有一对孪生节点，孪生和为 1 + 100000 = 100001 。`

### [约束]

- 链表的节点数目是 `[2, 10^5]` 范围内的 **偶数** 。
- `1 <= Node.val <= 10^5`

### [Hints]

<details>
  <summary>提示 1</summary>
  How can "reversing" a part of the linked list help find the answer?

  
</details>

<details>
  <summary>提示 2</summary>
  We know that the twin of the i-th node is the (n-1-i)-th node. If we reverse the second half of the linked list, the twin of the i-th node will be the i-th node in the reversed second half.

  
</details>

<details>
  <summary>提示 3</summary>
  How can two pointers be used to find every twin sum optimally?

  
</details>

<details>
  <summary>提示 4</summary>
  Use two different pointers pointing to the first nodes of the two halves of the linked list. The second pointer will point to the first node of the reversed half, which is the (n-1-i)th node in the original linked list. By moving both pointers forward at the same time, we find all twin sums.

  
</details>

## 思路

题目要求我们在链表中寻找最大孪生和。第 `i` 个节点的孪生节点是第 `(n - 1 - i)` 个节点。

如果是普通的数组，我们可以很容易地用两个分别从首尾出发的指针来计算和（`arr[i] + arr[n - 1 - i]`）。但是，链表不支持随机访问，也不支持反向遍历。

为了在不使用额外空间（比如将值存入数组或栈）的情况下高效解决这个问题，我们可以结合使用 **快慢指针** 和 **反转链表** 技巧：
1. 通过快慢指针，我们可以定位到链表的正中间。因为链表节点数为偶数，慢指针会自然停在后半部分的起始位置。
2. 将链表的后半部分进行原地反转后，当我们同时从前半部分起点和反转后的后半部分起点遍历时，第 `(n - 1 - i)` 个节点就会刚好与第 `i` 个节点对齐。
3. 接着，我们只需同时遍历这两个部分，计算每一对孪生节点的和，并记录观察到的最大值即可。

## 步骤

1. **寻找中间节点：** 初始化两个指针 `slow` 和 `fast`，都从 `head` 开始。`slow` 每次走一步，`fast` 每次走两步。当 `fast` 到达链表末尾时，`slow` 刚好停在后半部分的开头。
2. **反转后半部分：** 从 `slow` 指针开始，反转剩下的节点。使用三个指针（`prev`、`curr`、`nextNode`）来执行反转操作。循环结束后，`prev` 将指向反转后的后半部分的头节点。
3. **计算孪生和：** 初始化指针 `firstHalf` 指向原链表的 `head`，指针 `secondHalf` 指向 `prev`（即反转后的后半部分的头节点）。
4. 当 `secondHalf` 不为空时循环：
   - 计算 `currentSum = firstHalf.val + secondHalf.val`。
   - 更新 `maxSum = max(maxSum, currentSum)`。
   - 将 `firstHalf` 和 `secondHalf` 都向前移动一步。
5. 返回 `maxSum`。

## 复杂度

> - **时间复杂度：** `O(n)`。我们遍历一次找到中点耗时 `O(n/2)`，遍历一次反转后半部分耗时 `O(n/2)`，最后遍历一次计算和耗时 `O(n/2)`。总体时间复杂度是线性的 `O(n)`。
- **空间复杂度：** `O(1)`。在所有操作中，我们只使用了几个额外的指针变量（`slow`、`fast`、`prev`、`curr` 等），因此算法只需要严格的常数级额外空间。

- 时间复杂度: ``.
- 空间复杂度: ``.

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

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**coder.id**](https://www.coder.id) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.coder.id`，极具职业含金量的专属域名。

>
> [**立即前往 coder.id 打造你的个人品牌 →**](https://www.coder.id)

---

访问原文链接：[2130. 链表最大孪生和 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/2130-maximum-twin-sum-of-a-linked-list)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

