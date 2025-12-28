# 13. Roman to Integer - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [13. Roman to Integer - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/13-roman-to-integer) for a better experience!

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

- The character-to-value mapping can be done using a `Map`.
- Intuitively, you add the value of each number you encounter to `result`, iterating from left to right.
- But consider cases like `IV`, where the value of the current character is greater than the value of the previous character. In this case, how should you update the value of `result`?
<details><summary>Click to view the answer</summary><p>Subtract "the value of the previous character * 2".</p></details>

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

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

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [13. Roman to Integer - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/13-roman-to-integer) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

