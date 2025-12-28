# 605. Can Place Flowers - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [605. Can Place Flowers - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/605-can-place-flowers) for a better experience!

LeetCode link: [605. Can Place Flowers](https://leetcode.com/problems/can-place-flowers), difficulty: **Easy**.

## LeetCode description of "605. Can Place Flowers"

You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in **adjacent** plots.

Given an integer array `flowerbed` containing `0`'s and `1`'s, where `0` means empty and `1` means not empty, and an integer `n`, return `true` if `n` new flowers can be planted in the `flowerbed` without violating the no-adjacent-flowers rule and `false` otherwise.

### [Example 1]

**Input**: `flowerbed = [1,0,0,0,1], n = 1`

**Output**: `true`

### [Example 2]

**Input**: `flowerbed = [1,0,0,0,1], n = 2`

**Output**: `false`

### [Constraints]

- `1 <= flowerbed.length <= 2 * 10^4`
- `flowerbed[i]` is `0` or `1`.
- There are no two adjacent flowers in `flowerbed`.
- `0 <= n <= flowerbed.length`

## Intuition

Check each empty plot (`0`). If both adjacent plots are empty (or boundaries), plant a flower (set to `1`) and count. Return `true` if the final count ≥ `n`, otherwise `false`.

## Pattern of "Greedy Algorithm"

The `Greedy Algorithm` is a strategy that makes the locally optimal choice at each step with the hope of leading to a "globally optimal" solution. In other words, "local optima" can result in "global optima."

## Step-by-Step Solution

1. Initialize counter `count = 0`.
2. Iterate through each plot:
    - If current is `1`, skip.
    - If current is `0` and both adjacent are `0` (or boundaries), plant (`1`), increment `count`.
3. Return `count >= n`.

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Python

```python
class Solution:
    def canPlaceFlowers(self, flowerbed: List[int], n: int) -> bool:
        count = 0

        for i in range(len(flowerbed)):
            if flowerbed[i] == 1:
                continue

            if (i == 0 or flowerbed[i - 1] == 0) and \
               (i == len(flowerbed) - 1 or flowerbed[i + 1] == 0):
                flowerbed[i] = 1
                count += 1

        return count >= n
```

## Java

```java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int count = 0;

        for (int i = 0; i < flowerbed.length; i++) {
            if (flowerbed[i] == 1) {
                continue;
            }

            if ((i == 0 || flowerbed[i - 1] == 0) && 
                (i == flowerbed.length - 1 || flowerbed[i + 1] == 0)) {
                flowerbed[i] = 1;
                count++;
            }
        }

        return count >= n;
    }
}
```

## C++

```cpp
class Solution {
public:
    bool canPlaceFlowers(vector<int>& flowerbed, int n) {
        int count = 0;

        for (int i = 0; i < flowerbed.size(); i++) {
            if (flowerbed[i] == 1) {
                continue;
            }

            if ((i == 0 || flowerbed[i - 1] == 0) && 
                (i == flowerbed.size() - 1 || flowerbed[i + 1] == 0)) {
                flowerbed[i] = 1;
                count++;
            }
        }

        return count >= n;
    }
};
```

## JavaScript

```javascript
var canPlaceFlowers = function(flowerbed, n) {
  let count = 0;

  for (let i = 0; i < flowerbed.length; i++) {
    if (flowerbed[i] === 1) {
      continue;
    }

    if ((i === 0 || flowerbed[i - 1] === 0) && 
      (i === flowerbed.length - 1 || flowerbed[i + 1] === 0)) {
      flowerbed[i] = 1;
      count++;
    }
  }

  return count >= n;  
};

```

## Go

```go
func canPlaceFlowers(flowerbed []int, n int) bool {
    count := 0

    for i := 0; i < len(flowerbed); i++ {
        if flowerbed[i] == 1 {
            continue
        }

        if (i == 0 || flowerbed[i - 1] == 0) && 
           (i == len(flowerbed) - 1 || flowerbed[i + 1] == 0) {
            flowerbed[i] = 1
            count++
        }
    }

    return count >= n
}

```

## C#

```csharp
public class Solution
{
    public bool CanPlaceFlowers(int[] flowerbed, int n)
    {
        int count = 0;

        for (int i = 0; i < flowerbed.Length; i++)
        {
            if (flowerbed[i] == 1)
            {
                continue;
            }

            if ((i == 0 || flowerbed[i - 1] == 0) && 
                (i == flowerbed.Length - 1 || flowerbed[i + 1] == 0))
                {
                flowerbed[i] = 1;
                count++;
            }
        }

        return count >= n;
    }
}
```

## Ruby

```ruby
def can_place_flowers(flowerbed, n)
  count = 0

  flowerbed.each_with_index do |plot, i|
    next if plot == 1

    if (i == 0 || flowerbed[i - 1] == 0) && 
       (i == flowerbed.length - 1 || flowerbed[i + 1] == 0)
      flowerbed[i] = 1
      count += 1
    end
  end

  count >= n
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
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [605. Can Place Flowers - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/605-can-place-flowers) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

