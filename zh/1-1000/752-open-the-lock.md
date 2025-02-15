# 752. 打开转盘锁 - 力扣题解最佳实践
力扣链接：[752. 打开转盘锁](https://leetcode.cn/problems/open-the-lock) ，难度：**中等**。

## 力扣“752. 打开转盘锁”问题描述
你有一个带有四个圆形拨轮的转盘锁。每个拨轮都有10个数字： `'0', '1', '2', '3', '4', '5', '6', '7', '8', '9'` 。每个拨轮可以自由旋转：例如把 `9` 变为 `0`，`0` 变为 `9` 。每次旋转都只能旋转一个拨轮的一位数字。

锁的初始数字为 `'0000'` ，一个代表四个拨轮的数字的字符串。

列表 `deadends` 包含了一组死亡数字，一旦拨轮的数字和列表里的任何一个元素相同，这个锁将会被永久锁定，无法再被旋转。

字符串 `target` 代表可以解锁的数字，你需要给出*解锁需要的**最小**旋转次数*，如果无论如何不能解锁，返回 `-1` 。

### [示例 1]
**输入**: `deadends = ["0201","0101","0102","1212","2002"], target = "0202"`

**输出**: `6`

**解释**:
```
可能的移动序列为 "0000" -> "1000" -> "1100" -> "1200" -> "1201" -> "1202" -> "0202"。
注意 "0000" -> "0001" -> "0002" -> "0102" -> "0202" 这样的序列是不能解锁的，
因为当拨动到 "0102" 时这个锁就会被锁定。
```

### [示例 2]
**输入**: `deadends = ["8888"], target = "0009"`

**输出**: `1`

**解释**: `把最后一位反向旋转一次即可 "0000" -> "0009"。`

### [示例 3]
**输入**: `["8887","8889","8878","8898","8788","8988","7888","9888"], target = "8888"`

**输出**: `-1`

**解释**: `无法旋转到目标数字且不被锁定。`

### [约束]
- `1 <= deadends.length <= 500`
- `deadends[i].length == 4`
- `target.length == 4`
- `target` **不在** `deadends` 之中
- `target` 和 `deadends[i]` 仅由若干位数字组成

### [提示]
<details>
  <summary>提示 1</summary>
  We can think of this problem as a shortest path problem on a graph: there are `10000` nodes (strings `'0000'` to `'9999'`), and there is an edge between two nodes if they differ in one digit, that digit differs by 1 (wrapping around, so `'0'` and `'9'` differ by 1), and if *both* nodes are not in `deadends`.
</details>

## 思路
我们可以把这个问题想像为一个`求无向图的最短路径`问题。

`图`中最多有`10000`个顶点，从顶点`'0000'`到顶点`'9999'`，但`deadends`代表的顶点要从图中移除。如果两个顶点只相差一个数字，那么它们之间有一条边。

### 题解 1: 广度优先搜索
![](../../images/binary_tree_BFS_1.gif)

* As shown in the figure above, **Breadth-First Search** can be thought of as visiting vertices in rounds and rounds. Actually, whenever you see a question is about
  getting `minimum number` of something of a graph, `Breadth-First Search` would probably help.

* `Breadth-First Search` emphasizes first-in-first-out, so a **queue** is needed.

### 题解 2: A* (A-Star) 算法

重头戏来了！

`A* (A-Star) 算法` 可以用于极大提升 `广度优先搜索` 的性能。

`广度优先搜索` 对每一个顶点都同等对待，这样难免性能会差。

`A* (A-Star) 算法` 会对每一个`顶点`与`目标顶点`的**距离**进行计算，**距离近的顶点优先处理**，性能提升会很大。

#### A* (A-Star) 算法的两（三）个关键动作
1. 要用 `priority_queue`。
2. 计算距离的函数要**精心设计**。设计不好，将导致不易察觉的结果错误!
3. 在特殊情况下，单纯地用`距离`作为`priority_queue`的排序依据还不够，还要**调整一下**，比如与`步数`变量值相加（本例子不涉及）。

## Complexity
> `N` 是 `deadends.length`.

### 题解 1: 广度优先搜索
* 时间: `O(10^4)`.
* 空间: `O(N)`.

### 题解 2: A* (A-Star) 算法
* 时间: `O(5 * 4 * 4 * 2 + N)`.
* 空间: `O(N)`.

## Python
### 题解 1: 广度优先搜索
```python
class Solution:
        def openLock(self, deadends: List[str], target_digits: str) -> int:
            if '0000' == target_digits:
                return 0

            self.deadends = set(deadends)
            if '0000' in deadends:
                return -1

            self.queue = deque(['0000'])
            self.deadends.add('0000')
            self.target_digits = target_digits
            result = 0

            while self.queue:
                result += 1
                queue_size = len(self.queue)

                for _ in range(queue_size):
                    digits = self.queue.popleft()

                    if self.turn_one_slot(digits):
                        return result

            return -1

        def turn_one_slot(self, digits):
            for i in range(len(digits)):
                for digit in closest_digits(int(digits[i])):
                    new_digits = f'{digits[:i]}{digit}{digits[i + 1:]}'

                    if new_digits == self.target_digits:
                        return True

                    if new_digits in self.deadends:
                        continue

                    self.queue.append(new_digits)
                    self.deadends.add(new_digits)


def closest_digits(digit):
    if digit == 0:
        return (9, 1)

    if digit == 9:
        return (8, 0)

    return (digit - 1, digit + 1)
```

### 题解 2: A* (A-Star) 算法
```python
class Solution:
    def openLock(self, deadends: List[str], target_digits: str) -> int:
        if '0000' == target_digits:
            return 0

        deadends = set(deadends)
        if '0000' in deadends:
            return -1

        self.target_digits = target_digits

        priority_queue = [(self.distance('0000'), '0000', 0)]

        while priority_queue:
            _, digits, turns = heapq.heappop(priority_queue)

            for i in range(4):
                for digit in closest_digits(int(digits[i])):
                    new_digits = f'{digits[:i]}{digit}{digits[i + 1:]}'

                    if new_digits == target_digits:
                        return turns + 1

                    if new_digits in deadends:
                        continue

                    heapq.heappush(
                        priority_queue,
                        (self.distance(new_digits), new_digits, turns + 1)
                    )
                    deadends.add(new_digits)

        return -1

    def distance(self, digits):
        result = 0

        # 0 1 2 3 4 5 6 7 8 9
        # 0 1 2 3 4 5 6 7 8 9
        # 0 1 2 3 4 5 6 7 8 9
        # 0 1 2 3 4 5 6 7 8 9
        for i in range(4):
            # 'Euclidean Distance' is widely used in 'A* Algorithm'.
            result += abs(int(self.target_digits[i]) - int(digits[i])) ** 2

        return result ** 0.5


def closest_digits(digit):
    if digit == 0:
        return (9, 1)

    if digit == 9:
        return (8, 0)

    return (digit - 1, digit + 1)
```

## JavaScript
```javascript
// Welcome to create a PR to complete the code of this language, thanks!
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
