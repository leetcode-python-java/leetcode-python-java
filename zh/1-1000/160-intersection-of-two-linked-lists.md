# 160. 相交链表 - 力扣题解最佳实践
力扣链接：[160. 相交链表](https://leetcode.cn/problems/intersection-of-two-linked-lists) ，难度：**简单**。

## 力扣“160. 相交链表”问题描述
给你两个单链表的头节点 `headA` 和 `headB` ，请你找出并返回两个单链表相交的起始节点。如果两个链表不存在相交节点，返回 `null` 。

图示两个链表在节点 `c1` 开始相交：

![](../../images/examples/160.png)

题目数据 **保证** 整个链式结构中**不存在环**。

**注意**，函数返回结果后，链表必须 **保持其原始结构** 。

### [示例 1]
![](../../images/examples/160_1.png)

**输入**: `listA = [4,1,8,4,5], listB = [5,6,1,8,4,5]`

**输出**: `Intersected at '8'`

### [示例 2]
![](../../images/examples/160_2.png)

**输入**: `intersectVal = 2, listA = [1,9,1,2,4], listB = [3,2,4]`

**输出**: `Intersected at '2'`

### [示例 3]
![](../../images/examples/160_3.png)

**输入**: `listA = [2,6,4], listB = [1,5]`

**输出**: `No intersection`

### [约束]
- `listA` 中节点数目为 `m`
- `listB` 中节点数目为 `n`
- `1 <= m, n <= 3 * 10**4`
- `1 <= Node.val <= 10**5`

**进阶**：你能否设计一个时间复杂度 `O(m + n)` 、仅用 `O(1)` 内存的解决方案？

## 思路
1. 先把A, B两个链表的节点数计算出来。链表A的节点数为`node_count_a`，链表B的节点数为`node_count_b`。
2. 假如`node_count_b > node_count_a`，那么对链表B做`node_count_b - node_count_a`次`node = node.next` 操作。
3. 这时，两个链表同时重复进行`node = node.next`操作，直到找到相同的节点或者其中一个链表已经到尾部。

## 步骤
1. 先把A, B两个链表的节点数计算出来。链表A的节点数为`node_count_a`，链表B的节点数为`node_count_b`。
```python
node_count_a = 0
node_count_b = 0

node = headA
while node:
    node_count_a += 1
    node = node.next
```

2. 假如`node_count_b > node_count_a`，那么对链表B做`node_count_b - node_count_a`次`node = node.next` 操作。
```python
bigger = headA
smaller = headB

if node_count_b > node_count_a:
    bigger = headB
    smaller = headA

for _ in range(abs(node_count_b - node_count_a)):
    bigger = bigger.next
```

3. 这时，两个链表同时重复进行`node = node.next`操作，直到找到相同的节点或者其中一个链表已经到尾部。
```python
while bigger and smaller:
    if bigger == smaller:
        return bigger

    bigger = bigger.next
    smaller = smaller.next

return None
```

## 复杂度
* 时间：`O(m + n)`。
* 空间：`O(1)`。

## Java
```java
/**
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        var nodeCountA = 0;
        var nodeCountB = 0;

        var node = headA;
        while (node != null) {
            nodeCountA += 1;
            node = node.next;
        }

        node = headB;
        while (node != null) {
            nodeCountB += 1;
            node = node.next;
        }

        var bigger = headA;
        var smaller = headB;

        if (nodeCountB > nodeCountA) {
            bigger = headB;
            smaller = headA;
        }

        for (var i = 0; i < Math.abs(nodeCountB - nodeCountA); i++) {
            bigger = bigger.next;
        }

        while (bigger != null && smaller != null) {
            if (bigger == smaller) {
                return bigger;
            }

            bigger = bigger.next;
            smaller = smaller.next;
        }

        return null;
    }
}
```

## Python
```python
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        node_count_a = 0
        node_count_b = 0

        node = headA
        while node:
            node_count_a += 1
            node = node.next

        node = headB
        while node:
            node_count_b += 1
            node = node.next

        bigger = headA
        smaller = headB

        if node_count_b > node_count_a:
            bigger = headB
            smaller = headA

        for _ in range(abs(node_count_b - node_count_a)):
            bigger = bigger.next

        while bigger and smaller:
            if bigger == smaller:
                return bigger

            bigger = bigger.next
            smaller = smaller.next

        return None
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
var getIntersectionNode = function (headA, headB) {
  let nodeCountA = 0
  let nodeCountB = 0

  let node = headA;
  while (node != null) {
    nodeCountA += 1
    node = node.next
  }

  node = headB
  while (node != null) {
    nodeCountB += 1
    node = node.next
  }

  let bigger = headA
  let smaller = headB

  if (nodeCountB > nodeCountA) {
    bigger = headB
    smaller = headA
  }

  for (var i = 0; i < Math.abs(nodeCountB - nodeCountA); i++) {
    bigger = bigger.next
  }

  while (bigger != null && smaller != null) {
    if (bigger == smaller) {
        return bigger
    }

    bigger = bigger.next
    smaller = smaller.next
  }

  return null
};
```

## C#
```c#
/**
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) { val = x; }
 * }
 */
public class Solution
{
    public ListNode GetIntersectionNode(ListNode headA, ListNode headB)
    {
        int nodeCountA = 0;
        int nodeCountB = 0;

        var node = headA;
        while (node != null)
        {
            nodeCountA += 1;
            node = node.next;
        }

        node = headB;
        while (node != null)
        {
            nodeCountB += 1;
            node = node.next;
        }

        var bigger = headA;
        var smaller = headB;

        if (nodeCountB > nodeCountA)
        {
            bigger = headB;
            smaller = headA;
        }

        for (int i = 0; i < Math.Abs(nodeCountB - nodeCountA); i++)
        {
            bigger = bigger.next;
        }

        while (bigger != null && smaller != null)
        {
            if (bigger == smaller)
            {
                return bigger;
            }

            bigger = bigger.next;
            smaller = smaller.next;
        }

        return null;
    }
}
```

## Go
```go
// Welcome to create a PR to complete the code of this language, thanks!
```

## Ruby
```ruby
# Welcome to create a PR to complete the code of this language, thanks!
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
