# 1768. Merge Strings Alternately - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired. We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [1768. Merge Strings Alternately - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/1768-merge-strings-alternately) for a better experience!

LeetCode link: [1768. Merge Strings Alternately](https://leetcode.com/problems/merge-strings-alternately), difficulty: **Easy**.

## LeetCode description of "1768. Merge Strings Alternately"

You are given two strings `word1` and `word2`. Merge the strings by adding letters in alternating order, starting with `word1`. If a string is longer than the other, append the additional letters onto the end of the merged string.

Return *the merged string*.

### [Example 1]

**Input**: `word1 = "abc", word2 = "pqr"`

**Output**: `"apbqcr"`

**Explanation**: 

<div class="highlight"><pre class="highlight plaintext"><code>The merged string will be merged as so:
word1:  a   b   c
word2:    p   q   r
merged: a p b q c r
</code></pre></div>

### [Example 2]

**Input**: `word1 = "ab", word2 = "pqrs"`

**Output**: `"apbqrs"`

**Explanation**: 

<div class="highlight"><pre class="highlight plaintext"><code>Notice that as word2 is longer, "rs" is appended to the end.
word1:  a   b 
word2:    p   q   r   s
merged: a p b q   r   s
</code></pre></div>

### [Example 3]

**Input**: `word1 = "abcd", word2 = "pq"`

**Output**: `"apbqcd"`

**Explanation**: 

<div class="highlight"><pre class="highlight plaintext"><code>Notice that as word1 is longer, "cd" is appended to the end.
word1:  a   b   c   d
word2:    p   q 
merged: a p b q c   d
</code></pre></div>

### [Constraints]

- `1 <= word1.length, word2.length <= 100`
- `word1` and `word2` consist of lowercase English letters.

### [Hints]

<details>
  <summary>Hint 1</summary>
  Use two pointers, one pointer for each string. Alternately choose the character from each pointer, and move the pointer upwards.

  
</details>

## Intuition

The problem asks us to merge two strings, `word1` and `word2`, by taking characters alternately, starting with `word1`. If one string is longer than the other, the remaining characters of the longer string should be appended to the end of the merged result.

The core idea is to iterate through both strings simultaneously, picking one character from `word1` and then one from `word2`, and adding them to our result. This process continues as long as we have characters available in *both* strings.

Once we run out of characters in the shorter string, we simply take all the remaining characters from the longer string and append them to our result.

## Step-by-Step Solution

1.  Initialize an empty string (or a list of characters, or a string builder) to store the merged result.
2.  Determine the lengths of `word1` and `word2`. Let these be `n1` and `n2`.
3.  Find the minimum of these two lengths, say `min_len = min(n1, n2)`. This `min_len` is the number of characters we can pick alternately from both strings.
4.  Iterate from `i = 0` up to `min_len - 1`:
    - Append the `i`-th character of `word1` to the result.
    - Append the `i`-th character of `word2` to the result.
5.  After the loop, we have processed `min_len` characters from both strings.
6.  Determine which string potentially has leftover characters. Let this be `longer_word`.
    - If the length of `word1` (`n1`) is greater than `min_len`, then `longer_word` is `word1`.
    - Otherwise `longer_word` is `word2`.
7.  Append the remaining part of `longer_word` (i.e., `longer_word` from index `min_len` onwards) to the `result`.
8.  Return the final merged string.

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(N)`.

## Python

```python
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        min_size = min(len(word1), len(word2))
        result = ""

        for i in range(min_size):
            result += f'{word1[i]}{word2[i]}'

        longer_word = word1 if len(word1) > min_size else word2

        return result + longer_word[min_size:]
```

## Java

```java
class Solution {
    public String mergeAlternately(String word1, String word2) {
        int minSize = Math.min(word1.length(), word2.length());
        StringBuilder result = new StringBuilder();

        for (int i = 0; i < minSize; i++) {
            result.append(word1.charAt(i)).append(word2.charAt(i));
        }

        String longerWord = (word1.length() > word2.length()) ? word1 : word2;
        result.append(longerWord.substring(minSize));

        return result.toString();
    }
}
```

## C++

```cpp
class Solution {
public:
    string mergeAlternately(string word1, string word2) {
        int min_size = min(word1.length(), word2.length());
        string result;

        for (int i = 0; i < min_size; ++i) {
            result += word1[i];
            result += word2[i];
        }

        auto& longer_word = (word1.length() > min_size) ? word1 : word2;
        result += longer_word.substr(min_size);

        return result;
    }
};
```

## JavaScript

```javascript
var mergeAlternately = function(word1, word2) {
  const minSize = Math.min(word1.length, word2.length);
  let result = "";

  for (let i = 0; i < minSize; i++) {
    result += word1[i] + word2[i];
  }

  const longerWord = word1.length > word2.length ? word1 : word2;
  result += longerWord.slice(minSize);

  return result;
};
```

## Go

```go
func mergeAlternately(word1, word2 string) string {
	minSize := int(math.Min(float64(len(word1)), float64(len(word2))))
	var result strings.Builder

	for i := 0; i < minSize; i++ {
		result.WriteByte(word1[i])
		result.WriteByte(word2[i])
	}

	longerWord := word1
	if len(word2) > len(word1) {
		longerWord = word2
	}
	result.WriteString(longerWord[minSize:])

	return result.String()
}
```

## C#

```csharp
public class Solution
{
    public string MergeAlternately(string word1, string word2)
    {
        int minSize = Math.Min(word1.Length, word2.Length);
        var result = new StringBuilder();

        for (int i = 0; i < minSize; i++)
            result.Append(word1[i]).Append(word2[i]);

        string longerWord = word1.Length > word2.Length ? word1 : word2;
        result.Append(longerWord.Substring(minSize));

        return result.ToString();
    }
}
```

## Ruby

```ruby
def merge_alternately(word1, word2)
  min_size = [ word1.size, word2.size ].min
  result = ""

  min_size.times { |i| result << word1[i] << word2[i] }

  longer_word = word1.size > word2.size ? word1 : word2
  result << longer_word[min_size..]

  result
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired. We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [1768. Merge Strings Alternately - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/1768-merge-strings-alternately) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

