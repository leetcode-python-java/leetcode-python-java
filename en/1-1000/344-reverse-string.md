# 344. Reverse String - LeetCode solutions in Python/Java/C++ and more

Visit original link: [344. Reverse String - LeetCode solutions in Python/Java/C++ and more](https://leetcodepython.com/en/leetcode/344-reverse-string) for a better experience!

LeetCode link: [344. Reverse String](https://leetcode.com/problems/reverse-string), difficulty: **Easy**.

## LeetCode description of "344. Reverse String"

Write a function that reverses a string. The input string is given as an array of characters `s`.

You must do this by modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) with `O(1)` extra memory.

### [Example 1]

**Input**: `s = ["h","e","l","l","o"]`

**Output**: `["o","l","l","e","h"]`

### [Example 2]

**Input**: `s = ["H","a","n","n","a","h"]`

**Output**: `["h","a","n","n","a","H"]`

### [Constraints]

- `1 <= s.length <= 10^5`
- `s[i]` is a [printable ascii character](https://en.wikipedia.org/wiki/ASCII#Printable_characters).

### [Hints]

<details>
  <summary>Hint 1</summary>
  The entire logic for reversing a string is based on using the opposite directional two-pointer approach!

  
</details>

## Intuition

1. This problem can be solved in one line of code using the built-in `sort()` method of the programming language. If this question is asked in an interview, the questioner should be testing how to do it without the built-in method.
2. Use **two pointers** with **opposite directions**, initially one pointer points to the index `0` and the other pointer points to the index `s.length - 1`.
3. Traverse the elements of the array, and the loop condition is `while (left < right)`. In the loop body, `left += 1`, `right -= 1`.
4. In the loop body, swap the two values.
5. The above is the template for `two pointers` in `opposite directions`.

## Steps

1. Use two pointers with **opposite directions**, initially one pointer points to the index `0` and the other pointer points to the index `s.length - 1`.

    ```ruby
    left = 0
    right = s.length - 1
    ```

2. Traverse the elements of the array, and the loop condition is `while (left < right)`. In the loop body, `left += 1`, `right -= 1`.

    ```ruby
    left = 0
    right = s.length - 1
    
    while left < right # 1
      left += 1 # 2
      right -= 1 # 3
    end
    ```

3. In the loop body, swap the two values.

    ```ruby
    left = 0
    right = s.length - 1
    
    while left < right
      s[left], s[right] = s[right], s[left] # 1
    
      left += 1
      right -= 1
    end
    ```

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Java

```java
class Solution {
    public void reverseString(char[] s) {
        var left = 0;
        var right = s.length - 1;

        while (left < right) {
            var leftValue = s[left];
            s[left] = s[right];
            s[right] = leftValue;

            left++;
            right--;
        }
    }
}
```

## Python

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        left = 0
        right = len(s) - 1

        while left < right:
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1
```

## C++

```cpp
class Solution {
public:
    void reverseString(vector<char>& s) {
        auto left = 0;
        auto right = s.size() - 1;

        while (left < right) {
            swap(s[left], s[right]);

            left++;
            right--;
        }
    }
};
```

## JavaScript

```javascript
var reverseString = function (s) {
  let left = 0
  let right = s.length - 1

  while (left < right) {
    [s[left], s[right]] = [s[right], s[left]]

    left++
    right--
  }
};
```

## C#

```csharp
public class Solution
{
    public void ReverseString(char[] s)
    {
        int left = 0;
        int right = s.Length - 1;

        while (left < right)
        {
            (s[left], s[right]) = (s[right], s[left]);

            left++;
            right--;
        }
    }
}
```

## Go

```go
func reverseString(s []byte)  {
    left := 0
    right := len(s) - 1

    for left < right {
        s[left], s[right] = s[right], s[left]

        left++
        right--
    }
}
```

## Ruby

```ruby
def reverse_string(s)
  left = 0
  right = s.size - 1

  while left < right
    s[left], s[right] = s[right], s[left]

    left += 1
    right -= 1
  end
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCodePython.com](https://leetcodepython.com): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [344. Reverse String - LeetCode solutions in Python/Java/C++ and more](https://leetcodepython.com/en/leetcode/344-reverse-string).

GitHub repository: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

