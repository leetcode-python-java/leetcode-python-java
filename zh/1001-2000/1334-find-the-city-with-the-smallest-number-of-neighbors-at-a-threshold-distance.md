# 1334. 阈值距离内邻居最少的城市 - 力扣题解最佳实践
力扣链接：[1334. 阈值距离内邻居最少的城市](https://leetcode.cn/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance) ，难度：**中等**。

## 力扣“1334. 阈值距离内邻居最少的城市”问题描述
有 `n` 个城市，按从 `0` 到 `n-1` 编号。给你一个边数组 `edges`，其中 `edges[i] = [fromi, toi, weighti]` 代表 `from_i` 和 `to_i` 两个城市之间的双向加权边，距离阈值是一个整数 `distanceThreshold`。

返回在路径距离限制为 `distanceThreshold` 以内可到达城市最少的城市。如果有多个这样的城市，则返回编号**最大**的城市。

注意，连接城市 _**i**_ 和 _**j**_ 的路径的距离等于沿该路径的所有边的权重之和。

### [示例 1]
![](../../images/examples/1334_1.png)

**输入**: `n = 4, edges = [[0,1,3],[1,2,1],[1,3,4],[2,3,1]], distanceThreshold = 4`

**输出**: `3`

**解释**:
```
城市分布图如上。
每个城市阈值距离 distanceThreshold = 4 内的邻居城市分别是：
城市 0 -> [城市 1, 城市 2] 
城市 1 -> [城市 0, 城市 2, 城市 3] 
城市 2 -> [城市 0, 城市 1, 城市 3] 
城市 3 -> [城市 1, 城市 2] 
城市 0 和 3 在阈值距离 4 以内都有 2 个邻居城市，但是我们必须返回城市 3，因为它的编号最大。
```

### [示例 2]
![](../../images/examples/1334_2.png)

**输入**: `n = 5, edges = [[0,1,2],[0,4,8],[1,2,3],[1,4,2],[2,3,1],[3,4,1]], distanceThreshold = 2`

**输出**: `0`

**解释**:
```
城市分布图如上。 
每个城市阈值距离 distanceThreshold = 2 内的邻居城市分别是：
城市 0 -> [城市 1] 
城市 1 -> [城市 0, 城市 4] 
城市 2 -> [城市 3, 城市 4] 
城市 3 -> [城市 2, 城市 4]
城市 4 -> [城市 1, 城市 2, 城市 3] 
城市 0 在阈值距离 2 以内只有 1 个邻居城市。
```

### [约束]
- `2 <= n <= 100`
- `1 <= edges.length <= n * (n - 1) / 2`
- `edges[i].length == 3`
- `0 <= from_i < to_i < n`
- `1 <= weight_i, distanceThreshold <= 10^4`
- 所有 `(from_i, to_i)` 都是不同的。

### [提示]
<details>
  <summary>提示 1</summary>
  Use Floyd-Warshall's algorithm to compute any-point to any-point distances. (Or can also do Dijkstra from every node due to the weights are non-negative).
</details>

<details>
  <summary>提示 2</summary>
  For each city calculate the number of reachable cities within the threshold, then search for the optimal city.
</details>

## Intuition
就像`提示`据说的，你可以使用 **Floyd-Warshall 算法** 计算任意两点之间的最短距离。

或者，你可以多次调用 **Dijkstra 算法**，每次调用时用不同的城市做为`起始城市`。

或者，你可以多次调用 **集合优化的 Bellman-Ford 算法**，每次调用时用不同的城市做为`起始城市`。

## Complexity
* Time: `O(N^3)`.
* Space: `O(N^2)`.

## Python
```python
class Solution:
    def findTheCity(self, n: int, edges: List[List[int]], distance_threshold: int) -> int:
        dp = []

        for i in range(n):
            dp.append([float('inf')] * n)
            dp[i][i] = 0

        for i, j, weight in edges:
            dp[i][j] = weight
            dp[j][i] = weight

        for k in range(n):
            for i in range(n):
                for j in range(n):
                    dp[i][j] = min(
                        dp[i][j],
                        dp[i][k] + dp[k][j],
                    )

        result = -1
        min_count = float('inf')

        for i, row in enumerate(dp):
            count = len([distance for distance in row if distance <= distance_threshold])

            if count <= min_count:
                min_count = count
                result = i

        return result
```

## JavaScript
```javascript
// Welcome to create a PR to complete the code of this language, thanks!
```

## Java
```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## C++
```cpp
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

## C, Kotlin, Swift, Rust or other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
