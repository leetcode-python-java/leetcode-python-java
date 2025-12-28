# 232. 用栈实现队列 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**leader.me**](https://www.leader.me) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[232. 用栈实现队列 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/232-implement-queue-using-stacks)，体验更佳！

力扣链接：[232. 用栈实现队列](https://leetcode.cn/problems/implement-queue-using-stacks), 难度等级：**简单**。

## LeetCode “232. 用栈实现队列”问题描述

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

**输入**: `["MyQueue", "push", "push", "peek", "pop", "empty"] [[], [1], [2], [], [], []]`

**输出**: `[null, null, null, 1, 1, false]`

**解释**: 

<p>MyQueue myQueue = new MyQueue();<br>
myQueue.push(1); // queue is: [1]<br>
myQueue.push(2); // queue is: <a href="leftmost%20is%20front%20of%20the%20queue" rel="nofollow" target="_blank">1, 2</a><br>
myQueue.peek(); // return 1<br>
myQueue.pop(); // return 1, queue is [2]<br>
myQueue.empty(); // return false</p>


### [约束]

- `1 <= x <= 9`
- 最多调用 `100` 次 `push`、`pop`、`peek` 和 `empty`
- 假设所有操作都是有效的 （例如，一个空的队列不会调用 `pop` 或者 `peek` 操作）


**进阶：** 你能否实现每个操作均摊时间复杂度为 `O(1)` 的队列？换句话说，执行 `n` 个操作的总时间复杂度为 `O(n)` ，即使其中一个操作可能花费较长时间。

## 思路

- 用两个栈实现一个队列，直觉的想法是一个栈`stack_in`专门用于`push`，另一个栈`stack_out`专门用于`pop`。

- `push`可以很容易，直接`push`就好了，这样`pop`就没有那么容易了。如何做呢？
    <details><summary>点击查看答案</summary><p> 栈是后进先出，队列是先进先出，二者是相反的，所以直接从`stack_in`中`pop`是不行的，得把`stack_in`中的元素反向加到`stack_out`中，再`pop`。</p></details>

## 复杂度

> `pop` 和 `peek` 看起来是 `O(n)`，实际是`O(1)`。因为如果一次`dump_into_stack_out`操作了`m`个数，之后的`m`次，每次`pop`都是`O(1)`。

- 时间复杂度: `push O(1), pop O(1), peek O(1), empty O(1)`.
- 空间复杂度: `O(n)`.

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

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**leader.me**](https://www.leader.me) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.cto.page`、`name.engineer.dev` 等极具职业含金量的专属域名。
> - 🔗 **超酷超短个人主页：** 获得极其简练的社交名片，如 `is.bio/yourname` 或 `an.dev/yourname`。
>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[232. 用栈实现队列 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/232-implement-queue-using-stacks)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

