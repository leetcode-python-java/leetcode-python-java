# 344. Reverse String - LeetCode Solution
LeetCode problem link: [344. Reverse String](https://leetcode.com/problems/reverse-string),
[344. 反转字符串](https://leetcode.cn/problems/reverse-string)

[中文题解](#中文题解)

## LeetCode problem description
Write a function that reverses a string. The input string is given as an array of characters `s`.

You must do this by modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) with `O(1)` extra memory.

Difficulty: **Easy**

### [Example 1]

**Input**: `s = ["h","e","l","l","o"]`

**Output**: `["o","l","l","e","h"]`

### [Example 2]
**Input**: `s = ["H","a","n","n","a","h"]`

**Output**: `["h","a","n","n","a","H"]`

### [Constraints]
- `1 <= s.length <= 105`
- `s[i]` is a [printable ascii character](https://en.wikipedia.org/wiki/ASCII#Printable_characters).

<details>
  <summary>Hint 1</summary>
  The entire logic for reversing a string is based on using the opposite directional two-pointer approach!
</details>

## Intuition behind the Solution
[中文题解](#中文题解)

1. This problem can be solved in one line of code using the built-in `sort()` method of the programming language. If this question is asked in an interview, the questioner should be testing how to do it without the built-in method.
2. Use **two pointers** with **opposite directions**, initially one pointer points to the index `0` and the other pointer points to the index `s.length - 1`.
3. Traverse the elements of the array, and the loop condition is `while (left < right)`. In the loop body, `left += 1`, `right -= 1`.
4. In the loop body, swap the two values.
5. The above is the template for `two pointers` in `opposite directions`.

## Approach
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
* Time: `O(n)`.
* Space: `O(1)`.

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
```c#
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

## 力扣“344. 反转字符串”问题描述
力扣链接：[344. 反转字符串](https://leetcode.cn/problems/reverse-string), 难度: **简单**。

编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 `s` 的形式给出。

不要给另外的数组分配额外的空间，你必须 **原地** **修改输入数组**、使用 `O(1)` 的额外空间解决这一问题。

### [示例 1]
**输入**: `s = ["h","e","l","l","o"]`

**输出**: `["o","l","l","e","h"]`

# 中文题解
## 思路
1. 这种问题用编程语言内置的`sort()`方法可以一行代码解决。如果面试中出这种题目，出题人考察的应该是不用内置方法如何做。
2. 用**方向相对**的两个指针，最初时一个指针指向下标`0`，另一个指针指向下标`s.length - 1`。
3. 遍历数组元素，循环条件为`while (left < right)`。在循环体内，`left += 1`, `right -= 1`。
4. 在循环体内，交换数组中两个下标对应的值。
5. 以上为`方向相对`的**双指针**的模板。

## 步骤
1. 用**方向相对的两个指针**，最初时一个指针指向下标`0`，另一个指针指向下标`s.length - 1`。
```ruby
left = 0
right = s.length - 1
```

2. 遍历数组元素，循环条件为`while (left < right)`。在循环体内，`left += 1`, `right -= 1`。
```ruby
left = 0
right = s.length - 1

while left < right # 1
  left += 1 # 2
  right -= 1 # 3
end
```

3. 在循环体内，交换数组中两个下标对应的值。
```ruby
left = 0
right = s.length - 1

while left < right
  s[left], s[right] = s[right], s[left] # 1

  left += 1
  right -= 1
end
```
