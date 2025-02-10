# LeetCode 827. Making A Large Island's Solution
LeetCode link: [827. Making A Large Island](https://leetcode.com/problems/making-a-large-island/)

## LeetCode problem description
You are given an `n x n` binary matrix `grid`. You are allowed to change at most one `0` to be `1`.

Return the size of the largest island in `grid` after applying this operation.

An island is a 4-directionally connected group of `1`s.

### Example 1
```
Input: grid = [
    [1,0],
    [0,1]
]
Output: 3
Explanation: Change one 0 to 1 and connect two 1s, then we get an island with area = 3.
```

### Example 2
```
Input: grid = [
    [1,1],
    [1,0]
]
Output: 4
Explanation: Change the 0 to 1 and make the island bigger, only one island with area = 4.
```
### Example 3
```
Input: grid = [
    [1,1],
    [1,1]
]
Output: 4
Explanation: Can't change any 0 to 1, only one island with area = 4.
```

### Constraints
- `n == grid.length`
- `n == grid[i].length`
- `1 <= n <= 500`
- `grid[i][j]` is either `0` or `1`.

## Intuition
This problem is hard. Before solving this problem, you can do the following two problems first:

- [200. Number of Islands](200-number-of-islands.md)
- [695. Max Area of Island](695-max-area-of-island.md)

The island problem can be abstracted into a **graph theory** problem. This is an **undirected graph**:

![](../../images/graph_undirected_1.svg)

And this graph may have multiple **connected components** (islands):

![](../../images/graph_undirected_2.png)

## Approach
1. Change one vertex from `0` to `1` to make the largest island means combining the adjacent islands of a `0` vertex.
1. We can mark an island's lands with one same id (`island_id`), and mark another island's lands with another `island_id`. To mark a land, just change its value to the `island_id`.
1. Use a `map` (or an `array`) to map each `island_id` to its `area`.
1. How to calculate the area of an island? Using `Depth-First Search` or `Breadth-First Search`. See [695. Max Area of Island](695-max-area-of-island.md).
1. Iterate through each `0` (water), then sum the `areas` of neighboring islands.
1. Record the max area and return it.

## Complexity
* Time: `O(n * n)`.
* Space: `O(n * n)`.

## Python
```python
from collections import defaultdict

class Solution:
    def __init__(self):
        self.island_id = 2
        self.island_id_to_area = defaultdict(int)

    def largestIsland(self, grid: List[List[int]]) -> int:
        self.grid = grid
        max_area = 0

        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if self.grid[i][j] == 1:
                    self.depth_first_search(i, j)
                    self.island_id += 1

        has_water = False

        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if self.grid[i][j] == 0:
                    has_water = True
                    max_area = max(max_area, self.combined_islands_area(i, j))

        if not has_water:
            return len(grid) * len(grid[0])

        return max_area
    
    def depth_first_search(self, i, j):
        if i < 0 or j < 0 or i >= len(self.grid) or j >= len(self.grid[0]):
            return

        if self.grid[i][j] != 1:
            return

        self.grid[i][j] = self.island_id
        self.island_id_to_area[self.island_id] += 1

        for a, b in [
            (-1, 0),
            (0, -1), (0, 1),
            (1, 0)
        ]:
            m = i + a
            n = j + b
            self.depth_first_search(m, n)
    
    def combined_islands_area(self, i, j):
        island_ids = set()

        for a, b in [
            (-1, 0),
            (0, -1), (0, 1),
            (1, 0)
        ]:
            m = i + a
            n = j + b

            if m < 0 or n < 0 or m >= len(self.grid) or n >= len(self.grid[0]):
                continue

            if self.grid[m][n] != 0:
                island_ids.add(self.grid[m][n])
        
        area = 1

        for island_id in island_ids:
            area += self.island_id_to_area[island_id]

        return area
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
