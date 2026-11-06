# 3691. Maximum Total Subarray Value II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at coder.id →**](https://www.coder.id)

Visit original link: [3691. Maximum Total Subarray Value II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/3691-maximum-total-subarray-value-ii) for a better experience!

LeetCode link: [3691. Maximum Total Subarray Value II](https://leetcode.com/problems/maximum-total-subarray-value-ii), difficulty: **Difficulty/**.

## LeetCode description of "3691. Maximum Total Subarray Value II"

You are given an integer array `nums` of length `n` and an integer `k`.

You must select **exactly** `k` **distinct** non-empty subarrays `nums[l..r]` of `nums`. Subarrays may overlap, but the exact same subarray (same `l` and `r`) **cannot** be chosen more than once.

The **value** of a subarray `nums[l..r]` is defined as: `max(nums[l..r]) - min(nums[l..r])`.

The **total value** is the sum of the **values** of all chosen subarrays.

Return the **maximum** possible total value you can achieve.

A **subarray** is a contiguous **non-empty** sequence of elements within an array.

### [Example 1]

**Input**: `nums = [1,3,2], k = 2`

**Output**: `4`

**Explanation**: 

<p>One optimal approach is:<br>
- Choose <code>nums[0..1] = [1, 3]</code>. The maximum is 3 and the minimum is 1, giving a value of <code>3 - 1 = 2</code>.<br>
- Choose <code>nums[0..2] = [1, 3, 2]</code>. The maximum is still 3 and the minimum is still 1, so the value is also <code>3 - 1 = 2</code>.<br>
Adding these gives <code>2 + 2 = 4</code>.</p>


### [Example 2]

**Input**: `nums = [4,2,5,1], k = 3`

**Output**: `12`

**Explanation**: 

<p>One optimal approach is:<br>
- Choose <code>nums[0..3] = [4, 2, 5, 1]</code>. The maximum is 5 and the minimum is 1, giving a value of <code>5 - 1 = 4</code>.<br>
- Choose <code>nums[1..3] = [2, 5, 1]</code>. The maximum is 5 and the minimum is 1, so the value is also <code>4</code>.<br>
- Choose <code>nums[2..3] = [5, 1]</code>. The maximum is 5 and the minimum is 1, so the value is again <code>4</code>.<br>
Adding these gives <code>4 + 4 + 4 = 12</code>.</p>


### [Constraints]

- `1 <= n == nums.length <= 5 * 10^4`
- `0 <= nums[i] <= 10^9`
- `1 <= k <= min(10^5, n * (n + 1) / 2)`

### [Hints]

<details>
  <summary>Hint 1</summary>
  For fixed `l`, the sequence `v(l,r)=max(nums[l..r])-min(nums[l..r])` is non-increasing as `r` moves left.

  
</details>

<details>
  <summary>Hint 2</summary>
  Build RMQs (sparse tables) for range max/min so each `v(l,r)` is queryable in `O(1)`.

  
</details>

<details>
  <summary>Hint 3</summary>
  Use a max-heap with `v(l,n-1)` for all `l`; pop the largest `k` times, and after popping an entry from `(l,r)` push `(l,r-1)` if `r>l`.

  
</details>

## Intuition

The problem asks us to find `k` distinct subarrays that maximize the total value, where the value of a subarray is defined as its maximum element minus its minimum element. We can observe that for a fixed starting index `l`, as the ending index `r` moves to the left (i.e., the subarray shrinks), the maximum element can only decrease or stay the same, and the minimum element can only increase or stay the same. Therefore, the value `v(l, r)` is non-increasing as `r` decreases. This monotonic property suggests a Greedy approach using a Priority Queue (Max-Heap), similar to finding the K-th largest sum. We can use a Sparse Table (RMQ) to compute the value of any subarray in O(1) time. We initialize the Max-Heap with the largest possible subarrays starting from each index `l`, which are `(l, n-1)`. Then, we repeatedly pop the subarray with the maximum value. If we pop a subarray `(l, r)`, the next best candidate starting at `l` is `(l, r-1)`, so we push it into the heap. We repeat this process `k` times to accumulate the maximum total value.

## Step-by-Step Solution

1. **Build Sparse Tables:** Construct two sparse tables, one for range maximum queries and one for range minimum queries. This requires `O(N log N)` time and space. Precompute logarithms to answer queries in `O(1)`.
2. **Initialize Priority Queue:** Create a max-heap. For each valid starting index `l` from `0` to `n-1`, query the value of the subarray `(l, n-1)` using the sparse tables, and push a tuple containing `(value, l, r)` into the heap, where `r = n - 1`.
3. **Extract K Subarrays:** Loop exactly `k` times. In each iteration, pop the element with the maximum `value` from the max-heap.
4. **Accumulate Value and Push Next:** Add the popped `value` to our total answer. If the popped element has `r > l`, the next largest subarray starting at `l` is `(l, r-1)`. Query its value and push the new tuple `(new_value, l, r-1)` into the max-heap.
5. **Return Total Value:** After `k` iterations, return the accumulated total value. Use 64-bit integers for the sum as the result can be large.

## Complexity

> - **Time Complexity:** `O(N log N + K log N)`. Building the Sparse Tables takes `O(N log N)` time. The max-heap initially takes `O(N)` to build. We perform `K` extraction and insertion operations on the heap, each taking `O(log N)` time. Since `K <= 10^5` and `N <= 5 * 10^4`, the overall time complexity is highly efficient.
- **Space Complexity:** `O(N log N)`. The two Sparse Tables require `O(N log N)` space to store the minimum and maximum values for intervals of length power of 2. The priority queue stores up to `N` elements at any time, requiring `O(N)` space. Thus, the total space complexity is dominated by the Sparse Tables.

- Time complexity: ``.
- Space complexity: ``.

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

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**coder.id**](https://www.coder.id) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.coder.id`.
>
> [**Build Your Programmer Brand at coder.id →**](https://www.coder.id)

---

Visit original link: [3691. Maximum Total Subarray Value II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/3691-maximum-total-subarray-value-ii) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

