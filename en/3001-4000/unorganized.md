```ruby
Problem.all.order(created_at: :desc).map do |problem| puts problem.id.to_s + '. ' + problem.title;  end
```

```
125. Valid Palindrome
14. Longest Common Prefix
58. Length of Last Word
13. Roman to Integer
169. Majority Element
88. Merge Sorted Array
605. Can Place Flowers
5. Longest Palindromic Substring
3494. Find the Minimum Amount of Time to Brew Potions
833. Find And Replace in String
49. Group Anagrams
3478. Choose K Elements With Maximum Sum
144. Binary Tree Preorder Traversal
1334. Find the City With the Smallest Number of Neighbors at a Threshold Distance
787. Cheapest Flights Within K Stops
743. Network Delay Time
433. Minimum Genetic Mutation
752. Open the Lock
1514. Path with Maximum Probability
207. Course Schedule
1584. Min Cost to Connect All Points
685. Redundant Connection II
684. Redundant Connection
1971. Find if Path Exists in Graph
127. Word Ladder
827. Making A Large Island
695. Max Area of Island
463. Island Perimeter
200. Number of Islands
797. All Paths From Source to Target
84. Largest Rectangle in Histogram
42. Trapping Rain Water
496. Next Greater Element I
739. Daily Temperatures
72. Edit Distance
583. Delete Operation for Two Strings
392. Is Subsequence
53. Maximum Subarray
1035. Uncrossed Lines
1143. Longest Common Subsequence
718. Maximum Length of Repeated Subarray
300. Longest Increasing Subsequence
674. Longest Continuous Increasing Subsequence
309. Best Time to Buy and Sell Stock with Cooldown
188. Best Time to Buy and Sell Stock IV
123. Best Time to Buy and Sell Stock III
714. Best Time to Buy and Sell Stock with Transaction Fee
122. Best Time to Buy and Sell Stock II
121. Best Time to Buy and Sell Stock
139. Word Break
279. Perfect Squares
322. Coin Change
377. Combination Sum IV
518. Coin Change II
474. Ones and Zeroes
494. Target Sum
1049. Last Stone Weight II
416. Partition Equal Subset Sum
337. House Robber III
213. House Robber II
198. House Robber
509. Fibonacci Number
225. Implement Stack using Queues
20. Valid Parentheses
232. Implement Queue using Stacks
18. 4Sum
459. Repeated Substring Pattern
541. Reverse String II
28. Find the Index of the First Occurrence in a String
15. 3Sum
454. 4Sum II
202. Happy Number
383. Ransom Note
1. Two Sum
242. Valid Anagram
349. Intersection of Two Arrays
24. Swap Nodes in Pairs
19. Remove Nth Node From End of List
707. Design Linked List
160. Intersection of Two Linked Lists
206. Reverse Linked List
203. Remove Linked List Elements
26. Remove Duplicates from Sorted Array
503. Next Greater Element II
303. Range Sum Query - Immutable
209. Minimum Size Subarray Sum
59. Spiral Matrix II
977. Squares of a Sorted Array
704. Binary Search
27. Remove Element
344. Reverse String
443. String Compression
334. Increasing Triplet Subsequence
238. Product of Array Except Self
151. Reverse Words in a String
345. Reverse Vowels of a String
1431. Kids With the Greatest Number of Candies
1071. Greatest Common Divisor of Strings
1768. Merge Strings Alternately
```

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

|Algorithm name|Focus|Key implementation methods|mark visited|
|Prim's algorithm|Vertices||
|Kruskal's algorithm|Edges|Union-Find|
|Dijkstra's algorithm|Vertices||
|Bellman-Ford algorithm|Edges(Vertices+Edges for SPFA)||
|Dijkstra's by heap sort - min_distance = A*|
UnionFind + Heap sort = Kruskal
BFS + heap sort = A*

Add a table to show the differences between A-Start and breadth-first search

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

### Graph
- 417 https://leetcode.com/problems/pacific-atlantic-water-flow/
- 399 https://leetcode.com/problems/evaluate-division/ union-find
- 1976 https://leetcode.com/problems/number-of-ways-to-arrive-at-destination/ both use Dijkstra or Bellman-Ford can solve it.
- 1263 https://leetcode.com/problems/minimum-moves-to-move-a-box-to-their-target-location/ A-star
- 695. Max Area of Island 2 other ways should be added with code
- 827 making-a-large-island breadth-first-search should be added with code

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
- 417 https://leetcode.com/problems/pacific-atlantic-water-flow/
- 1584-min-cost-to-connect-all-points-2.md
- 1514-path-with-maximum-probability.md
- 1334 https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance
- 752 a star Add A* for 127?
- 3464 https://leetcode.cn/problems/maximize-the-distance-between-points-on-a-square
- https://leetcode.cn/problems/closest-equal-element-queries/
- https://leetcode.cn/problems/rotate-array

## other finished problems
- https://leetcode.com/problems/k-closest-points-to-origin/
- https://leetcode.com/problems/find-special-substring-of-length-k/
- https://leetcode.cn/problems/eat-pizzas/
- https://leetcode.cn/problems/merge-intervals/
- https://leetcode.cn/problems/longest-consecutive-sequence
- https://leetcode.cn/problems/container-with-most-water
- https://leetcode.cn/problems/longest-substring-without-repeating-characters
- https://leetcode.cn/problems/product-of-array-except-self/
- https://leetcode.cn/problems/set-matrix-zeroes/
- https://leetcode.cn/problems/copy-list-with-random-pointer/
- https://leetcode.cn/problems/sort-list/
- https://leetcode.cn/problems/maximum-depth-of-binary-tree/
- https://leetcode.cn/problems/invert-binary-tree/
- https://leetcode.cn/problems/symmetric-tree/
- https://leetcode.cn/problems/binary-tree-level-order-traversal
- https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree
- https://leetcode.cn/problems/validate-binary-search-tree
- https://leetcode.cn/problems/kth-smallest-element-in-a-bst
- https://leetcode.cn/problems/binary-tree-right-side-view/
- https://leetcode.cn/problems/flatten-binary-tree-to-linked-list/
- https://leetcode.cn/problems/positions-of-large-groups/
- https://leetcode.cn/problems/masking-personal-information
- https://leetcode.cn/problems/flipping-an-image/
- https://leetcode.cn/contest/weekly-contest-442/problems/maximum-containers-on-a-ship
- 

## Other algorithm
* 线段树 https://leetcode.cn/problems/fruits-into-baskets-iii




https://leetcode.cn/problems/closest-equal-element-queries
# Timeout1
# class Solution:
#   def solveQueries(self, nums: List[int], queries: List[int]) -> List[int]:
#     n = len(nums)
#   answer = []
#
#   for i in range(len(queries)):
#     index = queries[i]
#     num = nums[index]
#
#     k = 1
#
#     while k < n:
#       if num == nums[(index + k) % n]:
#         answer.append(k)
#       break
#
#       if num == nums[index - k]:
#         answer.append(k)
#       break
#
#       k += 1
#
#       if k == n:
#         answer.append(-1)
#
#       return answer
