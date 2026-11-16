# 49. Group Anagrams - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at coder.id →**](https://www.coder.id)

Visit original link: [49. Group Anagrams - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/49-group-anagrams) for a better experience!

LeetCode link: [49. Group Anagrams](https://leetcode.com/problems/group-anagrams), difficulty: **Medium**.

## LeetCode description of "49. Group Anagrams"

Given an array of strings `strs`, group the **anagrams** together. You can return the answer in **any order**.

> An anagram is a word or phrase formed by rearranging the letters of a different word or phrase, using all the original letters exactly once.

### [Example 1]

**Input**: `strs = ["eat", "tea", "tan", "ate", "nat", "bat"]`

**Output**: `[["bat"],["nat","tan"],["ate","eat","tea"]]`

### [Example 2]

**Input**: `strs = [""]`

**Output**: `[[""]]`

### [Example 3]

**Input**: `strs = ["a"]`

**Output**: `[["a"]]`

### [Constraints]

- `1 <= strs.length <= 10^4`
- `0 <= strs[i].length <= 100`
- `strs[i]` consists of lowercase English letters.

## Intuition

- Two strings, `bat` and `atb`, what is the fastest way to know that they are anagrams?

    <details><summary>Click to view the answer</summary><p>Sort each string in alphabetical order, and then compare the sorted strings. If they are equal, then they are anagrams.</p></details>

- But after sorting, the original string is not taken into account, and the result is the grouping of the original string. How to solve it?

    <details><summary>Click to view the answer</summary><p> Use tuples, that is, put the alphabetically sorted string and the original string in a tuple, like this: `("abt", "bat")`.</p></details>

- All that remains to do is to group this tuple array. What is the easiest way to group?

    <details><summary>Click to view the answer</summary><p> Use `Map`, `key` is the alphabetically sorted string, and value is the array of the original string.</p></details>

## Complexity

> M = string.length

- Time complexity: `O(N * M * logM)`.
- Space complexity: `O(N)`.

## Python

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        pairs = [(''.join(sorted(string)), string) for string in strs]

        ordered_to_original = defaultdict(list)

        for ordered, original in pairs:
            ordered_to_original[ordered].append(original)

        return list(ordered_to_original.values())

# More concise solution:
class Solution:
    def groupAnagrams(self, strs: list[str]) -> list[list[str]]:
        s_to_list = defaultdict(list)

        for s in strs:
            s_to_list[
                ''.join(sorted(s))
            ].append(s)
        
        print(s_to_list) # defaultdict(<class 'list'>, {'aet': ['eat', 'tea', 'ate'], 'ant': ['tan', 'nat'], 'abt': ['bat']})

        return list(s_to_list.values())

```

## Ruby

```ruby
# @param {String[]} strs
# @return {String[][]}
def group_anagrams(strs)
  result = Hash.new([])
  strs.each do |str|
    result[str.chars.sort.join] += [str]
  end
  result.values
end

# Or solution 2: More concise way

# @param {String[]} strs
# @return {String[][]}
def group_anagrams(strs)
  strs.group_by { |string| string.chars.sort }.values
end
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

Visit original link: [49. Group Anagrams - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/49-group-anagrams) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

