# LeetCode skills
If you want to solve problems in the most understandable way, please look for Coding5DotCom.

## Array
* Array is consecutive in memory.
* Cannot delete an item. Actually, it is overwrite. Delete a item of array will call the latter items move 1 to left. So it is `O(n)` time complexity.
* C++ 2D array is also consecutive. But Java is not.

## Hash function
You want to store students' information into a hash table. 
You want to query information by a student's name.
* `index = theHashFunction(student_name)` `the_information = the_hash_table[index]`.

## Binary tree unified stack iteration
`boolean mark` solution.

## Other Algorithms
### Recursion
* Recursion steps:
    1. Determine the parameters
    2. Determine the recursion logic
    3. Determine the return value
    4. Determine the exit logic

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

## Solutions which need a perfection
- 583 https://leetcode.cn/problems/delete-operation-for-two-strings/ would be better use https://leetcode.cn/problems/delete-operation-for-two-strings/submissions/597725071/ as the first option.

## Skipped problems/solutions
- 704 Binary Search Algorithm 
- 27 Fast and Slow Pointers

- 1047 https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/
- 150 https://leetcode.cn/problems/evaluate-reverse-polish-notation/
- 239 https://leetcode.cn/problems/sliding-window-maximum/ tag `monotonic queue`
- 347 https://leetcode.cn/problems/top-k-frequent-elements/ tag `heap sort`

### Binary Tree
* Remember to add the recursion steps (described above in this doc) first

- 144 https://leetcode.cn/problems/binary-tree-preorder-traversal/
- 94 https://leetcode.cn/problems/binary-tree-inorder-traversal/
- 145 https://leetcode.cn/problems/binary-tree-postorder-traversal/
- 102 https://leetcode.cn/problems/binary-tree-level-order-traversal/
    - 107 https://leetcode.cn/problems/binary-tree-level-order-traversal-ii/
    - 199 https://leetcode.cn/problems/binary-tree-right-side-view/
    - 637 https://leetcode.cn/problems/average-of-levels-in-binary-tree/
    - 429 https://leetcode.cn/problems/n-ary-tree-level-order-traversal/
    - 515 https://leetcode.cn/problems/find-largest-value-in-each-tree-row/
    - 116 https://leetcode.cn/problems/populating-next-right-pointers-in-each-node/
    - 117 https://leetcode.cn/problems/populating-next-right-pointers-in-each-node-ii/
    - 111 https://leetcode.cn/problems/minimum-depth-of-binary-tree/
    - 513 https://leetcode.cn/problems/find-bottom-left-tree-value
    
- 104 https://leetcode.cn/problems/maximum-depth-of-binary-tree/
- 226 https://leetcode.cn/problems/invert-binary-tree/
- 101 https://leetcode.cn/problems/symmetric-tree/
  - 100 https://leetcode.cn/problems/same-tree/description/
  - 572 https://leetcode.cn/problems/subtree-of-another-tree/

- 222 https://leetcode.cn/problems/count-complete-tree-nodes/
- 110 https://leetcode.cn/problems/balanced-binary-tree/ 2 ways
- 257 https://leetcode.cn/problems/binary-tree-paths/
- 404 https://leetcode.cn/problems/sum-of-left-leaves/
- 112 https://leetcode.cn/problems/path-sum/
- 105 https://leetcode.cn/problems/construct-binary-tree-from-preorder-and-inorder-traversal/
- 106 https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/
- 654 https://leetcode.cn/problems/maximum-binary-tree/
- 617 https://leetcode.cn/problems/merge-two-binary-trees/
- 700 https://leetcode.cn/problems/search-in-a-binary-search-tree/
- 530 https://leetcode.cn/problems/minimum-absolute-difference-in-bst/
    783 https://leetcode.com/problems/minimum-distance-between-bst-nodes/ is the same
- 501 https://leetcode.cn/problems/find-mode-in-binary-search-tree/
- 701 https://leetcode.cn/problems/insert-into-a-binary-search-tree/ Carl's solution is shorter, but may hard to understand and think about
- 450 https://leetcode.cn/problems/delete-node-in-a-bst/ Carl's solution is shorter
- 669 https://leetcode.cn/problems/trim-a-binary-search-tree/description/
- 108 https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree/
- 538 https://leetcode.cn/problems/convert-bst-to-greater-tree/

### Backtracking
- 77 https://leetcode.cn/problems/combinations/
- 216 https://leetcode.cn/problems/combination-sum-iii/
- 39 https://leetcode.cn/problems/combination-sum/
- 17 https://leetcode.cn/problems/letter-combinations-of-a-phone-number/
- 78 https://leetcode.cn/problems/subsets/
- 90 https://leetcode.cn/problems/subsets-ii/
- 40 https://leetcode.cn/problems/combination-sum-ii/
- 131 https://leetcode.cn/problems/palindrome-partitioning/
- 93 https://leetcode.cn/problems/restore-ip-addresses/
- 491 https://leetcode.cn/problems/non-decreasing-subsequences/
- 46 https://leetcode.cn/problems/permutations/
- 332 https://leetcode.cn/problems/reconstruct-itinerary/
- 51 https://leetcode.cn/problems/n-queens/

### Greedy Algorithm
- 455 https://leetcode.cn/problems/assign-cookies/
- 376 https://leetcode.cn/problems/wiggle-subsequence/
- 53 https://leetcode.cn/problems/maximum-subarray/
- 122 https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/
- 55 https://leetcode.cn/problems/jump-game/
- 45 https://leetcode.cn/problems/jump-game-ii/
- 1005 https://leetcode.cn/problems/maximize-sum-of-array-after-k-negations/
- 135 https://leetcode.cn/problems/candy/
- 860 https://leetcode.cn/problems/lemonade-change/
- 406 https://leetcode.cn/problems/queue-reconstruction-by-height/
- 452 https://leetcode.cn/problems/minimum-number-of-arrows-to-burst-balloons
- 435 https://leetcode.cn/problems/non-overlapping-intervals/
- 763 https://leetcode.cn/problems/partition-labels/
- 56  https://leetcode.cn/problems/merge-intervals/
- 738 https://leetcode.cn/problems/monotone-increasing-digits/
- 968 https://leetcode.cn/problems/binary-tree-cameras/

### Dynamic programming
- 70 https://leetcode.cn/problems/climbing-stairs/
- 746 https://leetcode.cn/problems/min-cost-climbing-stairs/
- 62 https://leetcode.cn/problems/unique-paths/
- 63 https://leetcode.cn/problems/unique-paths-ii/
- 343 https://leetcode.cn/problems/integer-break/
- 115 https://leetcode.cn/problems/distinct-subsequences/

#### backpack problems
- 279 https://leetcode.cn/problems/perfect-squares/ can have solution 2

#### palindrome issue key: from middle, 2-d, +1 or +2, dp.size = len(s), do it on left-bottom side.
- 647 https://leetcode.cn/problems/palindromic-substrings/ very hard
- 516 https://leetcode.cn/problems/longest-palindromic-subsequence/

### Failed in 2 rounds
- 222 https://leetcode.cn/problems/count-complete-tree-nodes/
- 236 https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-tree/
- 40 https://leetcode.cn/problems/combination-sum-ii/
- 131 https://leetcode.cn/problems/palindrome-partitioning/
- 332 https://leetcode.cn/problems/reconstruct-itinerary/
- 51 https://leetcode.cn/problems/n-queens/
- 37 https://leetcode.cn/problems/sudoku-solver
- 96 https://leetcode.cn/problems/unique-binary-search-trees/ Finished but slow.
- 115 https://leetcode.cn/problems/distinct-subsequences/
- 647 https://leetcode.cn/problems/palindromic-substrings/ https://leetcode.cn/problems/palindromic-substrings/submissions/597748845/
- 516 https://leetcode.cn/problems/longest-palindromic-subsequence/

2005-02-09 day 2
