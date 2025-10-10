# 383. 赎金信 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

访问原文链接：[383. 赎金信 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/383-ransom-note)，体验更佳！

力扣链接：[383. 赎金信](https://leetcode.cn/problems/ransom-note), 难度等级：**简单**。

## LeetCode “383. 赎金信”问题描述

给你两个字符串：`ransomNote` 和 `magazine` ，判断 `ransomNote` 能不能由 `magazine` 里面的字符构成。

如果可以，返回 `true` ；否则返回 `false` 。

`magazine` 中的每个字符只能在 `ransomNote` 中使用一次。

### [示例 1]

**输入**: `ransomNote = "a", magazine = "b"`

**输出**: `false`

### [示例 2]

**输入**: `ransomNote = "aa", magazine = "ab"`

**输出**: `false`

### [示例 3]

**输入**: `ransomNote = "aa", magazine = "aab"`

**输出**: `true`

### [约束]

- `1 <= ransomNote.length, magazine.length <= 10^5`
- `ransomNote` 和 `magazine` 由小写英文字母组成

## 思路

1. 本题等同于求`magazine`是否能包含`ransomNote`中的所有字符。
2. 先对`magazine`进行统计，得出每个字符对应的字数，结果存储在`Map`中。每一次都是一个加一的操作。
3. 下一步做什么？
    <details><summary>点击查看答案</summary><p>遍历`ransomNote`，对当前字符对应的数量进行减一操作（反向操作）。如果某个字符的数量小于0，则返回`false`。</p></details>

## 步骤

1. 先对`magazine`进行字符和字数统计，结果存储在`Map`中。

	```javascript
	charToCount = new Map()
	
	for (character in magazine) {
	  charToCount[character] += 1
	}
	```

2. 然后，遍历`ransomNote`，并对`Map`中的数据进行反向操作。如果某个字符的字数小于0，则返回`false`。

	```javascript
	charToCount = new Map()
	
	for (character in magazine) {
	  charToCount[character] += 1
	}
	
	for (character in ransomNote) {
	  charToCount[character] -= 1
	
	  if (charToCount[character] < 0) {
	    return false
	  }
	}
	
	return true
	```

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(N)`.

## Java

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        var charToCount = new HashMap<Character, Integer>();

        for (var character : magazine.toCharArray()) {
            charToCount.put(character, charToCount.getOrDefault(character, 0) + 1);
        }

        for (var character : ransomNote.toCharArray()) {
            charToCount.put(character, charToCount.getOrDefault(character, 0) - 1);

            if (charToCount.get(character) < 0) {
                return false;
            }
        }

        return true;
    }
}
```

## Python

```python
# from collections import defaultdict

class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        char_to_count = defaultdict(int)

        for char in magazine:
            char_to_count[char] += 1

        for char in ransomNote:
            char_to_count[char] -= 1

            if char_to_count[char] < 0:
                return False

        return True
```

## JavaScript

```javascript
var canConstruct = function (ransomNote, magazine) {
  const charToCount = new Map()

  for (const character of magazine) {
    charToCount.set(character, (charToCount.get(character) || 0) + 1)
  }

  for (const character of ransomNote) {
    charToCount.set(character, (charToCount.get(character) || 0) - 1)

    if (charToCount.get(character) < 0) {
      return false
    }
  }

  return true
};
```

## C#

```csharp
public class Solution
{
    public bool CanConstruct(string ransomNote, string magazine)
    {
        var charToCount = new Dictionary<char, int>();

        foreach (char character in magazine)
            charToCount[character] = charToCount.GetValueOrDefault(character, 0) + 1;

        foreach (char character in ransomNote)
        {
            charToCount[character] = charToCount.GetValueOrDefault(character, 0) - 1;

            if (charToCount[character] < 0)
            {
                return false;
            }
        }

        return true;
    }
}
```

## Ruby

```ruby
def can_construct(ransom_note, magazine)
  char_to_count = Hash.new(0)

  magazine.each_char { |c| char_to_count[c] += 1 }

  ransom_note.each_char do |c|
    char_to_count[c] -= 1
    return false if char_to_count[c] < 0
  end

  true
end
```

## Go

```go
func canConstruct(ransomNote string, magazine string) bool {
    charToCount := make(map[rune]int)
    
    for _, char := range magazine {
        charToCount[char]++
    }
    
    for _, char := range ransomNote {
        charToCount[char]--
        
        if charToCount[char] < 0 {
            return false
        }
    }
    
    return true
}
```

## C++

```cpp
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        unordered_map<char, int> char_to_count;
        
        for (char character : magazine) {
            char_to_count[character]++;
        }
        
        for (char character : ransomNote) {
            char_to_count[character]--;
            
            if (char_to_count[character] < 0) {
                return false;
            }
        }
        
        return true;
    }
};
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.blog](https://leetcode.blog/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[383. 赎金信 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/383-ransom-note).

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

