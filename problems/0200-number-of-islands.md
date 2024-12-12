# 200. Number of Islands
LeetCode problem: [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)

## LeetCode problem description
Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return the number of islands.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

### Example 1
```
Input: grid = [
    ["1","1","1","1","0"],
    ["1","1","0","1","0"],
    ["1","1","0","0","0"],
    ["0","0","0","0","0"]
]
Output: 1
```

### Example 2
```
Input: grid = [
    ["1","1","0","0","0"],
    ["1","1","0","0","0"],
    ["0","0","1","0","0"],
    ["0","0","0","1","1"]
]
Output: 3
```

### Constraints
- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 300`
- `grid[i][j]` is `'0'` or `'1'`.

## Thoughts
This problem can be solved using **[Breadth-First Search of a Graph](https://en.wikipedia.org/wiki/Breadth-first_search)**.

1. Find the first land point.
1. Use `Breadth-First Search` to find all the adjacent land points of the first land point.
    * Will need to use a `queue` (or a `stack`) to process those points.
    * Mark each found land point as `V` which represents `visited`.
1. When a round of `Breadth-First Search` is done (all surrounded by water), an island is found (`counter++`).
1. Find another non-visited land point.
1. Repeat the above steps until all the land points have been `visited`.

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Complexity
* Time: `O(n * m)`.
* Space: `O(n * m)`.

## Python
```python
class Solution:
    def __init__(self):
        self.grid = None
        self.point_queue = deque()

    def numIslands(self, grid: List[List[str]]) -> int:
        island_count = 0
        self.grid = grid

        for i, row in enumerate(grid):
            for j, item in enumerate(row):
                if item == '1':
                    island_count += 1
                    self.breadth_first_search((i, j))

        return island_count

    def breadth_first_search(self, point):
        self.point_queue.append(point)

        while self.point_queue:
            i, j = self.point_queue.popleft()

            if i < 0 or i >= len(self.grid):
                continue

            if j < 0 or j >= len(self.grid[0]):
                continue

            if self.grid[i][j] != '1':
                continue

            self.grid[i][j] = 'V'

            for adjacent_point in [
                (i - 1, j),
                (i + 1, j),
                (i, j - 1),
                (i, j + 1)
            ]:
                self.point_queue.append(adjacent_point)
```

## Java
```java
class Solution {
    Stack<int[]> pointStack = new Stack<>();
    char[][] grid;

    public int numIslands(char[][] grid) {
        this.grid = grid;
        var islandCount = 0;

        for (var i = 0; i < grid.length; i++) {
            for (var j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == '1') {
                    islandCount++;

                    breadthFirstSearch(new int[]{i, j});
                }
            }
        }

        return islandCount;
    }

    void breadthFirstSearch(int[] point) {
        pointStack.push(point);

        while (!pointStack.empty()) {
            point = pointStack.pop();
            int i = point[0];
            int j = point[1];

            if (i < 0 || i >= grid.length) {
                continue;
            }

            if (j < 0 || j >= grid[0].length) {
                continue;
            }

            if (grid[i][j] != '1') {
                continue;
            }

            grid[i][j] = 'V';

            int[][] adjacentPoints = {
                {i - 1, j},
                {i + 1, j},
                {i, j - 1},
                {i, j + 1}
            };
            for (var adjacentPoint : adjacentPoints) {
                pointStack.push(adjacentPoint);
            }
        }
    }
}
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
let grid
let pointStack

var numIslands = function (grid_) {
  grid = grid_
  pointStack = []
  let islandCount = 0

  grid.forEach((row, i) => {
    row.forEach((item, j) => {
      if (item === '1') {
        islandCount++

        breadthFirstSearch([i, j])
      }
    })
  })

  return islandCount
};

function breadthFirstSearch(point) {
  pointStack.push(point)

  while (pointStack.length > 0) {
    const [i, j] = pointStack.pop()

    if (i < 0 || i >= grid.length) {
      continue
    }

    if (j < 0 || j >= grid[0].length) {
      continue
    }

    if (grid[i][j] != '1') {
      continue
    }

    grid[i][j] = 'V';

    [
      [i - 1, j],
      [i + 1, j],
      [i, j - 1],
      [i, j + 1]
    ].forEach((adjacentPoint) => pointStack.push(adjacentPoint))
  }
}
```

## C#
```c#
public class Solution
{
    Stack<int[]> pointStack = new Stack<int[]>();
    char[][] grid;

    public int NumIslands(char[][] grid)
    {
        this.grid = grid;
        int islandCount = 0;

        for (var i = 0; i < grid.Length; i++)
        {
            for (var j = 0; j < grid[0].Length; j++)
            {
                if (grid[i][j] == '1')
                {
                    islandCount++;

                    breadthFirstSearch([i, j]);
                }
            }
        }

        return islandCount;
    }

    void breadthFirstSearch(int[] point)
    {
        pointStack.Push(point);

        while (pointStack.Count > 0)
        {
            point = pointStack.Pop();
            int i = point[0];
            int j = point[1];

            if (i < 0 || i >= grid.Length)
            {
                continue;
            }
            if (j < 0 || j >= grid[0].Length) {
                continue;
            }
            if (grid[i][j] != '1')
            {
                continue;
            }

            grid[i][j] = 'V';

            int[][] adjacentPoints = [
                [i + 1, j],
                [i - 1, j],
                [i, j + 1],
                [i, j - 1]
            ];
            foreach (var adjacentPoint in adjacentPoints) {
                pointStack.Push(adjacentPoint);
            }
        }
    }
}
```

## Go
```go
// Best solutions are at https://github.com/gazeldx/leetcode-best-practice
// Welcome to create a PR to complete the code of this language, thanks!
```

## Ruby
```ruby
# Best solutions are at https://github.com/gazeldx/leetcode-best-practice
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
