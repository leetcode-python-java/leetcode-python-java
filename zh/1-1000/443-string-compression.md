# 443. 压缩字符串 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

访问原文链接：[443. 压缩字符串 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/443-string-compression)，体验更佳！

力扣链接：[443. 压缩字符串](https://leetcode.cn/problems/string-compression), 难度等级：**中等**。

## LeetCode “443. 压缩字符串”问题描述

给你一个字符数组 `chars` ，请使用下述算法压缩：

从一个空字符串 `s` 开始。对于 `chars` 中的每组 **连续重复字符** ：

如果这一组长度为 `1` ，则将字符追加到 `s` 中。
否则，需要向 `s` 追加字符，后跟这一组的长度。
压缩后得到的字符串 `s` **不应该直接返回** ，需要转储到字符数组 `chars` 中。需要注意的是，如果组长度为 `10` 或 `10` 以上，则在 `chars` 数组中会被拆分为多个字符。

请在 **修改完输入数组后** ，返回该数组的新长度。

你必须设计并实现一个只使用常量额外空间的算法来解决此问题。

### [示例 1]

**输入**: `chars = ["a","a","b","b","c","c","c"]`

**输出**: `Return 6, and the first 6 characters of the input array should be: ["a","2","b","2","c","3"]`

**解释**: 

<p>&quot;aa&quot; 被 &quot;a2&quot; 替代。&quot;bb&quot; 被 &quot;b2&quot; 替代。&quot;ccc&quot; 被 &quot;c3&quot; 替代。</p>


### [示例 2]

**输入**: `chars = ["a"]`

**输出**: `Return 1, and the first character of the input array should be: ["a"]`

**解释**: `唯一的组是“a”，它保持未压缩，因为它是一个字符。`

### [示例 3]

**输入**: `chars = ["a","b","b","b","b","b","b","b","b","b","b","b","b"]`

**输出**: `Return 4, and the first 4 characters of the input array should be: ["a","b","1","2"].`

**解释**: 

<p>由于字符 &quot;a&quot; 不重复，所以不会被压缩。&quot;bbbbbbbbbbbb&quot; 被 “b12” 替代。</p>


### [约束]

- `1 <= chars.length <= 2000`
- `chars[i]` 可以是小写英文字母、大写英文字母、数字或符号

### [Hints]

<details>
  <summary>提示 1</summary>
  How do you know if you are at the end of a consecutive group of characters?


  
</details>

## 思路

我们使用双指针（一个读指针 `fast` 和一个写指针 `slow`）以及一个计数器 `count` 来实现原地压缩。

1. **初始化**：
    - 在输入数组 `chars` 的末尾追加一个哨兵字符（例如空格 " "）。这能确保最后一组连续字符也能在循环内被正确处理。Java 和 C# 不适用，因为数组长度固定。
    - `slow = 0`：`slow` 指针指向当前写入段的起始字符，它也是最终压缩数组的长度。
    - `count = 1`：记录当前连续字符 `chars[slow]` 的出现次数。

2. **遍历与压缩**：
    - `fast` 指针从索引 `1` 开始遍历数组 `chars`（直到哨兵字符）。
    - **情况一：字符重复**（`chars[fast]` 等于 `chars[slow]`）
        - 递增 `count`。
    - **情况二：字符不重复**（`chars[fast]` 不等于 `chars[slow]`）
        - **情况1：计数等于1**
            - 请你实现相关逻辑 
        - **情况2：计数大于1**
            - 请你实现相关逻辑 

3. **返回结果**：
    - 当 `fast` 指针遍历完整个数组（包括哨兵）后，`slow` 指针的值即为压缩后数组的新长度。

## “快慢指针技术”的模式

```java
int slow = 0; // slow pointer
// ...

for (int fast = 1; fast < array_length; fast++) { // 本行是关键!
    if (condition_1) {
        // ...
        continue; // 'continue' 比 'else' 好，因为 'else' 会引入更多的缩进空格！
    }

    if (condition_2) {
        // ...
        continue; // 'continue' 比 'else' 好
    }

    // condition_3
    // ...
    slow++;
    // ...
}

return something;
```

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Python

```python
class Solution:
    def compress(self, chars: List[str]) -> int:
        chars.append(" ") # Append an extra special char to process the last char easier
        slow = 0 # Slow pointer. This is the answer.
        count = 1 # Count of consecutive repeating characters

        for fast in range(1, len(chars)):
            if chars[fast] == chars[slow]:
                count += 1
                continue # 'continue' is better than 'else' because 'else' will introduce more indents

            if count == 1:
                slow += 1
                # Don't need to append the 'count' when count is 1.
                chars[slow] = chars[fast]
                continue # 'continue' is better than 'else' because 'else' will introduce more indents

            # Append the 'count'
            for c in str(count):
                slow += 1
                chars[slow] = c

            slow += 1
            chars[slow] = chars[fast]
            count = 1

        return slow
```

## Java

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public int compress(char[] chars) {
        int slow = 0; // Slow pointer. This is the answer.
        int count = 1; // Count of consecutive repeating characters

        for (int fast = 1; fast <= chars.length; fast++) { // it is "<=", not "<"
            var charFast = (fast == chars.length ? ' ' : chars[fast]);

            if (charFast == chars[slow]) {
                count++;
                continue; // 'continue' is better than 'else' because 'else' will introduce more indents
            }

            if (count == 1) {
                slow++;
                // Don't need to append the 'count' when count is 1.
                if (slow < chars.length) {
                    chars[slow] = charFast;
                }
                continue; // 'continue' is better than 'else' because 'else' will introduce more indents
            }

            // Append the 'count'
            for (char c : String.valueOf(count).toCharArray()) {
                slow++;
                chars[slow] = c;
            }

            slow++;
            if (slow < chars.length) {
                chars[slow] = charFast;
            }
            count = 1;
        }

        return slow;
    }
}
```

## C++

```cpp
class Solution {
public:
    int compress(vector<char>& chars) {
        chars.push_back(' '); // Append an extra special char to process the last char easier
        int slow = 0; // Slow pointer. This is the answer.
        int count = 1; // Count of consecutive repeating characters

        for (int fast = 1; fast < chars.size(); ++fast) {
            if (chars[fast] == chars[slow]) {
                count++;
                continue; // 'continue' is better than 'else' because 'else' will introduce more indents
            }

            if (count == 1) {
                slow++;
                // Don't need to append the 'count' when count is 1.
                chars[slow] = chars[fast];
                continue; // 'continue' is better than 'else' because 'else' will introduce more indents
            }

            // Append the 'count'
            for (char c : to_string(count)) {
                slow++;
                chars[slow] = c;
            }

            slow++;
            chars[slow] = chars[fast];
            count = 1;
        }

        return slow;
    }
};
```

## C#

```csharp
public class Solution
{
    public int Compress(char[] chars)
    {
        int slow = 0; // Slow pointer. This is the answer.
        int count = 1; // Count of consecutive repeating characters

        for (int fast = 1; fast <= chars.Length; fast++)
        { // it is "<=", not "<"
            char charFast = (fast == chars.Length ? ' ' : chars[fast]);

            if (charFast == chars[slow])
            {
                count++;
                continue; // 'continue' is better than 'else' because 'else' will introduce more indents
            }

            if (count == 1)
            {
                slow++;
                // Don't need to append the 'count' when count is 1.
                if (slow < chars.Length)
                {
                    chars[slow] = charFast;
                }
                continue; // 'continue' is better than 'else' because 'else' will introduce more indents
            }

            // Append the 'count'
            foreach (char c in count.ToString())
            {
                slow++;
                chars[slow] = c;
            }

            slow++;
            if (slow < chars.Length)
            {
                chars[slow] = charFast;
            }
            count = 1;
        }

        return slow;
    }
}
```

## JavaScript

```javascript
/**
 * @param {character[]} chars
 * @return {number}
 */
var compress = function(chars) {
    chars.push(' ') // Append an extra special char to process the last char easier
    let slow = 0 // Slow pointer. This is the answer.
    let count = 1 // Count of consecutive repeating characters

    for (let fast = 1; fast < chars.length; fast++) {
        if (chars[fast] === chars[slow]) {
            count++
            continue // 'continue' is better than 'else' because 'else' will introduce more indents
        }

        if (count === 1) {
            slow++
            // Don't need to append the 'count' when count is 1.
            chars[slow] = chars[fast]
            continue // 'continue' is better than 'else' because 'else' will introduce more indents
        }

        // Append the 'count'
        for (const c of count.toString()) {
            slow++
            chars[slow] = c
        }

        slow++
        chars[slow] = chars[fast]
        count = 1
    }

    return slow
}
```

## Go

```go
// A test cannot pass. Reason is still unknown

func compress(chars []byte) int {
    chars = append(chars, ' ') // Append an extra special char to process the last char easier
    slow := 0 // Slow pointer. This is the answer.
    count := 1 // Count of consecutive repeating characters

    for fast := 1; fast < len(chars); fast++ {
        if chars[fast] == chars[slow] {
            count++
            continue // 'continue' is better than 'else' because 'else' will introduce more indents
        }

        if count == 1 {
            slow++
            // Don't need to append the 'count' when count is 1.
            chars[slow] = chars[fast]
            continue // 'continue' is better than 'else' because 'else' will introduce more indents
        }

        // Append the 'count'
        for _, c := range strconv.Itoa(count) {
            slow++
            chars[slow] = byte(c)
        }

        slow++
        chars[slow] = chars[fast]
        count = 1
    }

    return slow
}
```

## Ruby

```ruby
# @param {Character[]} chars
# @return {Integer}
def compress(chars)
  chars << " " # Append an extra special char to process the last char easier
  slow = 0 # Slow pointer. This is the answer.
  count = 1 # Count of consecutive repeating characters

  (1...chars.length).each do |fast|
    if chars[fast] == chars[slow]
      count += 1
      next # 'next' is better than 'else' because 'else' will introduce more indents
    end

    if count == 1
      slow += 1
      # Don't need to append the 'count' when count is 1.
      chars[slow] = chars[fast]
      next # 'next' is better than 'else' because 'else' will introduce more indents
    end

    # Append the 'count'
    count.to_s.each_char do |c|
      slow += 1
      chars[slow] = c
    end

    slow += 1
    chars[slow] = chars[fast]
    count = 1
  end

  slow
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.blog](https://leetcode.blog/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[443. 压缩字符串 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/443-string-compression).

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

