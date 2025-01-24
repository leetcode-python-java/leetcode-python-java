# 509. Fibonacci Number
LeetCode link: [509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)

## LeetCode problem description
The **Fibonacci numbers**, commonly denoted `F(n)` form a sequence, called the **Fibonacci sequence**, such that each number is the sum of the two preceding ones, starting from `0` and `1`. That is,

> F(0) = 0, F(1) = 1
> F(n) = F(n - 1) + F(n - 2), for n > 1.

Given `n`, calculate `F(n)`.

```
------------------------------------------------------------------------
[Example 1]

Input: n = 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
------------------------------------------------------------------------
[Example 2]

Input: n = 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
------------------------------------------------------------------------
[Example 3]

Input: n = 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
------------------------------------------------------------------------
[Constraints]

0 <= n <= 30
------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Dynamic programming**.

Detailed solutions will be given later, and now only the best practices in 4 to 7 languages are given.

### Complexity
* Time: `O(n)`.
* Space: `O(n)`.

## C#
### Solution 1: Recursion
```c#
public class Solution {
    IDictionary<int, int> numToFibNum = new Dictionary<int, int>();

    public int Fib(int n) {
        if (n <= 1) {
            return n;
        }

        if (numToFibNum.ContainsKey(n)) {
            return numToFibNum[n];
        }

        numToFibNum[n] = Fib(n - 1) + Fib(n - 2);

        return numToFibNum[n];
    }
}
```

### Solution 2: Dynamic programming
```c#
public class Solution
{
    public int Fib(int n)
    {
        if (n <= 1)
            return n;

        var dp = new int[n + 1];
        dp[1] = 1;

        for (var i = 2; i < dp.Length; i++)
        {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }
}
```

### Solution 3: Dynamic programming ('dp.length' is 2)
```c#
public class Solution
{
    public int Fib(int n)
    {
        if (n <= 1)
            return n;

        int[] dp = [0, 1];

        for (var i = 2; i <= n; i++)
        {
            var dc = (int[])dp.Clone();

            dp[0] = dc[1];
            dp[1] = dc[0] + dc[1];
        }

        return dp[1];
    }
}
```

## Python
### Solution 1: Recursion
```python
class Solution:
    @cache
    def fib(self, n: int) -> int:
        if n <= 1:
            return n

        return self.fib(n - 1) + self.fib(n - 2)
```

### Solution 2: Dynamic programming
```python
class Solution:
    def fib(self, n: int) -> int:
        if n == 0:
            return 0

        dp = [0] * (n + 1)
        dp[1] = 1

        for i in range(2, len(dp)):
            dp[i] = dp[i - 1] + dp[i - 2]

        return dp[-1]
```

### Solution 3: Dynamic programming ('dp.length' is 2)
```python
class Solution:
    def fib(self, n: int) -> int:
        if n == 0:
            return 0

        dp = [0, 1]

        for i in range(2, n + 1):
            dc = dp.copy()

            dp[0] = dc[1]
            dp[1] = dc[0] + dc[1]

        return dp[1]
```

## C++
### Solution 1: Recursion
```cpp
class Solution {
public:
    int fib(int n) {
        if (n <= 1) {
            return n;
        }

        if (num_to_fib_num_.contains(n)) {
            return num_to_fib_num_[n];
        }

        num_to_fib_num_[n] = fib(n - 1) + fib(n - 2);

        return num_to_fib_num_[n];
    }

private:
    unordered_map<int, int> num_to_fib_num_;
};
```

### Solution 2: Dynamic programming
```c++
class Solution {
public:
    int fib(int n) {
        if (n <= 1) {
            return n;
        }

        auto dp = vector<int>(n + 1);
        dp[1] = 1;

        for (auto i = 2; i < dp.size(); i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }
};
```

### Solution 3: Dynamic programming ('dp.length' is 2)
```c++
class Solution {
public:
    int fib(int n) {
        if (n <= 1) {
            return n;
        }

        vector dp = {0, 1};

        for (auto i = 2; i <= n; i++) {
            auto dc = dp;

            dp[0] = dc[1];
            dp[1] = dc[0] + dc[1];
        }

        return dp[1];
    }
};
```

## Java
### Solution 1: Recursion
```java
class Solution {
    var numToFibNum = new HashMap<Integer, Integer>();

    public int fib(int n) {
        if (n <= 1) {
            return n;
        }

        if (numToFibNum.containsKey(n)) {
            return numToFibNum.get(n);
        }

        numToFibNum.put(n, fib(n - 1) + fib(n - 2));

        return numToFibNum.get(n);
    }
}
```

### Solution 2: Dynamic programming
```java
class Solution {
    public int fib(int n) {
        if (n <= 1) {
            return n;
        }

        var dp = new int[n + 1];
        dp[1] = 1;

        for (var i = 2; i < dp.length; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }
}
```

### Solution 3: Dynamic programming ('dp.length' is 2)
```java
class Solution {
    public int fib(int n) {
        if (n <= 1) {
            return n;
        }

        int[] dp = {0, 1};

        for (var i = 2; i <= n; i++) {
            var dc = dp.clone();

            dp[0] = dc[1];
            dp[1] = dc[0] + dc[1];
        }

        return dp[1];
    }
}
```

## JavaScript
### Solution 1: Recursion
```javascript
const numToFibNum = new Map()

var fib = function (n) {
    if (n <= 1) {
        return n
    }

    if (numToFibNum.has(n)) {
        return numToFibNum.get(n)
    }

    numToFibNum.set(n, fib(n - 1) + fib(n - 2))

    return numToFibNum.get(n)
};
```

### Solution 2: Dynamic programming
```javascript
var fib = function (n) {
    if (n <= 1) {
        return n
    }

    const dp = Array(n + 1).fill(0)
    dp[1] = 1

    for (let i = 2; i < dp.length; i++) {
        dp[i] = dp[i - 1] + dp[i - 2]
    }

    return dp[n]
};
```

### Solution 3: Dynamic programming ('dp.length' is 2)
```javascript
var fib = function (n) {
    if (n <= 1) {
        return n
    }

    const dp = [0, 1]

    for (let i = 2; i <= n; i++) {
        const dc = [...dp]

        dp[0] = dc[1]
        dp[1] = dc[0] + dc[1]
    }

    return dp[1]
};
```

## Go
### Solution 1: Recursion
```go
func fib(m int) int {
    numToFibNum := map[int]int{}

    var fibonacci func (int) int

    fibonacci = func (n int) int {
        if n <= 1 {
            return n
        }

        if result, ok := numToFibNum[n]; ok {
            return result
        }

        numToFibNum[n] = fibonacci(n - 1) + fibonacci(n - 2)
        return numToFibNum[n]
    }

    return fibonacci(m)
}
```

### Solution 2: Dynamic programming
```go
func fib(n int) int {
    if n == 0 {
        return 0
    }

    dp := make([]int, n + 1)
    dp[1] = 1

    for i := 2; i <= n; i++ {
        dp[i] = dp[i - 2] + dp[i - 1]
    }

    return dp[n]
}
```

### Solution 3: Dynamic programming ('dp.length' is 2)
```go
func fib(n int) int {
    if n == 0 {
        return 0
    }

    dp := []int{0, 1}

    for i := 2; i <= n; i++ {
        dc := slices.Clone(dp)

        dp[0] = dc[1]
        dp[1] = dc[0] + dc[1]
    }

    return dp[1]
}
```

## Ruby
### Solution 1: Recursion
```ruby
def fib(n)
  return n if n <= 1

  @cache = {} if @cache.nil?

  return @cache[n] if @cache.key?(n)

  @cache[n] = fib(n - 1) + fib(n - 2)

  @cache[n]
end
```

### Solution 2: Dynamic programming
```ruby
def fib(n)
  return 0 if n == 0

  dp = Array.new(n + 1, 0)
  dp[1] = 1

  (2...dp.size).each do |i|
    dp[i] = dp[i - 1] + dp[i - 2]
  end

  dp[-1]
end
```

### Solution 3: Dynamic programming ('dp.length' is 2)
```ruby
def fib(n)
  return 0 if n == 0

  dp = [0, 1]

  (2..n).each do |i|
    dc = dp.clone

    dp[0] = dc[1]
    dp[1] = dc[0] + dc[1]
  end

  dp[1]
end
```

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
