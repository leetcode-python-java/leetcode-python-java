# 787. K 站中转内最便宜的航班 - 力扣题解最佳实践
力扣链接：[787. K 站中转内最便宜的航班](https://leetcode.cn/problems/cheapest-flights-within-k-stops)，难度: **中等**。

## 力扣“787. K 站中转内最便宜的航班”问题描述
有 `n` 个城市通过一些航班连接。给你一个数组 `flights` ，其中 `flights[i] = [fromi, toi, pricei]` ，表示该航班都从城市 `fromi` 开始，以价格 `pricei` 抵达 `toi`。

现在给定所有的城市和航班，以及出发城市 `src` 和目的地 `dst`，你的任务是找到出一条最多经过 `k` 站中转的路线，使得从 `src` 到 `dst` 的 **价格最便宜** ，并返回该价格。 如果不存在这样的路线，则输出 `-1`。

### [示例 1]
![](../../images/examples/787_1.png)

**输入**: `n = 4, flights = [[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]], src = 0, dst = 3, k = 1`

**输出**: `700`

**解释**:
```
城市航班图如上
从城市 0 到城市 3 经过最多 1 站的最佳路径用红色标记，费用为 100 + 600 = 700。
请注意，通过城市 [0, 1, 2, 3] 的路径更便宜，但无效，因为它经过了 2 站。
```

### [示例 2]
**输入**: `n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 1`

**输出**: `200`

**解释**: 
```
城市航班图如上
从城市 0 到城市 2 经过最多 1 站的最佳路径标记为红色，费用为 100 + 100 = 200。
```

### [示例 3]
**输入**: `n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 0`

**输出**: `500`

**解释**: 
```
城市航班图如上
从城市 0 到城市 2 不经过站点的最佳路径标记为红色，费用为 500。
```

### [约束]
- `1 <= n <= 100`
- `0 <= flights.length <= (n * (n - 1) / 2)`
- `flights[i].length == 3`
- `0 <= from_i, to_i < n`
- `from_i != to_i`
- `1 <= price_i <= 10000`
- 航班没有重复，且不存在自环
- `0 <= src, dst, k < n`
- `src != dst`

## 思路
本题可用 **Bellman-Ford算法** 解决。

**Bellman-Ford算法**的详细说明，请参考 [743. 网络延迟时间](./743-network-delay-time.md)。

## 复杂度
**V**: 顶点数量，**E**: 边的数量。

* 时间: `O(K * E)`.
* 空间: `O(V)`.

## Python
```python
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, k: int) -> int:
        min_costs = [float('inf')] * n
        min_costs[src] = 0

        for _ in range(k + 1):
            min_costs_clone = min_costs.copy()

            for from_city, to_city, price in flights:
                if min_costs_clone[from_city] == float('inf'):
                    continue

                cost = min_costs_clone[from_city] + price

                if cost < min_costs[to_city]:
                    min_costs[to_city] = cost

        if min_costs[dst] == float('inf'):
            return -1

        return min_costs[dst]
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
