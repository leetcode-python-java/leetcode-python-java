# 13. Roman to Integer - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

Visit original link: [13. Roman to Integer - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.to/en/leetcode/13-roman-to-integer) for a better experience!

LeetCode link: [13. Roman to Integer](https://leetcode.com/problems/roman-to-integer), difficulty: **Easy**.

## LeetCode description of "13. Roman to Integer"

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, `2` is written as `II` in Roman numeral, just two ones added together. `12` is written as `XII`, which is simply `X` + `II`. The number `27` is written as `XXVII`, which is `XX` + `V` + `II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

`I` can be placed before `V` (5) and `X` (10) to make 4 and 9.
`X` can be placed before `L` (50) and `C` (100) to make 40 and 90.
`C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer.

### [Example 1]

**Input**: `s = "III"`

**Output**: `3`

### [Example 2]

**Input**: `s = "IV"`

**Output**: `4`

### [Example 3]

**Input**: `s = "IX"`

**Output**: `9`

### [Example 4]

**Input**: `s = "LVIII"`

**Output**: `58`

**Explanation**: `L = 50, V= 5, III = 3.`

### [Example 5]

**Input**: `s = "MCMXCIV"`

**Output**: `1994`

**Explanation**: `M = 1000, CM = 900, XC = 90, IV = 4.`

### [Constraints]

- `1 <= s.length <= 15`
- `s` contains only the characters `('I', 'V', 'X', 'L', 'C', 'D', 'M')`.
- It is **guaranteed** that `s` is a valid roman numeral in the range `[1, 3999]`.

### [Hints]

<details>
  <summary>Hint 1</summary>
  Problem is simpler to solve by working the string from back to front and using a map.

  
</details>

## Intuition

* The correspondence between characters and values can be represented with a `Map`.
* The intuition is to add the value to `result` whenever a digit is encountered.
* But cases like `IV` may occur, so you need to consider whether to process from left to right or from right to left. Which processing direction do you choose?
    <details><summary>Click to view the answer</summary><p> Processing from right to left is more convenient, because once you see that the current character and the previous character form a specific combination, you can handle it directly. </p></details> 
* How do you deal with cases like `IV`?
    <details><summary>Click to view the answer</summary><p> Just handle it in reverse. In the forward direction you do addition, but now you do subtraction. </p></details>

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

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

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCode.to](https://leetcode.to): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [13. Roman to Integer - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.to/en/leetcode/13-roman-to-integer).

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).
