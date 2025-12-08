# 509. Fibonacci Number - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired. We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform designed specifically for programmers.
>
> **The All-In-One Powerhouse for Your Career:**
> - 📄 **Professional Resume:** Create a dynamic, tech-focused resume that stands out to recruiters.
> - 🎨 **Visual Portfolio:** Automatically aggregate your GitHub contributions and projects into a stunning showcase.
> - ✍️ **Tech Blog:** Share your knowledge and build authority with a clean, distraction-free blogging space.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [509. Fibonacci Number - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/509-fibonacci-number) for a better experience!

LeetCode link: [509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number), difficulty: **Easy**.

## LeetCode description of "509. Fibonacci Number"

The **Fibonacci numbers**, commonly denoted `F(n)` form a sequence, called the **Fibonacci sequence**, such that each number is the sum of the two preceding ones, starting from `0` and `1`. That is,

> F(0) = 0, F(1) = 1
> F(n) = F(n - 1) + F(n - 2), for n > 1.

Given `n`, calculate `F(n)`.

### [Example 1]

**Input**: `n = 2`

**Output**: `1`

**Explanation**: `F(2) = F(1) + F(0) = 1 + 0 = 1`

### [Example 2]

**Input**: `n = 3`

**Output**: `2`

**Explanation**: `F(3) = F(2) + F(1) = 1 + 1 = 2`

### [Example 3]

**Input**: `n = 4`

**Output**: `3`

**Explanation**: `F(4) = F(3) + F(2) = 2 + 1 = 3`

### [Constraints]

0 <= n <= 30

## Intuition 1



## Pattern of "Recursion"

Recursion is an important concept in computer science and mathematics, which refers to the method by which a function calls itself **directly or indirectly** in its definition.

### The core idea of ​​recursion

- **Self-call**: A function calls itself during execution.
- **Base case**: Equivalent to the termination condition. After reaching the base case, the result can be returned without recursive calls to prevent infinite loops.
- **Recursive step**: The step by which the problem gradually approaches the "base case".

## Complexity

> If no Map is added to cache known results, the time complexity will rise to O( 2^N )

- Time complexity: `O(N)`.
- Space complexity: `O(N)`.

## C#

```csharp
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

## Python

```python
class Solution:
    @cache
    def fib(self, n: int) -> int:
        if n <= 1:
            return n

        return self.fib(n - 1) + self.fib(n - 2)
```

## C++

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

## Java

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

## JavaScript

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

## Go

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

## Ruby

```ruby
def fib(n)
  return n if n <= 1

  @cache = {} if @cache.nil?

  return @cache[n] if @cache.key?(n)

  @cache[n] = fib(n - 1) + fib(n - 2)

  @cache[n]
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## Intuition 2



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

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(N)`.

## C#

```csharp
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

## Python

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

## C++

```cpp
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

## Java

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

## JavaScript

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

## Go

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

## Ruby

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

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## Intuition 3



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

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## C#

```csharp
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

```cpp
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

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired. We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform designed specifically for programmers.
>
> **The All-In-One Powerhouse for Your Career:**
> - 📄 **Professional Resume:** Create a dynamic, tech-focused resume that stands out to recruiters.
> - 🎨 **Visual Portfolio:** Automatically aggregate your GitHub contributions and projects into a stunning showcase.
> - ✍️ **Tech Blog:** Share your knowledge and build authority with a clean, distraction-free blogging space.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [509. Fibonacci Number - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/509-fibonacci-number) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

