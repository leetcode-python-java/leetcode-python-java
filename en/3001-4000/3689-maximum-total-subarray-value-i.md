# 3689. Maximum Total Subarray Value I - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at coder.id →**](https://www.coder.id)

Visit original link: [3689. Maximum Total Subarray Value I - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/3689-maximum-total-subarray-value-i) for a better experience!

LeetCode link: [3689. Maximum Total Subarray Value I](https://leetcode.com/problems/maximum-total-subarray-value-i), difficulty: **Medium**.

## LeetCode description of "3689. Maximum Total Subarray Value I"

You are given an integer array `nums` of length `n` and an integer `k`.

You need to choose **exactly** `k` non-empty subarrays `nums[l..r]` of `nums`. Subarrays may overlap, and the exact same subarray (same `l` and `r`) **can** be chosen more than once.

The **value** of a subarray `nums[l..r]` is defined as: `max(nums[l..r]) - min(nums[l..r])`.

The **total value** is the sum of the **values** of all chosen subarrays.

Return the **maximum** possible total value you can achieve.

### [Example 1]

**Input**: `nums = [1,3,2], k = 2`

**Output**: `4`

**Explanation**: 

<p>One optimal approach is:<br>
- Choose <code>nums[0..1] = [1, 3]</code>. The maximum is 3 and the minimum is 1, giving a value of <code>3 - 1 = 2</code>.<br>
- Choose <code>nums[0..2] = [1, 3, 2]</code>. The maximum is still 3 and the minimum is still 1, so the value is also <code>3 - 1 = 2</code>.<br>
Adding these gives <code>2 + 2 = 4</code>.</p>


### [Example 2]

**Input**: `nums = [4,2,5,1], k = 3`

**Output**: `12`

**Explanation**: 

<p>One optimal approach is:<br>
- Choose <code>nums[0..3] = [4, 2, 5, 1]</code>. The maximum is 5 and the minimum is 1, giving a value of <code>5 - 1 = 4</code>.<br>
- Choose <code>nums[0..3] = [4, 2, 5, 1]</code>. The maximum is 5 and the minimum is 1, so the value is also <code>4</code>.<br>
- Choose <code>nums[2..3] = [5, 1]</code>. The maximum is 5 and the minimum is 1, so the value is again <code>4</code>.<br>
Adding these gives <code>4 + 4 + 4 = 12</code>.</p>


### [Constraints]

- `1 <= n == nums.length <= 5 * 10^4`
- `0 <= nums[i] <= 10^9`
- `1 <= k <= 10^5`

### [Hints]

<details>
  <summary>Hint 1</summary>
  Choose the whole subarray `k` times.

  
</details>

## Intuition

The problem asks us to find exactly `k` subarrays such that the sum of `max(subarray) - min(subarray)` across all chosen subarrays is maximized. We are allowed to choose overlapping subarrays and even the exact same subarray multiple times.

A key observation here is that for any subarray `nums[l..r]`, its maximum value can never exceed the global maximum of the entire array, and its minimum value can never be less than the global minimum of the entire array. Mathematically, `max(nums[l..r]) <= max(nums)` and `min(nums[l..r]) >= min(nums)`. 

Thus, the value of *any* subarray is bounded by `max(nums) - min(nums)`. Since we want to maximize the sum of exactly `k` subarrays, and we are allowed to pick the exact same subarray multiple times, the optimal strategy is simply to pick the entire array `nums` exactly `k` times.

The problem boils down to finding the global maximum and minimum elements of the array, calculating their difference, and multiplying that difference by `k`.

## Step-by-Step Solution

1. **Find the Global Extremes:** Iterate through the array `nums` exactly once to find the maximum value (`maxVal`) and the minimum value (`minVal`).
2. **Calculate the Difference:** Subtract the global minimum from the global maximum to get the maximum possible value for a single subarray (`maxVal - minVal`).
3. **Multiply by `k`:** Since we can choose the entire array `k` times, multiply the difference by `k` to get the maximum total value.
4. **Handle Large Numbers:** The result can be up to `10^5 * 10^9 = 10^{14}`, which exceeds the 32-bit signed integer limit. Ensure the calculation uses 64-bit integers (e.g., `long` in Java/C#, `long long` in C++) to prevent overflow.

## Complexity

> - **Time Complexity:** `O(N)`, where `N` is the length of the array. We only need to iterate through the array once to find the maximum and minimum values.
- **Space Complexity:** `O(1)`. We only use a few extra variables to keep track of the maximum and minimum values, which requires constant extra space.

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Python

```python
class Solution:
    def maxTotalValue(self, nums: List[int], k: int) -> int:
        # We can find the global maximum and minimum of the entire array using built-in functions.
        # The time complexity of max() and min() is O(N) each, making the total O(N).
        max_val = max(nums)
        min_val = min(nums)
        
        # The optimal approach is to pick the entire array exactly k times.
        # This gives us the absolute maximum difference possible.
        # Python automatically handles arbitrarily large integers, so no overflow concerns.
        return k * (max_val - min_val)
```

## Java

```java
class Solution {
    public long maxTotalValue(int[] nums, int k) {
        // Initialize max and min values with the first element of the array
        int maxVal = nums[0];
        int minVal = nums[0];
        
        // Iterate through the array to find the global maximum and minimum
        for (int num : nums) {
            if (num > maxVal) {
                maxVal = num;
            }
            if (num < minVal) {
                minVal = num;
            }
        }
        
        // The maximum value for a single subarray is maxVal - minVal.
        // We multiply this by k to get the maximum total value.
        // Cast k to a long before multiplication to prevent 32-bit integer overflow.
        return (long) k * (maxVal - minVal);
    }
}
```

## JavaScript

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var maxTotalValue = function(nums, k) {
    // Initialize the global extreme values
    let maxVal = nums[0];
    let minVal = nums[0];
    
    // Iterate through the array once to find the global max and min.
    // We do not use Math.max(...nums) because it can throw a Maximum Call Stack Size 
    // Exceeded error if the array is very large (e.g. 50,000 elements).
    for (let i = 1; i < nums.length; i++) {
        if (nums[i] > maxVal) maxVal = nums[i];
        if (nums[i] < minVal) minVal = nums[i];
    }
    
    // Return the difference multiplied by k.
    // JS numbers are double-precision floats, which safely represent integers up to 2^53 - 1.
    // Our max possible answer is 10^14, which fits comfortably without needing BigInt.
    return k * (maxVal - minVal);
};
```

## C++

```cpp
class Solution {
public:
    long long maxTotalValue(vector<int>& nums, int k) {
        // Initialize max and min with the first element
        int maxVal = nums[0];
        int minVal = nums[0];
        
        // Find the global maximum and minimum in the array
        for (int num : nums) {
            if (num > maxVal) maxVal = num;
            if (num < minVal) minVal = num;
        }
        
        // We choose the entire array k times.
        // The maximum possible value is 10^14, which exceeds the 32-bit int limit.
        // So we cast k to long long to perform 64-bit arithmetic.
        return (long long) k * (maxVal - minVal);
    }
};
```

## C#

```csharp
public class Solution {
    public long MaxTotalValue(int[] nums, int k) {
        // Initialize the extreme values using the first element
        int maxVal = nums[0];
        int minVal = nums[0];
        
        // Iterate over all elements to find the global maximum and minimum
        foreach (int num in nums) {
            if (num > maxVal) maxVal = num;
            if (num < minVal) minVal = num;
        }
        
        // Since max difference is 10^9 and k is 10^5, the product can be 10^14.
        // We explicitly cast to long to avoid 32-bit integer overflow.
        return (long) k * (maxVal - minVal);
    }
}
```

## Go

```go
func maxTotalValue(nums []int, k int) int64 {
    // Start by assuming the first element is both the max and the min
    maxVal := nums[0]
    minVal := nums[0]
    
    // Make a single pass through the array to update max and min
    for _, num := range nums {
        if num > maxVal {
            maxVal = num
        }
        if num < minVal {
            minVal = num
        }
    }
    
    // Calculate the difference and multiply by k.
    // Cast everything to int64 to avoid overflow since the answer can be up to 10^14.
    return int64(k) * int64(maxVal - minVal)
}
```

## Ruby

```ruby
# @param {Integer[]} nums
# @param {Integer} k
# @return {Integer}
def max_total_value(nums, k)
    # Ruby arrays have highly optimized built-in methods for max and min.
    # We find the global maximum and minimum.
    max_val = nums.max
    min_val = nums.min
    
    # We can pick the entire array exactly k times to get the maximum sum.
    # Ruby automatically handles large integers seamlessly, so no overflow occurs.
    k * (max_val - min_val)
end
```

## Rust

```rust
impl Solution {
    pub fn max_total_value(nums: Vec<i32>, k: i32) -> i64 {
        // Initialize max and min with the first element of the array
        let mut max_val = nums[0];
        let mut min_val = nums[0];
        
        // Iterate through the array to find the global extreme values
        for &num in nums.iter() {
            if num > max_val { max_val = num; }
            if num < min_val { min_val = num; }
        }
        
        // Calculate the maximum difference
        let diff = (max_val - min_val) as i64;
        
        // Multiply by k using 64-bit integer arithmetic to prevent overflow
        (k as i64) * diff
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun maxTotalValue(nums: IntArray, k: Int): Long {
        // Assume the first element is both the minimum and maximum
        var maxVal = nums[0]
        var minVal = nums[0]
        
        // Iterate through all elements to find the global max and min
        for (num in nums) {
            if (num > maxVal) maxVal = num
            if (num < minVal) minVal = num
        }
        
        // Cast k and the difference to Long to prevent 32-bit integer overflow.
        // The max possible value is 10^14.
        return k.toLong() * (maxVal - minVal).toLong()
    }
}
```

## Swift

```swift
class Solution {
    func maxTotalValue(_ nums: [Int], _ k: Int) -> Int {
        // Initialize extremes using the first element
        var maxVal = nums[0]
        var minVal = nums[0]
        
        // Single pass to find the global maximum and minimum
        for num in nums {
            if num > maxVal { maxVal = num }
            if num < minVal { minVal = num }
        }
        
        // Swift's Int is 64-bit on 64-bit platforms, which safely holds 10^14.
        // Simply return the difference multiplied by k.
        return k * (maxVal - minVal)
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
> We recommend [**coder.id**](https://www.coder.id) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.coder.id`.
>
> [**Build Your Programmer Brand at coder.id →**](https://www.coder.id)

---

Visit original link: [3689. Maximum Total Subarray Value I - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/3689-maximum-total-subarray-value-i) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

