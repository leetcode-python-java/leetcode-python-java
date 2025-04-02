# 416. Partition Equal Subset Sum - LeetCode Best Practices

Visit original link: [416. Partition Equal Subset Sum - LeetCode Best Practices](https://leetcoder.net/en/leetcode/416-partition-equal-subset-sum) for a better experience!

LeetCode link: [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum), difficulty: **Medium**.

## LeetCode description of "416. Partition Equal Subset Sum"

Given an integer array `nums`, return `true` if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or `false` otherwise.

### [Example 1]

**Input**: `nums = [1,5,11,5]`

**Output**: `true`

**Explanation**: 

<p>The array can be partitioned as [1, 5, 5] and [11].</p>


### [Example 2]

**Input**: `nums = [1,2,3,5]`

**Output**: `false`

**Explanation**: 

<p>The array cannot be partitioned into equal sum subsets.</p>


### [Constraints]

- `1 <= nums.length <= 200`
- `1 <= nums[i] <= 100`

## Intuition 1

- When we first see this problem, we might want to loop through all subsets of the array. If there is a subset whose sum is equal to `half of the sum`, then return `true`. This can be achieved with a `backtracking algorithm`, but after seeing the constraint `nums.length <= 200`, we can estimate that the program will time out.
- This problem can be solved using the `0/1 knapsack problem` algorithm.

## Steps

1. Determine the **meaning** of the `dp[j]`
    - `dp[j]` represents whether it is possible to `sum` the first `i` `nums` to get `j`.
    - `dp[j]` is a boolean.

2. Determine the `dp` array's initial value
   - Use an example:

       ```
       nums = [1,5,11,5], so 'half of the sum' is 11.
       The `size` of the knapsack is `11 + 1`, and the `items` are `nums`.
       So after initialization, the 'dp' array would be:
       #    0 1 2 3 4 5 6 7 8 9 10 11
       #    T F F F F F F F F F F  F  # dp
       # 1  
       # 5  
       # 11 
       # 5  
       ```
    - `dp[0]` is set to `true`, indicating that an empty knapsack can be achieved by not putting any items in it. In addition, it is used as the starting value, and the subsequent `dp[j]` will depend on it. If it is `false`, all values of `dp[j]` will be `false`.
    - `dp[j] = false (j != 0)`, indicating that it is impossible to get `j` with no `nums`.
3. Fill in the `dp` grid data "in order" according to an example.

    ```
    1. Use the first num '1'.
    #    0 1 2 3 4 5 6 7 8 9 10 11
    #    T F F F F F F F F F F  F
    # 1  T T F F F F F F F F F  F # dp
    ```

    ```
    2. Use the second num '5'.
    #    0 1 2 3 4 5 6 7 8 9 10 11
    #    T F F F F F F F F F F  F
    # 1  T T F F F F F F F F F  F
    # 5  T T F F F T T F F F F  F
    ```

    ```
    3. Use the third num '11'.
    #    0 1 2 3 4 5 6 7 8 9 10 11
    #    T F F F F F F F F F F  F
    # 1  T T F F F F F F F F F  F
    # 5  T T F F F T T F F F F  F
    # 11 T T F F F T T F F F F  T
    ```

    ```
    3. Use the last num '5'.
    #    0 1 2 3 4 5 6 7 8 9 10 11
    #    T F F F F F F F F F F  F
    # 1  T T F F F F F F F F F  F
    # 5  T T F F F T T F F F F  F
    # 11 T T F F F T T F F F F  T
    # 5  T T F F F T T F F F T  T # dp
    ```
4. Based on the `dp` grid data, derive the "recursive formula".

    ```cpp
    dp[j] = dp[j] || dp[j - nums[i]]
    ```

5. Write a program and print the `dp` array. If it is not as expected, adjust it.

## Complexity

- Time complexity: `O(n * sum/2)`.
- Space complexity: `O(sum/2)`.

## Python

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        sum_ = sum(nums)

        if sum_ % 2 == 1:
            return False

        dp = [False] * ((sum_ // 2) + 1)
        dp[0] = True

        for num in nums:
            # If not traversing in reverse order, the newly assigned value `dp[j]` will act as `dp[j - num]` later,
            # then the subsequent `dp[j]` will be affected. But each `num` can only be used once!
            j = len(dp) - 1
            while j >= num:
                dp[j] = dp[j] or dp[j - num]
                j -= 1

        return dp[-1]
```

## C#

```csharp
public class Solution
{
    public bool CanPartition(int[] nums)
    {
        int sum = nums.Sum();

        if (sum % 2 == 1)
            return false;

        var dp = new bool[sum / 2 + 1];
        dp[0] = true;

        foreach (var num in nums)
        {
            for (var j = dp.GetUpperBound(0); j >= num; j--)
            {
                dp[j] = dp[j] || dp[j - num];
            }
        }

        return dp.Last();
    }
}
```

## C++

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        auto sum = reduce(nums.begin(), nums.end());

        if (sum % 2 == 1) {
            return false;
        }

        auto dp = vector<bool>(sum / 2 + 1);
        dp[0] = true;

        for (auto num : nums) {
            for (auto j = dp.size() - 1; j >= num; j--) {
                dp[j] = dp[j] || dp[j - num];
            }
        }

        return dp.back();
    }
};
```

## Java

```java
class Solution {
    public boolean canPartition(int[] nums) {
        var sum = IntStream.of(nums).sum();
        
        if (sum % 2 == 1) {
            return false;
        }

        var dp = new boolean[sum / 2 + 1];
        dp[0] = true;

        for (var num : nums) {
            for (var j = dp.length - 1; j >= num; j--) {
                dp[j] = dp[j] || dp[j - num];
            }
        }

        return dp[dp.length - 1];
    }
}
```

## JavaScript

```javascript
var canPartition = function (nums) {
  const sum = _.sum(nums)

  if (sum % 2 == 1) {
    return false
  }

  const dp = Array(sum / 2 + 1).fill(false)
  dp[0] = true

  for (const num of nums) {
    for (let j = dp.length - 1; j >= num; j--) {
      dp[j] = dp[j] || dp[j - num]
    }
  }

  return dp.at(-1)
};
```

## Go

```go
func canPartition(nums []int) bool {
    sum := 0
    for _, num := range nums {
        sum += num
    }

    if sum % 2 == 1 {
        return false
    }

    dp := make([]bool, sum / 2 + 1)
    dp[0] = true

    for _, num := range nums {
        for j := len(dp) - 1; j >= num; j-- {
            dp[j] = dp[j] || dp[j - num]
        }
    }

    return dp[len(dp) - 1]
}
```

## Ruby

```ruby
def can_partition(nums)
  sum = nums.sum

  return false if sum % 2 == 1

  dp = Array.new(sum / 2 + 1, false)
  dp[0] = true

  nums.each do |num|
    (num...dp.size).reverse_each do |j|
      dp[j] = dp[j] || dp[j - num]
    end
  end

  dp[-1]
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## Intuition 2

In solution 1, the traversal order is **from right to left** which really matters.

During the interview, you need to remember it. Is there any way to not worry about the traversal order?

<details><summary>Click to view the answer</summary><p> As long as you copy the original `dp` and reference the value of the copy, you don't have to worry about the original `dp` value being modified. </p></details>

## Complexity

- Time complexity: `O(n * sum/2)`.
- Space complexity: `O(n * sum/2)`.

## Python

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        sum_ = sum(nums)

        if sum_ % 2 == 1:
            return False

        dp = [False] * ((sum_ // 2) + 1)
        dp[0] = True

        for num in nums:
            # Make a copy of the 'dp' that has not been modified to eliminate distractions.
            dc = dp.copy()

            for j in range(num, len(dp)): # any order is fine
                dp[j] = dc[j] or dc[j - num] # Use 'dc' instead of 'dp' because 'dp' will be modified.

        return dp[-1]
```

## C#

```csharp
public class Solution
{
    public bool CanPartition(int[] nums)
    {
        int sum = nums.Sum();

        if (sum % 2 == 1)
            return false;

        var dp = new bool[sum / 2 + 1];
        dp[0] = true;

        foreach (var num in nums)
        {
            var dc = (bool[])dp.Clone();

            for (var j = num; j < dp.Length; j++)
            {
                dp[j] = dc[j] || dc[j - num];
            }
        }

        return dp.Last();
    }
}
```

## C++

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        auto sum = reduce(nums.begin(), nums.end());

        if (sum % 2 == 1) {
            return false;
        }

        auto dp = vector<bool>(sum / 2 + 1);
        dp[0] = true;

        for (auto num : nums) {
            auto dc = dp;

            for (auto j = num; j < dp.size(); j++) {
                dp[j] = dc[j] || dc[j - num];
            }
        }

        return dp.back();
    }
};
```

## Java

```java
class Solution {
    public boolean canPartition(int[] nums) {
        var sum = IntStream.of(nums).sum();
        
        if (sum % 2 == 1) {
            return false;
        }

        var dp = new boolean[sum / 2 + 1];
        dp[0] = true;

        for (var num : nums) {
            var dc = dp.clone();

            for (var j = num; j < dp.length; j++) {
                dp[j] = dc[j] || dc[j - num];
            }
        }

        return dp[dp.length - 1];
    }
}
```

## JavaScript

```javascript
var canPartition = function (nums) {
  const sum = _.sum(nums)

  if (sum % 2 == 1) {
    return false
  }

  const dp = Array(sum / 2 + 1).fill(false)
  dp[0] = true

  for (const num of nums) {
    const dc = [...dp]

    for (let j = num; j < dp.length; j++) {
      dp[j] = dc[j] || dc[j - num]
    }
  }

  return dp.at(-1)
};
```

## Go

```go
func canPartition(nums []int) bool {
    sum := 0
    for _, num := range nums {
        sum += num
    }

    if sum % 2 == 1 {
        return false
    }

    dp := make([]bool, sum / 2 + 1)
    dp[0] = true

    for _, num := range nums {
        dc := slices.Clone(dp)

        for j := num; j < len(dp); j++ {
            dp[j] = dc[j] || dc[j - num]
        }
    }

    return dp[len(dp) - 1]
}
```

## Ruby

```ruby
def can_partition(nums)
  sum = nums.sum

  return false if sum % 2 == 1

  dp = Array.new(sum / 2 + 1, false)
  dp[0] = true

  nums.each do |num|
    dc = dp.clone

    (num...dp.size).each do |j|
      dp[j] = dc[j] || dc[j - num]
    end
  end

  dp[-1]
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [leetcoder.net](https://leetcoder.net): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [416. Partition Equal Subset Sum - LeetCode Best Practices](https://leetcoder.net/en/leetcode/416-partition-equal-subset-sum).

GitHub repository: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

