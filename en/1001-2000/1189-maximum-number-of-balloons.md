# 1189. Maximum Number of Balloons - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

Visit original link: [1189. Maximum Number of Balloons - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/1189-maximum-number-of-balloons) for a better experience!

LeetCode link: [1189. Maximum Number of Balloons](https://leetcode.com/problems/maximum-number-of-balloons), difficulty: **Easy**.

## LeetCode description of "1189. Maximum Number of Balloons"

Given a string `text`, you want to use the characters of `text` to form as many instances of the word **"balloon"** as possible.

You can use each character in `text` **at most once**. Return the maximum number of instances that can be formed.

### [Example 1]

![](../../images/examples/1189_1.jpg)

**Input**: `text = "nlaebolko"`

**Output**: `1`

### [Example 2]

![](../../images/examples/1189_2.jpg)

**Input**: `text = "loonbalxballpoon"`

**Output**: `2`

### [Example 3]

**Input**: `text = "leetcode"`

**Output**: `0`

### [Constraints]

- `1 <= text.length <= 10^4`
- `text` consists of lower case English letters only.
- **Note:** This question is the same as 2287: Rearrange Characters to Make Target String.

### [Hints]

<details>
  <summary>Hint 1</summary>
  Count the frequency of letters in the given string.

  
</details>

<details>
  <summary>Hint 2</summary>
  Find the letter that can make the minimum number of instances of the word "balloon".

  
</details>

## Intuition

To form the word "balloon", we specifically need the characters 'b', 'a', 'l', 'o', and 'n'. Note that the characters 'l' and 'o' each appear twice in the word "balloon", while the others appear only once.

Therefore, the maximum number of times we can form "balloon" is bottlenecked by the character that is least available relative to its required amount. We can simply count the frequency of all characters in the string, halve the counts of 'l' and 'o' (since we need 2 of each per word), and then find the minimum count among the 5 required characters.

## Step-by-Step Solution

1. Initialize an array or hash map `cnt` of size 26 to count the frequencies of each lowercase English letter in the given `text`.
2. Iterate through each character in `text` and increment its corresponding count in `cnt`.
3. Since the word "balloon" requires two 'l's and two 'o's, integer-divide `cnt['l']` and `cnt['o']` by 2.
4. The maximum number of "balloon"s we can form is the minimum value among the counts of 'b', 'a', 'l', 'o', and 'n'.
5. Return this minimum value.

## Complexity

> - **Time Complexity**: `O(N)`, where `N` is the length of the string `text`. We only need to traverse the string once to count the characters, and finding the minimum takes `O(1)` time since we only check 5 specific characters.
- **Space Complexity**: `O(1)` or `O(C)`, where `C` is the size of the character set (26 for lowercase English letters). The size of the counting array is constant.

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Python

```python
class Solution:
    def maxNumberOfBalloons(self, text: str) -> int:
        # Count the frequency of all characters in the text
        cnt = Counter(text)
        
        # 'l' and 'o' are required twice for each "balloon"
        cnt['l'] //= 2
        cnt['o'] //= 2
        
        # Return the minimum frequency among the required characters
        return min(cnt[c] for c in "balon")
```

## Java

```java
class Solution {
    public int maxNumberOfBalloons(String text) {
        int[] cnt = new int[26];
        
        // Count the frequency of each character
        for (char c : text.toCharArray()) {
            cnt[c - 'a']++;
        }
        
        // Halve the counts for 'l' and 'o' since "balloon" needs two of each
        cnt['l' - 'a'] /= 2;
        cnt['o' - 'a'] /= 2;
        
        // Find the minimum count among 'b', 'a', 'l', 'o', 'n'
        int ans = Integer.MAX_VALUE;
        for (char c : "balon".toCharArray()) {
            ans = Math.min(ans, cnt[c - 'a']);
        }
        
        return ans;
    }
}
```

## JavaScript

```javascript
/**
 * @param {string} text
 * @return {number}
 */
var maxNumberOfBalloons = function(text) {
    const cnt = new Array(26).fill(0);
    
    // Count the frequency of each character
    for (let i = 0; i < text.length; i++) {
        cnt[text.charCodeAt(i) - 97]++;
    }
    
    // Calculate the max instances by checking bottlenecks
    // 1: 'b', 0: 'a', 11: 'l' (needs 2), 14: 'o' (needs 2), 13: 'n'
    return Math.min(
        cnt[1],
        cnt[0],
        Math.floor(cnt[11] / 2),
        Math.floor(cnt[14] / 2),
        cnt[13]
    );
};
```

## Cpp

```cpp
class Solution {
public:
    int maxNumberOfBalloons(string text) {
        int cnt[26] = {0};
        
        // Count the frequency of each character
        for (char c : text) {
            cnt[c - 'a']++;
        }
        
        // Halve the counts for 'l' and 'o'
        cnt['l' - 'a'] /= 2;
        cnt['o' - 'a'] /= 2;
        
        int ans = INT_MAX;
        string target = "balon";
        
        // Find the minimum available count among the required characters
        for (char c : target) {
            ans = min(ans, cnt[c - 'a']);
        }
        
        return ans;
    }
};
```

## Csharp

```csharp
public class Solution {
    public int MaxNumberOfBalloons(string text) {
        int[] cnt = new int[26];
        
        // Count the frequency of each character
        foreach (char c in text) {
            cnt[c - 'a']++;
        }
        
        // Halve the counts for 'l' and 'o'
        cnt['l' - 'a'] /= 2;
        cnt['o' - 'a'] /= 2;
        
        int ans = int.MaxValue;
        
        // Find the minimum available count among the required characters
        foreach (char c in "balon") {
            ans = Math.Min(ans, cnt[c - 'a']);
        }
        
        return ans;
    }
}
```

## Go

```go
func maxNumberOfBalloons(text string) int {
    cnt := [26]int{}
    
    // Count the frequency of each character
    for _, c := range text {
        cnt[c-'a']++
    }
    
    // Halve the counts for 'l' and 'o'
    cnt['l'-'a'] /= 2
    cnt['o'-'a'] /= 2
    
    ans := 1 << 30
    
    // Find the minimum available count among the required characters
    for _, c := range "balon" {
        if cnt[c-'a'] < ans {
            ans = cnt[c-'a']
        }
    }
    
    return ans
}
```

## Ruby

```ruby
# @param {String} text
# @return {Integer}
def max_number_of_balloons(text)
    cnt = Array.new(26, 0)
    
    # Count the frequency of each character
    text.each_char do |c|
        cnt[c.ord - 97] += 1
    end
    
    # Halve the counts for 'l' and 'o'
    cnt['l'.ord - 97] /= 2
    cnt['o'.ord - 97] /= 2
    
    ans = Float::INFINITY
    
    # Find the minimum available count among the required characters
    "balon".each_char do |c|
        ans = [ans, cnt[c.ord - 97]].min
    end
    
    ans
end
```

## Rust

```rust
impl Solution {
    pub fn max_number_of_balloons(text: String) -> i32 {
        let mut cnt = [0; 26];
        
        // Count the frequency of each character
        for c in text.chars() {
            cnt[(c as u8 - b'a') as usize] += 1;
        }
        
        // Halve the counts for 'l' and 'o'
        cnt[(b'l' - b'a') as usize] /= 2;
        cnt[(b'o' - b'a') as usize] /= 2;
        
        let mut ans = i32::MAX;
        
        // Find the minimum available count among the required characters
        for c in "balon".chars() {
            ans = ans.min(cnt[(c as u8 - b'a') as usize]);
        }
        
        ans
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun maxNumberOfBalloons(text: String): Int {
        val cnt = IntArray(26)
        
        // Count the frequency of each character
        for (c in text) {
            cnt[c - 'a']++
        }
        
        // Halve the counts for 'l' and 'o'
        cnt['l' - 'a'] /= 2
        cnt['o' - 'a'] /= 2
        
        var ans = Int.MAX_VALUE
        
        // Find the minimum available count among the required characters
        for (c in "balon") {
            ans = Math.min(ans, cnt[c - 'a'])
        }
        
        return ans
    }
}
```

## Swift

```swift
class Solution {
    func maxNumberOfBalloons(_ text: String) -> Int {
        var cnt = Array(repeating: 0, count: 26)
        let aAscii = Character("a").asciiValue!
        
        // Count the frequency of each character
        for c in text {
            cnt[Int(c.asciiValue! - aAscii)] += 1
        }
        
        // Halve the counts for 'l' and 'o'
        cnt[Int(Character("l").asciiValue! - aAscii)] /= 2
        cnt[Int(Character("o").asciiValue! - aAscii)] /= 2
        
        var ans = Int.max
        
        // Find the minimum available count among the required characters
        for c in "balon" {
            ans = min(ans, cnt[Int(c.asciiValue! - aAscii)])
        }
        
        return ans
    }
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
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.leader.me`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [1189. Maximum Number of Balloons - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/1189-maximum-number-of-balloons) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

