# 160. 相交链表 - 力扣Python/Java/C++等题解

访问原文链接：[160. 相交链表 - 力扣Python/Java/C++等题解](https://leetcodepython.com/zh/leetcode/160-intersection-of-two-linked-lists)，体验更佳！

力扣链接：[160. 相交链表](https://leetcode.cn/problems/intersection-of-two-linked-lists), 难度：**简单**。

## LeetCode “160. 相交链表”问题描述

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
- `1 <= m, n <= 3 * 10^4`
- `1 <= Node.val <= 10^5`

 <br>
**进阶**：你能否设计一个时间复杂度 `O(m + n)` 、仅用 `O(1)` 内存的解决方案？

## 思路

这是一个典型的“相遇”问题，最好转化为现实的场景去加强理解。

假设你是A，B是你追求的对象，终点是学校。在上学的路上，靠后面的路程是你们都要经过的，靠前面的路程是各走各的。节点间距假定为一公里。

现在，某个早晨，你们同时都吃完了早饭，要骑车去学校了。而你有个目标：和B相遇，聊上几句，你会怎么做？(以示例一为例)

<details><summary>点击查看答案</summary><p>你一定是先测算出她家比你家到学校远多少公里，然后**等她走完这些公里后，再出发**。这样就一定能相遇。相遇的节点就是答案。

1. 先把A, B两个链表的节点数计算出来。链表A的节点数为`node_count_a`，链表B的节点数为`node_count_b`。
2. 假如`node_count_b > node_count_a`，那么对链表B做`node_count_b - node_count_a`次`node = node.next` 操作。
3. 这时，两个链表同时重复进行`node = node.next`操作，直到找到相同的节点或者其中一个链表已经到尾部。
</p></details>

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

- 时间复杂度: `O(m + n)`.
- 空间复杂度: `O(1)`.

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

```csharp
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

## Ruby

```ruby
# Definition for singly-linked list.
# class ListNode
#   attr_accessor :val, :next
#   def initialize(val)
#     @val = val
#     @next = nil
#   end
# end

# @param {ListNode} head_a
# @param {ListNode} head_b
# @return {ListNode}
def getIntersectionNode(head_a, head_b)
  node_count_a = 0
  node_count_b = 0

  node = head_a
  while node
    node_count_a += 1
    node = node.next
  end

  node = head_b
  while node
    node_count_b += 1
    node = node.next
  end

  bigger = head_a
  smaller = head_b

  if node_count_b > node_count_a
    bigger = head_b
    smaller = head_a
  end

  (node_count_b - node_count_a).abs.times do
    bigger = bigger.next
  end

  while bigger && smaller
    return bigger if bigger == smaller

    bigger = bigger.next
    smaller = smaller.next
  end

  nil
end
```

## C++

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *head_a, ListNode *head_b) {
        int node_count_a = 0;
        int node_count_b = 0;
        
        ListNode *node = head_a;
        while (node) {
            node_count_a += 1;
            node = node->next;
        }
        
        node = head_b;
        while (node) {
            node_count_b += 1;
            node = node->next;
        }
        
        ListNode *bigger = head_a;
        ListNode *smaller = head_b;
        
        if (node_count_b > node_count_a) {
            bigger = head_b;
            smaller = head_a;
        }
        
        for (int i = 0; i < abs(node_count_b - node_count_a); i++) {
            bigger = bigger->next;
        }
        
        while (bigger && smaller) {
            if (bigger == smaller) {
                return bigger;
            }
            
            bigger = bigger->next;
            smaller = smaller->next;
        }
        
        return nullptr;
    }
};
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
func getIntersectionNode(headA, headB *ListNode) *ListNode {
    nodeCountA := 0
    nodeCountB := 0

    node := headA
    for node != nil {
        nodeCountA++
        node = node.Next
    }

    node = headB
    for node != nil {
        nodeCountB++
        node = node.Next
    }

    bigger := headA
    smaller := headB

    if nodeCountB > nodeCountA {
        bigger = headB
        smaller = headA
    }

    difference := nodeCountB - nodeCountA
    if difference < 0 {
        difference = -difference
    }

    for i := 0; i < difference; i++ {
        bigger = bigger.Next
    }

    for bigger != nil && smaller != nil {
        if bigger == smaller {
            return bigger
        }
        bigger = bigger.Next
        smaller = smaller.Next
    }

    return nil
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCodePython.com](https://leetcodepython.com/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[160. 相交链表 - 力扣Python/Java/C++等题解](https://leetcodepython.com/zh/leetcode/160-intersection-of-two-linked-lists).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

