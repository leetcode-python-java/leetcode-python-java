# 13. 罗马数字转整数 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **进阶你的开发者身份**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **专业简历 (Resume)：** 告别平庸，生成一份令猎头和面试官眼前一亮的动态技术简历。
> - 🎨 **作品集 (Portfolio)：** 自动聚合 GitHub 贡献与项目经历，将枯燥的代码转化为极具冲击力的视觉作品集。
> - ✍️ **技术博客 (Blog)：** 在纯净、专注的写作空间分享技术见解，树立你的行业影响力。
>
> [**立即前往 Show.dev 打造你的专属品牌 →**](https://www.show.dev)

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
- 直觉是见到一个数字就把值加到 `result` 中。
- 但可能出现类似 `IV` 这样的情况，要考虑是从左到右处理还是从右到左处理这种情况。你选择的处理方向是？ 
    <details><summary>点击查看答案</summary><p>从右向左处理比较方便，因为一但看到当前字符与前一个字符是特定组合，就可以直接处理。</p></details>
- 如何处理 `IV` 这样的情况呢？
    <details><summary>点击查看答案</summary><p>反向处理就好了。正向是做加法，现在做减法。</p></details>

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Ruby

```ruby
# @param {String} s
# @return {Integer}
def roman_to_int(s)
  symbol_to_value = {
    'I' => 1,
    'V' => 5,
    'X' => 10,
    'L' => 50,
    'C' => 100,
    'D' => 500,
    'M' => 1000,
  }
  result = 0
  previous_char = nil

  (s.size - 1).downto(0).each do |i|
    char = s[i]
    if ('I' == char && ['V', 'X'].include?(previous_char)) || 
       ('X' == char && ['L', 'C'].include?(previous_char)) ||
       ('C' == char && ['D', 'M'].include?(previous_char))
      result -= symbol_to_value[char]
    else
      result += symbol_to_value[char]
    end
    previous_char = char
  end

  result
end
```

## Python

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        symbol_to_value = {
            'I': 1,
            'V': 5,
            'X': 10,
            'L': 50,
            'C': 100,
            'D': 500,
            'M': 1000,
        }
        result = 0
        previous_char = None

        for i in range(len(s) - 1, -1, -1):
            char = s[i]

            if ('I' == char and previous_char in ['V', 'X']) or \
               ('X' == char and previous_char in ['L', 'C']) or \
               ('C' == char and previous_char in ['D', 'M']):
                result -= symbol_to_value[char]
            else:
                result += symbol_to_value[char]

            previous_char = char

        return result
```

## Java

```java
class Solution {
    public int romanToInt(String s) {
        Map<Character, Integer> symbolToValue = new HashMap<>();
        symbolToValue.put('I', 1);
        symbolToValue.put('V', 5);
        symbolToValue.put('X', 10);
        symbolToValue.put('L', 50);
        symbolToValue.put('C', 100);
        symbolToValue.put('D', 500);
        symbolToValue.put('M', 1000);
        
        var result = 0;
        Character previousChar = null;

        for (var i = s.length() - 1; i >= 0; i--) {
            var currentChar = s.charAt(i);

            if (previousChar != null && (
                (currentChar == 'I' && (previousChar == 'V' || previousChar == 'X')) ||
                (currentChar == 'X' && (previousChar == 'L' || previousChar == 'C')) ||
                (currentChar == 'C' && (previousChar == 'D' || previousChar == 'M')))) {
                result -= symbolToValue.get(currentChar);
            } else {
                result += symbolToValue.get(currentChar);
            }
            
            previousChar = currentChar;
        }
        
        return result;
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **进阶你的开发者身份**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **专业简历 (Resume)：** 告别平庸，生成一份令猎头和面试官眼前一亮的动态技术简历。
> - 🎨 **作品集 (Portfolio)：** 自动聚合 GitHub 贡献与项目经历，将枯燥的代码转化为极具冲击力的视觉作品集。
> - ✍️ **技术博客 (Blog)：** 在纯净、专注的写作空间分享技术见解，树立你的行业影响力。
>
> [**立即前往 Show.dev 打造你的专属品牌 →**](https://www.show.dev)

---

访问原文链接：[13. 罗马数字转整数 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/13-roman-to-integer)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

