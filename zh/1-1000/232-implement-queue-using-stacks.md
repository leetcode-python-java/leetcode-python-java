# 232. Implement Queue using Stacks - LeetCode Solution
LeetCode English link: [232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks)

LeetCode Chinese link: [232. 用栈实现队列](https://leetcode.cn/problems/implement-queue-using-stacks)

[中文题解](#中文题解)

## LeetCode problem description
Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (`push`, `peek`, `pop`, and `empty`).

Implement the `MyQueue` class:

- `void push(int x)` Pushes element x to the back of the queue.
- `int pop()` Removes the element from the front of the queue and returns it.
- `int peek()` Returns the element at the front of the queue.
- `boolean empty()` Returns `true` if the queue is empty, `false` otherwise.

**Notes:**

- You must use **only** standard operations of a stack, which means only `push to top`, `peek/pop from top`, `size`, and `is empty` operations are valid.
- Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.

Difficulty: **Easy**

### [Example 1]
**Input**:
```ruby
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
```

**Output**: `[null, null, null, 1, 1, false]`

**Explanation**:
```java
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
```

### [Constraints]
- `1 <= x <= 9`
- At most `100` calls will be made to `push`, `pop`, `peek`, and `empty`.
- All the calls to `pop` and `peek` are valid.

**Follow-up**: Can you implement the queue such that each operation is amortized `O(1)` time complexity? In other words, performing `n` operations will take overall `O(n)` time even if one of those operations may take longer.

## Intuition
[中文题解](#中文题解)


## Approach


## Complexity
* Time: `O()`.
* Space: `O()`.

## Java
```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## Python
```python
class MyQueue:
    def __init__(self):
        self.stack_in = []
        self.stack_out = []

    def push(self, x: int) -> None:
        self.stack_in.append(x)

    def pop(self) -> int:
        self.fill_out_if_empty()
        return self.stack_out.pop()

    def peek(self) -> int:
        self.fill_out_if_empty()
        return self.stack_out[-1]

    def empty(self) -> bool:
        return not self.stack_out and not self.stack_in

    def fill_out_if_empty(self) -> int:
        if not self.stack_out:
            while self.stack_in:
                self.stack_out.append(self.stack_in.pop())
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
var MyQueue = function () {
  this.stackIn = []
  this.stackOut = []
};

MyQueue.prototype.push = function (x) {
  this.stackIn.push(x)
};

MyQueue.prototype.pop = function () {
  this.fillOutIfEmpty()
  return this.stackOut.pop()
};

MyQueue.prototype.peek = function () {
  this.fillOutIfEmpty()
  return this.stackOut.at(-1)
};

MyQueue.prototype.empty = function () {
  return this.stackOut.length === 0 && this.stackIn.length === 0
};

MyQueue.prototype.fillOutIfEmpty = function () {
  if (this.stackOut.length === 0) {
    while (this.stackIn.length > 0) {
      this.stackOut.push(this.stackIn.pop())
    }
  }
}
```

## C#
```c#
// Welcome to create a PR to complete the code of this language, thanks!
```

## Go
```go
// Welcome to create a PR to complete the code of this language, thanks!
```

## Ruby
```ruby
# Welcome to create a PR to complete the code of this language, thanks!
```

## C, Kotlin, Swift, Rust or other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```

## 力扣“232. 用栈实现队列”问题描述
力扣链接：[232. 用栈实现队列](https://leetcode.cn/problems/implement-queue-using-stacks), 难度: **简单**。

请你仅使用两个栈实现先入先出队列。队列应当支持一般队列支持的所有操作（`push`、`pop`、`peek`、`empty`）：

实现 `MyQueue` 类：

- `void push(int x)` 将元素 `x` 推到队列的末尾
- `int pop()` 从队列的开头移除并返回元素
- `int peek()` 返回队列开头的元素
- `boolean empty()` 如果队列为空，返回 `true` ；否则，返回 `false`

**说明：**

你 **只能** 使用标准的栈操作 —— 也就是只有 `push to top`, `peek/pop from top`, `size`, 和 `is empty` 操作是合法的。
你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可。

### [示例 1]
**输入**:
```ruby
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
```

**输出**: `[null, null, null, 1, 1, false]`

# 中文题解
## 思路
1. 

## 步骤
1. 
