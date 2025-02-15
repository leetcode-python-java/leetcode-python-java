# 752. Open the Lock - Best Practices of LeetCode Solutions
LeetCode link: [752. Open the Lock](https://leetcode.com/problems/open-the-lock), difficulty: **Medium**.

## LeetCode description of "752. Open the Lock"
You have a lock in front of you with 4 circular wheels. Each wheel has 10 slots: `'0', '1', '2', '3', '4', '5', '6', '7', '8', '9'`. The wheels can rotate freely and wrap around: for example we can turn `9` to be `0`, or `0` to be `9`. Each move consists of turning one wheel one slot.

The lock initially starts at `0000`, a string representing the state of the 4 wheels.

You are given a list of `deadends` dead ends, meaning if the lock displays any of these codes, the wheels of the lock will stop turning and you will be unable to open it.

Given a `target` representing the value of the wheels that will unlock the lock, return _the **minimum total number** of turns required to open the lock, or `-1` if it is impossible_.

### [Example 1]
**Input**: `deadends = ["0201","0101","0102","1212","2002"], target = "0202"`

**Output**: `6`

**Explanation**:
```
A sequence of valid moves would be "0000" -> "1000" -> "1100" -> "1200" -> "1201" -> "1202" -> "0202".
Note that a sequence like "0000" -> "0001" -> "0002" -> "0102" -> "0202" would be invalid,
because the wheels of the lock become stuck after the display becomes the dead end "0102".
```

### [Example 2]
**Input**: `deadends = ["8888"], target = "0009"`

**Output**: `1`

**Explanation**:
```
We can turn the last wheel in reverse to move from "0000" -> "0009".
```

### [Example 3]
**Input**: `["8887","8889","8878","8898","8788","8988","7888","9888"], target = "8888"`

**Output**: `-1`

**Explanation**: `We cannot reach the target without getting stuck.`

### [Constraints]
- `1 <= deadends.length <= 500`
- `deadends[i].length == 4`
- `target.length == 4`
- `target` **will not be** in the list `deadends`.
- `target` and `deadends[i]` consist of digits only.

### [Hints]
<details>
  <summary>Hint 1</summary>
  We can think of this problem as a shortest path problem on a graph: there are `10000` nodes (strings `'0000'` to `'9999'`), and there is an edge between two nodes if they differ in one digit, that digit differs by 1 (wrapping around, so `'0'` and `'9'` differ by 1), and if *both* nodes are not in `deadends`.
</details>

## Intuition
We can think of this problem as a shortest path problem on a graph: there are `10000` nodes (strings `'0000'` to `'9999'`), and there is an edge between two nodes if they differ in one digit, that digit differs by 1 (wrapping around, so `'0'` and `'9'` differ by 1), and if *both* nodes are not in `deadends`.

### Solution 1: Breadth-First Search
![](../../images/binary_tree_BFS_1.gif)

* As shown in the figure above, **Breadth-First Search** can be thought of as visiting vertices in rounds and rounds. Actually, whenever you see a question is about
  getting `minimum number` of something of a graph, `Breadth-First Search` would probably help.

* `Breadth-First Search` emphasizes first-in-first-out, so a **queue** is needed.

### Solution 2: A* (A-Star) Algorithm

**A-Star Algorithm** can be used to improve the performance of **Breadth-First Search Algorithm**.

**Breadth-First Search** treats each vertex equally, which inevitably leads to poor performance.

The `A* (A-Star) algorithm` calculates the **distance** between each `vertex` and the `target vertex`, and **prioritizes vertices with closer distances**, which is equivalent to indicating which vertex to process next, so the performance is greatly improved!

#### A* (A-Star) Algorithm Has Two (or Three) Key Actions
1. Use `priority_queue`.
2. The function for calculating `distance` should be **carefully designed** (poor design will lead to **subtle** errors in the results).
3. In special cases, simply using `distance` as the sorting basis of `priority_queue` is not enough, and it is also necessary to **adjust** (for example, add it to the `number of steps` variable value) to make the last few steps accurate (not involved in this example, yet in this one [1197. Minimum Knight Moves](https://leetcode.com/problems/minimum-knight-moves/)).

## Complexity
> `N` is the length of `deadends`.

### Solution 1: Breadth-First Search
* Time: `O(10^4)`.
* Space: `O(N)`.

### Solution 2: A* (A-Star) Algorithm
* Time: `O(5 * 4 * 4 * 2 + N)`.
* Space: `O(N)`.

## Python
### Solution 1: Breadth-First Search
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

### Solution 2: A* (A-Star) Algorithm
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
