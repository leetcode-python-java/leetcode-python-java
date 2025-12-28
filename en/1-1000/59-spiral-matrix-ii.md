# 59. Spiral Matrix II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [59. Spiral Matrix II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/59-spiral-matrix-ii) for a better experience!

LeetCode link: [59. Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii), difficulty: **Medium**.

## LeetCode description of "59. Spiral Matrix II"

Given a positive integer `n`, generate an `n x n` matrix filled with elements from *1* to *n<sup>2</sup>* in spiral order.

### [Example 1]

![](../../images/examples/59_1.jpg)

**Input**: `n = 3`

**Output**: `[[1,2,3],[8,9,4],[7,6,5]]`

### [Example 2]

**Input**: `n = 1`

**Output**: `[[1]]`

### [Constraints]

- `1 <= n <= 20`

## Intuition

- The difficulty of this question lies in how to get the next position of the current position in a two-dimensional array.

- You can write a method `get_increment(i, j)`, which is specifically used to get the change between the next position and the current position.

## Step-by-Step Solution

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

- Time complexity: `O(N * N)`.
- Space complexity: `O(N * N)`.

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

```csharp
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

## Ruby

```ruby
def generate_matrix(n)
  @matrix = Array.new(n) { Array.new(n) }
  @increments = [[0, 1], [1, 0], [0, -1], [-1, 0]]
  @increment_index = 0

  i = 0
  j = 0
  num = 1

  while num <= n * n
    @matrix[i][j] = num
    num += 1

    increment = get_increment(i, j)
    i += increment[0]
    j += increment[1]
  end

  @matrix
end

private

def get_increment(i, j)
  increment = @increments[@increment_index]
  next_i = i + increment[0]
  next_j = j + increment[1]

  if next_i < 0 || next_i >= @matrix.size ||
    next_j < 0 || next_j >= @matrix.size ||
    @matrix[next_i][next_j]
    @increment_index += 1
    @increment_index %= @increments.size
  end

  @increments[@increment_index]
end
```

## Go

```go
type spiralMatrix struct {
    matrix        [][]int
    increments    [][2]int
    incrementIndex int
}

func (sm *spiralMatrix) getIncrement(i, j int) [2]int {
    currentIncrement := sm.increments[sm.incrementIndex]
    nextI := i + currentIncrement[0]
    nextJ := j + currentIncrement[1]

    if nextI < 0 || nextI >= len(sm.matrix) || 
       nextJ < 0 || nextJ >= len(sm.matrix) || 
       sm.matrix[nextI][nextJ] != 0 {
        sm.incrementIndex = (sm.incrementIndex + 1) % len(sm.increments)
    }
    return sm.increments[sm.incrementIndex]
}

func generateMatrix(n int) [][]int {
    sm := &spiralMatrix{
        matrix: make([][]int, n),
        increments: [][2]int{{0, 1}, {1, 0}, {0, -1}, {-1, 0}},
        incrementIndex: 0,
    }

    for i := range sm.matrix {
        sm.matrix[i] = make([]int, n)
    }

    i, j, num := 0, 0, 1

    for num <= n * n {
        sm.matrix[i][j] = num
        num++

        increment := sm.getIncrement(i, j)
        i += increment[0]
        j += increment[1]
    }

    return sm.matrix
}
```

## C++

```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        matrix_ = vector<vector<int>>(n, vector<int>(n, 0));
        increments_ = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
        increment_index_ = 0;
        
        int i = 0;
        int j = 0;
        int num = 1;
        
        while (num <= n * n) {
            matrix_[i][j] = num;
            num++;
            
            vector<int> increment = getIncrement(i, j);
            i += increment[0];
            j += increment[1];
        }
        
        return matrix_;
    }

private:
    vector<vector<int>> matrix_;
    vector<vector<int>> increments_;
    int increment_index_;
    
    vector<int> getIncrement(int i, int j) {
        vector<int> increment = increments_[increment_index_];
        int next_i = i + increment[0];
        int next_j = j + increment[1];
        
        if (
            next_i < 0 || next_i >= matrix_.size() ||
            next_j < 0 || next_j >= matrix_.size() ||
            matrix_[next_i][next_j] > 0
        ) {
            increment_index_++;
            increment_index_ %= increments_.size();
        }
        
        return increments_[increment_index_];
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
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [59. Spiral Matrix II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/59-spiral-matrix-ii) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

