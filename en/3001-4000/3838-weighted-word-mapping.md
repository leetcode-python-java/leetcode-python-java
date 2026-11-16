# 3838. Weighted Word Mapping - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at coder.id →**](https://www.coder.id)

Visit original link: [3838. Weighted Word Mapping - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/3838-weighted-word-mapping) for a better experience!

LeetCode link: [3838. Weighted Word Mapping](https://leetcode.com/problems/weighted-word-mapping), difficulty: **Medium**.

## LeetCode description of "3838. Weighted Word Mapping"

You are given an array of strings `words`, where each string represents a word containing lowercase English letters.

You are also given an integer array `weights` of length 26, where `weights[i]` represents the weight of the `i^{th}` lowercase English letter.

The **weight** of a word is defined as the **sum** of the weights of its characters.

For each word, take its weight modulo 26 and map the result to a lowercase English letter using reverse alphabetical order (`0 -> 'z', 1 -> 'y', ..., 25 -> 'a'`).

Return a string formed by concatenating the mapped characters for all words in order.

### [Example 1]

**Input**: `words = ["abcd","def","xyz"], weights = [5,3,12,14,1,2,3,2,10,6,6,9,7,8,7,10,8,9,6,9,9,8,3,7,7,2]`

**Output**: `"rij"`

**Explanation**: 

<ul>
<li>The weight of <code>&quot;abcd&quot;</code> is <code>5 + 3 + 12 + 14 = 34</code>. The result modulo 26 is <code>34 % 26 = 8</code>, which maps to <code>&#39;r&#39;</code>.</li>
<li>The weight of <code>&quot;def&quot;</code> is <code>14 + 1 + 2 = 17</code>. The result modulo 26 is <code>17 % 26 = 17</code>, which maps to <code>&#39;i&#39;</code>.</li>
<li>The weight of <code>&quot;xyz&quot;</code> is <code>7 + 7 + 2 = 16</code>. The result modulo 26 is <code>16 % 26 = 16</code>, which maps to <code>&#39;j&#39;</code>.</li>
</ul>

<p>Thus, the string formed by concatenating the mapped characters is <code>&quot;rij&quot;</code>.</p>


### [Example 2]

**Input**: `words = ["a","b","c"], weights = [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]`

**Output**: `"yyy"`

**Explanation**: 

<p>Each word has weight 1. The result modulo 26 is <code>1 % 26 = 1</code>, which maps to <code>&#39;y&#39;</code>.<br>
Thus, the string formed by concatenating the mapped characters is <code>&quot;yyy&quot;</code>.</p>


### [Example 3]

**Input**: `words = ["abcd"], weights = [7,5,3,4,3,5,4,9,4,2,2,7,10,2,5,10,6,1,2,2,4,1,3,4,4,5]`

**Output**: `"g"`

**Explanation**: 

<p>The weight of <code>&quot;abcd&quot;</code> is <code>7 + 5 + 3 + 4 = 19</code>. The result modulo 26 is <code>19 % 26 = 19</code>, which maps to <code>&#39;g&#39;</code>.<br>
Thus, the string formed by concatenating the mapped characters is <code>&quot;g&quot;</code>.</p>


### [Constraints]

- `1 <= words.length <= 100`
- `1 <= words[i].length <= 10`
- `weights.length == 26`
- `1 <= weights[i] <= 100`
- `words[i]` consists of lowercase English letters.

### [Hints]

<details>
  <summary>Hint 1</summary>
  For each word, sum character weights using `weights[c - 'a']`

  
</details>

<details>
  <summary>Hint 2</summary>
  Take the sum modulo `26`

  
</details>

<details>
  <summary>Hint 3</summary>
  Map the value to a character using reverse order: `char = 'z' - value`

  
</details>

<details>
  <summary>Hint 4</summary>
  Append all mapped characters in order to form the result string

  
</details>

## Intuition

The problem is a straightforward simulation of mapping rules. For each string in the given `words` array, we need to calculate a "weight". This weight is the sum of the weights of all characters in the word, where the character's weight is determined by mapping its alphabetical index to the `weights` array.

After finding the sum, we apply the modulo 26 operation. Finally, we map this resulting value to a character in reverse alphabetical order, which mathematically corresponds to subtracting the value from the ASCII code of `'z'` and converting it back to a character. We concatenate the resulting characters for all words and return the final string.

## Step-by-Step Solution

1. Initialize an empty list or string builder to collect the mapped characters.
2. Iterate through each `word` in the `words` array.
3. For each `word`, initialize a `sum` to 0. Iterate through each character `c` in the word, and add `weights[c - 'a']` to `sum`.
4. Take the calculated `sum` modulo 26 to get the mapped value.
5. Convert this value to a character using the reverse alphabetical rule: `char = 'z' - value`.
6. Append the computed character to the string builder.
7. After processing all words, return the concatenated string.

## Complexity

> - **Time Complexity:** `O(N * M)`
  We iterate through all `N` words in the array, and for each word, we iterate through its `M` characters. Thus, the time complexity is strictly proportional to the total number of characters across all words.
- **Space Complexity:** `O(N)`
  We use a string builder or array to store the resulting mapped character for each word. Since there are `N` words, the resulting string will have length `N`. Thus, the auxiliary space is `O(N)`.

- Time complexity: `O(N * M)`.
- Space complexity: `O(N * M)`.

## Python

```python
class Solution:
    def mapWordWeights(self, words: List[str], weights: List[int]) -> str:
        # Array to store the mapped characters for each word
        result = []
        
        # Iterate over each word in the input list
        for word in words:
            # Calculate the sum of weights for the characters in the current word
            word_weight = 0
            for char in word:
                # Get the weight of the character by mapping it to its index (0 for 'a', 1 for 'b', etc.)
                word_weight += weights[ord(char) - ord('a')]
            
            # Take the sum modulo 26 as specified in the problem
            mapped_val = word_weight % 26
            
            # Map the value to a character using reverse alphabetical order ('z' - value)
            mapped_char = chr(ord('z') - mapped_val)
            
            # Append the mapped character to the result list
            result.append(mapped_char)
            
        # Join the characters into a single string and return
        return "".join(result)
```

## Java

```java
class Solution {
    public String mapWordWeights(String[] words, int[] weights) {
        // Use a StringBuilder for efficient string concatenation
        StringBuilder result = new StringBuilder();
        
        // Iterate through each word in the array
        for (String word : words) {
            int wordWeight = 0;
            
            // Sum the weights of all characters in the current word
            for (char c : word.toCharArray()) {
                // Determine the 0-indexed position of the character
                wordWeight += weights[c - 'a'];
            }
            
            // Modulo 26 operation
            int mappedVal = wordWeight % 26;
            
            // Calculate the mapped character using reverse alphabetical order
            // Since 'z' is the starting point (0 -> 'z'), we subtract the mapped value
            char mappedChar = (char) ('z' - mappedVal);
            
            // Append the mapped character to our result
            result.append(mappedChar);
        }
        
        // Convert the StringBuilder to String and return
        return result.toString();
    }
}
```

## JavaScript

```javascript
/**
 * @param {string[]} words
 * @param {number[]} weights
 * @return {string}
 */
var mapWordWeights = function(words, weights) {
    // Array to collect the resulting characters
    let result = [];
    
    // Process each word one by one
    for (let word of words) {
        let wordWeight = 0;
        
        // Sum up the weight of each character in the word
        for (let i = 0; i < word.length; i++) {
            // Find the character code difference from 'a'
            let charIndex = word.charCodeAt(i) - 97; // 97 is the ASCII for 'a'
            wordWeight += weights[charIndex];
        }
        
        // Apply modulo 26 to the sum
        let mappedVal = wordWeight % 26;
        
        // Map it back to a character starting backwards from 'z' (ASCII 122)
        let mappedChar = String.fromCharCode(122 - mappedVal);
        
        // Push to the result array
        result.push(mappedChar);
    }
    
    // Join the array into a string and return
    return result.join('');
};
```

## C++

```cpp
class Solution {
public:
    string mapWordWeights(vector<string>& words, vector<int>& weights) {
        // String to store the concatenated mapped characters
        string result = "";
        
        // Process each word in the input
        for (const string& word : words) {
            int wordWeight = 0;
            
            // Sum the weights corresponding to each character
            for (char c : word) {
                // Find the index by subtracting the ASCII value of 'a'
                wordWeight += weights[c - 'a'];
            }
            
            // Perform the modulo 26 operation
            int mappedVal = wordWeight % 26;
            
            // Deduct the mapped value from 'z' to get the reversed mapped character
            char mappedChar = 'z' - mappedVal;
            
            // Append it to the result string
            result += mappedChar;
        }
        
        return result;
    }
};
```

## C#

```csharp
public class Solution {
    public string mapWordWeights(string[] words, int[] weights) {
        // StringBuilder is optimal for creating strings character by character
        System.Text.StringBuilder result = new System.Text.StringBuilder();
        
        // Iterate over each string in words
        foreach (string word in words) {
            int wordWeight = 0;
            
            // Calculate total weight of the word
            foreach (char c in word) {
                // c - 'a' yields the 0-based index of the alphabet
                wordWeight += weights[c - 'a'];
            }
            
            // Modulo 26 ensures the value is between 0 and 25
            int mappedVal = wordWeight % 26;
            
            // Map the value in reverse order (0 -> 'z', 1 -> 'y', etc.)
            char mappedChar = (char)('z' - mappedVal);
            
            // Append the mapped character
            result.Append(mappedChar);
        }
        
        // Return the final concatenated string
        return result.ToString();
    }
}
```

## Go

```go
func mapWordWeights(words []string, weights []int) string {
    // Use a byte slice to efficiently build the result string
    result := make([]byte, 0, len(words))
    
    // Iterate through all the words
    for _, word := range words {
        wordWeight := 0
        
        // Iterate through each character of the word
        for i := 0; i < len(word); i++ {
            // Find character index (0-25) by subtracting ASCII of 'a'
            charIndex := word[i] - 'a'
            wordWeight += weights[charIndex]
        }
        
        // Take modulo 26
        mappedVal := wordWeight % 26
        
        // Reverse alphabetical mapping: 'z' - mappedVal
        mappedChar := byte('z' - mappedVal)
        
        // Append the character to our byte slice
        result = append(result, mappedChar)
    }
    
    // Convert byte slice back to string
    return string(result)
}
```

## Ruby

```ruby
# @param {String[]} words
# @param {Integer[]} weights
# @return {String}
def map_word_weights(words, weights)
    result = ""
    
    # Process each word individually
    words.each do |word|
        word_weight = 0
        
        # Iterate over each character's byte value
        word.each_byte do |byte|
            # byte of 'a' is 97, so we subtract 97 to get the index
            char_index = byte - 97
            word_weight += weights[char_index]
        end
        
        # Take the weight modulo 26
        mapped_val = word_weight % 26
        
        # Convert the reverse alphabetical mapped value back to a character
        # 'z'.ord is 122
        mapped_char = (122 - mapped_val).chr
        
        # Append the character to the result string
        result << mapped_char
    end
    
    result
end
```

## Rust

```rust
impl Solution {
    pub fn map_word_weights(words: Vec<String>, weights: Vec<i32>) -> String {
        // String to store our concatenated results
        let mut result = String::with_capacity(words.len());
        
        // Iterate over all words
        for word in words {
            let mut word_weight = 0;
            
            // Calculate the total weight of the word
            for c in word.bytes() {
                // b'a' is the byte value of 'a'
                let char_index = (c - b'a') as usize;
                word_weight += weights[char_index];
            }
            
            // Modulo 26 operation
            let mapped_val = word_weight % 26;
            
            // Map the value to reverse alphabetical order (b'z' is 122)
            let mapped_char = (b'z' - mapped_val as u8) as char;
            
            // Push the character to our result string
            result.push(mapped_char);
        }
        
        result
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun mapWordWeights(words: Array<String>, weights: IntArray): String {
        // StringBuilder is used to concatenate characters efficiently
        val result = java.lang.StringBuilder()
        
        // Loop over each word in the array
        for (word in words) {
            var wordWeight = 0
            
            // Calculate the sum of weights for the characters in the word
            for (c in word) {
                wordWeight += weights[c - 'a']
            }
            
            // Modulo 26 for the mapping rule
            val mappedVal = wordWeight % 26
            
            // Calculate reverse alphabetical character starting from 'z'
            val mappedChar = ('z' - mappedVal).toChar()
            
            // Append the mapped character to the StringBuilder
            result.append(mappedChar)
        }
        
        // Return the accumulated characters as a string
        return result.toString()
    }
}
```

## Swift

```swift
class Solution {
    func mapWordWeights(_ words: [String], _ weights: [Int]) -> String {
        // String to collect the mapped characters
        var result = ""
        
        // Process each word in the array
        for word in words {
            var wordWeight = 0
            
            // Sum the weights of the characters in the current word
            for char in word {
                // Get the ASCII value of the character and subtract ASCII of 'a'
                let charIndex = Int(char.asciiValue!) - Int(Character("a").asciiValue!)
                wordWeight += weights[charIndex]
            }
            
            // Take the sum modulo 26
            let mappedVal = wordWeight % 26
            
            // Map the value using reverse alphabetical order
            let mappedAscii = Int(Character("z").asciiValue!) - mappedVal
            let mappedChar = Character(UnicodeScalar(mappedAscii)!)
            
            // Append the mapped character
            result.append(mappedChar)
        }
        
        return result
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
> We recommend [**coder.id**](https://www.coder.id) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.coder.id`.
>
> [**Build Your Programmer Brand at coder.id →**](https://www.coder.id)

---

Visit original link: [3838. Weighted Word Mapping - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/3838-weighted-word-mapping) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

