# 209. Minimum Size Subarray Sum - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

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

Visit original link: [209. Minimum Size Subarray Sum - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/209-minimum-size-subarray-sum) for a better experience!

LeetCode link: [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum), difficulty: **Medium**.

## LeetCode description of "209. Minimum Size Subarray Sum"

Given an array of positive integers `nums` and a positive integer `target`, return *the* ***minimal length*** *of a* ***subarray*** *whose sum is greater than or equal to `target`*. If there is no such subarray, return `0` instead.

> A **subarray** is a contiguous non-empty sequence of elements within an array.

### [Example 1]

**Input**: `target = 7, nums = [2,3,1,2,4,3]`

**Output**: `2`

**Explanation**: 

<p>The subarray [4,3] has the minimal length under the problem constraint.</p>


### [Example 2]

**Input**: `target = 4, nums = [1,4,4]`

**Output**: `1`

**Explanation**: `target = 11, nums = [1,1,1,1,1,1,1,1]`

### [Example 3]

**Input**: `target = 11, nums = [1,1,1,1,1,1,1,1]`

**Output**: `0`

### [Constraints]

- `1 <= target <= 10^9`
- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^4`

## Intuition

For **subarray** problems, you can consider using **Sliding Window Technique**, which is similar to the **Fast & Slow Pointers Approach**.

## Step-by-Step Solution

1. Iterate over the `nums` array, the `index` of the element is named `fastIndex`. Although inconspicuous, this is the most important logic of the *Fast & Slow Pointers Approach*. Please memorize it.

2. `sum += nums[fast_index]`.

    ```java
    var minLength = Integer.MAX_VALUE;
    var sum = 0;
    var slowIndex = 0;
	
    for (var fastIndex = 0; fastIndex < nums.length; fastIndex++) { // This line the most important logic of the `Fast and Slow Pointers Technique`.
        sum += nums[fastIndex]; // 1
    }
	
    return minLength;
    ```

3. Control of `slowIndex`:

	```java
	var minLength = Integer.MAX_VALUE;
	var sum = 0;
	var slowIndex = 0;
	
	for (var fastIndex = 0; fastIndex < nums.length; fastIndex++) {
	    sum += nums[fastIndex];
	
	    while (sum >= target) { // 1
	        minLength = Math.min(minLength, fastIndex - slowIndex + 1); // 2
	        sum -= nums[slowIndex]; // 3
	        slowIndex++; // 4
	    }
	}
	
	if (minLength == Integer.MAX_VALUE) { // 5
	    return 0; // 6
	}
	
	return minLength;
	```


## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Java

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        var minLength = Integer.MAX_VALUE;
        var sum = 0;
        var slowIndex = 0;

        for (var fastIndex = 0; fastIndex < nums.length; fastIndex++) { // This line is the most important. You'd better memorize it.
            sum += nums[fastIndex];

            while (sum >= target) {
                minLength = Math.min(minLength, fastIndex - slowIndex + 1);
                sum -= nums[slowIndex];
                slowIndex++;
            }
        }

        if (minLength == Integer.MAX_VALUE) {
            return 0;
        }

        return minLength;
    }
}
```

## Python

```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        min_length = float('inf')
        sum_ = 0
        slow_index = 0

        for fast_index, num in enumerate(nums): # This line is the most important. You'd better memorize it.
            sum_ += num

            while sum_ >= target:
                min_length = min(min_length, fast_index - slow_index + 1)
                sum_ -= nums[slow_index]
                slow_index += 1

        if min_length == float('inf'):
            return 0

        return min_length
```

## JavaScript

```javascript
var minSubArrayLen = function (target, nums) {
  let minLength = Number.MAX_SAFE_INTEGER
  let sum = 0
  let slowIndex = 0

  nums.forEach((num, fastIndex) => { // This line is the most important. You'd better memorize it.
    sum += num

    while (sum >= target) {
      minLength = Math.min(minLength, fastIndex - slowIndex + 1)
      sum -= nums[slowIndex]
      slowIndex++
    }
  })

  if (minLength == Number.MAX_SAFE_INTEGER) {
    return 0
  }

  return minLength
};
```

## C#

```csharp
public class Solution
{
    public int MinSubArrayLen(int target, int[] nums)
    {
        int minLength = Int32.MaxValue;
        int sum = 0;
        int slowIndex = 0;

        for (int fastIndex = 0; fastIndex < nums.Length; fastIndex++) // This line is the most important. You'd better memorize it.
        {
            sum += nums[fastIndex];

            while (sum >= target)
            {
                minLength = Math.Min(minLength, fastIndex - slowIndex + 1);
                sum -= nums[slowIndex];
                slowIndex++;
            }
        }

        if (minLength == Int32.MaxValue)
            return 0;

        return minLength;
    }
}
```

## Go

```go
func minSubArrayLen(target int, nums []int) int {
    minLength := math.MaxInt32
    sum := 0
    slowIndex := 0

    for fastIndex := 0; fastIndex < len(nums); fastIndex++ { // This line is the most important. You'd better memorize it.
        sum += nums[fastIndex]

        for sum >= target {
            minLength = min(minLength, fastIndex - slowIndex + 1)
            sum -= nums[slowIndex]
            slowIndex++
        }
    }

    if minLength == math.MaxInt32 {
        return 0
    }

    return minLength
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
```

## Ruby

```ruby
# @param {Integer} target
# @param {Integer[]} nums
# @return {Integer}
def min_sub_array_len(target, nums)
  min_length = Float::INFINITY
  sum = 0
  slow_index = 0

  nums.each_with_index do |num, fast_index| # This line is the most important. You'd better memorize it.
    sum += num

    while sum >= target
      min_length = [min_length, fast_index - slow_index + 1].min
      sum -= nums[slow_index]
      slow_index += 1
    end
  end

  min_length == Float::INFINITY ? 0 : min_length
end
```

## C++

```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int min_length = INT_MAX;
        int sum = 0;
        int slow_index = 0;
        
        for (int fast_index = 0; fast_index < nums.size(); fast_index++) {
            sum += nums[fast_index];
            
            while (sum >= target) {
                min_length = min(min_length, fast_index - slow_index + 1);
                sum -= nums[slow_index];
                slow_index++;
            }
        }
        
        if (min_length == INT_MAX) {
            return 0;
        }
        
        return min_length;
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

Visit original link: [209. Minimum Size Subarray Sum - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/209-minimum-size-subarray-sum) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

