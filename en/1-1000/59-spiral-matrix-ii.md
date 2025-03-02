# 59. Spiral Matrix II - Best Practices of LeetCode Solutions
LeetCode link: [59. Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii)

## LeetCode problem description
Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n * n` in spiral order.

### Example 1
![](../../images/examples/59_1.jpg)
```ruby
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
```

### Example 2
```ruby
Input: n = 1
Output: [[1]]
```

### Constraints
- `1 <= n <= 20`

## Intuition
* The difficulty of this question lies in the control of the two-dimensional array index.

* You only need to use a `get_increment(i, j)` function to specifically control the index of the next two-dimensional array.

## Steps to the Solution
1. Initialize `increments` and `increment_index`:

    ```python
    increments = [(0, 1), (1, 0), (0, -1), (-1, 0)] # (i, j) right, down, left, up
    increment_index = 0
    ```

2. Core logic:

    ```python
    while num <= n * n:
        matrix[i][j] = num
        num += 1
    
        increment = get_increment(i, j)
        i += increment[0]
        j += increment[1]
    ```

3. For function `get_increment(i, j)`, it should return a pair like `[0, 1]`. First verify whether the current increment is valid. If not, use the next increment.

   ```python
   def get_increment(i, j):
        increment = increments[increment_index]
        i += increment[0]
        j += increment[1]
   
        if (
            i < 0 or i >= len(matrix) or
            j < 0 or j >= len(matrix) or
            matrix[i][j] is not None
        ): # not valid, use next increment
            increment_index += 1
            increment_index %= len(self.increments)
   
        return increments[increment_index]
   ```

## Complexity
* Time: `O(n * n)`.
* Space: `O(n * n)`.

## Java
```java
class Solution {
    private int[][] matrix;
    private int[][] increments = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    private int incrementIndex = 0;

    public int[][] generateMatrix(int n) {
        matrix = new int[n][n];
        var i = 0;
        var j = 0;
        var num = 1;
        
        while (num <= n * n) {
            matrix[i][j] = num;
            num++;

            var increment = getIncrement(i, j);
            i += increment[0];
            j += increment[1];
        }

        return matrix;
    }

    private int[] getIncrement(int i, int j) {
        var increment = increments[incrementIndex];
        i += increment[0];
        j += increment[1];

        if (
            i < 0 || i >= matrix.length || 
            j < 0 || j >= matrix.length || 
            matrix[i][j] > 0
        ) {
            incrementIndex += 1;
            incrementIndex %= increments.length;
        }

        return increments[incrementIndex];
    }
}
```

## Python
```python
class Solution:
    def __init__(self):
        self.matrix = None
        self.increments = [(0, 1), (1, 0), (0, -1), (-1, 0)]
        self.increment_index = 0

    def generateMatrix(self, n: int) -> List[List[int]]:
        self.matrix = [[None] * n for _ in range(n)]
        i = 0
        j = 0
        num = 1
        
        while num <= n * n:
            self.matrix[i][j] = num
            num += 1

            increment = self.get_increment(i, j)
            i += increment[0]
            j += increment[1]

        return self.matrix

    def get_increment(self, i, j):
        increment = self.increments[self.increment_index]
        i += increment[0]
        j += increment[1]

        if (
            i < 0 or i >= len(self.matrix) or
            j < 0 or j >= len(self.matrix) or
            self.matrix[i][j]
        ):
            self.increment_index += 1
            self.increment_index %= len(self.increments)

        return self.increments[self.increment_index]
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
let matrix
const increments = [[0, 1], [1, 0], [0, -1], [-1, 0]]
let incrementIndex

var generateMatrix = function (n) {
  matrix = Array(n).fill().map(() => Array(n).fill(0))
  incrementIndex = 0

  let i = 0
  let j = 0
  let num = 1

  while (num <= n * n) {
    matrix[i][j] = num
    num++

    const increment = getIncrement(i, j)
    i += increment[0]
    j += increment[1]
  }

  return matrix
};

function getIncrement(i, j) {
  const increment = increments[incrementIndex]
  i += increment[0]
  j += increment[1]

  if (
    i < 0 || i >= matrix.length ||
    j < 0 || j >= matrix.length ||
    matrix[i][j] > 0
  ) {
    incrementIndex += 1
    incrementIndex %= increments.length
  }

  return increments[incrementIndex]
}
```

## C#
```c#
public class Solution
{
    int[][] matrix;
    int[][] increments = { new[] {0, 1}, new[] {1, 0}, new[] {0, -1}, new[] {-1, 0} };
    int incrementIndex = 0;

    public int[][] GenerateMatrix(int n)
    {
        matrix = new int[n][];
        
        for (int k = 0; k < n; k++)
            matrix[k] = new int[n];
        
        int i = 0;
        int j = 0;
        int num = 1;

        while (num <= n * n)
        {
            matrix[i][j] = num;
            num++;

            int[] increment = getIncrement(i, j);
            i += increment[0];
            j += increment[1];
        }

        return matrix;
    }

    int[] getIncrement(int m, int n)
    {
        int[] increment = increments[incrementIndex];
        int i = m + increment[0];
        int j = n + increment[1];

        if (
            i < 0 || i >= matrix.GetLength(0) || 
            j < 0 || j >= matrix.GetLength(0) || 
            matrix[i][j] > 0
        )
        {
            incrementIndex += 1;
            incrementIndex %= increments.Length;
        }

        return increments[incrementIndex];
    }
}
```

## Go
```go
// Welcome to create a PR to complete the code of this language, thanks!
```

## Ruby
```ruby
# Welcome to create a PR to complete the code of this language, thanks!
```

## C
```c
// Welcome to create a PR to complete the code of this language, thanks!
```

## Kotlin
```kotlin
// Welcome to create a PR to complete the code of this language, thanks!
```

## Swift
```swift
// Welcome to create a PR to complete the code of this language, thanks!
```

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
