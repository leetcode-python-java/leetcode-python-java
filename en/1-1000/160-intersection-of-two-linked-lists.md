# 160. Intersection of Two Linked Lists - Best Practices of LeetCode Solutions
LeetCode link: [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists), difficulty: **Easy**.

## LeetCode description of "160. Intersection of Two Linked Lists"
Given the heads of two singly linked-lists `headA` and `headB`, return _the node at which the two lists intersect_. If the two linked lists have no intersection at all, return `null`.

For example, the following two linked lists begin to intersect at node `c1`:

![](../../images/examples/160.png)

The test cases are generated such that there are **no cycles** anywhere in the entire linked structure.

**Note** that the linked lists must **retain their original structure** after the function returns.

### [Example 1]
![](../../images/examples/160_1.png)

**Input**: `listA = [4,1,8,4,5], listB = [5,6,1,8,4,5]`

**Output**: `Intersected at '8'`

### [Example 2]
![](../../images/examples/160_2.png)

**Input**: `intersectVal = 2, listA = [1,9,1,2,4], listB = [3,2,4]`

**Output**: `Intersected at '2'`

### [Example 3]
![](../../images/examples/160_3.png)

**Input**: `listA = [2,6,4], listB = [1,5]`

**Output**: `No intersection`

### [Constraints]
- The number of nodes of `listA` is in the `m`.
- The number of nodes of `listB` is in the `n`.
- `1 <= m, n <= 3 * 10^4`
- `1 <= Node.val <= 10^5`

**Follow up**: Could you write a solution that runs in `O(m + n)` time and use only `O(1)` memory?

## Intuition
This is a typical "encounter" problem, and it is best to transform it into a real-life scenario to enhance understanding.

Suppose you are A, and you are pursuing B. The destination is school. On the way to school, the distance at the back is what you both have to go through, and the distance at the front is for each of you to go your own way. The node spacing is assumed to be one kilometer.

Now, one morning, you both finished breakfast at the same time and are going to ride your bike to school. And you have a goal: to meet B and chat with him/her for a few words. What will you do? (Take Example 1 as an example)

You must first calculate how many kilometers her home is farther from the school than your home, and then wait for her to walk these kilometers before setting off. As long as you have the same speed, you will definitely meet, and the node where you meet is the answer.

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
