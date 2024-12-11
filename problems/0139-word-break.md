# 139. Word Break
LeetCode problem: [139. Word Break](https://leetcode.com/problems/word-break/)

## LeetCode problem description
> Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be **reused multiple times** in the segmentation.

```
---------------------------------------------------------------------------------------------
[Example 1]

Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
---------------------------------------------------------------------------------------------
[Example 2]

Input: s = "applepenapple", wordDict = ["apple","pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
---------------------------------------------------------------------------------------------
[Constraints]

1 <= s.length <= 300
1 <= wordDict.length <= 1000
1 <= wordDict[i].length <= 20
's' and 'wordDict[i]' consist of only lowercase English letters.
All the strings of 'wordDict' are unique.
---------------------------------------------------------------------------------------------
```

## Thoughts
This is a `Unbounded Knapsack Problem`.

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Complexity
* Time: `O(n * m)`.
* Space: `O(n)`.

## C#
```c#
public class Solution
{
    public bool WordBreak(string s, IList<string> wordDict)
    {
        var dp = new bool[s.Length + 1];
        dp[0] = true;

        for (var i = 1; i < dp.Length; i++)
        {
            foreach (var word in wordDict)
            {
                if (dp[i])
                {
                    break;
                }

                if (i >= word.Length)
                {
                    dp[i] = dp[i - word.Length] && word == s[(i - word.Length)..i];
                }
            }
        }

        return dp.Last();
    }
}
```

## Python
```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        dp = [False] * (len(s) + 1)
        dp[0] = True

        for i in range(1, len(dp)):
            for word in wordDict:
                if dp[i]:
                    break

                if i >= len(word):
                    dp[i] = dp[i - len(word)] and word == s[i - len(word):i]

        return dp[-1]
```

## C++
```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        auto dp = vector<bool>(s.size() + 1);
        dp[0] = true;

        for (auto i = 1; i < dp.size(); i++) {
            for (auto word : wordDict) {
                if (dp[i]) {
                    break;
                }
                if (i >= word.size()) {
                    dp[i] = dp[i - word.size()] &&
                            word == s.substr(i - word.size(), word.size());
                }
            }
        }

        return dp.back();
    }
};
```

## Java
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        var dp = new boolean[s.length() + 1];
        dp[0] = true;

        for (var i = 1; i < dp.length; i++) {
            for (var word : wordDict) {
                if (dp[i]) {
                    break;
                }
                if (i >= word.length()) {
                    dp[i] = dp[i - word.length()] &&
                            word.equals(s.substring(i - word.length(), i));
                }
            }
        }

        return dp[dp.length - 1];
    }
}
```

## JavaScript
```
var wordBreak = function (s, wordDict) {
  const dp = Array(s.length + 1).fill(false)
  dp[0] = true

  for (let i = 1; i < dp.length; i++) {
    for (const word of wordDict) {
      if (dp[i]) {
        break
      }
      if (i >= word.length) {
        dp[i] = dp[i - word.length] && word == s.slice(i - word.length, i)
      }
    }
  }

  return dp.at(-1)
};
```

## Go
```go
func wordBreak(s string, wordDict []string) bool {
    dp := make([]bool, len(s) + 1)
    dp[0] = true

    for i := 1; i < len(dp); i++ {
        for _, word := range wordDict {
            if dp[i] {
                break
            }
            if i >= len(word) {
                dp[i] = dp[i - len(word)] && word == s[i - len(word):i]
            }
        }
    }

    return dp[len(dp) - 1]
}
```

## Ruby
```ruby
def word_break(s, word_dict)
  dp = Array.new(s.size + 1, false)
  dp[0] = true

  (1...dp.size).each do |i|
    word_dict.each do |word|
      break if dp[i]

      if i >= word.size
        dp[i] = dp[i - word.size] && word == s[(i - word.size)...i]
      end
    end
  end

  dp[-1]
end
```

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
