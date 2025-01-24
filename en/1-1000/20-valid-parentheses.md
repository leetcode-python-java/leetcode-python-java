# 20. Valid Parentheses - Best Practices of LeetCode Solutions
LeetCode link: [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses), difficulty: **Easy**

## Description of "20. Valid Parentheses"
Given a string `s` containing just the characters `(`, `)`, `{`, `}`, `[` and `]`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

### [Example 1]
**Input**: `s = "()"`

**Output**: `true`

### [Example 2]
**Input**: `s = "()[]{}"`

**Output**: `true`

### [Example 3]
**Input**: `s = "(]"`

**Output**: `false`

### [Example 4]
**Input**: `s = "([])"`

**Output**: `true`

### [Constraints]
- `1 <= s.length <= 10000`
- `s` consists of parentheses only `()[]{}`.

### Hints
<details>
  <summary>Hint 1</summary>
  Use a stack of characters.
</details>

<details>
  <summary>Hint 2</summary>
  When you encounter an opening bracket, push it to the top of the stack.
</details>

<details>
  <summary>Hint 3</summary>
  When you encounter a closing bracket, check if the top of the stack was the opening for it. If yes, pop it from the stack. Otherwise, return false.
</details>

## Intuition
1. Bracket matching focuses on the `previous character` and the `current character`. There are two situations to consider:
    1. If the `current character` is a left bracket, there is no need to match it and it can be saved directly.
    2. If the `current character` is a right bracket, and the `previous character` and the `current character` are paired, both characters can disappear; otherwise, if the pairing fails, `false` is returned directly.
2. This scenario that focuses on the `previous character` and the `current character` is suitable for implementation with a `stack`.
3. The mapping relationship between left and right brackets can be saved in a `Map`.
4. Finally, if the stack is empty, it means that all pairings are successful and `true` is returned; otherwise, `false` is returned.

## Complexity
* Time: `O(N)`.
* Space: `O(N)`.

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
