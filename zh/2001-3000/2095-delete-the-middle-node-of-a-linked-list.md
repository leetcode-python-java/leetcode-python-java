# 2095. 删除链表的中间节点 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 coder.id 打造你的开发者个人IP →**](https://www.coder.id)

访问原文链接：[2095. 删除链表的中间节点 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/2095-delete-the-middle-node-of-a-linked-list)，体验更佳！

力扣链接：[2095. 删除链表的中间节点](https://leetcode.cn/problems/delete-the-middle-node-of-a-linked-list), 难度等级：**中等**。

## LeetCode “2095. 删除链表的中间节点”问题描述

给你一个链表的头节点 `head` 。**删除** 链表的 **中间节点** ，并返回修改后的链表的头节点 `head` 。

长度为 `n` 链表的中间节点是从头数起第 `⌊n / 2⌋` 个节点（下标从 **0** 开始），其中 `⌊x⌋` 表示小于或等于 `x` 的最大整数。

- 对于 `n` = `1`、`2`、`3`、`4` 和 `5` 的情况，中间节点的下标分别是 `0`、`1`、`1`、`2` 和 `2` 。

### [示例 1]

**输入**: `head = [1,3,4,7,1,2,6]`

**输出**: `[1,3,4,1,2,6]`

**解释**: 

<p>上图表示给出的链表。节点的下标分别标注在每个节点的下方。<br>
由于 n = 7 ，值为 7 的节点 3 是中间节点，用红色标注。<br>
返回结果为移除节点后的新链表。</p>


### [示例 2]

**输入**: `head = [1,2,3,4]`

**输出**: `[1,2,4]`

**解释**: 

<p>上图表示给出的链表。<br>
对于 n = 4 ，值为 3 的节点 2 是中间节点，用红色标注。</p>


### [示例 3]

**输入**: `head = [2,1]`

**输出**: `[2]`

**解释**: 

<p>上图表示给出的链表。<br>
对于 n = 2 ，值为 1 的节点 1 是中间节点，用红色标注。<br>
值为 2 的节点 0 是移除节点 1 后剩下的唯一一个节点。</p>


### [示例 4]

**输入**: `head = [1,3,4,7,1,2,6]`

**输出**: `[1,3,4,1,2,6]`

**解释**: 

<p>上图表示给出的链表。节点的下标分别标注在每个节点的下方。<br>
由于 n = 7 ，值为 7 的节点 3 是中间节点，用红色标注。<br>
返回结果为移除节点后的新链表。</p>


### [示例 5]

**输入**: `head = [1,2,3,4]`

**输出**: `[1,2,4]`

**解释**: 

<p>上图表示给出的链表。<br>
对于 n = 4 ，值为 3 的节点 2 是中间节点，用红色标注。</p>


### [示例 6]

**输入**: `head = [2,1]`

**输出**: `[2]`

**解释**: 

<p>上图表示给出的链表。<br>
对于 n = 2 ，值为 1 的节点 1 是中间节点，用红色标注。<br>
值为 2 的节点 0 是移除节点 1 后剩下的唯一一个节点。</p>


### [示例 7]

**输入**: `head = [1,3,4,7,1,2,6]`

**输出**: `[1,3,4,1,2,6]`

**解释**: 

<p>上图表示给出的链表。节点的下标分别标注在每个节点的下方。<br>
由于 n = 7 ，值为 7 的节点 3 是中间节点，用红色标注。<br>
返回结果为移除节点后的新链表。</p>


### [示例 8]

**输入**: `head = [1,2,3,4]`

**输出**: `[1,2,4]`

**解释**: 

<p>上图表示给出的链表。<br>
对于 n = 4 ，值为 3 的节点 2 是中间节点，用红色标注。</p>


### [示例 9]

**输入**: `head = [2,1]`

**输出**: `[2]`

**解释**: 

<p>上图表示给出的链表。<br>
对于 n = 2 ，值为 1 的节点 1 是中间节点，用红色标注。<br>
值为 2 的节点 0 是移除节点 1 后剩下的唯一一个节点。</p>


### [约束]

- 链表中节点的数目在范围 `[1, 10^5]` 内
- `1 <= Node.val <= 10^5`

### [Hints]

<details>
  <summary>提示 1</summary>
  If a point with a speed s moves n units in a given time, a point with speed 2 * s will move 2 * n units at the same time. Can you use this to find the middle node of a linked list?

  
</details>

<details>
  <summary>提示 2</summary>
  If you are given the middle node, the node before it, and the node after it, how can you modify the linked list?

  
</details>

<details>
  <summary>提示 3</summary>
  If a point with a speed s moves n units in a given time, a point with speed 2 * s will move 2 * n units at the same time. Can you use this to find the middle node of a linked list?

  
</details>

<details>
  <summary>提示 4</summary>
  If you are given the middle node, the node before it, and the node after it, how can you modify the linked list?

  
</details>

<details>
  <summary>提示 5</summary>
  If a point with a speed s moves n units in a given time, a point with speed 2 * s will move 2 * n units at the same time. Can you use this to find the middle node of a linked list?

  
</details>

<details>
  <summary>提示 6</summary>
  If you are given the middle node, the node before it, and the node after it, how can you modify the linked list?

  
</details>

## 思路

要单次遍历删除链表的中间节点，我们可以使用经典的 **快慢指针** 方法（也称为龟兔赛跑算法）。

当我们在链表中移动两个指针时：
- **慢指针 (slow)** 每次移动一步。
- **快指针 (fast)** 每次移动两步。

因为快指针的移动速度恰好是慢指针的两倍，所以当快指针到达链表末尾时，慢指针将正好停在中间节点的位置！

但是，要在单向链表中*删除*一个节点，我们实际上需要修改要删除节点*之前*那个节点的 `next` 指针。因此，我们有两个选择：
1. 维护一个 `previous` 指针紧跟在慢指针后面。
2. 巧妙地初始化指针：我们可以创建一个指向 `head` 的 `dummy` 虚拟头节点，让慢指针从 `dummy` 开始，而快指针从 `head` 开始。这样当 `fast` 到达末尾时，`slow` 就会正好指向中间节点的**前一个**节点。

虚拟头节点的方法非常简洁，并且可以毫不费力地处理边界情况（例如只有一个元素的链表）。

## 步骤

1. **处理边界情况：** 如果链表只有一个节点（`head.next == null`），返回 `null`，因为中间节点就是唯一节点，删除后链表为空。（我们也可以使用虚拟节点统一处理）。
2. **初始化虚拟节点：** 创建一个 `dummy` 节点，使其 `dummy.next = head`。
3. **初始化指针：** 设置 `slow = dummy`，`fast = head`。
4. **遍历链表：** 当 `fast != null` 且 `fast.next != null` 时循环。
   - `slow` 移动一步：`slow = slow.next`。
   - `fast` 移动两步：`fast = fast.next.next`。
5. **删除中间节点：** 循环结束时，`slow` 正好指向中间节点的前一个节点。通过 `slow.next = slow.next.next` 绕过中间节点即可将其删除。
6. **返回结果：** 返回 `dummy.next`（即修改后链表的新头节点）。

## 复杂度

> - **时间复杂度：** `O(N)`
  我们使用快指针遍历链表。快指针需要走 `N / 2` 步到达末尾。因为每一步都是常数时间操作，所以总的时间复杂度是线性的。
- **空间复杂度：** `O(1)`
  无论链表多长，我们只使用了三个额外的指针（`dummy`、`slow`、`fast`）。因此，空间复杂度是严格的常数级。

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

访问原文链接：[2095. 删除链表的中间节点 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/2095-delete-the-middle-node-of-a-linked-list)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

