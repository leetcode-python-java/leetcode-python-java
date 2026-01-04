# 13. 罗马数字转整数 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**leader.me**](https://www.leader.me) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.leader.me`，极具职业含金量的专属域名。
>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[13. 罗马数字转整数 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/13-roman-to-integer)，体验更佳！

力扣链接：[13. 罗马数字转整数](https://leetcode.cn/problems/roman-to-integer), 难度等级：**简单**。

## LeetCode “13. 罗马数字转整数”问题描述

罗马数字包含以下七种字符: `I`， `V`， `X`， `L`，`C`，`D` 和 `M`。

```
字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```
例如， 罗马数字 `2` 写做 `II` ，即为两个并列的 `1` 。`12` 写做 `XII` ，即为 `X` + `II` 。 `27` 写做  `XXVII`, 即为 `XX` + `V` + `II` 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 `IIII`，而是 `IV`。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 `IX`。这个特殊的规则只适用于以下六种情况：

- I 可以放在 `V` (5) 和 `X` (10) 的左边，来表示 4 和 9。
- X 可以放在 `L` (50) 和 `C` (100) 的左边，来表示 40 和 90。
- C 可以放在 `D` (500) 和 `M` (1000) 的左边，来表示 400 和 900。

给定一个罗马数字，将其转换成整数。

### [示例 1]

**输入**: `s = "III"`

**输出**: `3`

### [示例 2]

**输入**: `s = "IV"`

**输出**: `4`

### [示例 3]

**输入**: `s = "IX"`

**输出**: `9`

### [示例 4]

**输入**: `s = "LVIII"`

**输出**: `58`

**解释**: `L = 50, V= 5, III = 3.`

### [示例 5]

**输入**: `s = "MCMXCIV"`

**输出**: `1994`

**解释**: `M = 1000, CM = 900, XC = 90, IV = 4.`

### [约束]

- `1 <= s.length <= 15`
- `s` 仅含字符 `('I', 'V', 'X', 'L', 'C', 'D', 'M')`
- 题目数据保证 `s` 是一个有效的罗马数字，且表示整数在范围 `[1, 3999]` 内
- 题目所给测试用例皆符合罗马数字书写规则，不会出现跨位等情况。
- IL 和 IM 这样的例子并不符合题目要求，49 应该写作 XLIX，999 应该写作 CMXCIX 。

### [Hints]

<details>
  <summary>提示 1</summary>
  Problem is simpler to solve by working the string from back to front and using a map.

  
</details>

## 思路

- 字符与数值的对应关系可以用 `Map`。 
- 直觉是见到一个数字就把值加到 `result` 中，从左向右遍历。
- 但考虑出现类似 `IV` 这样的情况，即“当前的字符对应的值”大于“前一个字符对应的值”。这时，应该如何进行 `result` 数值更新？
    <details><summary>点击查看答案</summary><p>减去“前一个字符对应的值 * 2”。</p></details>


## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Ruby

```ruby
# @param {String} s
# @return {Integer}
def roman_to_int(s)
  char_to_num = {
    "I" => 1,
    "V" => 5,
    "X" => 10,
    "L" => 50,
    "C" => 100,
    "D" => 500,
    "M" => 1000,
  }
  result = 0

  s.chars.each_with_index do |c, i|
    result += char_to_num[c]
    next if i == 0
    
    if char_to_num[s[i - 1]] < char_to_num[c]
      result -= char_to_num[s[i - 1]] * 2
    end
  end

  result
end
```

## Python

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        char_to_num = {
            "I": 1,
            "V": 5,
            "X": 10,
            "L": 50,
            "C": 100,
            "D": 500,
            "M": 1000,
        }
        result = 0

        for i, c in enumerate(s):
            result += char_to_num[c]

            if i == 0:
                continue
            
            # If the previous value is smaller than the current, 
            # subtract it twice (once because it was added, once for the rule)
            if char_to_num[s[i - 1]] < char_to_num[c]:
                result -= char_to_num[s[i - 1]] * 2

        return result
```

## Java

```java
class Solution {
    public int romanToInt(String s) {
        Map<Character, Integer> charToNum = new HashMap<>();
        charToNum.put('I', 1);
        charToNum.put('V', 5);
        charToNum.put('X', 10);
        charToNum.put('L', 50);
        charToNum.put('C', 100);
        charToNum.put('D', 500);
        charToNum.put('M', 1000);

        int result = 0;

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            result += charToNum.get(c);

            if (i == 0) {
                continue;
            }

            // If previous value is smaller than current, subtract it twice
            if (charToNum.get(s.charAt(i - 1)) < charToNum.get(c)) {
                result -= charToNum.get(s.charAt(i - 1)) * 2;
            }
        }

        return result;
    }
}
```

## C++

```cpp
class Solution {
public:
    int romanToInt(string s) {
        unordered_map<char, int> char_to_num = {
            {'I', 1},
            {'V', 5},
            {'X', 10},
            {'L', 50},
            {'C', 100},
            {'D', 500},
            {'M', 1000}
        };
        int result = 0;

        for (int i = 0; i < s.length(); i++) {
            result += char_to_num[s[i]];

            if (i == 0) continue;

            // If the previous character's value is less than the current,
            // subtract that previous value twice.
            if (char_to_num[s[i - 1]] < char_to_num[s[i]]) {
                result -= char_to_num[s[i - 1]] * 2;
            }
        }

        return result;
    }
};
```

## JavaScript

```javascript
/**
 * @param {string} s
 * @return {number}
 */
const romanToInt = function(s) {
    const charToNum = {
        'I': 1,
        'V': 5,
        'X': 10,
        'L': 50,
        'C': 100,
        'D': 500,
        'M': 1000
    };
    let result = 0;

    for (let i = 0; i < s.length; i++) {
        const currentVal = charToNum[s[i]];
        result += currentVal;

        if (i === 0) {
            continue;
        }

        const prevVal = charToNum[s[i - 1]];

        // If the previous value is smaller than the current, 
        // subtract it twice (adjusting for the previous addition)
        if (prevVal < currentVal) {
            result -= prevVal * 2;
        }
    }

    return result;
};
```

## C#

```csharp
public class Solution
{
    public int RomanToInt(string s)
    {
        var charToNum = new Dictionary<char, int>
        {
            {'I', 1},
            {'V', 5},
            {'X', 10},
            {'L', 50},
            {'C', 100},
            {'D', 500},
            {'M', 1000}
        };

        int result = 0;

        for (int i = 0; i < s.Length; i++)
        {
            int currentVal = charToNum[s[i]];
            result += currentVal;

            if (i == 0)
            {
                continue;
            }

            int prevVal = charToNum[s[i - 1]];

            // If the previous value is less than the current, 
            // subtract it twice to correct the total.
            if (prevVal < currentVal)
            {
                result -= prevVal * 2;
            }
        }

        return result;
    }
}
```

## Go

```go
func romanToInt(s string) int {
    charToNum := map[rune]int{
        'I': 1,
        'V': 5,
        'X': 10,
        'L': 50,
        'C': 100,
        'D': 500,
        'M': 1000,
    }

    result := 0
    // Converting string to a slice of runes for easy indexing
    runes := []rune(s)

    for i, c := range runes {
        result += charToNum[c]

        if i == 0 {
            continue
        }

        // If the previous value is smaller than the current,
        // subtract it twice (adjusting for the previous addition)
        if charToNum[runes[i - 1]] < charToNum[c] {
            result -= charToNum[runes[i - 1]] * 2
        }
    }

    return result
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**leader.me**](https://www.leader.me) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.leader.me`，极具职业含金量的专属域名。

>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[13. 罗马数字转整数 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/13-roman-to-integer)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

