# 3691. 最大子数组总值 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 coder.id 打造你的开发者个人IP →**](https://www.coder.id)

访问原文链接：[3691. 最大子数组总值 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/3691-maximum-total-subarray-value-ii)，体验更佳！

力扣链接：[3691. 最大子数组总值 II](https://leetcode.cn/problems/maximum-total-subarray-value-ii), 难度等级：**Difficulty/**。

## LeetCode “3691. 最大子数组总值 II”问题描述

给你一个长度为 `n` 的整数数组 `nums` 和一个整数 `k`。

你必须从 `nums` 中选择 **恰好** `k` 个 **不同** 的非空子数组 `nums[l..r]`。子数组可以重叠，但同一个子数组（相同的 `l` 和 `r`）**不能**被选择超过一次。

子数组 `nums[l..r]` 的 **值** 定义为：`max(nums[l..r]) - min(nums[l..r])`。

**总值** 是所有被选子数组的 **值** 之和。

返回你能实现的 **最大** 可能总值。

**子数组** 是数组中连续的 **非空** 元素序列。

### [示例 1]

**输入**: `nums = [1,3,2], k = 2`

**输出**: `4`

**解释**: 

<p>一种最优的方法是：<br>
- 选择 <code>nums[0..1] = [1, 3]</code>。最大值为 3，最小值为 1，得到的值为 <code>3 - 1 = 2</code>。<br>
- 选择 <code>nums[0..2] = [1, 3, 2]</code>。最大值仍为 3，最小值仍为 1，所以值也是 <code>3 - 1 = 2</code>。<br>
将它们相加得到 <code>2 + 2 = 4</code>。</p>


### [示例 2]

**输入**: `nums = [4,2,5,1], k = 3`

**输出**: `12`

**解释**: 

<p>一种最优的方法是：<br>
- 选择 <code>nums[0..3] = [4, 2, 5, 1]</code>。最大值为 5，最小值为 1，得到的值为 <code>5 - 1 = 4</code>。<br>
- 选择 <code>nums[1..3] = [2, 5, 1]</code>。最大值为 5，最小值为 1，所以值也是 <code>4</code>。<br>
- 选择 <code>nums[2..3] = [5, 1]</code>。最大值为 5，最小值为 1，所以值同样是 <code>4</code>。<br>
将它们相加得到 <code>4 + 4 + 4 = 12</code>。</p>


### [约束]

- `1 <= n == nums.length <= 5 * 10^4`
- `0 <= nums[i] <= 10^9`
- `1 <= k <= min(10^5, n * (n + 1) / 2)`

### [Hints]

<details>
  <summary>提示 1</summary>
  For fixed `l`, the sequence `v(l,r)=max(nums[l..r])-min(nums[l..r])` is non-increasing as `r` moves left.

  
</details>

<details>
  <summary>提示 2</summary>
  Build RMQs (sparse tables) for range max/min so each `v(l,r)` is queryable in `O(1)`.

  
</details>

<details>
  <summary>提示 3</summary>
  Use a max-heap with `v(l,n-1)` for all `l`; pop the largest `k` times, and after popping an entry from `(l,r)` push `(l,r-1)` if `r>l`.

  
</details>

## 思路

问题要求我们找到 `k` 个不同的子数组，使得它们的总值最大，其中子数组的值定义为其最大元素减去最小元素。我们可以观察到一个单调性：对于固定的起始索引 `l`，当结束索引 `r` 向左移动（即子数组缩小）时，最大元素只能减少或保持不变，最小元素只能增加或保持不变。因此，值 `v(l, r)` 随着 `r` 的减小是非递增的。这种单调性提示我们可以使用基于优先队列（最大堆）的贪心算法，类似于寻找第 K 大子数组和的思路。我们可以使用稀疏表（Sparse Table）在 O(1) 时间内查询任何子数组的最大值和最小值。我们首先将以每个索引 `l` 为起点的最长子数组 `(l, n-1)` 放入最大堆中。然后，我们不断弹出具有最大值的子数组。如果弹出的子数组是 `(l, r)`，那么以 `l` 为起点的下一个最佳候选子数组是 `(l, r-1)`，我们将它压入堆中。重复此过程 `k` 次即可累加得到最大的总值。

## 步骤

1. **构建稀疏表（Sparse Table）：** 构建两个稀疏表，一个用于区间最大值查询，另一个用于区间最小值查询。这需要 `O(N log N)` 的时间和空间。预计算对数数组，以便在 `O(1)` 时间内回答查询。
2. **初始化优先队列：** 创建一个最大堆。对于从 `0` 到 `n-1` 的每个有效起始索引 `l`，利用稀疏表查询子数组 `(l, n-1)` 的值，并将包含 `(value, l, r)` 的元组推入堆中，其中 `r = n - 1`。
3. **提取 K 个子数组：** 循环恰好 `k` 次。在每次迭代中，从最大堆中弹出具有最大 `value` 的元素。
4. **累加总值并压入下一个候选：** 将弹出的 `value` 加到我们的总答案中。如果弹出的元素满足 `r > l`，则以 `l` 为起点的下一个最大子数组是 `(l, r-1)`。查询其值并将新元组 `(new_value, l, r-1)` 推入最大堆。
5. **返回总值：** 在 `k` 次迭代后，返回累加的总值。因为结果可能很大，所以总和需要使用 64 位整数（如 long 或 long long）。

## 复杂度

> - **时间复杂度：** `O(N log N + K log N)`。构建稀疏表需要 `O(N log N)` 的时间。初始构建最大堆需要 `O(N)` 的时间。我们在堆上执行 `K` 次弹出和插入操作，每次操作需要 `O(log N)` 的时间。由于 `K <= 10^5` 且 `N <= 5 * 10^4`，整体时间复杂度非常高效。
- **空间复杂度：** `O(N log N)`。两个稀疏表需要 `O(N log N)` 的空间来存储长度为 2 的幂次区间的最小值和最大值。优先队列在任何时候最多存储 `N` 个元素，需要 `O(N)` 的空间。因此，总的空间复杂度由稀疏表决定。

- 时间复杂度: ``.
- 空间复杂度: ``.

## Python

```python
import heapq

class Solution:
    def maxTotalValue(self, nums: List[int], k: int) -> int:
        n = len(nums)
        if n == 0 or k == 0:
            return 0
            
        # Precompute logarithms for O(1) range queries
        log = [0] * (n + 1)
        for i in range(2, n + 1):
            log[i] = log[i // 2] + 1
            
        # K is the maximum power of 2 needed
        K = log[n] + 1
        
        # Initialize Sparse Tables for min and max
        mn = [[0] * K for _ in range(n)]
        mx = [[0] * K for _ in range(n)]
        
        # Base case: intervals of length 1 (2^0)
        for i in range(n):
            mn[i][0] = nums[i]
            mx[i][0] = nums[i]
            
        # Build Sparse Tables for intervals of length 2^j
        j = 1
        while (1 << j) <= n:
            i = 0
            while i + (1 << j) - 1 < n:
                mn[i][j] = min(mn[i][j - 1], mn[i + (1 << (j - 1))][j - 1])
                mx[i][j] = max(mx[i][j - 1], mx[i + (1 << (j - 1))][j - 1])
                i += 1
            j += 1
            
        # Helper function to query the value of subarray nums[L..R] in O(1)
        def query(L: int, R: int) -> int:
            j = log[R - L + 1]
            min_val = min(mn[L][j], mn[R - (1 << j) + 1][j])
            max_val = max(mx[L][j], mx[R - (1 << j) + 1][j])
            return max_val - min_val

        # Initialize the priority queue (max-heap). Python's heapq is a min-heap,
        # so we store negative values to simulate a max-heap.
        pq = []
        for i in range(n):
            val = query(i, n - 1)
            pq.append((-val, i, n - 1))
            
        # Heapify the list in O(N) time
        heapq.heapify(pq)
        
        ans = 0
        # Extract the maximum value k times
        for _ in range(k):
            neg_val, l, r = heapq.heappop(pq)
            ans += -neg_val
            
            # If the subarray can be shrunk from the right, push the new subarray
            if r - 1 >= l:
                val = query(l, r - 1)
                heapq.heappush(pq, (-val, l, r - 1))
                
        return ans
```

## Ruby

```ruby
class MaxHeap
  def initialize
    @data = []
  end

  def push(val, l, r)
    @data << { val: val, l: l, r: r }
    sift_up(@data.length - 1)
  end

  def pop
    return nil if @data.empty?
    top = @data.first
    bottom = @data.pop
    if @data.length > 0
      @data[0] = bottom
      sift_down(0)
    end
    top
  end

  private

  def sift_up(i)
    while i > 0
      p = (i - 1) / 2
      if @data[i][:val] > @data[p][:val]
        @data[i], @data[p] = @data[p], @data[i]
        i = p
      else
        break
      end
    end
  end

  def sift_down(i)
    n = @data.length
    loop do
      max_idx = i
      left = 2 * i + 1
      right = 2 * i + 2
      
      max_idx = left if left < n && @data[left][:val] > @data[max_idx][:val]
      max_idx = right if right < n && @data[right][:val] > @data[max_idx][:val]
      
      if max_idx != i
        @data[i], @data[max_idx] = @data[max_idx], @data[i]
        i = max_idx
      else
        break
      end
    end
  end
end

# @param {Integer[]} nums
# @param {Integer} k
# @return {Integer}
def max_total_value(nums, k)
  n = nums.length
  return 0 if n == 0 || k == 0
  
  log = Array.new(n + 1, 0)
  (2..n).each { |i| log[i] = log[i / 2] + 1 }
  
  k_len = log[n] + 1
  mn = Array.new(n) { Array.new(k_len, 0) }
  mx = Array.new(n) { Array.new(k_len, 0) }
  
  (0...n).each do |i|
    mn[i][0] = nums[i]
    mx[i][0] = nums[i]
  end
  
  (1...k_len).each do |j|
    i = 0
    while i + (1 << j) - 1 < n
      mn[i][j] = [mn[i][j - 1], mn[i + (1 << (j - 1))][j - 1]].min
      mx[i][j] = [mx[i][j - 1], mx[i + (1 << (j - 1))][j - 1]].max
      i += 1
    end
  end
  
  query = ->(l, r) {
    j = log[r - l + 1]
    min_val = [mn[l][j], mn[r - (1 << j) + 1][j]].min
    max_val = [mx[l][j], mx[r - (1 << j) + 1][j]].max
    max_val - min_val
  }
  
  pq = MaxHeap.new
  (0...n).each do |i|
    pq.push(query.call(i, n - 1), i, n - 1)
  end
  
  ans = 0
  k.times do
    top = pq.pop
    break unless top
    
    ans += top[:val]
    
    if top[:r] - 1 >= top[:l]
      pq.push(query.call(top[:l], top[:r] - 1), top[:l], top[:r] - 1)
    end
  end
  
  ans
end
```

## JavaScript

```javascript
class MaxHeap {
    constructor() {
        this.data = [];
    }
    push(val, l, r) {
        this.data.push({val, l, r});
        this.up(this.data.length - 1);
    }
    pop() {
        if (this.data.length === 0) return null;
        const top = this.data[0];
        const bottom = this.data.pop();
        if (this.data.length > 0) {
            this.data[0] = bottom;
            this.down(0);
        }
        return top;
    }
    up(i) {
        while (i > 0) {
            const p = Math.floor((i - 1) / 2);
            if (this.data[i].val > this.data[p].val) {
                const temp = this.data[i];
                this.data[i] = this.data[p];
                this.data[p] = temp;
                i = p;
            } else {
                break;
            }
        }
    }
    down(i) {
        const n = this.data.length;
        while (true) {
            let maxIndex = i;
            const left = 2 * i + 1;
            const right = 2 * i + 2;
            if (left < n && this.data[left].val > this.data[maxIndex].val) {
                maxIndex = left;
            }
            if (right < n && this.data[right].val > this.data[maxIndex].val) {
                maxIndex = right;
            }
            if (maxIndex !== i) {
                const temp = this.data[i];
                this.data[i] = this.data[maxIndex];
                this.data[maxIndex] = temp;
                i = maxIndex;
            } else {
                break;
            }
        }
    }
}

/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var maxTotalValue = function(nums, k) {
    const n = nums.length;
    if (n === 0 || k === 0) return 0;
    
    // Precompute logarithms for O(1) range queries
    const log = new Int32Array(n + 1);
    for (let i = 2; i <= n; i++) {
        log[i] = log[Math.floor(i / 2)] + 1;
    }
    
    const K = log[n] + 1;
    
    // Using typed arrays for Sparse Tables to optimize memory and speed
    // We flatten the 2D array to 1D for typed array compatibility
    const mn = new Int32Array(n * K);
    const mx = new Int32Array(n * K);
    
    // Base case: intervals of length 1 (2^0)
    for (let i = 0; i < n; i++) {
        mn[i * K + 0] = nums[i];
        mx[i * K + 0] = nums[i];
    }
    
    // Build Sparse Tables for intervals of length 2^j
    for (let j = 1; (1 << j) <= n; j++) {
        for (let i = 0; i + (1 << j) - 1 < n; i++) {
            const idx1 = i * K + (j - 1);
            const idx2 = (i + (1 << (j - 1))) * K + (j - 1);
            mn[i * K + j] = Math.min(mn[idx1], mn[idx2]);
            mx[i * K + j] = Math.max(mx[idx1], mx[idx2]);
        }
    }
    
    // Helper function to query the value of subarray nums[L..R] in O(1)
    const query = (L, R) => {
        const j = log[R - L + 1];
        const idx1 = L * K + j;
        const idx2 = (R - (1 << j) + 1) * K + j;
        const minVal = Math.min(mn[idx1], mn[idx2]);
        const maxVal = Math.max(mx[idx1], mx[idx2]);
        return maxVal - minVal;
    };
    
    const heap = new MaxHeap();
    for (let i = 0; i < n; i++) {
        heap.push(query(i, n - 1), i, n - 1);
    }
    
    let ans = 0;
    for (let i = 0; i < k; i++) {
        const top = heap.pop();
        if (!top) break;
        
        ans += top.val;
        const { l, r } = top;
        
        if (r - 1 >= l) {
            heap.push(query(l, r - 1), l, r - 1);
        }
    }
    
    return ans;
};
```

## Java

```java
import java.util.PriorityQueue;

class Solution {
    public long maxTotalValue(int[] nums, int k) {
        int n = nums.length;
        if (n == 0 || k == 0) return 0;
        
        // Precompute logarithms for O(1) range queries
        int[] log = new int[n + 1];
        for (int i = 2; i <= n; i++) {
            log[i] = log[i / 2] + 1;
        }
        
        int K = log[n] + 1;
        int[][] mn = new int[n][K];
        int[][] mx = new int[n][K];
        
        // Base case: intervals of length 1 (2^0)
        for (int i = 0; i < n; i++) {
            mn[i][0] = nums[i];
            mx[i][0] = nums[i];
        }
        
        // Build Sparse Tables for intervals of length 2^j
        for (int j = 1; (1 << j) <= n; j++) {
            for (int i = 0; i + (1 << j) - 1 < n; i++) {
                mn[i][j] = Math.min(mn[i][j - 1], mn[i + (1 << (j - 1))][j - 1]);
                mx[i][j] = Math.max(mx[i][j - 1], mx[i + (1 << (j - 1))][j - 1]);
            }
        }
        
        // Priority Queue stores long arrays: {value, l, r}
        // Ordered by value in descending order to simulate a max-heap
        PriorityQueue<long[]> pq = new PriorityQueue<>((a, b) -> Long.compare(b[0], a[0]));
        
        // Initializing the max-heap with subarrays starting at l and ending at n-1
        for (int i = 0; i < n; i++) {
            long val = query(i, n - 1, mn, mx, log);
            pq.offer(new long[]{val, i, n - 1});
        }
        
        long ans = 0;
        // Extract the maximum value k times
        for (int i = 0; i < k; i++) {
            long[] current = pq.poll();
            if (current == null) break;
            long val = current[0];
            int l = (int) current[1];
            int r = (int) current[2];
            
            ans += val;
            
            // If the subarray can be shrunk from the right, push the new subarray
            if (r - 1 >= l) {
                long newVal = query(l, r - 1, mn, mx, log);
                pq.offer(new long[]{newVal, l, r - 1});
            }
        }
        
        return ans;
    }
    
    // Helper function to query the value of subarray nums[L..R] in O(1)
    private long query(int L, int R, int[][] mn, int[][] mx, int[] log) {
        int j = log[R - L + 1];
        long minVal = Math.min(mn[L][j], mn[R - (1 << j) + 1][j]);
        long maxVal = Math.max(mx[L][j], mx[R - (1 << j) + 1][j]);
        return maxVal - minVal;
    }
}
```

## Cpp

```cpp
#include <vector>
#include <queue>
#include <algorithm>
#include <tuple>

using namespace std;

class Solution {
public:
    long long maxTotalValue(vector<int>& nums, int k) {
        int n = nums.size();
        if (n == 0 || k == 0) return 0;
        
        // Precompute logarithms for O(1) range queries
        vector<int> log(n + 1, 0);
        for (int i = 2; i <= n; i++) {
            log[i] = log[i / 2] + 1;
        }
        
        int K = log[n] + 1;
        vector<vector<int>> mn(n, vector<int>(K));
        vector<vector<int>> mx(n, vector<int>(K));
        
        // Base case: intervals of length 1 (2^0)
        for (int i = 0; i < n; i++) {
            mn[i][0] = nums[i];
            mx[i][0] = nums[i];
        }
        
        // Build Sparse Tables for intervals of length 2^j
        for (int j = 1; (1 << j) <= n; j++) {
            for (int i = 0; i + (1 << j) - 1 < n; i++) {
                mn[i][j] = min(mn[i][j - 1], mn[i + (1 << (j - 1))][j - 1]);
                mx[i][j] = max(mx[i][j - 1], mx[i + (1 << (j - 1))][j - 1]);
            }
        }
        
        // Lambda to query the value of subarray nums[L..R] in O(1)
        auto query = [&](int L, int R) -> long long {
            int j = log[R - L + 1];
            long long minVal = min(mn[L][j], mn[R - (1 << j) + 1][j]);
            long long maxVal = max(mx[L][j], mx[R - (1 << j) + 1][j]);
            return maxVal - minVal;
        };
        
        // Priority Queue stores tuples of (value, l, r)
        // By default, C++ priority_queue is a max-heap, which perfectly fits our needs.
        using Element = tuple<long long, int, int>;
        priority_queue<Element> pq;
        
        for (int i = 0; i < n; i++) {
            pq.push({query(i, n - 1), i, n - 1});
        }
        
        long long ans = 0;
        for (int i = 0; i < k; i++) {
            if (pq.empty()) break;
            auto [val, l, r] = pq.top();
            pq.pop();
            
            ans += val;
            
            // If the subarray can be shrunk from the right, push the new subarray
            if (r - 1 >= l) {
                pq.push({query(l, r - 1), l, r - 1});
            }
        }
        
        return ans;
    }
};
```

## Csharp

```csharp
using System;
using System.Collections.Generic;

public class Solution {
    public long MaxTotalValue(int[] nums, int k) {
        int n = nums.Length;
        if (n == 0 || k == 0) return 0;
        
        // Precompute logarithms for O(1) range queries
        int[] log = new int[n + 1];
        for (int i = 2; i <= n; i++) {
            log[i] = log[i / 2] + 1;
        }
        
        int K = log[n] + 1;
        int[,] mn = new int[n, K];
        int[,] mx = new int[n, K];
        
        // Base case: intervals of length 1 (2^0)
        for (int i = 0; i < n; i++) {
            mn[i, 0] = nums[i];
            mx[i, 0] = nums[i];
        }
        
        // Build Sparse Tables for intervals of length 2^j
        for (int j = 1; (1 << j) <= n; j++) {
            for (int i = 0; i + (1 << j) - 1 < n; i++) {
                mn[i, j] = Math.Min(mn[i, j - 1], mn[i + (1 << (j - 1)), j - 1]);
                mx[i, j] = Math.Max(mx[i, j - 1], mx[i + (1 << (j - 1)), j - 1]);
            }
        }
        
        // PriorityQueue in .NET 6+ takes (element, priority).
        // Max heap can be simulated by providing a custom comparer or using negative priorities.
        // We will use descending comparer for long priority.
        var pq = new PriorityQueue<(int l, int r), long>(Comparer<long>.Create((a, b) => b.CompareTo(a)));
        
        // Helper function to query the value of subarray nums[L..R] in O(1)
        long Query(int L, int R) {
            int j = log[R - L + 1];
            long minVal = Math.Min(mn[L, j], mn[R - (1 << j) + 1, j]);
            long maxVal = Math.Max(mx[L, j], mx[R - (1 << j) + 1, j]);
            return maxVal - minVal;
        }
        
        // Initialize Max-Heap
        for (int i = 0; i < n; i++) {
            long val = Query(i, n - 1);
            pq.Enqueue((i, n - 1), val);
        }
        
        long ans = 0;
        for (int i = 0; i < k; i++) {
            if (pq.Count == 0) break;
            
            // Pop the maximum value
            pq.TryDequeue(out var element, out long val);
            ans += val;
            
            // Push the next candidate
            if (element.r - 1 >= element.l) {
                long newVal = Query(element.l, element.r - 1);
                pq.Enqueue((element.l, element.r - 1), newVal);
            }
        }
        
        return ans;
    }
}
```

## Go

```go
package main

import (
	"container/heap"
)

// Item represents an element in the priority queue
type Item struct {
	val int64
	l   int
	r   int
}

// PriorityQueue implements heap.Interface and holds Items.
type PriorityQueue []Item

func (pq PriorityQueue) Len() int { return len(pq) }

// Max-heap: We want the maximum value at the root
func (pq PriorityQueue) Less(i, j int) bool {
	return pq[i].val > pq[j].val
}

func (pq PriorityQueue) Swap(i, j int) {
	pq[i], pq[j] = pq[j], pq[i]
}

func (pq *PriorityQueue) Push(x interface{}) {
	item := x.(Item)
	*pq = append(*pq, item)
}

func (pq *PriorityQueue) Pop() interface{} {
	old := *pq
	n := len(old)
	item := old[n-1]
	*pq = old[0 : n-1]
	return item
}

func maxTotalValue(nums []int, k int) int64 {
	n := len(nums)
	if n == 0 || k == 0 {
		return 0
	}

	// Precompute logarithms for O(1) range queries
	logArr := make([]int, n+1)
	for i := 2; i <= n; i++ {
		logArr[i] = logArr[i/2] + 1
	}

	K := logArr[n] + 1
	mn := make([][]int, n)
	mx := make([][]int, n)
	for i := 0; i < n; i++ {
		mn[i] = make([]int, K)
		mx[i] = make([]int, K)
		mn[i][0] = nums[i]
		mx[i][0] = nums[i]
	}

	// Build Sparse Tables for intervals of length 2^j
	for j := 1; (1 << j) <= n; j++ {
		for i := 0; i+(1<<j)-1 < n; i++ {
			min1, min2 := mn[i][j-1], mn[i+(1<<(j-1))][j-1]
			if min2 < min1 {
				mn[i][j] = min2
			} else {
				mn[i][j] = min1
			}

			max1, max2 := mx[i][j-1], mx[i+(1<<(j-1))][j-1]
			if max2 > max1 {
				mx[i][j] = max2
			} else {
				mx[i][j] = max1
			}
		}
	}

	// Helper function to query the value of subarray nums[L..R] in O(1)
	query := func(L, R int) int64 {
		j := logArr[R-L+1]
		minVal, min2 := mn[L][j], mn[R-(1<<j)+1][j]
		if min2 < minVal {
			minVal = min2
		}
		maxVal, max2 := mx[L][j], mx[R-(1<<j)+1][j]
		if max2 > maxVal {
			maxVal = max2
		}
		return int64(maxVal - minVal)
	}

	pq := make(PriorityQueue, n)
	for i := 0; i < n; i++ {
		pq[i] = Item{
			val: query(i, n-1),
			l:   i,
			r:   n - 1,
		}
	}
	heap.Init(&pq)

	var ans int64 = 0
	for i := 0; i < k; i++ {
		if pq.Len() == 0 {
			break
		}
		item := heap.Pop(&pq).(Item)
		ans += item.val

		if item.r-1 >= item.l {
			heap.Push(&pq, Item{
				val: query(item.l, item.r-1),
				l:   item.l,
				r:   item.r - 1,
			})
		}
	}

	return ans
}
```

## Rust

```rust
use std::collections::BinaryHeap;
use std::cmp::{min, max};

// A struct to store in BinaryHeap
#[derive(Eq, PartialEq)]
struct State {
    val: i64,
    l: usize,
    r: usize,
}

// Implement Ord and PartialOrd to make BinaryHeap a max-heap based on `val`
impl Ord for State {
    fn cmp(&self, other: &Self) -> std::cmp::Ordering {
        self.val.cmp(&other.val)
    }
}

impl PartialOrd for State {
    fn partial_cmp(&self, other: &Self) -> Option<std::cmp::Ordering> {
        Some(self.cmp(other))
    }
}

impl Solution {
    pub fn max_total_value(nums: Vec<i32>, k: i32) -> i64 {
        let n = nums.len();
        let k = k as usize;
        if n == 0 || k == 0 {
            return 0;
        }

        // Precompute logarithms for O(1) range queries
        let mut log = vec![0; n + 1];
        for i in 2..=n {
            log[i] = log[i / 2] + 1;
        }

        let max_k = log[n] + 1;
        let mut mn = vec![vec![0; max_k]; n];
        let mut mx = vec![vec![0; max_k]; n];

        // Base case: intervals of length 1 (2^0)
        for i in 0..n {
            mn[i][0] = nums[i];
            mx[i][0] = nums[i];
        }

        // Build Sparse Tables for intervals of length 2^j
        for j in 1..max_k {
            let mut i = 0;
            while i + (1 << j) - 1 < n {
                mn[i][j] = min(mn[i][j - 1], mn[i + (1 << (j - 1))][j - 1]);
                mx[i][j] = max(mx[i][j - 1], mx[i + (1 << (j - 1))][j - 1]);
                i += 1;
            }
        }

        // Helper function to query the value of subarray nums[L..R] in O(1)
        let query = |l: usize, r: usize| -> i64 {
            let j = log[r - l + 1];
            let min_val = min(mn[l][j], mn[r - (1 << j) + 1][j]) as i64;
            let max_val = max(mx[l][j], mx[r - (1 << j) + 1][j]) as i64;
            max_val - min_val
        };

        // Initialize the priority queue (max-heap)
        let mut pq = BinaryHeap::new();
        for i in 0..n {
            pq.push(State {
                val: query(i, n - 1),
                l: i,
                r: n - 1,
            });
        }

        let mut ans: i64 = 0;
        for _ in 0..k {
            if let Some(state) = pq.pop() {
                ans += state.val;

                // If the subarray can be shrunk from the right, push the new subarray
                if state.r > state.l {
                    let next_r = state.r - 1;
                    pq.push(State {
                        val: query(state.l, next_r),
                        l: state.l,
                        r: next_r,
                    });
                }
            } else {
                break;
            }
        }

        ans
    }
}
```

## Kotlin

```kotlin
import java.util.PriorityQueue

class Solution {
    fun maxTotalValue(nums: IntArray, k: Int): Long {
        val n = nums.size
        if (n == 0 || k == 0) return 0L

        // Precompute logarithms for O(1) range queries
        val log = IntArray(n + 1)
        for (i in 2..n) {
            log[i] = log[i / 2] + 1
        }

        val K = log[n] + 1
        val mn = Array(n) { IntArray(K) }
        val mx = Array(n) { IntArray(K) }

        // Base case: intervals of length 1 (2^0)
        for (i in 0 until n) {
            mn[i][0] = nums[i]
            mx[i][0] = nums[i]
        }

        // Build Sparse Tables for intervals of length 2^j
        for (j in 1 until K) {
            var i = 0
            while (i + (1 shl j) - 1 < n) {
                mn[i][j] = minOf(mn[i][j - 1], mn[i + (1 shl (j - 1))][j - 1])
                mx[i][j] = maxOf(mx[i][j - 1], mx[i + (1 shl (j - 1))][j - 1])
                i++
            }
        }

        // Helper function to query the value of subarray nums[L..R] in O(1)
        fun query(L: Int, R: Int): Long {
            val j = log[R - L + 1]
            val minVal = minOf(mn[L][j], mn[R - (1 shl j) + 1][j]).toLong()
            val maxVal = maxOf(mx[L][j], mx[R - (1 shl j) + 1][j]).toLong()
            return maxVal - minVal
        }

        // Priority Queue stores long arrays: {value, l, r}
        // Ordered by value in descending order to simulate a max-heap
        val pq = PriorityQueue<LongArray> { a, b -> b[0].compareTo(a[0]) }

        // Initializing the max-heap with subarrays starting at l and ending at n-1
        for (i in 0 until n) {
            val valAt = query(i, n - 1)
            pq.offer(longArrayOf(valAt, i.toLong(), (n - 1).toLong()))
        }

        var ans = 0L
        // Extract the maximum value k times
        for (i in 0 until k) {
            val current = pq.poll() ?: break
            val value = current[0]
            val l = current[1].toInt()
            val r = current[2].toInt()

            ans += value

            // If the subarray can be shrunk from the right, push the new subarray
            if (r - 1 >= l) {
                val newVal = query(l, r - 1)
                pq.offer(longArrayOf(newVal, l.toLong(), (r - 1).toLong()))
            }
        }

        return ans
    }
}
```

## Swift

```swift
class Solution {
    struct State: Comparable {
        let val: Int
        let l: Int
        let r: Int
        
        static func < (lhs: State, rhs: State) -> Bool {
            return lhs.val < rhs.val
        }
    }
    
    // A simple MaxHeap implementation for Swift
    struct MaxHeap<T: Comparable> {
        private var elements: [T] = []
        
        var isEmpty: Bool { elements.isEmpty }
        
        mutating func insert(_ value: T) {
            elements.append(value)
            siftUp(from: elements.count - 1)
        }
        
        mutating func extractMax() -> T? {
            guard !elements.isEmpty else { return nil }
            if elements.count == 1 {
                return elements.removeLast()
            }
            let value = elements[0]
            elements[0] = elements.removeLast()
            siftDown(from: 0)
            return value
        }
        
        private mutating func siftUp(from index: Int) {
            var child = index
            var parent = (child - 1) / 2
            while child > 0 && elements[child] > elements[parent] {
                elements.swapAt(child, parent)
                child = parent
                parent = (child - 1) / 2
            }
        }
        
        private mutating func siftDown(from index: Int) {
            var parent = index
            while true {
                let left = 2 * parent + 1
                let right = 2 * parent + 2
                var candidate = parent
                
                if left < elements.count && elements[left] > elements[candidate] {
                    candidate = left
                }
                if right < elements.count && elements[right] > elements[candidate] {
                    candidate = right
                }
                
                if candidate == parent {
                    return
                }
                
                elements.swapAt(parent, candidate)
                parent = candidate
            }
        }
    }
    
    func maxTotalValue(_ nums: [Int], _ k: Int) -> Int {
        let n = nums.count
        if n == 0 || k == 0 { return 0 }
        
        // Precompute logarithms for O(1) range queries
        var log = [Int](repeating: 0, count: n + 1)
        if n >= 2 {
            for i in 2...n {
                log[i] = log[i / 2] + 1
            }
        }
        
        let K = log[n] + 1
        var mn = [[Int]](repeating: [Int](repeating: 0, count: K), count: n)
        var mx = [[Int]](repeating: [Int](repeating: 0, count: K), count: n)
        
        // Base case: intervals of length 1 (2^0)
        for i in 0..<n {
            mn[i][0] = nums[i]
            mx[i][0] = nums[i]
        }
        
        // Build Sparse Tables for intervals of length 2^j
        if K > 1 {
            for j in 1..<K {
                var i = 0
                while i + (1 << j) - 1 < n {
                    mn[i][j] = min(mn[i][j - 1], mn[i + (1 << (j - 1))][j - 1])
                    mx[i][j] = max(mx[i][j - 1], mx[i + (1 << (j - 1))][j - 1])
                    i += 1
                }
            }
        }
        
        // Helper function to query the value of subarray nums[L..R] in O(1)
        func query(L: Int, R: Int) -> Int {
            let j = log[R - L + 1]
            let minVal = min(mn[L][j], mn[R - (1 << j) + 1][j])
            let maxVal = max(mx[L][j], mx[R - (1 << j) + 1][j])
            return maxVal - minVal
        }
        
        var pq = MaxHeap<State>()
        for i in 0..<n {
            pq.insert(State(val: query(L: i, R: n - 1), l: i, r: n - 1))
        }
        
        var ans = 0
        for _ in 0..<k {
            guard let state = pq.extractMax() else { break }
            ans += state.val
            
            if state.r - 1 >= state.l {
                pq.insert(State(val: query(L: state.l, R: state.r - 1), l: state.l, r: state.r - 1))
            }
        }
        
        return ans
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**coder.id**](https://www.coder.id) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.coder.id`，极具职业含金量的专属域名。

>
> [**立即前往 coder.id 打造你的个人品牌 →**](https://www.coder.id)

---

访问原文链接：[3691. 最大子数组总值 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/3691-maximum-total-subarray-value-ii)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

