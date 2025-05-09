# 1431. Kids With the Greatest Number of Candies - LeetCode Python/Java/C++/JS code

Visit original link: [1431. Kids With the Greatest Number of Candies - LeetCode Python/Java/C++/JS code](https://leetcodepython.com/en/leetcode/1431-kids-with-the-greatest-number-of-candies) for a better experience!

LeetCode link: [1431. Kids With the Greatest Number of Candies](https://leetcode.com/problems/kids-with-the-greatest-number-of-candies), difficulty: **Easy**.

## LeetCode description of "1431. Kids With the Greatest Number of Candies"

There are `n` kids with candies. You are given an integer array `candies`, where each `candies[i]` represents the number of candies the `i-th` kid has, and an integer `extraCandies`, denoting the number of extra candies that you have.

Return a boolean array resu`lt of length `n`, where `result[i]` is `true` if, after giving the `i-th` kid all the `extraCandies`, they will have the **greatest** number of candies among all the kids, or `false` otherwise.

Note that **multiple** kids can have the **greatest** number of candies.

### [Example 1]

**Input**: `candies = [2,3,5,1,3], extraCandies = 3`

**Output**: `[true,true,true,false,true]`

**Explanation**: 

<p>If you give all extraCandies to:<br>
- Kid 1, they will have 2 + 3 = 5 candies, which is the greatest among the kids.<br>
- Kid 2, they will have 3 + 3 = 6 candies, which is the greatest among the kids.<br>
- Kid 3, they will have 5 + 3 = 8 candies, which is the greatest among the kids.<br>
- Kid 4, they will have 1 + 3 = 4 candies, which is not the greatest among the kids.<br>
- Kid 5, they will have 3 + 3 = 6 candies, which is the greatest among the kids.</p>


### [Example 2]

**Input**: `candies = [4,2,1,1,2], extraCandies = 1`

**Output**: `[true,false,false,false,false]`

**Explanation**: 

<p>There is only 1 extra candy.<br>
Kid 1 will always have the greatest number of candies, even if a different kid is given the extra candy.</p>


### [Example 3]

**Input**: `candies = [12,1,12], extraCandies = 10`

**Output**: `[true,false,true]`

### [Constraints]

- `n == candies.length`
- `2 <= n <= 100`
- `1 <= candies[i] <= 100`
- `1 <= extraCandies <= 50`

### [Hints]

<details>
  <summary>Hint 1</summary>
  For each kid check if candies[i] + extraCandies ≥ maximum in Candies[i].

  
</details>

## Intuition

1. Find the maximum number of candies among all kids
2. Check if each kid can reach or exceed this maximum after receiving extra candies

## Step by Step Solutions

1. `max_candy = candies.max` → Directly get the maximum value from the array
2. `candies.map { |c| c + extra_candy >= max_candy }` → Use `map` to iterate and check if each kid can have the most candies

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(N)`.

## Python

```python
class Solution:
    def kidsWithCandies(self, candies: List[int], extra_candy: int) -> List[bool]:
        max_candy = max(candies)
        result = []

        for candy in candies:
            result.append(candy + extra_candy >= max_candy)

        return result
```

## Java

```java
class Solution {
    public List<Boolean> kidsWithCandies(int[] candies, int extraCandy) {
        int maxCandy = Arrays.stream(candies).max().getAsInt();
        List<Boolean> result = new ArrayList<>();

        for (int candy : candies) {
            result.add(candy + extraCandy >= maxCandy);
        }

        return result;
    }
}
```

## C++

```cpp
class Solution {
public:
    vector<bool> kidsWithCandies(vector<int>& candies, int extraCandy) {
        int max_candy = *max_element(candies.begin(), candies.end());
        vector<bool> result;

        for (int candy : candies) {
            result.push_back(candy + extraCandy >= max_candy);
        }

        return result;
    }
};
```

## JavaScript

```javascript
var kidsWithCandies = function(candies, extraCandy) {
  const maxCandy = Math.max(...candies)
  return candies.map((candy) => candy + extraCandy >= maxCandy)
};

```

## Go

```go
func kidsWithCandies(candies []int, extraCandy int) []bool {
    maxCandy := candies[0]
    for _, candy := range candies {
        if candy > maxCandy {
            maxCandy = candy
        }
    }

    result := make([]bool, len(candies))
    for i, candy := range candies {
        result[i] = candy+extraCandy >= maxCandy
    }

    return result
}
```

## C#

```csharp
public class Solution
{
    public IList<bool> KidsWithCandies(int[] candies, int extraCandy)
    {
        int maxCandy = candies.Max();
        return candies.Select(candy => candy + extraCandy >= maxCandy).ToList();
    }
}
```

## Ruby

```ruby
def kids_with_candies(candies, extra_candy)
  max_candy = candies.max
  candies.map { |candy| candy + extra_candy >= max_candy }
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCodePython.com](https://leetcodepython.com): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [1431. Kids With the Greatest Number of Candies - LeetCode Python/Java/C++/JS code](https://leetcodepython.com/en/leetcode/1431-kids-with-the-greatest-number-of-candies).

GitHub repository: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

