# 20. 有效的括号 - LeetCode Python/Java/C++ 题解

访问原文链接：[20. 有效的括号 - LeetCode Python/Java/C++ 题解](https://leetcode.blog/zh/leetcode/20-valid-parentheses)，体验更佳！

力扣链接：[20. 有效的括号](https://leetcode.cn/problems/valid-parentheses), 难度等级：**简单**。

## LeetCode “20. 有效的括号”问题描述

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

### [Hints]

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

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(N)`.

## JavaScript

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function (s) {
  const closeToOpen = new Map([
    [')', '('],
    ['}', '{'],
    [']', '['],
  ])
  const stack = []

  for (const char of s) {
    if (!closeToOpen.has(char)) {
        // is open bracket
        stack.push(char)
        continue
    }
    // is close bracket

    if (stack.length === 0) {
        return false
    }

    // stack top value doesn't match the expected value
    if (stack.pop() != closeToOpen.get(char)) {
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
        # Map closing brackets to their opening brackets
        close_to_open = {
            ')': '(',
            '}': '{',
            ']': '[',
        }
        stack = []

        for char in s:
            if char not in close_to_open:
                # is open bracket
                stack.append(char)
                continue
            # is close bracket

            if not stack:
                return False

            # stack top value doesn't match the expected value
            if stack.pop() != close_to_open[char]:
                return False

        return not stack
```

## Java

```java
class Solution {
    public boolean isValid(String s) {
        // Map closing brackets to their opening brackets
        var closeToOpen = new HashMap<Character, Character>();
        closeToOpen.put(')', '(');
        closeToOpen.put('}', '{');
        closeToOpen.put(']', '[');

        var stack = new Stack<Character>();

        for (char c : s.toCharArray()) {
            if (!closeToOpen.containsKey(c)) {
                // is open bracket
                stack.push(c);
                continue;
            }
            // is close bracket

            if (stack.isEmpty()) {
                return false;
            }

            // stack top value doesn't match the expected value
            if (stack.pop() != closeToOpen.get(c)) {
                return false;
            }
        }

        return stack.isEmpty();
    }
}
```

## C++

```cpp
class Solution {
public:
    bool isValid(string s) {
        // Map closing brackets to their opening brackets
        unordered_map<char, char> closeToOpen = {
            {')', '('},
            {'}', '{'},
            {']', '['}
        };
        
        stack<char> st;
        
        for (char c : s) {
            if (closeToOpen.find(c) == closeToOpen.end()) {
                // is open bracket
                st.push(c);
                continue;
            }
            // is close bracket
            
            if (st.empty()) {
                return false;
            }
            
            // stack top value doesn't match the expected value
            if (st.top() != closeToOpen[c]) {
                return false;
            }
            
            st.pop();
        }
        
        return st.empty();
    }
};
```

## C#

```csharp
public class Solution
{
    public bool IsValid(string s)
    {
        // Map closing brackets to their opening brackets
        var closeToOpen = new Dictionary<char, char>()
        {
            {')', '('},
            {'}', '{'},
            {']', '['}
        };

        var stack = new Stack<char>();

        foreach (char c in s) {
            if (!closeToOpen.ContainsKey(c))
            {
                // is open bracket
                stack.Push(c);
                continue;
            }
            // is close bracket

            if (stack.Count == 0)
            {
                return false;
            }

            // stack top value doesn't match the expected value
            if (stack.Pop() != closeToOpen[c])
            {
                return false;
            }
        }

        return stack.Count == 0;
    }
}
```

## Go

```go
func isValid(s string) bool {
    // Map closing brackets to their opening brackets
    closeToOpen := map[rune]rune{
        ')': '(',
        '}': '{',
        ']': '[',
    }

    stack := []rune{}

    for _, char := range s {
        if _, isClose := closeToOpen[char]; !isClose {
            // is open bracket
            stack = append(stack, char)
            continue
        }
        // is close bracket

        if len(stack) == 0 {
            return false
        }

        lastChar := stack[len(stack) - 1]

        // stack top value doesn't match the expected value
        if lastChar != closeToOpen[char] {
            return false
        }

        stack = stack[:len(stack) - 1] // pop operation
    }

    return len(stack) == 0
}
```

## Ruby

```ruby
# @param {String} s
# @return {Boolean}
def is_valid(s)
  # Map closing brackets to their opening brackets
  close_to_open = {
    ')' => '(',
    '}' => '{',
    ']' => '['
  }

  stack = []

  s.each_char do |char|
    if !close_to_open.key?(char)
      # is open bracket
      stack.push(char)
      next
    end
    # is close bracket

    if stack.empty?
      return false
    end

    # stack top value doesn't match the expected value
    if stack.pop != close_to_open[char]
      return false
    end
  end

  stack.empty?
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.blog](https://leetcode.blog/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[20. 有效的括号 - LeetCode Python/Java/C++ 题解](https://leetcode.blog/zh/leetcode/20-valid-parentheses).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

