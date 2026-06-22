# 1189. “气球” 的最大数量 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[1189. “气球” 的最大数量 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/1189-maximum-number-of-balloons)，体验更佳！

力扣链接：[1189. “气球” 的最大数量](https://leetcode.cn/problems/maximum-number-of-balloons), 难度等级：**简单**。

## LeetCode “1189. “气球” 的最大数量”问题描述

给你一个字符串 `text`，你需要使用 `text` 中的字母来拼凑尽可能多的单词 **"balloon"（气球）**。

字符串 `text` 中的每个字母最多只能被使用一次。请你返回最多可以拼凑出多少个单词 **"balloon"**。

### [示例 1]

![](../../images/examples/1189_1.jpg)

**输入**: `text = "nlaebolko"`

**输出**: `1`

### [示例 2]

![](../../images/examples/1189_2.jpg)

**输入**: `text = "loonbalxballpoon"`

**输出**: `2`

### [示例 3]

**输入**: `text = "leetcode"`

**输出**: `0`

### [约束]

- `1 <= text.length <= 10^4`
- `text` 全部由小写英文字母组成
- **注意:** 本题与 2287 题重排字符形成目标字符串相同。

### [Hints]

<details>
  <summary>提示 1</summary>
  Count the frequency of letters in the given string.

  
</details>

<details>
  <summary>提示 2</summary>
  Find the letter that can make the minimum number of instances of the word "balloon".

  
</details>

## 思路

为了拼凑出单词 "balloon"，我们特别需要字符 'b', 'a', 'l', 'o' 和 'n'。需要注意的是，字符 'l' 和 'o' 在单词 "balloon" 中各出现了两次，而其他字符只出现了一次。
因此，我们能拼凑出 "balloon" 的最大数量，受限于相对需求量最匮乏的那个字符（木桶效应）。我们可以简单地统计字符串中所有字符的频率，将 'l' 和 'o' 的数量减半（因为每个单词需要 2 个），然后找出这 5 个必需字符频率中的最小值。

## 步骤

1. 初始化一个大小为 26 的数组或哈希表 `cnt`，用来统计给定字符串 `text` 中每个小写英文字母出现的频率。
2. 遍历 `text` 中的每个字符，并在 `cnt` 中递增对应字符的计数。
3. 因为单词 "balloon" 需要两个 'l' 和两个 'o'，所以将 `cnt['l']` 和 `cnt['o']` 的值整除以 2。
4. 我们最多能拼凑出的 "balloon" 数量，就是 'b', 'a', 'l', 'o' 和 'n' 这五个字符计数中的最小值。
5. 返回这个最小值。

## 复杂度

> - **时间复杂度**: `O(N)`，其中 `N` 是字符串 `text` 的长度。我们只需要遍历字符串一次来统计字符出现的次数，由于最后只检查 5 个特定字符的数量，求最小值的过程是 `O(1)` 的时间。
- **空间复杂度**: `O(1)` 或 `O(C)`，其中 `C` 是字符集的大小（对于小写英文字母，`C=26`）。计数数组的大小是常数级别的。

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

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

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**leader.me**](https://www.leader.me) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.leader.me`，极具职业含金量的专属域名。

>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[1189. “气球” 的最大数量 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/1189-maximum-number-of-balloons)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

