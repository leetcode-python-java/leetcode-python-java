# 200. Number of Islands (Solution 2: 'Depth-First Search' by Iteration)
LeetCode problem link: [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)

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

### Solution 1: 'Depth-First Search' by Recursion
Please click [Depth-First Search by Recursion Solution](0200-number-of-islands.md) for `200. Number of Islands` to view.

## Solution 2: 'Depth-First Search' by Iteration
![](../images/binary_tree_DFS_1.png)

In solution 1, we have known how to traverse a graph by recursion. Computer language support for recursive calls is implemented through stacks.
For every recursive solution, there is an iterative solution, which means the same problem can be solved using loops.
The benefit of using iteration is better program performance. After all, recursive calls are expensive.

Maintaining a stack by yourself can accomplish the same function as recursive calls.

From this sample code bellow, you can see that starting from a node, through recursive calls, it goes up until it can't go any further, turns right, and continues up. The priority order of directions is `up, right, down, and left`.
```python
adjacent_points = [
    (i, j - 1), # left
    (i + 1, j), # down
    (i, j + 1), # right
    (i - 1, j), # up
]
```

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
        self.point_stack = []

    def numIslands(self, grid: List[List[str]]) -> int:
        island_count = 0
        self.grid = grid

        for i, row in enumerate(grid):
            for j, value in enumerate(row):
                if value == '1':
                    island_count += 1

                    self.depth_first_search((i, j))

        return island_count

    def depth_first_search(self, point):
        self.point_stack.append(point)

        while self.point_stack:
            i, j = self.point_stack.pop()

            if i < 0 or i >= len(self.grid):
                continue

            if j < 0 or j >= len(self.grid[0]):
                continue

            if self.grid[i][j] != '1':
                continue

            self.grid[i][j] = 'V'

            self.point_stack.append((i, j - 1))
            self.point_stack.append((i + 1, j))
            self.point_stack.append((i, j + 1))
            self.point_stack.append((i - 1, j))
```

# Java
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

                    depthFirstSearch(new int[]{i, j});
                }
            }
        }

        return islandCount;
    }

    void depthFirstSearch(int[] point) {
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

            pointStack.push(new int[]{i, j - 1});
            pointStack.push(new int[]{i + 1, j});
            pointStack.push(new int[]{i, j + 1});
            pointStack.push(new int[]{i - 1, j});
        }
    }
}
```

# C++
```cpp
class Solution {
private:
    vector<vector<char>> grid_;
    stack<pair<int, int>> point_stack;

    void depth_first_search(int i1, int j1) {
        point_stack.push({i1, j1});

        while (!point_stack.empty()) {
            pair<int, int> point = point_stack.top();
            point_stack.pop();

            int i = point.first;
            int j = point.second;

            if (i < 0 || i >= grid_.size()) {
                continue;
            }

            if (j < 0 || j >= grid_[0].size()) {
                continue;
            }

            if (grid_[i][j] != '1') {
                continue;
            }

            grid_[i][j] = 'V';

            point_stack.push({i, j - 1});
            point_stack.push({i + 1, j});
            point_stack.push({i, j + 1});
            point_stack.push({i - 1, j});
        }
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
let pointStack

var numIslands = function (grid_) {
  grid = grid_
  pointStack = []
  let islandCount = 0

  grid.forEach((row, i) => {
    row.forEach((item, j) => {
      if (item === '1') {
        islandCount++

        depthFirstSearch([i, j])
      }
    })
  })

  return islandCount
};

function depthFirstSearch(point) {
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

    pointStack.push([i, j - 1])
    pointStack.push([i + 1, j])
    pointStack.push([i, j + 1])
    pointStack.push([i - 1, j])
  }
}
```

# C#
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

                    depthFirstSearch([i, j]);
                }
            }
        }

        return islandCount;
    }

    void depthFirstSearch(int[] point)
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
            if (j < 0 || j >= grid[0].Length)
            {
                continue;
            }
            if (grid[i][j] != '1')
            {
                continue;
            }

            grid[i][j] = 'V';

            pointStack.Push([i, j - 1]);
            pointStack.Push([i + 1, j]);
            pointStack.Push([i, j + 1]);
            pointStack.Push([i - 1, j]);
        }
    }
}
```

# Go
```go
var grid [][]byte
var pointStack = arraystack.New()

func numIslands(grid_ [][]byte) int {
    grid = grid_
    pointStack.Clear()
    islandCount := 0

    for i, row := range grid {
        for j, value := range row {
            if value == '1' {
                islandCount++

                depthFirstSearch([]int{i, j})
            }
        }
    }

    return islandCount
}

func depthFirstSearch(point []int) {
    pointStack.Push(point)

    for !pointStack.Empty() {
        point, _ := pointStack.Pop();

        i := point.([]int)[0]
        j := point.([]int)[1]

        if i < 0 || i >= len(grid) {
            continue
        }

        if j < 0 || j >= len(grid[0]) {
            continue
        }

        if grid[i][j] != '1' {
            continue
        }

        grid[i][j] = 'V'

        pointStack.Push([]int{i, j - 1})
        pointStack.Push([]int{i + 1, j})
        pointStack.Push([]int{i, j + 1})
        pointStack.Push([]int{i - 1, j})
    }
}
```

# Ruby
```ruby
def num_islands(grid)
  @grid = grid
  @point_stack = []
  island_count = 0

  @grid.each_with_index do |row, i|
    row.each_with_index do |value, j|
      if value == '1'
        depth_first_search([i, j])

        island_count += 1
      end
    end
  end

  island_count
end

def depth_first_search(point)
  @point_stack << point

  while !@point_stack.empty?
    point = @point_stack.pop

    i = point[0]
    j = point[1]

    next if i < 0 || i >= @grid.size
    
    next if j < 0 || j >= @grid[0].size
    
    next if @grid[i][j] != '1'

    @grid[i][j] = 'V'

    @point_stack << [i, j - 1]
    @point_stack << [i + 1, j]
    @point_stack << [i, j + 1]
    @point_stack << [i - 1, j]
  end
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
