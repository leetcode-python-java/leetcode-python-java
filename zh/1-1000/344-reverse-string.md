# 344. 反转字符串 - 力扣题解最佳实践

访问原文链接：[344. 反转字符串 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/344-reverse-string)，体验更佳！

力扣链接：[344. 反转字符串](https://leetcode.cn/problems/reverse-string), 难度：**简单**。

## 力扣“344. 反转字符串”问题描述

编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 `s` 的形式给出。

不要给另外的数组分配额外的空间，你必须 [原地](https://en.wikipedia.org/wiki/In-place_algorithm) **修改输入数组**、使用 `O(1)` 的额外空间解决这一问题。

### [示例 1]

**输入**: `s = ["h","e","l","l","o"]`

**输出**: `["o","l","l","e","h"]`

### [示例 2]

**输入**: `s = ["H","a","n","n","a","h"]`

**输出**: `["h","a","n","n","a","H"]`

### [约束]

- `1 <= s.length <= 10^5`
- `s[i]` 都是 ASCII 码表中的可打印字符

### [Hints]

<details>
  <summary>提示 1</summary>
  The entire logic for reversing a string is based on using the opposite directional two-pointer approach!

  
</details>

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

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

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

亲爱的力扣人，为了您更好的刷题体验，请访问 [leetcoder.net](https://leetcoder.net/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[344. 反转字符串 - 力扣题解最佳实践](https://leetcoder.net/zh/leetcode/344-reverse-string).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

