# 232. Implement Queue using Stacks - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [232. Implement Queue using Stacks - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/232-implement-queue-using-stacks) for a better experience!

LeetCode link: [232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks), difficulty: **Easy**.

## LeetCode description of "232. Implement Queue using Stacks"

Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (`push`, `peek`, `pop`, and `empty`).

Implement the `MyQueue` class:

- `void push(int x)` Pushes element x to the back of the queue.
- `int pop()` Removes the element from the front of the queue and returns it.
- `int peek()` Returns the element at the front of the queue.
- `boolean empty()` Returns `true` if the queue is empty, `false` otherwise.

**Notes:**

- You must use **only** standard operations of a stack, which means only `push to top`, `peek/pop from top`, `size`, and `is empty` operations are valid.
- Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.

### [Example 1]

**Input**: `["MyQueue", "push", "push", "peek", "pop", "empty"] [[], [1], [2], [], [], []]`

**Output**: `[null, null, null, 1, 1, false]`

**Explanation**: 

<p>MyQueue myQueue = new MyQueue();<br>
myQueue.push(1); // queue is: [1]<br>
myQueue.push(2); // queue is: <a href="leftmost%20is%20front%20of%20the%20queue" rel="nofollow" target="_blank">1, 2</a><br>
myQueue.peek(); // return 1<br>
myQueue.pop(); // return 1, queue is [2]<br>
myQueue.empty(); // return false</p>


### [Constraints]

- `1 <= x <= 9`
- At most `100` calls will be made to `push`, `pop`, `peek`, and `empty`.
- All the calls to `pop` and `peek` are valid.


**Follow-up**: Can you implement the queue such that each operation is amortized `O(1)` time complexity? In other words, performing `n` operations will take overall `O(n)` time even if one of those operations may take longer.

## Intuition

- To implement a queue with two stacks, the intuitive idea is that one stack `stack_in` is dedicated to `push`, and the other stack `stack_out` is dedicated to `pop`.

- `Push` can be easy, just `push` directly, then `pop` is not so easy. How to do it?
    <details><summary>Click to view the answer</summary><p> Stack is last in first out, queue is first in first out, the two are opposite, so it is not possible to `pop` directly from `stack_in`. You have to add the elements in `stack_in` to `stack_out` in reverse, and then `pop`. </p></details>

## Complexity

> `pop` and `peek` appear to be `O(n)`, but they are actually `O(1)`. This is because if `dump_into_stack_out` operates on `m` numbers at a time, then each `pop` operation for the next `m` times is `O(1)`.

- Time complexity: `push O(1), pop O(1), peek O(1), empty O(1)`.
- Space complexity: `O(n)`.

## Python

```python
class MyQueue:
    def __init__(self):
        self.stack_in = []
        self.stack_out = []

    def push(self, x: int) -> None:
        self.stack_in.append(x)

    def pop(self) -> int:
        self.dump_into_stack_out_if_it_is_empty()
        return self.stack_out.pop()

    def peek(self) -> int:
        self.dump_into_stack_out_if_it_is_empty()
        return self.stack_out[-1]

    def empty(self) -> bool:
        return not self.stack_out and not self.stack_in

    def dump_into_stack_out_if_it_is_empty(self) -> int:
        if not self.stack_out:
            while self.stack_in:
                self.stack_out.append(self.stack_in.pop())
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
  this.dumpIntoStackOutWhenItIsEmpty()
  return this.stackOut.pop()
};

MyQueue.prototype.peek = function () {
  this.dumpIntoStackOutWhenItIsEmpty()
  return this.stackOut.at(-1)
};

MyQueue.prototype.empty = function () {
  return this.stackOut.length === 0 && this.stackIn.length === 0
};

MyQueue.prototype.dumpIntoStackOutWhenItIsEmpty = function () {
  if (this.stackOut.length === 0) {
    while (this.stackIn.length > 0) {
      this.stackOut.push(this.stackIn.pop())
    }
  }
}
```

## Java

```java
import java.util.Stack;

class MyQueue {
    private Stack<Integer> stackIn;
    private Stack<Integer> stackOut;

    public MyQueue() {
        stackIn = new Stack<>();
        stackOut = new Stack<>();
    }
    
    public void push(int x) {
        stackIn.push(x);
    }
    
    public int pop() {
        dumpIntoStackOutWhenItIsEmpty();
        return stackOut.pop();
    }
    
    public int peek() {
        dumpIntoStackOutWhenItIsEmpty();
        return stackOut.peek();
    }
    
    public boolean empty() {
        return stackIn.empty() && stackOut.empty();
    }
    
    private void dumpIntoStackOutWhenItIsEmpty() {
        if (stackOut.empty()) {
            while (!stackIn.empty()) {
                stackOut.push(stackIn.pop());
            }
        }
    }
}
```

## C++

```cpp
class MyQueue {
private:
    stack<int> stack_in_;
    stack<int> stack_out_;

    void dumpIntoStackOutWhenItIsEmpty() {
        if (stack_out_.empty()) {
            while (!stack_in_.empty()) {
                stack_out_.push(stack_in_.top());
                stack_in_.pop();
            }
        }
    }

public:
    MyQueue() {}
    
    void push(int x) {
        stack_in_.push(x);
    }
    
    int pop() {
        dumpIntoStackOutWhenItIsEmpty();
        int value = stack_out_.top();
        stack_out_.pop();
        return value;
    }
    
    int peek() {
        dumpIntoStackOutWhenItIsEmpty();
        return stack_out_.top();
    }
    
    bool empty() {
        return stack_in_.empty() && stack_out_.empty();
    }
};
```

## C#

```csharp
using System.Collections.Generic;

public class MyQueue
{
    private Stack<int> stackIn;
    private Stack<int> stackOut;

    public MyQueue()
    {
        stackIn = new Stack<int>();
        stackOut = new Stack<int>();
    }
    
    public void Push(int x)
    {
        stackIn.Push(x);
    }
    
    public int Pop()
    {
        DumpIntoStackOutWhenItIsEmpty();
        return stackOut.Pop();
    }
    
    public int Peek()
    {
        DumpIntoStackOutWhenItIsEmpty();
        return stackOut.Peek();
    }
    
    public bool Empty()
    {
        return stackIn.Count == 0 && stackOut.Count == 0;
    }
    
    private void DumpIntoStackOutWhenItIsEmpty()
    {
        if (stackOut.Count == 0)
        {
            while (stackIn.Count > 0)
            {
                stackOut.Push(stackIn.Pop());
            }
        }
    }
}
```

## Go

```go
type MyQueue struct {
  stackIn  []int
  stackOut []int
}

func Constructor() MyQueue {
  return MyQueue{
    stackIn:  make([]int, 0),
    stackOut: make([]int, 0),
  }
}

func (this *MyQueue) Push(x int) {
  this.stackIn = append(this.stackIn, x)
}

func (this *MyQueue) Pop() int {
  this.dumpIntoStackOutWhenItIsEmpty()
  top := this.stackOut[len(this.stackOut) - 1]
  this.stackOut = this.stackOut[:len(this.stackOut) - 1]
  return top
}

func (this *MyQueue) Peek() int {
  this.dumpIntoStackOutWhenItIsEmpty()
  return this.stackOut[len(this.stackOut) - 1]
}

func (this *MyQueue) Empty() bool {
  return len(this.stackIn) == 0 && len(this.stackOut) == 0
}

func (this *MyQueue) dumpIntoStackOutWhenItIsEmpty() {
  if len(this.stackOut) == 0 {
    for len(this.stackIn) > 0 {
      top := this.stackIn[len(this.stackIn) - 1]
      this.stackIn = this.stackIn[:len(this.stackIn) - 1]
      this.stackOut = append(this.stackOut, top)
    }
  }
}
```

## Ruby

```ruby
class MyQueue
  def initialize
    @stack_in = []
    @stack_out = []
  end

  def push(x)
    @stack_in.push(x)
  end

  def pop
    dump_into_stack_out_when_it_is_empty
    @stack_out.pop
  end

  def peek
    dump_into_stack_out_when_it_is_empty
    @stack_out.last
  end

  def empty
    @stack_in.empty? && @stack_out.empty?
  end

  private

  def dump_into_stack_out_when_it_is_empty
    if @stack_out.empty?
      while !@stack_in.empty?
        @stack_out.push(@stack_in.pop)
      end
    end
  end
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [232. Implement Queue using Stacks - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/232-implement-queue-using-stacks) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

