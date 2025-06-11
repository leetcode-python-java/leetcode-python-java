# 151. Reverse Words in a String - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

Visit original link: [151. Reverse Words in a String - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.to/en/leetcode/151-reverse-words-in-a-string) for a better experience!

LeetCode link: [151. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string), difficulty: **Medium**.

## LeetCode description of "151. Reverse Words in a String"

Given an input string `s`, reverse the order of the **words**.

A **word** is defined as a sequence of non-space characters. The **words** in `s` will be separated by at least one space.

Return *a string of the words in reverse order concatenated by a single space*.

**Note** that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

### [Example 1]

**Input**: `s = "the sky is blue"`

**Output**: `"blue is sky the"`

### [Example 2]

**Input**: `s = "  hello world  "`

**Output**: `"world hello"`

### [Example 3]

**Input**: `"a good   example"`

**Output**: `"example good a"`

### [Constraints]

- `1 <= s.length <= 10^4`
- `s` contains English letters (upper-case and lower-case), digits, and spaces `' '`.
- There is **at least one** word in `s`.

**Follow-up**: If the string data type is mutable in your language, can you solve it **in-place** with `O(1)` extra space?



## Intuition

1. Split the string into an array of words (need to remove empty strings)
2. Reverse the order of the words
3. Join the words with a single space

## Step by Step Solutions

1. Split the string using `split(' ')`
2. Remove empty strings
3. Reverse the word array using `reverse`
4. Merge into the final string using `join(' ')`

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(N)`.

## Python

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        words = [word for word in s.split(' ') if word]
        return ' '.join(words[::-1])
```

## Java

```java
class Solution {
    public String reverseWords(String s) {
        var wordList = new ArrayList<String>();
        var words = s.split(" ");

        for (var word : words) {
            if (!word.isEmpty()) {
                wordList.add(word);
            }
        }

        int left = 0;
        int right = wordList.size() - 1;
        while (left < right) {
            Collections.swap(wordList, left, right);
            left++;
            right--;
        }

        return String.join(" ", wordList);
    }
}
```

## C++

```cpp
class Solution {
public:
    string reverseWords(string s) {
        istringstream iss(s);
        string word;
        vector<string> word_list;

        // 1. Extract words from the string.
        // The istringstream >> operator automatically handles
        // multiple spaces between words and leading/trailing spaces.
        while (iss >> word) {
            word_list.push_back(word);
        }

        reverse(word_list.begin(), word_list.end());

        // 2. Join the words with a single space.
        string result = "";
        result = word_list[0];
        for (auto i = 1; i < word_list.size(); ++i) {
            result += " ";
            result += word_list[i];
        }

        return result;
    }
};

```

## JavaScript

```javascript
var reverseWords = function(s) {
  const words = s.split(' ').filter((word) => word !== '');
  return words.reverse().join(' ');
};
```

## Go

```go
func reverseWords(s string) string {
    words := strings.Fields(s) // Fields splits on whitespace and ignores multiple spaces

    // Reverse the words
    for i, j := 0, len(words) - 1; i < j; {
        words[i], words[j] = words[j], words[i]
        i += 1
        j -= 1
    }

    return strings.Join(words, " ")
}
```

## C#

```csharp
public class Solution {
    public string ReverseWords(string s) {
        // Split into words, remove empty entries, reverse
        var words = s.Split(new[] {' '}, StringSplitOptions.RemoveEmptyEntries).Reverse();
        return string.Join(" ", words);
    }
}
```

## Ruby

```ruby
def reverse_words(s)
  s.split(' ').reject(&:empty?).reverse.join(' ')
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCode.to](https://leetcode.to): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [151. Reverse Words in a String - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.to/en/leetcode/151-reverse-words-in-a-string).

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

