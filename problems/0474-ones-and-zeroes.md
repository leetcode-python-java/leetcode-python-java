# 474. Ones and Zeroes
LeetCode problem: [474. Ones and Zeroes](https://leetcode.com/problems/ones-and-zeroes/)

## LeetCode problem description
You are given an array of binary strings `strs` and two integers `m` and `n`.

Return the size of the largest subset of `strs` such that there are **at most** `m` `0`'s and `n` `1`'s in the subset.

A set `x` is a **subset** of a set `y` if all elements of `x` are also elements of `y`.

```
Example 1:

Input: strs = ["10","0001","111001","1","0"], m = 5, n = 3
Output: 4

Explanation: The largest subset with at most 5 0's and 3 1's is {"10", "0001", "1", "0"}, so the answer is 4.
Other valid but smaller subsets include {"0001", "1"} and {"10", "1", "0"}.
{"111001"} is an invalid subset because it contains 4 1's, greater than the maximum of 3.
---------------------------------------------------------------------------------------------------------------------

Example 2:

Input: strs = ["10","0","1"], m = 1, n = 1
Output: 2
Explanation: The largest subset is {"0", "1"}, so the answer is 2.
---------------------------------------------------------------------------------------------------------------------

Constraints:

1 <= strs.length <= 600
1 <= strs[i].length <= 100
'strs[i]' consists only of digits '0' and '1'.
1 <= m, n <= 100
```

## Thoughts
* This is a two-dimensional `01 Knapsack Problem`. The solution is to first solve the problem in one dimension totally and then expand it to two dimensions.

* Don't draw a grid that considers both dimensions together, that's too complicated.

* For example, let's only consider the case of `0`.

Example 1: `Input: strs = ["10","0001","111001","1","0"], m = 5, n = 3`.

* After initialization: `dp = [0] * (zero_count + 1)`.
* Finish this grid by using the `example 1`:
```
#    0 1 2 3 4 5
#    0 0 0 0 0 0
# 1  0 1 1 1 1 1 # "10" has 1 zero
# 3  0 1 1 1 2 2 # "0001" has 3 zeros
# 2  0 1 1 2 2 2 # "111001" has 2 zeros
# 0  1 2 2 3 3 3 # "1" has 0 zero
# 1  1 2 3 3 4 4 # "0" has 1 zero
```

* Got **Recurrence formula**:
```
dp[j] = max(
   dp[j],
   dp[j - zero_counts[i]] + 1
)
```

* The code that only considers the quantity limit of `0` is:
```python
class Solution:
    def findMaxForm(self, strs: List[str], m: int, n: int) -> int:
        max_zero_count = m
        dp = [0] * (max_zero_count + 1)

        for string in strs:
            zero_count, one_count = count_zero_one(string)

            for j in range(len(dp) - 1, zero_count - 1, -1): # must iterate in reverse order!
                dp[j] = max(dp[j], dp[j - zero_count] + 1)

        return dp[-1]


def count_zero_one(string):
    zero_count = 0
    one_count = 0

    for bit in string:
        if bit == '0':
            zero_count += 1
        else:
            one_count += 1

    return zero_count, one_count
```

* Now, you can consider the quantity limit of `1`. It should be handled similarly to `0` but in another dimension. Please see the complete code below.

## Python
```python
class Solution:
    def findMaxForm(self, strs: List[str], m: int, n: int) -> int:
        max_zero_count = m
        max_one_count = n

        dp = [[0] * (max_one_count + 1) for _ in range(max_zero_count + 1)]

        for string in strs:
            zero_count, one_count = count_zero_one(string)

            for i in range(len(dp) - 1, zero_count - 1, -1):
                for j in range(len(dp[0]) - 1, one_count - 1, -1):
                    dp[i][j] = max(dp[i][j], dp[i - zero_count][j - one_count] + 1)
        
        return dp[-1][-1]


def count_zero_one(string):
    zero_count = 0
    one_count = 0

    for bit in string:
        if bit == '0':
            zero_count += 1
        else:
            one_count += 1

    return zero_count, one_count
```

## C++
```

```

## Java
```java

```

## C#
```c#

```

## JavaScript
```javascript

```

## Go
```go

```

## Ruby
```ruby

```
