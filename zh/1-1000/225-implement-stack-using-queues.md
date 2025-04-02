# 225. 用队列实现栈 - 力扣题解最佳实践

访问原文链接：[225. 用队列实现栈 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/225-implement-stack-using-queues)，体验更佳！

力扣链接：[225. 用队列实现栈](https://leetcode.cn/problems/implement-stack-using-queues), 难度：**简单**。

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

**输入**: `["MyStack", "push", "push", "top", "pop", "empty"] [[], [1], [2], [], [], []]`

**输出**: `[null, null, null, 2, 2, false]`

**解释**: 

<p>MyStack myStack = new MyStack();<br>
myStack.push(1);<br>
myStack.push(2);<br>
myStack.top(); // return 2<br>
myStack.pop(); // return 2<br>
myStack.empty(); // return False</p>


### [约束]

- `1 <= x <= 9`
- 最多调用 `100` 次 `push`、`pop`、`top` 和 `empty`
- 每次调用 `pop` 和 `top` 都保证栈不为空

**进阶**：你能否仅用一个队列来实现栈。

## 思路 1

1. 使用的两个队列，一个队列用于输入和输出，另一个队列用于临时存储。
2. 用队列模拟栈的功能，有两种方案可供选择：
    1. 方案一：简化`pop()`和`top()`操作，复杂化`push(x)`操作。`push(x)`时，需要费力地把`x`插入到队列头部。
    2. 方案二：简化`push(x)`操作，复杂化`pop()`和`top()`操作。`pop()`或`top()`时，需要费力找到最后一个数据。
3. 方案一优点：代码量更少，因为它只需要复杂化一个方法，而方案二要复杂化两个方法；从逻辑上更容易理解，因为它把队列中的数据按`后入先出`的规则排好序了。

## 复杂度

- 时间复杂度: `push O(n), pop O(1), top O(1), empty O(1)`.
- 空间复杂度: `O(n)`.

## Python

```python
class MyStack:
    def __init__(self):
        self.queue = deque()
        self.queue_temp = deque()

    def push(self, x: int) -> None:
        # Move all 'queue' items to 'queue_temp'.
        while self.queue:
            self.queue_temp.append(
                self.queue.popleft()
            )
        
        # Emplaced 'x' at the first of 'queue' because 'queue' is empty.
        self.queue.append(x)

        # Move all 'queue_temp' items back to 'queue'.
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

## C++

```cpp
class MyStack {
private:
    queue<int> queue_;
    queue<int> queue_temp_;

public:
    MyStack() {}

    void push(int x) {
        // Step 1: Move all existing elements from main queue_ to temp_queue_
        while (!queue_.empty()) {
            queue_temp_.push(queue_.front());
            queue_.pop();
        }

        // Step 2: Add the new element to the now-empty main queue_
        // This ensures the newest element is at the front (LIFO behavior)
        queue_.push(x);

        // Step 3: Move all elements from temp_queue_ back to main queue_
        // This places all previous elements behind the new element
        while (!queue_temp_.empty()) {
            queue_.push(queue_temp_.front());
            queue_temp_.pop();
        }
    }

    int pop() {
        int val = queue_.front();
        queue_.pop();
        return val;
    }

    int top() { return queue_.front(); }

    bool empty() { return queue_.empty(); }
};
```

## Go

```go
type MyStack struct {
    // Main queue that stores elements in stack order
    queue []int
    // Temporary queue used during push operations
    queueTemp []int
}

func Constructor() MyStack {
    return MyStack{
        queue: []int{},
        queueTemp: []int{},
    }
}

func (this *MyStack) Push(x int)  {
    // Step 1: Move all existing elements from main queue to temp queue
    for len(this.queue) > 0 {
        // Remove from front and add to temp queue
        this.queueTemp = append(this.queueTemp, this.queue[0])
        this.queue = this.queue[1:]
    }
    
    // Step 2: Add the new element to the now-empty main queue
    // This ensures the newest element is at the front (LIFO behavior)
    this.queue = append(this.queue, x)
    
    // Step 3: Move all elements from temp queue back to main queue
    // This places all previous elements behind the new element
    for len(this.queueTemp) > 0 {
        // Remove from front and add to main queue
        this.queue = append(this.queue, this.queueTemp[0])
        this.queueTemp = this.queueTemp[1:]
    }
}

func (this *MyStack) Pop() int {
    val := this.queue[0]
    this.queue = this.queue[1:]
    return val
}

func (this *MyStack) Top() int {
    return this.queue[0]
}

func (this *MyStack) Empty() bool {
    return len(this.queue) == 0
}
```

## Ruby

```ruby
class MyStack
  def initialize
    @queue = [] # Main queue that stores elements in stack order
    @queue_temp = [] # Temporary queue used during push operations
  end

  def push(x)
    # Step 1: Move all existing elements from main queue to temp queue
    while !@queue.empty?
      @queue_temp.push(@queue.shift)
    end
    
    # Step 2: Add the new element to the now-empty main queue
    # This ensures the newest element is at the front (LIFO behavior)
    @queue.push(x)
    
    # Step 3: Move all elements from temp queue back to main queue
    # This places all previous elements behind the new element
    while !@queue_temp.empty?
      @queue.push(@queue_temp.shift)
    end
  end

  def pop
    @queue.shift
  end

  def top
    @queue.first
  end

  def empty
    @queue.empty?
  end
end
```

## JavaScript

```javascript
var MyStack = function () {
  this.queue = []
  this.queueTemp = []
};

MyStack.prototype.push = function (x) {
  while (this.queue.length > 0) {
    this.queueTemp.push(
      this.queue.shift() // remove from head
    )
  }

  this.queue.push(x)

  while (this.queueTemp.length > 0) {
    this.queue.push(
      this.queueTemp.shift() // remove from head
    )
  }
};

MyStack.prototype.pop = function () {
  return this.queue.shift() // remove from head
};

MyStack.prototype.top = function () {
  return this.queue[0]
};

MyStack.prototype.empty = function () {
  return this.queue.length === 0
};
```

## Java

```java
class MyStack {
    private Queue<Integer> queue;
    private Queue<Integer> queueTemp;

    public MyStack() {
        queue = new LinkedList<>(); // main queue
        queueTemp = new LinkedList<>();
    }
    
    public void push(int x) {
        // Move all elements from main queue to temporary queue
        while (!queue.isEmpty()) {
            queueTemp.offer(
                queue.poll()  // Remove from front (standard queue operation)
            );
        }
        
        // Add the new element to the now-empty main queue
        // This will be the first element to be removed (stack's top)
        queue.offer(x);
        
        // Move all elements back from temporary queue to main queue
        // This ensures newest elements are at the front of the queue
        while (!queueTemp.isEmpty()) {
            queue.offer(
                queueTemp.poll()  // Remove from front (standard queue operation)
            );
        }
    }
    
    public int pop() {
        return queue.poll();
    }
    
    public int top() {
        return queue.peek();
    }
    
    public boolean empty() {
        return queue.isEmpty();
    }
}
```

## C#

```csharp
public class MyStack
{
    private Queue<int> queue; // main queue
    private Queue<int> queueTemp;

    public MyStack()
    {
        queue = new Queue<int>();
        queueTemp = new Queue<int>();
    }
    
    public void Push(int x)
    {
        // Move all elements from main queue to temporary queue
        while (queue.Count > 0)
        {
            queueTemp.Enqueue(
                queue.Dequeue()
            );
        }
        
        // Add the new element to the now-empty main queue
        // This will be the first element to be removed (stack's top)
        queue.Enqueue(x);
        
        // Move all elements back from temporary queue to main queue
        // This ensures newest elements are at the front of the queue
        while (queueTemp.Count > 0)
        {
            queue.Enqueue(
                queueTemp.Dequeue()
            );
        }
    }
    
    public int Pop()
    {
        return queue.Dequeue();
    }
    
    public int Top()
    {
        return queue.Peek();
    }
    
    public bool Empty()
    {
        return queue.Count == 0;
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## 思路 2

1. 使用的两个队列，一个队列用于输入和输出，另一个队列用于临时存储。
2. 用队列模拟栈的功能，有两种方案可供选择：
    1. 方案一：简化`pop()`和`top()`操作，复杂化`push(x)`操作。`push(x)`时，需要费力地把`x`插入到队列头部。
    2. 方案二：简化`push(x)`操作，复杂化`pop()`和`top()`操作。`pop()`或`top()`时，需要费力找到最后一个数据。
3. 本文主要介绍`方案二`，方便读者对比这两个方案。

## 复杂度

- 时间复杂度: `push O(1), pop O(n), top O(n), empty O(1)`.
- 空间复杂度: `O(n)`.

## Python

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

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## 思路 3

- 可以只用一个队列实现栈。改动只在`push`方法。只需要想办法不借助另一个`queue_temp`，把`x`插入到队列的头部。
- 在实现`push`方法时，先`queue.push(x)`，这样，`x`就被插入到了队列尾部，但我们需要把`x`放到队列的头部。
- 把`x`前面的所有数据依次出队列，再入队列，就可以了。
- 执行`queue.length - 1`次`queue.push(queue.pop())`即可。

## 复杂度

- 时间复杂度: `push O(n), pop O(1), top O(1), empty O(1)`.
- 空间复杂度: `O(n)`.

## JavaScript

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

```python
from collections import deque


class MyStack:
    def __init__(self):
        self.queue = deque()

    def push(self, x: int) -> None:
        self.queue.append(x)
        
        # Rotate the queue to put the new element at the front
        # This is done by moving all existing elements to the back
        for _ in range(len(self.queue) - 1):
            self.queue.append(
                self.queue.popleft()
            )

    def pop(self) -> int:
        return self.queue.popleft()

    def top(self) -> int:
        return self.queue[0]

    def empty(self) -> bool:
        return not self.queue
```

## C++

```cpp
class MyStack {
private:
    queue<int> q_;

public:
    MyStack() {}
    
    void push(int x) {
        q_.push(x);
        
        // Rotate the queue to put the new element at the front
        // This is done by moving all existing elements to the back
        for (int i = 0; i < q_.size() - 1; i++) {
            q_.push(q_.front());  // Add front element to back
            q_.pop();            // Remove from front
        }
    }
    
    int pop() {
        int top = q_.front();
        q_.pop();
        return top;
    }
    
    int top() {
        return q_.front();
    }
    
    bool empty() {
        return q_.empty();
    }
};
```

## Go

```go
type MyStack struct {
    queue []int
}

func Constructor() MyStack {
    return MyStack{
        queue: make([]int, 0),
    }
}

func (this *MyStack) Push(x int) {
    // Add the new element to the queue
    this.queue = append(this.queue, x)
    
    // Rotate the queue to put the new element at the front
    // This is done by moving all existing elements to the back
    for i := 0; i < len(this.queue) - 1; i++ {
        // Move first element to the back
        this.queue = append(this.queue, this.queue[0])
        this.queue = this.queue[1:]
    }
}

func (this *MyStack) Pop() int {
    // Remove and return the first element (stack's top)
    top := this.queue[0]
    this.queue = this.queue[1:]
    return top
}

func (this *MyStack) Top() int {
    return this.queue[0]
}

func (this *MyStack) Empty() bool {
    return len(this.queue) == 0
}
```

## Ruby

```ruby
class MyStack
  def initialize
    @queue = []
  end

  def push(x)
    @queue.push(x)
    
    # Rotate the queue to put the new element at the front
    # This is done by moving all existing elements to the back
    (@queue.length - 1).times do
      @queue.push(@queue.shift)  # Move first element to the back
    end
  end

  def pop
    @queue.shift
  end

  def top
    @queue.first
  end

  def empty
    @queue.empty?
  end
end
```

## Java

```java
import java.util.LinkedList;
import java.util.Queue;

class MyStack {
    private Queue<Integer> queue;

    public MyStack() {
        queue = new LinkedList<>();
    }
    
    public void push(int x) {
        queue.offer(x);
        
        // Rotate the queue to put the new element at the front
        // This is done by moving all existing elements to the back
        for (int i = 0; i < queue.size() - 1; i++) {
            queue.offer(queue.poll());  // Move first element to the back
        }
    }
    
    public int pop() {
        return queue.poll();
    }
    
    public int top() {
        return queue.peek();
    }
    
    public boolean empty() {
        return queue.isEmpty();
    }
}
```

## C#

```csharp
using System.Collections.Generic;

public class MyStack
{
    private Queue<int> queue;

    public MyStack()
    {
        queue = new Queue<int>();
    }
    
    public void Push(int x)
    {
        queue.Enqueue(x);
        
        // Rotate the queue to put the new element at the front
        // This is done by moving all existing elements to the back
        for (int i = 0; i < queue.Count - 1; i++)
        {
            queue.Enqueue(queue.Dequeue());  // Move first element to the back
        }
    }
    
    public int Pop()
    {
        return queue.Dequeue();
    }
    
    public int Top()
    {
        return queue.Peek();
    }
    
    public bool Empty()
    {
        return queue.Count == 0;
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [leetcoder.net](https://leetcoder.net/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[225. 用队列实现栈 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/225-implement-stack-using-queues).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

