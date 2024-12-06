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
* This is a two-dimensional `0/1 Knapsack Problem`. The solution is to first solve the problem in one dimension once and for all and then expand it to two dimensions.

* It is no need to draw a grid that considers both dimensions together, that's too complicated.

* For example, let's first only consider the quantity limit of `0`.

Example 1: `Input: strs = ["10","0001","111001","1","0"], m = 5, n = 3`.

* After initialization: 
    ````
    max_zero_count = m
    dp = [0] * (max_zero_count + 1)`.
    ````
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
    def findMaxForm(self, strs: List[str], max_zero_count: int, n: int) -> int:
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

## C#
```c#
public class Solution {
    public int FindMaxForm(string[] strs, int maxZeroCount, int maxOneCount) {
        var dp = new int[maxZeroCount + 1, maxOneCount + 1];

        foreach (var str in strs) {
            var (zeroCount, oneCount) = CountZeroOne(str);

            for (var i = maxZeroCount; i >= zeroCount; i--) {
                for (var j = maxOneCount; j >= oneCount; j--) {
                    dp[i, j] = Math.Max(dp[i, j], dp[i - zeroCount, j - oneCount] + 1);
                }
            }
        }

        return dp[maxZeroCount, maxOneCount];
    }

    (int, int) CountZeroOne(string str) {
        var zeroCount = 0;
        var oneCount = 0;

        foreach (var bit in str) {
            if (bit == '0') {
                zeroCount++;
            } else {
                oneCount++;
            }
        }

        return (zeroCount, oneCount);
    }
}
```

## Python
```python
class Solution:
    def findMaxForm(self, strs: List[str], max_zero_count: int, max_one_count: int) -> int:
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
```c++
class Solution {
public:
    int findMaxForm(vector<string>& strs, int max_zero_count, int max_one_count) {
        vector<vector<int>> dp(max_zero_count + 1, vector<int>(max_one_count + 1, 0));

        for (auto& str : strs) {
            auto zero_count = 0;
            auto one_count = 0;

            for (auto bit : str) {
                if (bit == '0') {
                    zero_count++;
                } else {
                    one_count++;
                }
            }

            for (auto i = max_zero_count; i >= zero_count; i--) {
                for (auto j = max_one_count; j >= one_count; j--) {
                    dp[i][j] = max(dp[i][j], dp[i - zero_count][j - one_count] + 1);
                }
            }
        }

        return dp[max_zero_count][max_one_count];
    }
};
```

## Java
```java
class Solution {
    public int findMaxForm(String[] strs, int maxZeroCount, int maxOneCount) {
        var dp = new int[maxZeroCount + 1][maxOneCount + 1];

        for (var str : strs) {
            var zeroCount = 0;
            var oneCount = 0;

            for (var bit : str.toCharArray()) {
                if (bit == '0') {
                    zeroCount++;
                } else {
                    oneCount++;
                }
            }

            for (var i = maxZeroCount; i >= zeroCount; i--) {
                for (var j = maxOneCount; j >= oneCount; j--) {
                    dp[i][j] = Math.max(dp[i][j], dp[i - zeroCount][j - oneCount] + 1);
                }
            }
        }

        return dp[maxZeroCount][maxOneCount];
    }
}
```

## JavaScript
```javascript
var findMaxForm = function (strs, maxZeroCount, maxOneCount) {
  const dp = Array(maxZeroCount + 1).fill().map(
    () => Array(maxOneCount + 1).fill(0)
  )

  for (const str of strs) {
    const [zeroCount, oneCount] = countZeroOne(str)

    for (let i = dp.length - 1; i >= zeroCount; i--) {
      for (let j = dp[0].length - 1; j >= oneCount; j--) {
        dp[i][j] = Math.max(dp[i][j], dp[i - zeroCount][j - oneCount] + 1)
      }
    }
  }

  return dp.at(-1).at(-1)
};

function countZeroOne(str) {
  let zeroCount = 0
  let oneCount = 0

  for (const bit of str) {
    if (bit === '0') {
      zeroCount++
    } else {
      oneCount++
    }
  }

  return [zeroCount, oneCount]
}
```

## Go
```go
func findMaxForm(strs []string, maxZeroCount int, maxOneCount int) int {
    dp := make([][]int, maxZeroCount + 1)
    for i := range dp {
        dp[i] = make([]int, maxOneCount + 1)
    }

    for _, str := range strs {
        zeroCount, oneCount := countZeroOne(str)

        for i := len(dp) - 1; i >= zeroCount; i-- {
            for j := len(dp[0]) - 1; j >= oneCount; j-- {
                dp[i][j] = max(dp[i][j], dp[i - zeroCount][j - oneCount] + 1)
            }
        }
    }

    return dp[maxZeroCount][maxOneCount]
}

func countZeroOne(str string) (int, int) {
    zeroCount := 0
    oneCount := 0

    for _, bit := range str {
        if bit == '0' {
            zeroCount++
        } else {
            oneCount++
        }
    }

    return zeroCount, oneCount
}
```

## Ruby
```ruby
def find_max_form(strs, max_zero_count, max_one_count)
  dp = Array.new(max_zero_count + 1) do
    Array.new(max_one_count + 1, 0)
  end

  strs.each do |string|
    zero_count, one_count = count_zero_one(string)

    (zero_count...dp.size).reverse_each do |i|
      (one_count...dp[0].size).reverse_each do |j|
        dp[i][j] = [ dp[i][j], dp[i - zero_count][j - one_count] + 1 ].max
      end
    end
  end

  dp[-1][-1]
end

def count_zero_one(string)
  zero_count = 0
  one_count = 0

  string.each_char do |bit|
    if bit == '0'
      zero_count += 1
    else
      one_count += 1
    end
  end

  [ zero_count, one_count ]
end
```
