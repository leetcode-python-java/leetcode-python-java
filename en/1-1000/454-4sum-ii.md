# 454. 4Sum II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

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

Visit original link: [454. 4Sum II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/454-4sum-ii) for a better experience!

LeetCode link: [454. 4Sum II](https://leetcode.com/problems/4sum-ii), difficulty: **Medium**.

## LeetCode description of "454. 4Sum II"

Given four integer arrays `nums1`, `nums2`, `nums3`, and `nums4` all of length `n`, return the number of tuples `(i, j, k, l)` such that:

- `0 <= i, j, k, l < n`
- `nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0`

### [Example 1]

**Input**: `nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]`

**Output**: `2`

**Explanation**: 

<p>The two tuples are:</p>

<ol>
<li>(0, 0, 0, 1) -&gt; nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0</li>
<li>(1, 1, 0, 0) -&gt; nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0</li>
</ol>


### [Example 2]

**Input**: `nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]`

**Output**: `1`

### [Constraints]

- `n == nums1.length`
- `n == nums2.length`
- `n == nums3.length`
- `n == nums4.length`
- `1 <= n <= 200`
- `-2^28 <= nums1[i], nums2[i], nums3[i], nums4[i] <= 2^28`

## Intuition

1. Because the final requirement is to take one number from each group of numbers, the four groups of numbers can be split into **two groups of two**.
2. Count the number of each `sum`. Use `Map` to store, `key` is `sum`, `value` is `count`.
3. Iterate over `nums3` and `nums4`, if `-(num3 + num4)` exists in `keys` of `Map`, then `count` is included in the total.

## Step-by-Step Solution

1. Count the number of each `sum`. Use `Map` to store, `key` is `sum`, `value` is `count`.

	```python
	num_to_count = defaultdict(int)
	
	for num1 in nums1:
	    for num2 in nums2:
	        num_to_count[num1 + num2] += 1
	```

2. Iterate over `nums3` and `nums4`, if `-(num3 + num4)` exists in `keys` of `Map`, then `count` is included in the total.

	```python
	result = 0
	
	for num3 in nums3:
	    for num4 in nums4:
	        result += num_to_count[-(num3 + num4)]
	
	return result
	```

## Complexity

- Time complexity: `O(N * N)`.
- Space complexity: `O(N)`.

## Java

```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        var numToCount = new HashMap<Integer, Integer>();

        for (var num1 : nums1) {
            for (var num2 : nums2) {
                numToCount.put(
                    num1 + num2,
                    numToCount.getOrDefault(num1 + num2, 0) + 1
                );
            }
        }

        var result = 0;

        for (var num3 : nums3) {
            for (var num4 : nums4) {
                result += numToCount.getOrDefault(-(num3 + num4), 0);
            }
        }

        return result;
    }
}
```

## Python

```python
# from collections import defaultdict

class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        num_to_count = defaultdict(int)

        for num1 in nums1:
            for num2 in nums2:
                num_to_count[num1 + num2] += 1

        result = 0

        for num3 in nums3:
            for num4 in nums4:
                result += num_to_count[-(num3 + num4)]

        return result
```

## JavaScript

```javascript
var fourSumCount = function (nums1, nums2, nums3, nums4) {
  const numToCount = new Map()

  for (const num1 of nums1) {
    for (const num2 of nums2) {
      numToCount.set(num1 + num2, (numToCount.get(num1 + num2) || 0) + 1)
    }
  }

  let result = 0

  for (const num3 of nums3) {
    for (const num4 of nums4) {
      result += numToCount.get(-(num3 + num4)) || 0
    }
  }

  return result
};
```

## C#

```csharp
public class Solution
{
    public int FourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4)
    {
        var numToCount = new Dictionary<int, int>();

        foreach (int num1 in nums1)
        {
            foreach (int num2 in nums2)
            {
                numToCount[num1 + num2] = numToCount.GetValueOrDefault(num1 + num2, 0) + 1;
            }
        }

        int result = 0;

        foreach (int num3 in nums3)
        {
            foreach (int num4 in nums4)
            {
                result += numToCount.GetValueOrDefault(-(num3 + num4), 0);
            }
        }

        return result;
    }
}
```

## Ruby

```ruby
def four_sum_count(nums1, nums2, nums3, nums4)
  num_to_count = Hash.new(0)

  nums1.each do |num1|
    nums2.each do |num2|
      num_to_count[num1 + num2] += 1
    end
  end

  result = 0

  nums3.each do |num3|
    nums4.each do |num4|
      result += num_to_count[-(num3 + num4)]
    end
  end

  result
end
```

## Go

```go
func fourSumCount(nums1 []int, nums2 []int, nums3 []int, nums4 []int) int {
    // Create map to store sum frequencies from first two arrays
    sumCount := make(map[int]int)
    
    // Calculate all possible sums from nums1 and nums2
    for _, num1 := range nums1 {
        for _, num2 := range nums2 {
            sumCount[num1 + num2]++
        }
    }

    result := 0
    // Check complementary sums from nums3 and nums4
    for _, num3 := range nums3 {
        for _, num4 := range nums4 {
            // Add count of complementary sum that would make total zero
            result += sumCount[-(num3 + num4)]
        }
    }

    return result
}
```

## C++

```cpp
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        // Store sum frequencies from first two arrays
        unordered_map<int, int> sumCount;
        
        // Calculate all possible sums from nums1 and nums2
        for (int num1 : nums1) {
            for (int num2 : nums2) {
                sumCount[num1 + num2]++;
            }
        }

        int result = 0;
        // Check complementary sums from nums3 and nums4
        for (int num3 : nums3) {
            for (int num4 : nums4) {
                // Add occurrences of required complement sum
                result += sumCount[-(num3 + num4)];
            }
        }

        return result;
    }
};
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

Visit original link: [454. 4Sum II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/454-4sum-ii) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

