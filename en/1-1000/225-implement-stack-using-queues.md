# 225. Implement Stack using Queues - LeetCode Solution Best Practice
LeetCode link: [225. Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues), difficulty: **Easy**

## Description of "225. Implement Stack using Queues"
Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (`push`, `top`, `pop`, and `empty`).

Implement the `MyStack` class:

- `void push(int x)` Pushes element `x` to the top of the stack.
- `int pop()` Removes the element on the top of the stack and returns it.
- `int top()` Returns the element on the top of the stack.
- `boolean empty()` Returns `true` if the stack is empty, `false` otherwise.

**Notes**:

- You must use **only** standard operations of a queue, which means that only `push to back`, `peek/pop from front`, `size` and `is empty` operations are valid.
- Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue) as long as you use only a queue's standard operations.


### [Example 1]
**Input**:
```javascript
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
```

**Output**:
```javascript
[null, null, null, 2, 2, false]
```

**Explanation**:
```java
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // return 2
myStack.pop(); // return 2
myStack.empty(); // return False
```

### [Constraints]
- `1 <= x <= 9`
- At most `100` calls will be made to `push`, `pop`, `top`, and `empty`.
- All the calls to `pop` and `top` are valid.

### [Follow-up]
Can you implement the stack using only one queue?

## Intuition
1. Two queues are used, one for input and output, and the other for temporary storage.
2. There are two options for using queues to simulate the functions of a stack:
    1. Option 1: Simplify the `push(x)` operation and complicate the `pop()` and `top()` operations. When `pop()` or `top()`, you need to find the last data with effort.
    2. Option 2: Simplify the `pop()` and `top()` operations and complicate the `push(x)` operation. When `push(x)`, you need to insert `x` into the front of the queue with effort.
3. Advantages of Option 2: Less code; easier to understand logically because it sorts the data in the queue according to the `last in, first out` rule.
4. This article mainly introduces `Option 2`, and the code of `Option 1` is attached in `Python` section to facilitate readers to compare the two solutions.

## Complexity
* Time: `push O(n)`, `pop O(1)`, `top O(1)`, `empty O(1)`.
* Space: `O(n)`.

## Follow-up
- You can use only one queue to make it. The only change is in the `push` method. Just find a way to insert `x` to the front of the queue without using another `queue_temp`.
- When implementing the `push` method, first `queue.push(x)`, then execute `queue.length - 1` times `queue.push(queue.pop())`. The complete code is attached in `JavaScript` section.

## JavaScript
### Solution for option 2
```javascript
var MyStack = function () {
  this.queue = []
  this.queueTemp = []
};

MyStack.prototype.push = function (x) {
  while (this.queue.length > 0) {
    this.queueTemp.push(
      this.queue.shift()
    )
  }

  this.queue.push(x)

  while (this.queueTemp.length > 0) {
    this.queue.push(
      this.queueTemp.shift()
    )
  }
};

MyStack.prototype.pop = function () {
  return this.queue.shift()
};

MyStack.prototype.top = function () {
  return this.queue[0]
};

MyStack.prototype.empty = function () {
  return this.queue.length === 0
};
```

### Follow-up solution: use only one queue
```javascript
var MyStack = function () {
  this.queue = []
};

MyStack.prototype.push = function (x) {
  this.queue.push(x)

  _.times(
    this.queue.length - 1,
    () => this.queue.push(this.queue.shift())
  )
};

MyStack.prototype.pop = function () {
  return this.queue.shift()
};

MyStack.prototype.top = function () {
  return this.queue[0]
};

MyStack.prototype.empty = function () {
  return this.queue.length === 0
};
```

## Python
### Solution for option 1: Not recommended, for comparison only.
```python
class MyStack:
    def __init__(self):
        self.queue = deque()
        self.queue_temp = deque()

    def push(self, x: int) -> None:
        self.queue.append(x)

    def pop(self) -> int:
        while len(self.queue) > 1:
            self.queue_temp.append(
                self.queue.popleft()
            )

        value = self.queue.popleft()

        while self.queue_temp:
            self.queue.append(
                self.queue_temp.popleft()
            )

        return value

    def top(self) -> int:
        value = None

        while self.queue:
            value = self.queue.popleft()
            self.queue_temp.append(value)

        while self.queue_temp:
            self.queue.append(
                self.queue_temp.popleft()
            )

        return value

    def empty(self) -> bool:
        return len(self.queue) == 0
```

### Solution for option 2: It is short and easy to understand (recommended).
```python
class MyStack:
    def __init__(self):
        self.queue = deque()
        self.queue_temp = deque()

    def push(self, x: int) -> None:
        while self.queue:
            self.queue_temp.append(
                self.queue.popleft()
            )
        
        self.queue.append(x)

        while self.queue_temp:
            self.queue.append(
                self.queue_temp.popleft()
            )

    def pop(self) -> int:
        return self.queue.popleft()

    def top(self) -> int:
        return self.queue[0]

    def empty(self) -> bool:
        return len(self.queue) == 0
```

## Java
```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
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
