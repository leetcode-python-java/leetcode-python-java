# 200. Number of Islands (Solution 3: Breadth-First Search)
LeetCode link: [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)

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

![](../../images/graph_undirected_1.svg)

And this graph may have multiple **connected components** (islands):

![](../../images/graph_undirected_2.png)

Finding the number of islands is to find the number of `connected components`.

Walk from one vertex (land) to the adjacent vertices until all vertices on the island are visited.

## Steps
1. Find the first land.
1. Starting at the first land, find all the lands of the island.
    * There are two major ways to explore a `connected component` (island): **Breadth-First Search** and **Depth-First Search**.
    * For **Depth-First Search**, there are two ways to make it: `Recursive` and `Iterative`. So I will provide 3 solutions in total.
    * Mark each found land as `V` which represents `visited`. Visited lands don't need to be visited again.
1. After all lands on an island have been visited, look for the next non-visited land.
1. Repeat the above two steps until all the lands have been `visited`.

### Solution 1: 'Depth-First Search' by Recursion
Please click [Depth-First Search by Recursion Solution](200-number-of-islands.md) for `200. Number of Islands` to view.

## Solution 2: 'Depth-First Search' by Iteration
Please click [Depth-First Search by Iteration Solution](200-number-of-islands-2.md) for `200. Number of Islands` to view.

## Solution 3: Breadth-First Search
![](../../images/binary_tree_BFS_1.gif)

As shown in the figure above, **Breadth-First Search** can be thought of as visiting vertices in rounds and rounds.

`Breadth-First Search` emphasizes first-in-first-out, so a **queue** is needed.

## Complexity
* Time: `O(n * m)`.
* Space: `O(n * m)`.

## Python
```python
class Solution:
    def __init__(self):
        self.grid = None
        self.vertex_queue = deque()

    def numIslands(self, grid: List[List[str]]) -> int:
        island_count = 0
        self.grid = grid

        for i, row in enumerate(grid):
            for j, value in enumerate(row):
                if value == '1':
                    island_count += 1

                    self.breadth_first_search((i, j))

        return island_count

    def breadth_first_search(self, vertex):
        self.vertex_queue.append(vertex)

        while self.vertex_queue:
            i, j = self.vertex_queue.popleft()

            if i < 0 or i >= len(self.grid):
                continue

            if j < 0 or j >= len(self.grid[0]):
                continue

            if self.grid[i][j] != '1':
                continue

            self.grid[i][j] = 'V' # For island problems, its OK to mark visited at this place. For other graph problems, we need to use `visited_vertex_set` and mark visited as soon as enqueuing `vertex_queue`. Because the adjacent veticies could be a lot, and it will cause performance issue.

            self.vertex_queue.append((i - 1, j))
            self.vertex_queue.append((i, j + 1))
            self.vertex_queue.append((i + 1, j))
            self.vertex_queue.append((i, j - 1))
```

## Java
```java
class Solution {
    Queue<int[]> vertexQueue = new ArrayDeque<>();
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

    void breadthFirstSearch(int[] vertex) {
        vertexQueue.add(vertex);

        while (!vertexQueue.isEmpty()) {
            vertex = vertexQueue.poll();
            int i = vertex[0];
            int j = vertex[1];

            if (i < 0 || i >= grid.length) {
                continue;
            }

            if (j < 0 || j >= grid[0].length) {
                continue;
            }

            if (grid[i][j] != '1') {
                continue;
            }

            grid[i][j] = 'V'; // For island problems, its OK to mark visited at this place. For other graph problems, we need to use `visited_vertex_set` and mark visited as soon as enqueuing `vertex_queue`. Because the adjacent veticies could be a lot, and it will cause performance issue.

            vertexQueue.add(new int[]{i - 1, j});
            vertexQueue.add(new int[]{i, j + 1});
            vertexQueue.add(new int[]{i + 1, j});
            vertexQueue.add(new int[]{i, j - 1});
        }
    }
}
```

## C++
```cpp
class Solution {
private:
    vector<vector<char>> grid_;
    queue<pair<int, int>> vertex_queue;

    void breadth_first_search(int i1, int j1) {
        vertex_queue.push({i1, j1});

        while (!vertex_queue.empty()) {
            pair<int, int> vertex = vertex_queue.front();
            vertex_queue.pop();

            int i = vertex.first;
            int j = vertex.second;

            if (i < 0 || i >= grid_.size()) {
                continue;
            }

            if (j < 0 || j >= grid_[0].size()) {
                continue;
            }

            if (grid_[i][j] != '1') {
                continue;
            }

            grid_[i][j] = 'V'; // For island problems, its OK to mark visited at this place. For other graph problems, we need to use `visited_vertex_set` and mark visited as soon as enqueuing `vertex_queue`. Because the adjacent veticies could be a lot, and it will cause performance issue.

            vertex_queue.push({i - 1, j});
            vertex_queue.push({i, j + 1});
            vertex_queue.push({i + 1, j});
            vertex_queue.push({i, j - 1});
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

                    breadth_first_search(i, j);
                }
            }
        }

        return island_count;
    }
};
```

## JavaScript
```JavaScript
let grid
let vertexQueue

var numIslands = function (grid_) {
  grid = grid_
  vertexQueue = new Queue() // github.com/datastructures-js/queue
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

function breadthFirstSearch(vertex) {
  vertexQueue.enqueue(vertex)

  while (!vertexQueue.isEmpty()) {
    const [i, j] = vertexQueue.dequeue()

    if (i < 0 || i >= grid.length) {
      continue
    }

    if (j < 0 || j >= grid[0].length) {
      continue
    }

    if (grid[i][j] != '1') {
      continue
    }

    grid[i][j] = 'V'; // For island problems, its OK to mark visited at this place. For other graph problems, we need to use `visited_vertex_set` and mark visited as soon as enqueuing `vertex_queue`. Because the adjacent veticies could be a lot, and it will cause performance issue.

    vertexQueue.enqueue([i - 1, j])
    vertexQueue.enqueue([i, j + 1])
    vertexQueue.enqueue([i + 1, j])
    vertexQueue.enqueue([i, j - 1])
  }
}
```

## C#
```c#
public class Solution
{
    Queue<int[]> vertexQueue = new Queue<int[]>();
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

    void breadthFirstSearch(int[] vertex)
    {
        vertexQueue.Enqueue(vertex);

        while (vertexQueue.Count > 0)
        {
            vertex = vertexQueue.Dequeue();
            int i = vertex[0];
            int j = vertex[1];

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

            grid[i][j] = 'V'; // For island problems, its OK to mark visited at this place. For other graph problems, we need to use `visited_vertex_set` and mark visited as soon as enqueuing `vertex_queue`. Because the adjacent veticies could be a lot, and it will cause performance issue.

            vertexQueue.Enqueue([i - 1, j]);
            vertexQueue.Enqueue([i, j + 1]);
            vertexQueue.Enqueue([i + 1, j]);
            vertexQueue.Enqueue([i, j - 1]);
        }
    }
}
```

## Go
```go
var grid [][]byte
var vertexQueue = linkedlistqueue.New()

func numIslands(grid_ [][]byte) int {
    grid = grid_
    vertexQueue.Clear()
    islandCount := 0

    for i, row := range grid {
        for j, value := range row {
            if value == '1' {
                islandCount++

                breadthFirstSearch([]int{i, j})
            }
        }
    }

    return islandCount
}

func breadthFirstSearch(vertex []int) {
    vertexQueue.Enqueue(vertex)

    for !vertexQueue.Empty() {
        vertex, _ := vertexQueue.Dequeue();

        i := vertex.([]int)[0]
        j := vertex.([]int)[1]

        if i < 0 || i >= len(grid) {
            continue
        }

        if j < 0 || j >= len(grid[0]) {
            continue
        }

        if grid[i][j] != '1' {
            continue
        }

        grid[i][j] = 'V' // For island problems, its OK to mark visited at this place. For other graph problems, we need to use `visited_vertex_set` and mark visited as soon as enqueuing `vertex_queue`. Because the adjacent veticies could be a lot, and it will cause performance issue.

        vertexQueue.Enqueue([]int{i - 1, j})
        vertexQueue.Enqueue([]int{i, j + 1})
        vertexQueue.Enqueue([]int{i + 1, j})
        vertexQueue.Enqueue([]int{i, j - 1})
    }
}
```

## Ruby
```ruby
def num_islands(grid)
  @grid = grid
  @vertex_queue = Containers::Queue.new
  island_count = 0

  @grid.each_with_index do |row, i|
    row.each_with_index do |value, j|
      if value == '1'
        breadth_first_search([i, j])

        island_count += 1
      end
    end
  end

  island_count
end

def breadth_first_search(vertex)
  @vertex_queue.push(vertex)

  while !@vertex_queue.empty?
    vertex = @vertex_queue.pop

    i = vertex[0]
    j = vertex[1]

    next if i < 0 || i >= @grid.size
    
    next if j < 0 || j >= @grid[0].size
    
    next if @grid[i][j] != '1'

    @grid[i][j] = 'V' # For island problems, its OK to mark visited at this place. For other graph problems, we need to use `visited_vertex_set` and mark visited as soon as enqueuing `vertex_queue`. Because the adjacent veticies could be a lot, and it will cause performance issue.

    @vertex_queue << [i - 1, j]
    @vertex_queue << [i, j + 1]
    @vertex_queue << [i + 1, j]
    @vertex_queue << [i, j - 1]
  end
end
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
