# LeetCode 463. Island Perimeter's Solution
LeetCode problem link: [463. Island Perimeter](https://leetcode.com/problems/island-perimeter)

## LeetCode problem description
You are given `row x col` `grid` representing a map where `grid[i][j] = 1` represents land and `grid[i][j] = 0` represents water.

Grid cells are connected **horizontally/vertically** (not diagonally). The `grid` is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells).

The island doesn't have "lakes", meaning the water inside isn't connected to the water around the island. One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.

### Example 1
![](../../images/examples/463_1.png)
```
Input: grid = [
    [0,1,0,0],
    [1,1,1,0],
    [0,1,0,0],
    [1,1,0,0]
]
Output: 16
Explanation: The perimeter is the 16 yellow stripes in the image above.
```

### Example 2
```
Input: grid = [[1]]
Output: 4
```

### Example 3
```
Input: grid = [[1,0]]
Output: 4
```

### Constraints
- `row == grid.length`
- `col == grid[i].length`
- `1 <= row, col <= 100`
- `grid[i][j]` is `0` or `1`.
- There is exactly one island in `grid`.

## Intuition and Approach 1: Straightforward
1. To calculate the perimeter of an island, we simply add up the number of water-adjacent edges of all water-adjacent lands.
2. When traversing the grid, once land is found, the number of its adjacent water edges is calculated.

## Intuition 2
The island problem can be abstracted into a **graph theory** problem. This is an **undirected graph**:

![](../../images/graph_undirected_1.svg)

And this graph has only one **connected components** (island).

## Approach 2: Depth-First Search the Island
1. Find the first land.
1. Starting at the first land, find all the lands of the island.
    * There are two major ways to explore a `connected components` (island): **Depth-First Search** (DFS) and **Breadth-First Search** (BFS).
    * For **Depth-First Search**, there are two ways to make it: `Recursive` and `Iterative`. Here I will provide the `Recursive` solution.
        * If you want to know **Depth-First Search** `Iterative` solution, please see [200. Number of Islands (Depth-First Search by Iteration)](200-number-of-islands-2.md).
        * If you want to know **Breadth-First Search** solution, please see [200. Number of Islands (Breadth-First Search)](200-number-of-islands-3.md).
    * Mark each found land as `8` which represents `visited`. Visited lands don't need to be visited again.
1. To calculate the perimeter of an island, we simply add up the number of water-adjacent edges of all water-adjacent lands. 
1. To solve this problem, you don't really need to use `DFS` or `BFS`, but mastering `DFS` and `BFS` is absolutely necessary. 

## Complexity
* Time: `O(n * m)`.
* Space: `O(1)`.

## Python
### Solution 1: Straightforward
```python
class Solution:
    def __init__(self):
        self.perimeter = 0
        self.grid = None

    def islandPerimeter(self, grid: List[List[int]]) -> int:
        self.grid = grid

        for i, row in enumerate(self.grid):
            for j, value in enumerate(row):
                if value == 1:
                    self.perimeter += self.water_edges(i, j)
                    
        return self.perimeter
    
    def water_edges(self, i, j):
        result = 0
        result += self.water_edge(i - 1, j)
        result += self.water_edge(i, j + 1)
        result += self.water_edge(i + 1, j)
        result += self.water_edge(i, j - 1)
        return result

    def water_edge(self, i, j):
        if i < 0 or i >= len(self.grid):
            return 1

        if j < 0 or j >= len(self.grid[0]):
            return 1
        
        if self.grid[i][j] == 0:
            return 1
        
        return 0
```

### Solution 2: Depth-First Search the Island
```python
class Solution:
    def __init__(self):
        self.perimeter = 0
        self.grid = None

    def islandPerimeter(self, grid: List[List[int]]) -> int:
        self.grid = grid

        for i, row in enumerate(self.grid):
            for j, value in enumerate(row):
                if value == 1:
                    self.depth_first_search(i, j)
                    
                    return self.perimeter
    
    def depth_first_search(self, i, j):
        if i < 0 or i >= len(self.grid):
            return

        if j < 0 or j >= len(self.grid[0]):
            return
        
        if self.grid[i][j] != 1:
            return
        
        self.grid[i][j] = 8

        self.perimeter += self.water_edges(i, j)

        self.depth_first_search(i - 1, j)
        self.depth_first_search(i, j + 1)
        self.depth_first_search(i + 1, j)
        self.depth_first_search(i, j - 1)
    
    def water_edges(self, i, j):
        result = 0
        result += self.water_edge(i - 1, j)
        result += self.water_edge(i, j + 1)
        result += self.water_edge(i + 1, j)
        result += self.water_edge(i, j - 1)
        return result

    def water_edge(self, i, j):
        if i < 0 or i >= len(self.grid):
            return 1

        if j < 0 or j >= len(self.grid[0]):
            return 1
        
        if self.grid[i][j] == 0:
            return 1
        
        return 0
```

## Java
```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
// Welcome to create a PR to complete the code of this language, thanks!
```

## C#
```c#
// Welcome to create a PR to complete the code of this language, thanks!
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
