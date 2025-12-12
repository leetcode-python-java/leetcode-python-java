# 14. Longest Common Prefix - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**Like.dev**](https://www.like.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Like.dev →**](https://www.like.dev)

---

Visit original link: [14. Longest Common Prefix - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/14-longest-common-prefix) for a better experience!

LeetCode link: [14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix), difficulty: **Easy**.

## LeetCode description of "14. Longest Common Prefix"

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

### [Example 1]

**Input**: `strs = ["flower","flow","flight"]`

**Output**: `"fl"`

### [Example 2]

**Input**: `strs = ["dog","racecar","car"]`

**Output**: `""`

**Explanation**: 

<p>There is no common prefix among the input strings.</p>


### [Constraints]

- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` consists of only lowercase English letters if it is non-empty.

## Intuition

1. To find the longest common prefix, you can scan from left to right, using the characters of the first string as the baseline. 
1. If the current character in the other strings does not match the baseline character, return the result. After each round of iteration, add the baseline character to the common prefix.

## Complexity

- Time complexity: `O(M * N)`.
- Space complexity: `O(1)`.

## Ruby

```ruby
# @param {String[]} strs
# @return {String}
def longest_common_prefix(strs)
  result = ''

  (0...strs[0].size).each do |i|
    char = strs[0][i]

    strs[1..].each do |str|
      if str[i] != char
        return result
      end
    end

    result << char
  end

  result
end

```

## Python

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        result = ''

        for i in range(len(strs[0])):
            char = strs[0][i]

            for string in strs[1:]:
                if i >= len(string) or string[i] != char:
                    return result

            result += char

        return result
```

## Java

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        var result = "";

        for (var i = 0; i < strs[0].length(); i++) {
            var c = strs[0].charAt(i);
            
            for (var j = 1; j < strs.length; j++) {
                if (i >= strs[j].length() || strs[j].charAt(i) != c) {
                    return result;
                }
            }
            
            result += c;
        }

        return result;
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
> We recommend [**Like.dev**](https://www.like.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Like.dev →**](https://www.like.dev)

---

Visit original link: [14. Longest Common Prefix - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/14-longest-common-prefix) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

