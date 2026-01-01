# 225. Implement Stack using Queues - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**that.dev**](https://www.that.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.that.dev`.
>
> [**Build Your Programmer Brand at that.dev →**](https://www.that.dev)

---

Visit original link: [225. Implement Stack using Queues - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/225-implement-stack-using-queues) for a better experience!

LeetCode link: [225. Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues), difficulty: **Easy**.

## LeetCode description of "225. Implement Stack using Queues"

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

**Input**: `["MyStack", "push", "push", "top", "pop", "empty"] [[], [1], [2], [], [], []]`

**Output**: `[null, null, null, 2, 2, false]`

**Explanation**: 

<p>MyStack myStack = new MyStack();<br>
myStack.push(1);<br>
myStack.push(2);<br>
myStack.top(); // return 2<br>
myStack.pop(); // return 2<br>
myStack.empty(); // return False</p>


### [Constraints]

- `1 <= x <= 9`
- At most `100` calls will be made to `push`, `pop`, `top`, and `empty`.
- All the calls to `pop` and `top` are valid.

**Follow-up**: Can you implement the stack using only one queue?

## Intuition 1

1. Two queues are used, one for input and output, and the other for temporary storage.
2. There are two options for using queues to simulate the functions of a stack:
   1. Option 1: Simplify the `pop()` and `top()` operations and complicate the `push(x)` operation. When `push(x)`, you need to insert `x` into the front of the queue with effort. 
   2. Option 2: Simplify the `push(x)` operation and complicate the `pop()` and `top()` operations. When `pop()` or `top()`, you need to find the last data with effort.
3. Advantages of Option 1: Less code, because it only needs to complicate one method, while Solution 2 complicates two methods; easier to understand logically because it sorts the data in the queue according to the `last in, first out` rule.

## Complexity

- Time complexity: `push O(n), pop O(1), top O(1), empty O(1)`.
- Space complexity: `O(n)`.

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

## Intuition 2

1. Two queues are used, one for input and output, and the other for temporary storage.
2. There are two options for using queues to simulate the functions of a stack:
   1. Option 1: Simplify the `pop()` and `top()` operations and complicate the `push(x)` operation. When `push(x)`, you need to insert `x` into the front of the queue with effort. 
   2. Option 2: Simplify the `push(x)` operation and complicate the `pop()` and `top()` operations. When `pop()` or `top()`, you need to find the last data with effort.
3. This article mainly introduces `Option 2` to facilitate readers to compare the two solutions.

## Complexity

- Time complexity: `push O(1), pop O(n), top O(n), empty O(1)`.
- Space complexity: `O(n)`.

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

## Intuition 3

- You can use only one queue to make it. The only change is in the `push` method. Just find a way to insert `x` to the front of the queue without using another `queue_temp`.
- When implementing the `push` method, first `queue.push(x)`, so that `x` is inserted at the tail (back) of the queue, but we need to put `x` at the head (front) of the queue.
- Execute `queue.length - 1` times `queue.push(queue.pop())` to move all the data before `x` to the back of `x`.

## Complexity

- Time complexity: `push O(n), pop O(1), top O(1), empty O(1)`.
- Space complexity: `O(n)`.

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

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**that.dev**](https://www.that.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.that.dev`.
>
> [**Build Your Programmer Brand at that.dev →**](https://www.that.dev)

---

Visit original link: [225. Implement Stack using Queues - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/225-implement-stack-using-queues) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

