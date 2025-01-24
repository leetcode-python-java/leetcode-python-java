# 160. Intersection of Two Linked Lists - Best Practices of LeetCode Solutions
LeetCode link: [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists),
[160. 相交链表](https://leetcode.cn/problems/intersection-of-two-linked-lists)

[中文题解](#中文题解)

## LeetCode problem description
Given the heads of two singly linked-lists `headA` and `headB`, return _the node at which the two lists intersect_. If the two linked lists have no intersection at all, return `null`.

For example, the following two linked lists begin to intersect at node `c1`:

![](../../images/examples/160.png)

The test cases are generated such that there are **no cycles** anywhere in the entire linked structure.

**Note** that the linked lists must **retain their original structure** after the function returns.

Difficulty: **Easy**

### [Example 1]
![](../../images/examples/160_1.png)

**Input**: `listA = [4,1,8,4,5], listB = [5,6,1,8,4,5]`

**Output**: `Intersected at '8'`

### [Example 2]
![](../../images/examples/160_3.png)

**Input**: `listA = [2,6,4], listB = [1,5]`

**Output**: `No intersection`

### [Constraints]
- The number of nodes of `listA` is in the `m`.
- The number of nodes of `listB` is in the `n`.
- `1 <= m, n <= 3 * 10000`
- `1 <= Node.val <= 100000`

**Follow up**: Could you write a solution that runs in `O(m + n)` time and use only `O(1)` memory?

## Intuition
[中文题解](#中文题解)

1. First calculate the number of nodes in the two linked lists A and B. The number of nodes in linked list A is `node_count_a`, and the number of nodes in linked list B is `node_count_b`.
2. If `node_count_b > node_count_a`, then perform `node = node.next` for `node_count_b - node_count_a` times on linked list B.
3. At this time, repeat `node = node.next` on the two linked lists until the same node is found or one of the linked lists has reached the end.

## Steps
1. First calculate the number of nodes in the two linked lists A and B. The number of nodes in linked list A is `node_count_a`, and the number of nodes in linked list B is `node_count_b`.
```python
node_count_a = 0
node_count_b = 0

node = headA
while node:
    node_count_a += 1
    node = node.next
```

2. If `node_count_b > node_count_a`, then perform `node = node.next` for `node_count_b - node_count_a` times on linked list B.
```python
bigger = headA
smaller = headB

if node_count_b > node_count_a:
    bigger = headB
    smaller = headA

for _ in range(abs(node_count_b - node_count_a)):
    bigger = bigger.next
```

3. At this time, repeat `node = node.next` on the two linked lists until the same node is found or one of the linked lists has reached the end.
```python
while bigger and smaller:
    if bigger == smaller:
        return bigger

    bigger = bigger.next
    smaller = smaller.next

return None
```

## Complexity
* Time: `O(m + n)`.
* Space: `O(1)`.

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

## 问题描述
给你两个单链表的头节点 `headA` 和 `headB` ，请你找出并返回两个单链表相交的起始节点。如果两个链表不存在相交节点，返回 `null` 。

图示两个链表在节点 `c1` 开始相交：

![](../../images/examples/160.png)

题目数据 **保证** 整个链式结构中**不存在环**。

**注意**，函数返回结果后，链表必须 **保持其原始结构** 。

难度: **容易**

### [Example 1]
![](../../images/examples/160_1.png)

**输入**: `listA = [4,1,8,4,5], listB = [5,6,1,8,4,5]`

**输出**: `Intersected at '8'`

# 中文题解
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
