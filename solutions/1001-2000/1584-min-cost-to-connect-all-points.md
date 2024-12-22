# LeetCode 1584. Min Cost to Connect All Points' Solution
LeetCode problem link: [1584. Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points)

## LeetCode problem description
You are given an array `points` representing integer coordinates of some points on a 2D-plane, where `points[i] = [xi, yi]`.

The cost of connecting two points `[xi, yi]` and `[xj, yj]` is the manhattan distance between them: `|xi - xj| + |yi - yj|`, where `|val|` denotes the absolute value of `val`.

Return _the minimum cost to make all points connected_. All points are connected if there is **exactly one** simple path between any two points.

### Example 1
![](../../images/examples/1584_1_1.png)
```java
Input: points = [[0,0],[2,2],[3,10],[5,2],[7,0]]
Output: 20
Explanation: 
```
![](../../images/examples/1584_1_2.png)
```
We can connect the points as shown above to get the minimum cost of 20.
Notice that there is a unique path between every pair of points.
```

### Example 2
```java
Input: points = [[3,12],[-2,5],[-4,1]]
Output: 18
```

### Constraints
- `1 <= points.length <= 1000`
- `-1000000 <= xi, yi <= 1000000`
- All pairs `(xi, yi)` are distinct.

<details>
  <summary>Hint 1</summary>
  Connect each pair of points with a weighted edge, the weight being the manhattan distance between those points.
</details>

<details>
  <summary>Hint 2</summary>
  The problem is now the cost of minimum spanning tree in graph with above edges.
</details>

## Intuition
* Connect each pair of points with a **weighted** edge, the weight being the manhattan distance between those points.
* Cycles will increase the `cost`, so there is no cycle.
* A connected graph without cycles is called a tree.
* The problem is now the cost of **minimum spanning tree** in graph with above edges.
* A minimum spanning tree (MST) or minimum weight spanning tree is a subset of the edges of a connected, edge-weighted undirected graph that connects all the vertices together, without any cycles and with the minimum possible total edge weight.
* One of the solutions for `MST` is the **Prim algorithm**, which is a _greedy algorithm_ and also a _dynamic programming algorithm_.

### Prim algorithm
- Initially, add any point to an empty graph, for example, the point with index 0.
- Next, add the second point. This second point is the **closest** point to the first point.
- An `min_distances` (or call it `dp`) array is needed to store the distances of other points to the first point.
- After the second point is added, add the third point in the same way. The third point is the **closest** point to the first two points. This time, only the distances of other points to the second point need to be calculated, because their distances to the first point have already been calculated and stored in the `min_distances` array.
- Update the `min_distances` array, and the array is a rolling array.
- Finally, all points are added to the graph.

## Approach
Let us use the _common 5 steps_ to solve a _dynamic programming problem_.

### Common five steps in dynamic programming
1. Determine the **meaning** of the `min_distances[i]`
    * `min_distances[i]` represents the **minimum** `cost` (or call it `weight`, `distance`) of adding `points[i]` into current tree.
    * `min_distances[i]` is an integer.
2. Determine the `min_distances` array's initial value
    * Use the example 1 `points = [[0,0],[2,2],[3,10],[5,2],[7,0]]`:
   ```python
   After initialization, the 'min_distances' array would be:  
   #   0 1 2 3 4 # index
   #   0 i i i i # `i` repreents a very large number
   ```
3. Determine the `min_distances` array's recurrence formula
    * Try to complete the grid. In the process, you will get inspiration to derive the formula.
   ```python
   points = [[0,0],[2,2],[3,10],[5,2],[7,0]]
   #   0  1  2  3  4 # index
   #   v  4 13  7  7 # min_distances. current_index will become 1 later becaue 4 is the closet. `v` reprents this point is 'visited', and its value is fixed.  
   #   v  v  9  3  7 # min_distances. current_index will become 3 later becaue 3 is the closet
   #   v  v  9  v  4 # min_distances. current_index will become 4 later becaue 4 is the closet
   #   v  v  9  v  v # min_distances. current_index will become 2 later becaue it is the last one
   #   0  4  9  3  4 # min_distances: 0 + 4 + 9 + 3 + 4 = 20
   ```
    * We can derive the `Recurrence Formula`:
   ```python
   min_distances[i] = min(
       min_distances[i],
       abs(points[i][0] - points[current_index][0]) +
       abs(points[i][1] - points[current_index][1])    
   )
   ```
4. Determine the `min_distances` array's traversal order
    * The traversal order doesn't matter.
5. Check the `min_distances` array's value
    * Print the `min_distances` to see if it is as expected.

### The process of coding
* Initialize `min_distances` and do the first iteration.
```python
min_distances = [float('inf')] * len(points) # This is just the `dp` array
min_distances[0] = 0

for i, _ in enumerate(points):
    if i == 0:
        continue

    min_distances[i] = min(
        min_distances[i],
        abs(points[i][0] - points[0][0]) + \
        abs(points[i][1] - points[0][1])
    )
```

* Use `current_index` to replace the fixed index `0`:
```python
min_distances = [float('inf')] * len(points) # This is just the `dp` array
min_distances[0] = 0
current_index = 0

for i, _ in enumerate(points):
    if i == current_index:
        continue

    min_distances[i] = min(
        min_distances[i],
        abs(points[i][0] - points[current_index][0]) + \
        abs(points[i][1] - points[current_index][1])
    )
```

* Find the `next_index` of the point which is the **closest** to the existing tree.
```python
 class Solution:
    def minCostConnectPoints(self, points: List[List[int]]) -> int:
        min_distances = [float('inf')] * len(points) # This is just the `dp` array
        min_distances[0] = 0
        current_index = 0
        next_index = None
        min_distance = float('inf')

        for i, _ in enumerate(points):
            if i == current_index:
                continue

            min_distances[i] = min(
                min_distances[i],
                abs(points[i][0] - points[current_index][0]) + \
                abs(points[i][1] - points[current_index][1])
            )

            if min_distances[i] < min_distance:
                min_distance = min_distances[i]
                next_index = i

        current_index = next_index
```

* Use a loop to add each point. To do so, we need an array `visited` to record the indices of the points already added. 
```python
visited = [False] * len(points)
visited[current_index] = True

for i, point in enumerate(points):
    if visited[i]:
        continue
    
    # ...
```

* Return `sum(min_distances)`.

## Complexity
* Time: `O(n * n)`.
* Space: `O(n)`.

## Python
```python
class Solution:
    def minCostConnectPoints(self, points: List[List[int]]) -> int:
        min_distances = [float('inf')] * len(points) # This is just the `dp` array
        min_distances[0] = 0

        current_index = 0
        visited = [False] * len(points)

        while current_index is not None:
            visited[current_index] = True
            next_index = None
            min_distance = float('inf')

            for i, point in enumerate(points):
                if visited[i]:
                    continue

                min_distances[i] = min(
                    min_distances[i],
                    abs(point[0] - points[current_index][0]) + \
                    abs(point[1] - points[current_index][1])    
                )

                if min_distances[i] < min_distance:
                    min_distance = min_distances[i]
                    next_index = i
            
            current_index = next_index

        return sum(min_distances)
```

## Java
```java
class Solution {
    public int minCostConnectPoints(int[][] points) {
        var minDistances = new int[points.length]; // This is just the `dp` array
        Arrays.fill(minDistances, Integer.MAX_VALUE);
        minDistances[0] = 0;

        var currentIndex = 0;
        var visited = new boolean[points.length];

        while (currentIndex != -1) {
            visited[currentIndex] = true;
            var nextIndex = -1;
            var minDistance = Integer.MAX_VALUE;

            for (var i = 0; i < points.length; i++) {
                if (visited[i]) {
                    continue;
                }

                minDistances[i] = Math.min(
                    minDistances[i],
                    Math.abs(points[i][0] - points[currentIndex][0]) +
                    Math.abs(points[i][1] - points[currentIndex][1])
                );

                if (minDistances[i] < minDistance) {
                    minDistance = minDistances[i];
                    nextIndex = i;
                }
            }

            currentIndex = nextIndex;
        }

        return IntStream.of(minDistances).sum();
    }
}
```

## C++
```cpp
class Solution {
public:
    int minCostConnectPoints(vector<vector<int>>& points) {
        auto min_distances = vector<int>(points.size(), INT_MAX); // This is just the `dp` array
        min_distances[0] = 0;

        auto current_index = 0;
        auto visited = vector<bool>(points.size());

        while (current_index != -1) {
            visited[current_index] = true;
            auto next_index = -1;
            auto min_distance = INT_MAX;

            for (auto i = 0; i < points.size(); i++) {
                if (visited[i]) {
                    continue;
                }

                min_distances[i] = min(
                    min_distances[i],
                    abs(points[i][0] - points[current_index][0]) +
                    abs(points[i][1] - points[current_index][1])
                );

                if (min_distances[i] < min_distance) {
                    min_distance = min_distances[i];
                    next_index = i;
                }
            }

            current_index = next_index;
        }

        return reduce(min_distances.begin(), min_distances.end());
    }
};
```

## JavaScript
```javascript
var minCostConnectPoints = function (points) {
  const minDistances = Array(points.length).fill(Number.MAX_SAFE_INTEGER) // This is just the `dp` array
  minDistances[0] = 0

  let currentIndex = 0
  const visited = Array(points.length).fill(false)

  while (currentIndex != -1) {
    visited[currentIndex] = true
    let nextIndex = -1
    let minDistance = Number.MAX_SAFE_INTEGER

    for (let i = 0; i < points.length; i++) {
      if (visited[i]) {
        continue
      }

      minDistances[i] = Math.min(
          minDistances[i],
          Math.abs(points[i][0] - points[currentIndex][0]) +
          Math.abs(points[i][1] - points[currentIndex][1])
      )

      if (minDistances[i] < minDistance) {
        minDistance = minDistances[i]
        nextIndex = i
      }
    }

    currentIndex = nextIndex
  }

  return _.sum(minDistances)
};
```

## C#
```c#
public class Solution
{
    public int MinCostConnectPoints(int[][] points)
    {
        var minDistances = new int[points.Length]; // This is just the `dp` array
        Array.Fill(minDistances, Int32.MaxValue);
        minDistances[0] = 0;

        int currentIndex = 0;
        var visited = new bool[points.Length];

        while (currentIndex != -1)
        {
            visited[currentIndex] = true;
            int nextIndex = -1;
            int minDistance = Int32.MaxValue;

            for (int i = 0; i < points.Length; i++)
            {
                if (visited[i])
                {
                    continue;
                }

                minDistances[i] = Math.Min(
                    minDistances[i],
                    Math.Abs(points[i][0] - points[currentIndex][0]) +
                    Math.Abs(points[i][1] - points[currentIndex][1])
                );

                if (minDistances[i] < minDistance)
                {
                    minDistance = minDistances[i];
                    nextIndex = i;
                }
            }

            currentIndex = nextIndex;
        }

        return minDistances.Sum();
    }
}
```

## Go
```go
func minCostConnectPoints(points [][]int) int {
    minDistances := slices.Repeat([]int{math.MaxInt32}, len(points)) // This is just the `dp` array
    minDistances[0] = 0

    currentIndex := 0
    visited := make([]bool, len(points))

    for currentIndex != -1 {
        visited[currentIndex] = true
        nextIndex := -1
        minDistance := math.MaxInt32

        for i, point := range points {
            if visited[i] {
                continue
            }

            minDistances[i] = min(
                minDistances[i],
                int(
                    math.Abs(float64(point[0] - points[currentIndex][0])) +
                    math.Abs(float64(point[1] - points[currentIndex][1])),
                ),
            )

            if minDistances[i] < minDistance {
                minDistance = minDistances[i]
                nextIndex = i
            }
        }

        currentIndex = nextIndex
    }

    distanceSum := 0
    for _, distance := range minDistances {
        distanceSum += distance
    }

    return distanceSum
}
```

## Ruby
```ruby
def min_cost_connect_points(points)
  min_distances = Array.new(points.size, Float::INFINITY) # This is just the `dp` array.
  min_distances[0] = 0

  current_index = 0
  visited = Array.new(points.size, false)

  while !current_index.nil?
    visited[current_index] = true
    next_index = nil
    min_distance = Float::INFINITY

    points.each_with_index do |point, i|
      next if visited[i]

      min_distances[i] = [
        min_distances[i],
        (point[0] - points[current_index][0]).abs +
        (point[1] - points[current_index][1]).abs
      ].min

      if min_distances[i] < min_distance
        min_distance = min_distances[i]
        next_index = i
      end
    end

    current_index = next_index
  end

  min_distances.sum
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
