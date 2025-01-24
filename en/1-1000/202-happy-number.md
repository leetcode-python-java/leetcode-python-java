# 202. Happy Number - Best Practices of LeetCode Solutions
LeetCode problem link: [202. Happy Number](https://leetcode.com/problems/happy-number),
[202. 快乐数](https://leetcode.cn/problems/happy-number)

[中文题解](#中文题解)

## LeetCode problem description
Write an algorithm to determine if a number `n` is happy.

A **happy number** is a number defined by the following process:

* Starting with any positive integer, replace the number by the sum of the squares of its digits.
* Repeat the process until the number equals 1 (where it will stay), or it **loops endlessly in a cycle** which does not include 1.
* Those numbers for which this process **ends in 1** are happy.

Return `true` if `n` is _a happy number_, and `false` if not.

Difficulty: **Easy**

### [Example 1]
**Input**: `n = 19`

**Output**: `true`

**Explanation**
```
1**2 + 9**2 = 82
8**2 + 2**2 = 68
6**2 + 8**2 = 100
1**2 + 0**2 + 0**2 = 1
```

### [Example 2]
**Input**: `n = 2`

**Output**: `false`

### [Constraints]
- `1 <= n <= 2**31 - 1`

## Intuition
[中文题解](#中文题解)

1. It is more convenient to call `isHappy(n)` recursively. You only need to generate a new `n` as a parameter each time.
2. If `n` has already appeared, it means that the loop has been entered, and `return false`. You can use `Set` to save the `n` that has appeared.

## Steps
1. Generate a new `n` as the `isHappy(n)` parameter.
```javascript
let sum = 0

for (const digit of n.toString()) {
  sum += Math.pow(Number(digit), 2)
}

// omitted code

return isHappy(sum)
```

2. If `n` has already appeared, it means that the loop has been entered, and `return false`. You can use `Set` to save the `n` that has appeared.
```javascript
var isHappy = function (n, appearedNums) { // 0
  appearedNums ||= new Set() // 1
  let sum = 0

  for (const digit of n.toString()) {
    sum += Math.pow(Number(digit), 2)
  }

  if (sum == 1) {
    return true
  }

  if (appearedNums.has(sum)) { // 2
    return false
  }

  appearedNums.add(sum) // 3

  return isHappy(sum, appearedNums)
};
```

## Complexity
* Time: `O(log N)`.
* Space: `O(log N)`.

## Java
```java
class Solution {
    private HashSet<Integer> appearedNums = new HashSet<>();

    public boolean isHappy(int n) {
        appearedNums.add(n);

        var sum = 0;

        for (var digit : String.valueOf(n).toCharArray()) {
            sum += Math.pow(digit - '0', 2);
        }

        if (sum == 1) {
            return true;
        }
        
        if (appearedNums.contains(sum)) {
            return false;
        }

        return isHappy(sum);
    }
}
```

## Python
```python
class Solution:
    def __init__(self):
        self.appeared_nums = set()

    def isHappy(self, n: int) -> bool:
        self.appeared_nums.add(n)

        number = sum([int(digit) ** 2 for digit in str(n)])

        if number == 1:
            return True
        
        if number in self.appeared_nums:
            return False

        return self.isHappy(number)
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
var isHappy = function (n, appearedNums) {
  appearedNums ||= new Set()
  let sum = 0

  for (const digit of n.toString()) {
    sum += Math.pow(Number(digit), 2)
  }

  if (sum == 1) {
    return true
  }

  if (appearedNums.has(sum)) {
    return false
  }

  appearedNums.add(sum)

  return isHappy(sum, appearedNums)
};
```

## C#
```c#
public class Solution
{
    HashSet<int> appearedNums = new HashSet<int>();

    public bool IsHappy(int n)
    {
        appearedNums.Add(n);

        int sum = 0;

        foreach (char digit in n.ToString().ToCharArray())
            sum += (int)Math.Pow(digit - '0', 2);

        if (sum == 1)
            return true;
        
        if (appearedNums.Contains(sum))
            return false;

        return IsHappy(sum);
    }
}
```

## Go
```go
// Welcome to create a PR to complete the code of this language, thanks!
```

## Ruby
```ruby
# Welcome to create a PR to complete the code of this language, thanks!
```

## C
```c
// Welcome to create a PR to complete the code of this language, thanks!
```

## Kotlin
```kotlin
// Welcome to create a PR to complete the code of this language, thanks!
```

## Swift
```swift
// Welcome to create a PR to complete the code of this language, thanks!
```

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```

## 问题描述
编写一个算法来判断一个数 `n` 是不是快乐数。

「**快乐数**」 定义为：

* 对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和。
* 然后重复这个过程直到这个数变为 `1`，也可能是 **无限循环** 但始终变不到 `1`。
* 如果这个过程 **结果为** `1`，那么这个数就是快乐数。
* 如果 `n` 是 _快乐数_ 就返回 `true` ；不是，则返回 `false` 。

难度: **容易**

### [Example 1]
**输入**: `n = 19`

**输出**: `true`

**解释**
```
1**2 + 9**2 = 82
8**2 + 2**2 = 68
6**2 + 8**2 = 100
1**2 + 0**2 + 0**2 = 1
```

# 中文题解
## 思路
1. 递归调用`isHappy(n)`比较方便，每次只需要生成新的`n`作为参数。
2. 如果`n`已经出现过了，说明进入了循环，`return false`。可以用`Set`保存已经出现过的`n`。

## 步骤
1. 生成新的`n`作为`isHappy()`的参数。
```javascript
let sum = 0

for (const digit of n.toString()) {
  sum += Math.pow(Number(digit), 2)
}

// omitted code

return isHappy(sum)
```

2. 如果`n`已经出现过了，说明进入了循环，`return false`。可以用`Set`保存已经出现过的`n`。
```javascript
var isHappy = function (n, appearedNums) {
  appearedNums ||= new Set() // 1
  let sum = 0

  for (const digit of n.toString()) {
    sum += Math.pow(Number(digit), 2)
  }

  if (sum == 1) {
    return true
  }

  if (appearedNums.has(sum)) { // 2
    return false
  }

  appearedNums.add(sum) // 3

  return isHappy(sum, appearedNums)
};
```
