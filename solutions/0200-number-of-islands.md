# 200. Number of Islands (Solution 1: 'Depth-First Search' by Recursion)
LeetCode problem link: [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)

# LeetCode problem description
Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return the number of islands.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

## Example 1
```
Input: grid = [
    ["1","1","1","1","0"],
    ["1","1","0","1","0"],
    ["1","1","0","0","0"],
    ["0","0","0","0","0"]
]
Output: 1
```

## Example 2
```
Input: grid = [
    ["1","1","0","0","0"],
    ["1","1","0","0","0"],
    ["0","0","1","0","0"],
    ["0","0","0","1","1"]
]
Output: 3
```

## Constraints
- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 300`
- `grid[i][j]` is `'0'` or `'1'`.

# Thoughts
The island problem can be abstracted into a **graph theory** problem. This is an **undirected graph**:

![](../images/graph_undirected_1.svg)

And this graph may have multiple **connected components** (islands):

![](../images/graph_undirected_2.png)

Finding the number of islands is to find the number of `connected components`.

Walk from one node to the adjacent node until all nodes on the island are visited.

## Steps
1. Find the first land.
1. Starting at the first land, find all the lands of the island.
    * There are two major ways to explore a `connected components` (island): **Breadth-First Search** and **Depth-First Search**.
    * For **Depth-First Search**, there are two ways to make it: `Recursive` and `Iterative`. So I will provide 3 solutions in total.
    * Mark each found land as `V` which represents `visited`. Visited lands don't need to be visited again.
1. After all lands on an island have been visited, look for the next non-visited land.
1. Repeat the above two steps until all the lands have been `visited`.

## Solution 1: 'Depth-First Search' by Recursion
![](../images/binary_tree_DFS_1.png)

From this sample code bellow, you can see that starting from a node, through recursive calls, it goes up until it can't go any further, turns right, and continues up. The priority order of directions is `up, right, down, and left`.
```python
adjacent_points = [
   (i - 1, j), # up
   (i, j + 1), # right
   (i + 1, j), # down
   (i, j - 1), # left
]
```

## Solution 2: 'Depth-First Search' by Iteration
Please click [Depth-First Search by Iteration Solution](0200-number-of-islands-2.md) for `200. Number of Islands` to view.

## Solution 3: Breadth-First Search
Please click [Breadth-First Search Solution](0200-number-of-islands-3.md) for `200. Number of Islands` to view.

## Complexity
* Time: `O(n * m)`.
* Space: `O(n * m)`.

# Python
```python
class Solution:
    def __init__(self):
        self.grid = None

    def numIslands(self, grid: List[List[str]]) -> int:
        self.grid = grid
        island_count = 0

        for i, row in enumerate(grid):
            for j, value in enumerate(row):
                if value == '1':
                    island_count += 1

                    self.depth_first_search(i, j)

        return island_count

    def depth_first_search(self, i, j):
        if i < 0 or i >= len(self.grid):
            return

        if j < 0 or j >= len(self.grid[0]):
            return

        if self.grid[i][j] != '1':
            return

        self.grid[i][j] = 'V'

        self.depth_first_search(i - 1, j)
        self.depth_first_search(i, j + 1)
        self.depth_first_search(i + 1, j)
        self.depth_first_search(i, j - 1)
```

# Java
```java
class Solution {
    char[][] grid;

    public int numIslands(char[][] grid) {
        this.grid = grid;
        var islandCount = 0;

        for (var i = 0; i < grid.length; i++) {
            for (var j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == '1') {
                    islandCount++;

                    depthFirstSearch(i, j);
                }
            }
        }

        return islandCount;
    }

    void depthFirstSearch(int i, int j) {
        if (i < 0 || i >= grid.length) {
            return;
        }

        if (j < 0 || j >= grid[0].length) {
            return;
        }

        if (grid[i][j] != '1') {
            return;
        }

        grid[i][j] = 'V';

        depthFirstSearch(i - 1, j);
        depthFirstSearch(i, j + 1);
        depthFirstSearch(i + 1, j);
        depthFirstSearch(i, j - 1);
    }
}
```

# C++
```cpp
class Solution {
private:
    vector<vector<char>> grid_;

    void depth_first_search(int i, int j) {
        if (i < 0 || i >= grid_.size() || 
            j < 0 || j >= grid_[0].size() || 
            grid_[i][j] != '1') {
            return;
        }

        grid_[i][j] = 'V';

        depth_first_search(i - 1, j);
        depth_first_search(i, j + 1);
        depth_first_search(i + 1, j);
        depth_first_search(i, j - 1);
    }

public:
    int numIslands(vector<vector<char>>& grid) {
        grid_ = grid;
        auto island_count = 0;

        for (auto i = 0; i < grid_.size(); i++) {
            for (auto j = 0; j < grid_[0].size(); j++) {
                if (grid_[i][j] == '1') {
                    island_count++;

                    depth_first_search(i, j);
                }
            }
        }

        return island_count;
    }
};
```

# JavaScript
```JavaScript
let grid

var numIslands = function (grid_) {
  grid = grid_
  let islandCount = 0

  grid.forEach((row, i) => {
    row.forEach((value, j) => {
      if (value === '1') {
        islandCount++

        depthFirstSearch(i, j)
      }
    })
  })

  return islandCount
};

function depthFirstSearch(i, j) {
  if (i < 0 || i >= grid.length) {
    return
  }

  if (j < 0 || j >= grid[0].length) {
    return
  }

  if (grid[i][j] != '1') {
    return
  }

  grid[i][j] = 'V';

  depthFirstSearch(i - 1, j)
  depthFirstSearch(i, j + 1)
  depthFirstSearch(i + 1, j)
  depthFirstSearch(i, j - 1)
}
```

# C#
```c#
public class Solution
{
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

                    depthFirstSearch(i, j);
                }
            }
        }

        return islandCount;
    }

    void depthFirstSearch(int i, int j)
    {
        if (i < 0 || i >= grid.Length)
            return;

        if (j < 0 || j >= grid[0].Length)
            return;

        if (grid[i][j] != '1')
            return;

        grid[i][j] = 'V';

        depthFirstSearch(i - 1, j);
        depthFirstSearch(i, j + 1);
        depthFirstSearch(i + 1, j);
        depthFirstSearch(i, j - 1);
    }
}
```

# Go
```go
var grid [][]byte

func numIslands(grid_ [][]byte) int {
    grid = grid_
    islandCount := 0

    for i, row := range grid {
        for j, value := range row {
            if value == '1' {
                islandCount++

                depthFirstSearch(i, j)
            }
        }
    }

    return islandCount
}

func depthFirstSearch(i int, j int) {
    if i < 0 || i >= len(grid) {
        return
    }

    if j < 0 || j >= len(grid[0]) {
        return
    }

    if grid[i][j] != '1' {
        return
    }

    grid[i][j] = 'V'

    depthFirstSearch(i - 1, j)
    depthFirstSearch(i, j + 1)
    depthFirstSearch(i + 1, j)
    depthFirstSearch(i, j - 1)
}
```

# Ruby
```Ruby
def num_islands(grid)
  @grid = grid
  island_count = 0

  @grid.each_with_index do |row, i|
    row.each_with_index do |value, j|
      if value == '1'
        depth_first_search(i, j)

        island_count += 1
      end
    end
  end

  island_count
end

def depth_first_search(i, j)
  return if i < 0 || i >= @grid.size

  return if j < 0 || j >= @grid[0].size

  return if @grid[i][j] != '1'

  @grid[i][j] = 'V'

  depth_first_search(i - 1, j)
  depth_first_search(i, j + 1)
  depth_first_search(i + 1, j)
  depth_first_search(i, j - 1)
end
```

# C
```c
// Welcome to create a PR to complete the code of this language, thanks!
```

# Kotlin
```kotlin
// Welcome to create a PR to complete the code of this language, thanks!
```

# Swift
```swift
// Welcome to create a PR to complete the code of this language, thanks!
```

# Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

# Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
