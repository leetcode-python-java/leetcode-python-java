# 19. 删除链表的倒数第 N 个结点 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
> 我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 Show.dev 打造你的个人品牌 →**](https://www.show.dev)

---

访问原文链接：[19. 删除链表的倒数第 N 个结点 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/19-remove-nth-node-from-end-of-list)，体验更佳！

力扣链接：[19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list), 难度等级：**中等**。

## LeetCode “19. 删除链表的倒数第 N 个结点”问题描述

给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

### [示例 1]

![](../../images/examples/19_1.jpg)

**输入**: `head = [1,2,3,4,5], n = 2`

**输出**: `[1,2,3,5]`

### [示例 2]

**输入**: `head = [1], n = 1`

**输出**: `[]`

### [示例 3]

**输入**: `head = [1,2], n = 1`

**输出**: `[1]`

### [约束]

- 链表中结点的数目为 `sz`
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

### [Hints]

<details>
  <summary>提示 1</summary>
  Maintain two pointers and update one with a delay of n steps.

  
</details>

## 思路

1. 删除链表的倒数第 `N` 个结点，等同于删除链表的正数第 `node_count - N` 个结点。
2. 先求出`node_count`。
3. 在 `index == node_count - N` 时，进行删除节点操作：`node.next = node.next.next`。
4. 由于删除的节点可能是 `head`，所以使用虚拟节点 `dummy_node`，方便统一处理。

## 步骤

1. 求出`node_count`。

    ```ruby
    node_count = 0
    node = head
	
    while node
      node_count += 1
      node = node.next
    end
    ```

2. 在 `index == node_count - N`时，进行删除节点操作：`node.next = node.next.next`。

    ```ruby
    index = 0
    node = head
	
    while node
      if index == node_count - n
        node.next = node.next.next
        break
      end
	
      index += 1
      node = node.next
    end
    ```

3. 由于删除的节点可能是`head`，所以使用虚拟节点`dummy_node`，方便统一处理。

    ```ruby
    dummy_head = ListNode.new # 1
    dummy_head.next = head # 2
    node = dummy_head # 3
	
    # omitted code
	
    return dummy_head.next
    ```

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        var nodeCount = 0;
        var node = head;

        while (node != null) {
            nodeCount++;
            node = node.next;
        }

        var index = 0;
        var dummyHead = new ListNode(0, head);
        node = dummyHead;

        while (node != null) {
            if (index == nodeCount - n) {
                node.next = node.next.next;
                break;
            }

            index++;
            node = node.next;
        }

        return dummyHead.next;
    }
}
```

## Python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        node_count = 0
        node = head

        while node:
            node_count += 1
            node = node.next

        index = 0
        dummy_head = ListNode(next=head)
        node = dummy_head

        while node:
            if index == node_count - n:
                node.next = node.next.next
                break

            index += 1
            node = node.next

        return dummy_head.next
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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        auto node_count = 0;
        auto node = head;

        while (node != nullptr) {
            node_count += 1;
            node = node->next;
        }

        auto index = 0;
        auto dummy_head = new ListNode(0, head);
        node = dummy_head;

        for (auto i = 0; i < node_count - n; i++) {
            node = node->next;
        }

        auto target_node = node->next;
        node->next = node->next->next;
        delete target_node;

        auto result = dummy_head->next;
        delete dummy_head;
        return result;
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
var removeNthFromEnd = function (head, n) {
  let nodeCount = 0
  let node = head

  while (node != null) {
    nodeCount++
    node = node.next
  }

  let index = 0
  let dummyHead = new ListNode(0, head)
  node = dummyHead

  while (node != null) {
    if (index == nodeCount - n) {
        node.next = node.next.next
        break
    }

    index++
    node = node.next
  }

  return dummyHead.next
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
public class Solution
{
    public ListNode RemoveNthFromEnd(ListNode head, int n)
    {
        int nodeCount = 0;
        var node = head;

        while (node != null)
        {
            nodeCount++;
            node = node.next;
        }

        int index = 0;
        var dummyHead = new ListNode(0, head);
        node = dummyHead;

        while (node != null)
        {
            if (index == nodeCount - n)
            {
                node.next = node.next.next;
                break;
            }

            index++;
            node = node.next;
        }

        return dummyHead.next;
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
func removeNthFromEnd(head *ListNode, n int) *ListNode {
    nodeCount := 0
    node := head

    for node != nil {
        nodeCount++
        node = node.Next
    }

    index := 0
    dummyHead := &ListNode{0, head}
    node = dummyHead

    for node != nil {
        if index == nodeCount - n {
            node.Next = node.Next.Next
            break
        }

        index++
        node = node.Next
    }

    return dummyHead.Next
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

def remove_nth_from_end(head, n)
  node_count = 0
  node = head

  while node
    node_count += 1
    node = node.next
  end

  index = 0
  dummy_head = ListNode.new(0, head)
  node = dummy_head

  while node
    if index == node_count - n
      node.next = node.next.next
      break
    end

    index += 1
    node = node.next
  end

  dummy_head.next
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
> 我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 Show.dev 打造你的个人品牌 →**](https://www.show.dev)

---

访问原文链接：[19. 删除链表的倒数第 N 个结点 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/19-remove-nth-node-from-end-of-list)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

