# 20. Valid Parentheses - LeetCode Python/Java/C++/JS code

Visit original link: [20. Valid Parentheses - LeetCode Python/Java/C++/JS code](https://leetcodepython.com/en/leetcode/20-valid-parentheses) for a better experience!

LeetCode link: [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses), difficulty: **Easy**.

## LeetCode description of "20. Valid Parentheses"

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

### [Hints]

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

- Time complexity: `O(N)`.
- Space complexity: `O(N)`.

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

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCodePython.com](https://leetcodepython.com): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [20. Valid Parentheses - LeetCode Python/Java/C++/JS code](https://leetcodepython.com/en/leetcode/20-valid-parentheses).

GitHub repository: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

