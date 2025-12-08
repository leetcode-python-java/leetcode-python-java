# 53. Maximum Subarray - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired. We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [53. Maximum Subarray - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/53-maximum-subarray) for a better experience!

LeetCode link: [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray), difficulty: **Medium**.

## LeetCode description of "53. Maximum Subarray"

Given an integer array `nums`, find the `subarray` with the largest sum, and return its sum.

### [Example 1]

**Input**: `nums = [-2,1,-3,4,-1,2,1,-5,4]`

**Output**: `6`

**Explanation**: 

<p>The subarray [4,-1,2,1] has the largest sum 6.</p>


### [Example 2]

**Input**: `nums = [1]`

**Output**: `1`

**Explanation**: `The subarray [1] has the largest sum 1.`

### [Example 3]

**Input**: `nums = [5,4,-1,7,8]`

**Output**: `23`

**Explanation**: 

<p>The subarray [5,4,-1,7,8] has the largest sum 23.</p>


### [Constraints]

- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`

## Intuition 1

- This problem can be solved by using `Greedy Algorithm` (please see `solution 2`), yet here we will use another way.
- For `nums[i]`:
    1. If the `previous sum` is negative, we can discard `previous sum`;
    2. If the `previous sum` is positive, we can add `previous sum` to the `current sum`.
- Therefore, it meets the characteristics of a `dynamic programming` problem.

## Pattern of "Dynamic Programming"

"Dynamic Programming" requires the use of the `dp` array to store the results. The value of `dp[i][j]` can be converted from its previous (or multiple) values ​​through a formula. Therefore, the value of `dp[i][j]` is derived step by step, and it is related to the previous `dp` record value.

#### "Dynamic programming" is divided into five steps

1. Determine the **meaning** of each value of the array `dp`.
2. Initialize the value of the array `dp`.
3. Fill in the `dp` grid data **in order** according to an example.
4. Based on the `dp` grid data, derive the **recursive formula**.
5. Write a program and print the `dp` array. If it is not as expected, adjust it.

#### Detailed description of these five steps

1. Determine the **meaning** of each value of the array `dp`.
    - First determine whether `dp` is a one-dimensional array or a two-dimensional array. A `one-dimensional rolling array` means that the values ​​of the array are overwritten at each iteration. Most of the time, using `one-dimensional rolling array` instead of `two-dimensional array` can simplify the code; but for some problems, such as operating "two swappable arrays", for the sake of ease of understanding, it is better to use `two-dimensional array`.
    - Try to use the meaning of the `return value` required by the problem as the meaning of `dp[i]` (one-dimensional) or `dp[i][j]` (two-dimensional). It works about 60% of the time. If it doesn't work, try other meanings.
    - Try to save more information in the design. Repeated information only needs to be saved once in a `dp[i]`.
    - Use simplified meanings. If the problem can be solved with `boolean value`, don't use `numeric value`.
2. Initialize the value of the array `dp`. The value of `dp` involves two levels:
    1. The length of `dp`. Usually: `condition array length plus 1` or `condition array length`.
    2. The value of `dp[i]` or `dp[i][j]`. `dp[0]` or `dp[0][0]` sometimes requires special treatment.
3. Fill in the `dp` grid data **in order** according to an example.
    - The "recursive formula" is the core of the "dynamic programming" algorithm. But the "recursive formula" is obscure. If you want to get it, you need to make a table and use data to inspire yourself.
    - If the original example is not good enough, you need to redesign one yourself.
    - According to the example, fill in the `dp` grid data "in order", which is very important because it determines the traversal order of the code.
    - Most of the time, from left to right, from top to bottom. But sometimes it is necessary to traverse from right to left, from bottom to top, from the middle to the right (or left), such as the "palindrome" problems. Sometimes, it is necessary to traverse a line twice, first forward and then backward.
    - When the order is determined correctly, the starting point is determined. Starting from the starting point, fill in the `dp` grid data "in order". This order is also the order in which the program processes.
    - In this process, you will get inspiration to write a "recursive formula". If you can already derive the formula, you do not need to complete the grid.
4. Based on the `dp` grid data, derive the **recursive formula**.
    - There are three special positions to pay attention to: `dp[i - 1][j - 1]`, `dp[i - 1][j]` and `dp[i][j - 1]`, the current `dp[i][j]` often depends on them.
    - When operating "two swappable arrays", due to symmetry, we may need to use `dp[i - 1][j]` and `dp[i][j - 1]` at the same time.
5. Write a program and print the `dp` array. If it is not as expected, adjust it.
    - Focus on analyzing those values that are not as expected.

After reading the above, do you feel that "dynamic programming" is not that difficult? Try to solve this problem. 🤗

## Step-by-Step Solution

1. Determine the **meaning** of the `dp[i]`
    - Imagine that `dp[i]` represents the `largest sum` at index `i`. Is this okay?
        mark-detail `dp[i + 1]` cannot be calculated by `dp[i]`. So we have to change the meaning. mark-detail
- How to design it?
        mark-detail If `dp[i]` represents the `current sum` at index `i`, `dp[i + 1]` can be calculated by `dp[i]`. Finally, we can see that the `maximum sum` is recorded in the `current sum` array. mark-detail
2. Determine the `dp` array's initial value

    ```ruby
    nums = [-2,  1, -3,  4, -1,  2,  1, -5,  4]
    dp   = [-2,  1, -3,  4, -1,  2,  1, -5,  4]
    ```
3. Fill in the `dp` grid data "in order" according to an example.

    ```ruby
    nums = [-2,  1, -3,  4, -1,  2,  1, -5,  4]
    dp   = [-2,  1,  N,  N,  N,  N,  N,  N,  N] # N means don't pay attention to it now
    dp   = [-2,  1, -2,  N,  N,  N,  N,  N,  N]
    dp   = [-2,  1, -2,  4,  N,  N,  N,  N,  N]
    dp   = [-2,  1, -2,  4,  3,  N,  N,  N,  N]
    dp   = [-2,  1, -2,  4,  3,  5,  N,  N,  N]
    dp   = [-2,  1, -2,  4,  3,  5,  6,  N,  N]
    dp   = [-2,  1, -2,  4,  3,  5,  6,  1,  N]
    dp   = [-2,  1, -2,  4,  3,  5,  6,  1,  5]
    ```
4. Based on the `dp` grid data, derive the "recursive formula".

    ```python
    dp[i] = max(nums[i], dp[i - 1] + nums[i])
    ```
5. Write a program and print the `dp` array. If it is not as expected, adjust it.

## Complexity

- Time complexity: `O(n)`.
- Space complexity: `O(n)`.

## Python

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        dp = nums.copy()

        for i in range(1, len(dp)):
            dp[i] = max(nums[i], dp[i - 1] + nums[i])

        return max(dp)
```

## Java

```java
class Solution {
    public int maxSubArray(int[] nums) {
        var dp = nums.clone();
        
        for (var i = 1; i < dp.length; i++) {
            dp[i] = Math.max(nums[i], dp[i - 1] + nums[i]);
        }

        return IntStream.of(dp).max().getAsInt(); // if you want to beat 99%, refer to C# soluiton's comment 
    }
}
```

## JavaScript

```javascript
var maxSubArray = function (nums) {
  const dp = [...nums]

  for (let i = 1; i < dp.length; i++) {
    dp[i] = Math.max(nums[i], dp[i - 1] + nums[i])
  }

  return Math.max(...dp)
};
```

## Go

```go
func maxSubArray(nums []int) int {
    dp := slices.Clone(nums)

    for i := 1; i < len(nums); i++ {
        dp[i] = max(nums[i], dp[i - 1] + nums[i])
    }

    return slices.Max(dp)
}
```

## Ruby

```ruby
def max_sub_array(nums)
  dp = nums.clone

  (1...dp.size).each do |i|
    dp[i] = [ nums[i], dp[i - 1] + nums[i] ].max
  end

  dp.max
end
```

## C#

```csharp
public class Solution
{
    public int MaxSubArray(int[] nums)
    {
        var dp = (int[])nums.Clone();

        for (var i = 1; i < dp.Length; i++)
        {
            dp[i] = Math.Max(nums[i], dp[i - 1] + nums[i]);
        }

        return dp.Max(); // if you want to beat 99%, you can use a variable to collect the maximum value: `if (dp[i] > result) result = dp[i];`
    }
}
```

## C++

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        auto dp = nums;

        for (auto i = 1; i < dp.size(); i++) {
            dp[i] = max(nums[i], dp[i - 1] + nums[i]);
        }

        return *max_element(dp.begin(), dp.end());
    }
};
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## Intuition 2

- The "greedy" algorithm solution and the "dynamic programming" algorithm solution for this problem are essentially the same, both are "dynamic programming", but the "greedy" algorithm here changes from using the dp one-dimensional array and then reducing one dimension to using only two variables.
- The "greedy" algorithm here can be called "rolling variables". Just like "rolling array (one-dimensional)" corresponds to a two-dimensional array, one dimension can be reduced by rolling.

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Python

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        result = -float('inf')
        pre_sum = 0

        for num in nums:
            pre_sum = max(pre_sum + num, num)
            result = max(result, pre_sum)
        
        return result
```

## C++

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int result = INT_MIN;
        int pre_sum = 0;

        for (int num : nums) {
            pre_sum = max(pre_sum + num, num);
            result = max(result, pre_sum);
        }

        return result;
    }
};
```

## Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer}
def max_sub_array(nums)
  result = -Float::INFINITY
  pre_sum = 0

  nums.each do |num|
    pre_sum = [pre_sum + num, num].max
    result = [result, pre_sum].max
  end

  result
end
```

## Go

```go
func maxSubArray(nums []int) int {
    result := math.MinInt
    preSum := 0

    for _, num := range nums {
        preSum = max(preSum + num, num)
        if preSum > result {
            result = preSum
        }
    }

    return result
}
```

## JavaScript

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    let result = -Infinity;
    let preSum = 0;

    for (const num of nums) {
        preSum = Math.max(preSum + num, num);
        result = Math.max(result, preSum);
    }

    return result;
};
```

## C#

```csharp
public class Solution
{
    public int MaxSubArray(int[] nums)
    {
        int result = int.MinValue;
        int preSum = 0;

        foreach (int num in nums)
        {
            preSum = Math.Max(preSum + num, num);
            result = Math.Max(result, preSum);
        }

        return result;
    }
}
```

## Java

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int result = Integer.MIN_VALUE;
        int preSum = 0;

        for (int num : nums) {
            preSum = Math.max(preSum + num, num);
            result = Math.max(result, preSum);
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
> While mastering algorithms is key, showcasing your talent is what gets you hired. We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [53. Maximum Subarray - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/53-maximum-subarray) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

