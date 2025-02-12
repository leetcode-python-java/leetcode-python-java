# 20. 有效的括号 - 力扣题解最佳实践
力扣链接：[20. 有效的括号](https://leetcode.cn/problems/valid-parentheses) ，难度：**简单**。

## 力扣“20. 有效的括号”问题描述
给定一个只包括 `(`，`)`，`{`，`}`，`[`，`]` 的字符串 `s` ，判断字符串是否有效。

有效字符串需满足：

1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。
3. 每个右括号都有一个对应的相同类型的左括号。

### [示例 1]
**输入**: `s = "()"`

**输出**: `true`

### [示例 2]
**输入**: `s = "()[]{}"`

**输出**: `true`

### [示例 3]
**输入**: `s = "(]"`

**输出**: `false`

### [示例 4]
**输入**: `s = "([])"`

**输出**: `true`

### [约束]
- `1 <= s.length <= 10000`
- `s` 仅由括号 `()[]{}` 组成

### 提示
<details>
  <summary>提示 1</summary>
  Use a stack of characters.
</details>

<details>
  <summary>提示 2</summary>
  When you encounter an opening bracket, push it to the top of the stack.
</details>

<details>
  <summary>提示 3</summary>
  When you encounter a closing bracket, check if the top of the stack was the opening for it. If yes, pop it from the stack. Otherwise, return false.
</details>

## 思路
1. 括号匹配关注的主要是`前一个字符`与`当前字符`。有两种情况要考虑：
    1. 如果`当前字符`是左括号，则不需要匹配，直接保存起来。
    2. 如果`当前字符`是右括号，并且`前一个字符`与`当前字符`配成了一对，则这两个字符都可以**消失**了；反之，如果配对失败，直接返回`false`。
2. 这种关注`前一个字符`与`当前字符`的场景，适合用`栈`实现。
3. 左右括号之间的对应关系可以保存在一个`Map`中。
4. 最后，如果栈为空，说明全部配对成功，返回`true`；否则返回`false`。

## 复杂度
* 时间：`O(N)`。
* 空间：`O(N)`。

## JavaScript
```javascript
var isValid = function (s) {
  const rightToLeft = new Map([
    [')', '('],
    ['}', '{'],
    [']', '['],
  ])
  const stack = []

  for (const char of s) {
    if (!rightToLeft.has(char)) {
      stack.push(char)
    } else if (stack.length === 0 || stack.pop() != rightToLeft.get(char)) {
      return false
    }
  }

  return stack.length === 0
};
```

## Python
```python
class Solution:
    def isValid(self, s: str) -> bool:
        right_to_left = {
            ')': '(',
            '}': '{',
            ']': '[',
        }
        stack = []

        for char in s:
            if char not in right_to_left:
                stack.append(char)
            elif not stack or stack.pop() != right_to_left[char]:
                return False

        return not stack
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
