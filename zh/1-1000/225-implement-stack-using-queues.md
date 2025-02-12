# 225. 用队列实现栈 - 力扣题解最佳实践
力扣链接：[225. 用队列实现栈](https://leetcode.cn/problems/implement-stack-using-queues) ，难度：**简单**。

## 力扣“225. 用队列实现栈”问题描述
请你仅使用两个队列实现一个后入先出（LIFO）的栈，并支持普通栈的全部四种操作（`push`、`top`、`pop` 和 `empty`）。

实现 `MyStack` 类：

- `void push(int x)` 将元素 `x` 压入栈顶。
- `int pop()` 移除并返回栈顶元素。
- `int top()` 返回栈顶元素。
- `boolean empty()` 如果栈是空的，返回 `true`；否则，返回 `false`。

**注意**：

- 你只能使用队列的标准操作 —— 也就是 `push to back`、`peek/pop from front`、`size` 和 `is empty` 这些操作。
- 你所使用的语言也许不支持队列。 你可以使用 list （列表）或者 deque（双端队列）来模拟一个队列 , 只要是标准的队列操作即可。

### [示例 1]
**输入**:
```javascript
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
```

**输出**:
```javascript
[null, null, null, 2, 2, false]
```

**解释**:
```java
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // 返回 2
myStack.pop(); // 返回 2
myStack.empty(); // 返回 False
```

### [约束]
- `1 <= x <= 9`
- 最多调用 `100` 次 `push`、`pop`、`top` 和 `empty`
- 每次调用 `pop` 和 `top` 都保证栈不为空

## 思路
1. 使用的两个队列，一个队列用于输入和输出，另一个队列用于临时存储。
2. 用队列模拟栈的功能，有两种方案可供选择：
    1. 方案一：简化`push(x)`操作，复杂化`pop()`和`top()`操作。`pop()`或`top()`时，需要费力找到最后一个数据。
    2. 方案二：简化`pop()`和`top()`操作，复杂化`push(x)`操作。`push(x)`时，需要费力地把`x`插入到队列头部。
3. 方案二优点：代码量更少；从逻辑上更容易理解，因为它把队列中的数据按`后入先出`的规则排好序了。
4. 本文主要介绍`方案二`，`方案一`的代码附在`Python`章节中，方便读者对比这两个方案。

## 复杂度
* 时间：`push O(n)`, `pop O(1)`, `top O(1)`, `empty O(1)`。
* 空间：`O(n)`。

## 进阶
你能否仅用一个队列来实现栈？

### 进阶思路
- 可以只用一个队列实现栈。改动只在`push`方法。只需要想办法不借助另一个`queue_temp`，把`x`插入到队列的头部。
- 在实现`push`方法时，先`queue.push(x)`，这样，`x`就被插入到了队列尾部，但我们需要把`x`放到队列的头部。
- 把`x`前面的所有数据依次出队列，再入队列，就可以了。
- 执行`queue.length - 1`次`queue.push(queue.pop())`即可。完整代码附在`JavaScript`章节中。

## JavaScript
### 方案二
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

### 进阶方案：只使用一个队列
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
### 方案一：不推荐，仅用于对比。
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
        return not self.queue
```

### 方案二：推荐的方案。既短，又好理解。
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
        return not self.queue
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
