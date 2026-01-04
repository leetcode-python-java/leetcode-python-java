# 383. Ransom Note - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.leader.me`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [383. Ransom Note - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/383-ransom-note) for a better experience!

LeetCode link: [383. Ransom Note](https://leetcode.com/problems/ransom-note), difficulty: **Easy**.

## LeetCode description of "383. Ransom Note"

Given two strings `ransomNote` and `magazine`, return `true` if `ransomNote` can be constructed by using the letters from `magazine` and `false` otherwise.

Each letter in `magazine` can only be used once in `ransomNote`.

### [Example 1]

**Input**: `ransomNote = "a", magazine = "b"`

**Output**: `false`

### [Example 2]

**Input**: `ransomNote = "aa", magazine = "ab"`

**Output**: `false`

### [Example 3]

**Input**: `ransomNote = "aa", magazine = "aab"`

**Output**: `true`

### [Constraints]

- `1 <= ransomNote.length, magazine.length <= 10^5`
- `ransomNote` and `magazine` consist of lowercase English letters.

## Intuition

1. This question is equivalent to asking whether `magazine` can contain all the characters in `ransomNote`.

2. First count `magazine` to get the number of words corresponding to each character, and store the result in `Map`. Each time is an addition one operation.

3. What to do next?

    <details><summary>Click to view the answer</summary><p> Traverses `ransomNote` and subtracts one from the number corresponding to the current character (reverse operation). If the number of a character is less than 0, return `false`. </p></details>

## Step-by-Step Solution

1. First count the characters in `magazine`, and store the results in `Map`.

	```javascript
	charToCount = new Map()
	
	for (character in magazine) {
	  charToCount[character] += 1
	}
	```

2. Then, traverse `ransomNote` and perform reverse operations on the data in `Map`. If the count of a character is less than 0, return `false`.

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

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(N)`.

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

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.leader.me`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [383. Ransom Note - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/383-ransom-note) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

