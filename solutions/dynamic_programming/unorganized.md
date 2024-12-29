# LeetCode skills
## Array
* Array is consecutive in memory.
* Delete a item of array will call the latter items move 1 to left. So it is `O(n)` time complexity.
* C++ 2D array is also consecutive. But Java is not.

## Binary tree unified stack iteration
`boolean mark` solution.

## Dynamic programming
- [647. Palindromic Substrings](https://leetcode.cn/problems/palindromic-substrings/)
- [516. Longest Palindromic Subsequence](https://leetcode.cn/problems/longest-palindromic-subsequence/)
For solving the above two issues, we can use two-dimensional array. Remember the `magic word`: **回文串，用一半，内环反**.

The principle of `dynamic programming` is **from top to bottom, from left to right, from less to more, from near to far, from known to unknown**
and **take turns being the boss**.

## Monotonic stack
* Push indies one by one.
* Only the useful indies are kept in the stack. Useless indices are popped (or eaten by followed larger (or smaller) index).

## Graph theory
The principle of traversal (DFS or BFS) between `undirected graph` or `directed graph` are similar.
* First rule: don't visited nodes again. This rule make starting from a node to traverse the `undirected graph` have a direction.
* The adjacent nodes of `undirected graph` are its non-visited neighbors.
* The adjacent nodes of `directed graph` are its targeted nodes.

* Truth: An `undirected graph` can be understood as a **bidirectional** `directed graph`. Sometimes, we make use of it.

### Minimum spanning a tree
* `Prim's algorithm` can be used to minimum spanning a tree. It added the closest node to the tree each time. It uses a `min_distances`. It is recommended to use a `priority_queue`.
* `Kruskal's algorithm` can also be used to minimum spanning a tree, but it adds the shortest edge each time. To combine the two nodes of an edge, `UnionFind` is used.

### Shortest path
* This is graph, not a tree. It can have cycles and many connected components.
* `Dijkstra's algorithm` finds the shortest path from one vertex to all other vertices. It is like `Prim's algorithm`, also uses a `min_distances`, but the distance is to the original `source` vertex. All the weights of edges **must not be a negative value**.
* `Bellman_Ford algorithm` finds the shortest path from one vertex to all other vertices. It effectively works in the cases of **negative edges** and is able to **detect negative weight cycles**.
It also uses `min_distances`. Relaxation works by continuously shortening the calculated distance. It's straightforward and easily to be coded.
The improved way with a queue is commonly more efficient. Relaxing **All Edges** by `vertices.length – 1` times gives us _Single Source Shortest Path_ to all vertices.
* `Bellman_Ford algorithm` need to start from **one source** vertex each time and find the shortest paths to the source vertex. `Floyd–Warshall algorithm` can find all vertices' shortest paths.
* What `Floyd–Warshall algorithm` solves can also be done by iterating through `vertices` and apply `Bellman_Ford algorithm` on each vertex; But if it is a `Dense Graph`, `Floyd–Warshall algorithm` is faster.
* If all edges' weights are not negative, what `Floyd–Warshall algorithm` solves can also be done by iterating through `vertices` and apply `Dijkstra algorithm` on each vertex.
* The time complexity of running V times `Dijkstra algorithm` is `E * logE * V`.
* The time complexity of `Floyd–Warshall algorithm` is `V * V * V`. For a dense graph, `Floyd–Warshall algorithm` is still faster.
* `A* algorithm` use a `priority queue`, `pop()` to get the vertex closest to the destination vertex. We need to choose **proper math formula** to determine which one is the closest. We to the very near place of destination vertex, we can use some special method to make it can handle the last part.  

## Others
* Find all the prime numbers within 1000000.

# Features
* Add Google translate as a link. Link example: https://github-com.translate.goog/gazeldx/leetcode-solutions/blob/main/solutions/1-1000/122-best-time-to-buy-and-sell-stock-ii.md?_x_tr_sl=auto&_x_tr_tl=zh-CN&_x_tr_hl=en&_x_tr_pto=wapp