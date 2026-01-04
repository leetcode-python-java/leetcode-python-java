# 443. String Compression - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

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

Visit original link: [443. String Compression - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/443-string-compression) for a better experience!

LeetCode link: [443. String Compression](https://leetcode.com/problems/string-compression), difficulty: **Medium**.

## LeetCode description of "443. String Compression"

Given an array of characters `chars`, compress it using the following algorithm:

Begin with an empty string `s`. For each group of **consecutive repeating characters** in `chars`:

- If the group's length is `1`, append the character to `s`.
- Otherwise, append the character followed by the group's length.

The compressed string `s` **should not be returned separately**, but instead, be stored **in the input character array** `chars`. Note that group lengths that are `10` or longer will be split into multiple characters in `chars`.

After you are done **modifying the input array**, return *the new length of the array*.

You must write an algorithm that uses only constant extra space.

### [Example 1]

**Input**: `chars = ["a","a","b","b","c","c","c"]`

**Output**: `Return 6, and the first 6 characters of the input array should be: ["a","2","b","2","c","3"]`

**Explanation**: 

<p>The groups are &quot;aa&quot;, &quot;bb&quot;, and &quot;ccc&quot;. This compresses to &quot;a2b2c3&quot;.</p>


### [Example 2]

**Input**: `chars = ["a"]`

**Output**: `Return 1, and the first character of the input array should be: ["a"]`

**Explanation**: 

<p>The only group is &quot;a&quot;, which remains uncompressed since it&#39;s a single character.</p>


### [Example 3]

**Input**: `chars = ["a","b","b","b","b","b","b","b","b","b","b","b","b"]`

**Output**: `Return 4, and the first 4 characters of the input array should be: ["a","b","1","2"].`

**Explanation**: 

<p>The groups are &quot;a&quot; and &quot;bbbbbbbbbbbb&quot;. This compresses to &quot;ab12&quot;.</p>


### [Constraints]

- `1 <= chars.length <= 2000`
- `chars[i]` is a lowercase English letter, uppercase English letter, digit, or symbol.

### [Hints]

<details>
  <summary>Hint 1</summary>
  How do you know if you are at the end of a consecutive group of characters?


  
</details>

## Intuition

We use two pointers (a read pointer `fast` and a write pointer `slow`) and a counter `count` to achieve in-place compression.

1. **Initialization**:
    - Append a sentinel character (e.g., a space " ") to the end of the input array `chars`. This ensures that the last group of consecutive characters can also be correctly processed within the loop. Java and C# is a little different because array is fixed size.
    - `slow = 0`: The `slow` pointer points to the starting character of the current write segment, and it also represents the length of the final compressed array.
    - `count = 1`: Records the number of occurrences of the current consecutive character `chars[slow]`.

2.  **Traversal and Compression**:
    - The `fast` pointer starts traversing the array `chars` from index `1` (until the sentinel character).
    - **Case 1: Character Repetition** (`chars[fast]` is equal to `chars[slow]`)
        - Increment `count`.
    - **Case 2: Character Not Repeated** (`chars[fast]` is not equal to `chars[slow]`)
        - **Subcase 1: Count is 1**
            - Please implement it by yourself
        - **Subcase 2: Count is greater than 1**
            - Please implement it by yourself

3.  **Return Result**:
    - After the `fast` pointer has traversed the entire array (including the sentinel), the value of the `slow` pointer is the new length of the compressed array.


## Pattern of "Fast & Slow Pointers Technique"

```java
int slow = 0; // slow pointer
// ...

for (int fast = 1; fast < array_length; fast++) { // This line is the key!
    if (condition_1) {
        // ...
        continue; // 'continue' is better than 'else' because 'else' will introduce more indents
    }

    if (condition_2) {
        // ...
        continue; // 'continue' is better than 'else'
    }

    // condition_3
    // ...
    slow++;
    // ...
}

return something;
```

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Python

```python
class Solution:
    def compress(self, chars: List[str]) -> int:
        chars.append(" ") # Append an extra special char to process the last char easier
        slow = 0 # Slow pointer. This is the answer.
        count = 1 # Count of consecutive repeating characters

        for fast in range(1, len(chars)):
            if chars[fast] == chars[slow]:
                count += 1
                continue # 'continue' is better than 'else' because 'else' will introduce more indents

            if count == 1:
                slow += 1
                # Don't need to append the 'count' when count is 1.
                chars[slow] = chars[fast]
                continue # 'continue' is better than 'else' because 'else' will introduce more indents

            # Append the 'count'
            for c in str(count):
                slow += 1
                chars[slow] = c

            slow += 1
            chars[slow] = chars[fast]
            count = 1

        return slow
```

## Java

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public int compress(char[] chars) {
        int slow = 0; // Slow pointer. This is the answer.
        int count = 1; // Count of consecutive repeating characters

        for (int fast = 1; fast <= chars.length; fast++) { // it is "<=", not "<"
            var charFast = (fast == chars.length ? ' ' : chars[fast]);

            if (charFast == chars[slow]) {
                count++;
                continue; // 'continue' is better than 'else' because 'else' will introduce more indents
            }

            if (count == 1) {
                slow++;
                // Don't need to append the 'count' when count is 1.
                if (slow < chars.length) {
                    chars[slow] = charFast;
                }
                continue; // 'continue' is better than 'else' because 'else' will introduce more indents
            }

            // Append the 'count'
            for (char c : String.valueOf(count).toCharArray()) {
                slow++;
                chars[slow] = c;
            }

            slow++;
            if (slow < chars.length) {
                chars[slow] = charFast;
            }
            count = 1;
        }

        return slow;
    }
}
```

## C++

```cpp
class Solution {
public:
    int compress(vector<char>& chars) {
        chars.push_back(' '); // Append an extra special char to process the last char easier
        int slow = 0; // Slow pointer. This is the answer.
        int count = 1; // Count of consecutive repeating characters

        for (int fast = 1; fast < chars.size(); ++fast) {
            if (chars[fast] == chars[slow]) {
                count++;
                continue; // 'continue' is better than 'else' because 'else' will introduce more indents
            }

            if (count == 1) {
                slow++;
                // Don't need to append the 'count' when count is 1.
                chars[slow] = chars[fast];
                continue; // 'continue' is better than 'else' because 'else' will introduce more indents
            }

            // Append the 'count'
            for (char c : to_string(count)) {
                slow++;
                chars[slow] = c;
            }

            slow++;
            chars[slow] = chars[fast];
            count = 1;
        }

        return slow;
    }
};
```

## C#

```csharp
public class Solution
{
    public int Compress(char[] chars)
    {
        int slow = 0; // Slow pointer. This is the answer.
        int count = 1; // Count of consecutive repeating characters

        for (int fast = 1; fast <= chars.Length; fast++)
        { // it is "<=", not "<"
            char charFast = (fast == chars.Length ? ' ' : chars[fast]);

            if (charFast == chars[slow])
            {
                count++;
                continue; // 'continue' is better than 'else' because 'else' will introduce more indents
            }

            if (count == 1)
            {
                slow++;
                // Don't need to append the 'count' when count is 1.
                if (slow < chars.Length)
                {
                    chars[slow] = charFast;
                }
                continue; // 'continue' is better than 'else' because 'else' will introduce more indents
            }

            // Append the 'count'
            foreach (char c in count.ToString())
            {
                slow++;
                chars[slow] = c;
            }

            slow++;
            if (slow < chars.Length)
            {
                chars[slow] = charFast;
            }
            count = 1;
        }

        return slow;
    }
}
```

## JavaScript

```javascript
/**
 * @param {character[]} chars
 * @return {number}
 */
var compress = function(chars) {
    chars.push(' ') // Append an extra special char to process the last char easier
    let slow = 0 // Slow pointer. This is the answer.
    let count = 1 // Count of consecutive repeating characters

    for (let fast = 1; fast < chars.length; fast++) {
        if (chars[fast] === chars[slow]) {
            count++
            continue // 'continue' is better than 'else' because 'else' will introduce more indents
        }

        if (count === 1) {
            slow++
            // Don't need to append the 'count' when count is 1.
            chars[slow] = chars[fast]
            continue // 'continue' is better than 'else' because 'else' will introduce more indents
        }

        // Append the 'count'
        for (const c of count.toString()) {
            slow++
            chars[slow] = c
        }

        slow++
        chars[slow] = chars[fast]
        count = 1
    }

    return slow
}
```

## Go

```go
// A test cannot pass. Reason is still unknown

func compress(chars []byte) int {
    chars = append(chars, ' ') // Append an extra special char to process the last char easier
    slow := 0 // Slow pointer. This is the answer.
    count := 1 // Count of consecutive repeating characters

    for fast := 1; fast < len(chars); fast++ {
        if chars[fast] == chars[slow] {
            count++
            continue // 'continue' is better than 'else' because 'else' will introduce more indents
        }

        if count == 1 {
            slow++
            // Don't need to append the 'count' when count is 1.
            chars[slow] = chars[fast]
            continue // 'continue' is better than 'else' because 'else' will introduce more indents
        }

        // Append the 'count'
        for _, c := range strconv.Itoa(count) {
            slow++
            chars[slow] = byte(c)
        }

        slow++
        chars[slow] = chars[fast]
        count = 1
    }

    return slow
}
```

## Ruby

```ruby
# @param {Character[]} chars
# @return {Integer}
def compress(chars)
  chars << " " # Append an extra special char to process the last char easier
  slow = 0 # Slow pointer. This is the answer.
  count = 1 # Count of consecutive repeating characters

  (1...chars.length).each do |fast|
    if chars[fast] == chars[slow]
      count += 1
      next # 'next' is better than 'else' because 'else' will introduce more indents
    end

    if count == 1
      slow += 1
      # Don't need to append the 'count' when count is 1.
      chars[slow] = chars[fast]
      next # 'next' is better than 'else' because 'else' will introduce more indents
    end

    # Append the 'count'
    count.to_s.each_char do |c|
      slow += 1
      chars[slow] = c
    end

    slow += 1
    chars[slow] = chars[fast]
    count = 1
  end

  slow
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
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.leader.me`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [443. String Compression - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/443-string-compression) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

