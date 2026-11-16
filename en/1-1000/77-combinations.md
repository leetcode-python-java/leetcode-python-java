# 77. Combinations - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at coder.id →**](https://www.coder.id)

Visit original link: [77. Combinations - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/77-combinations) for a better experience!

LeetCode link: [77. Combinations](https://leetcode.com/problems/combinations), difficulty: **Medium**.

## LeetCode description of "77. Combinations"

Given two integers `n` and `k`, return *all possible combinations of* `k` *numbers chosen from the range* `[1, n]`.

You may return the answer in **any order**.

### [Example 1]

**Input**: `n = 4, k = 2`

**Output**: `[[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]`

**Explanation**: 

<div class="highlight"><pre class="highlight plaintext"><code>There are 4 choose 2 = 6 total combinations.
Note that combinations are unordered, i.e., [1,2] and [2,1] are considered to be the same combination.
</code></pre></div>

### [Example 2]

**Input**: `n = 1, k = 1`

**Output**: `[[1]]`

**Explanation**: `There is 1 choose 1 = 1 total combination.`

### [Constraints]

- `1 <= n <= 20`
- `1 <= k <= n`

## Intuition

To enumerate all combinations of `k` numbers chosen from the range `[1, n]`, we can use a classic **Backtracking** (a.k.a. **Depth-First Search**) strategy.

The central idea is simple: we build one combination **one number at a time**, and at every step we choose the next number to append.

The critical observation that makes this problem clean is **ordering**: this is precisely why the recursion carries a `start_index` parameter.

All numbers smaller than `start_index` have already been used (or deliberately skipped) at this point of the path, so they must **never** be reused.

Therefore, at each recursive call we only try candidates from `start_index` up to `n`.

When the current path already holds exactly `k` numbers, it is a **complete and valid** combination, so we store a **copy** of it into the results list.

Then, thanks to backtracking, we **undo** the last chosen number and continue with the next candidate.

This "choose, explore, un-choose" cycle is the heart of the algorithm.

## Step-by-Step Solution

1. **Define the recursive helper.** Create a function `backtracking(start_index)` that, at any moment, operates on the current partial combination stored in `self.result`.
2. **Define the base case.** At the very beginning of the helper, check whether the current path is complete:
   - If `len(self.result) == self.k`, the path holds exactly `k` numbers.
   - Append a **copy** of `self.result` into `self.results` (a copy is mandatory, because `self.result` will keep mutating).
   - Then `return` to stop extending this branch.
3. **Iterate over candidates.** Loop `i` from `start_index` to `self.n` (inclusive). Each `i` is a candidate for the next slot of the combination.
4. **Choose.** Append `i` to `self.result`.
5. **Explore.** Recursively call `backtracking(i + 1)`. Passing `i + 1` guarantees the next chosen number is **larger** than `i`, which enforces the strictly increasing order and removes duplicates.
6. **Un-choose (backtrack).** Pop the last element from `self.result`, restoring the path to the state before step 4, so the loop can try the next candidate.
7. **Kick off the search.** In the main `combine` method, set up the instance variables and call `backtracking(1)` to start from the smallest number `1`.
8. **Return the answer.** Finally, return `self.results`.

```
combine(n, k):
    result = []
    results = []
    backtracking(start_index = 1)

backtracking(start_index):
    if len(result) == k:
        results.append(copy of result)
        return
    for i in range(start_index, n + 1):
        result.append(i)          # choose
        backtracking(i + 1)       # explore
        result.pop()              # un-choose
```

## Complexity

- Time complexity: `O(k * C(n, k))`.
- Space complexity: `O(k)`.

## Python

```python
class Solution:
    def combine(self, n: int, k: int) -> list[list[int]]:
        # Store n and k as instance variables so the nested helper can read them.
        self.results = []   # Final list holding every valid combination.
        self.result = []    # Current path: one partial combination being built.
        self.k = k
        self.n = n

        # Start the search from the smallest candidate number 1.
        self.backtracking(1)

        return self.results

    def backtracking(self, start_index):
        # Base case: the path already has exactly k numbers, so it is complete.
        if len(self.result) == self.k:
            # Append a COPY of the path, because self.result keeps changing.
            self.results.append(self.result.copy())
            return

        # Try every candidate number from start_index up to n (inclusive).
        for i in range(start_index, self.n + 1):
            self.result.append(i)        # Choose i.
            self.backtracking(i + 1)     # Explore: next number must be larger.
            self.result.pop()            # Un-choose: undo the choice (backtrack).
```

## Java

```java
class Solution {
    // Final list holding every valid combination.
    private List<List<Integer>> results = new ArrayList<>();
    // Current path: one partial combination being built.
    private List<Integer> result = new ArrayList<>();
    private int n;
    private int k;

    public List<List<Integer>> combine(int n, int k) {
        this.n = n;
        this.k = k;
        // Reset the state so this method is safe to call again on the same instance.
        results = new ArrayList<>();
        result = new ArrayList<>();
        // Start the search from the smallest candidate number 1.
        backtracking(1);
        return results;
    }

    private void backtracking(int startIndex) {
        // Base case: the path already has exactly k numbers, so it is complete.
        if (result.size() == k) {
            // Store a COPY, because result is mutated afterwards.
            results.add(new ArrayList<>(result));
            return;
        }

        // Try every candidate number from startIndex up to n (inclusive).
        for (int i = startIndex; i <= n; i++) {
            result.add(i);                      // Choose i.
            backtracking(i + 1);                // Explore: next number must be larger.
            result.remove(result.size() - 1);   // Un-choose: undo the choice (backtrack).
        }
    }
}
```

## JavaScript

```javascript
/**
 * @param {number} n
 * @param {number} k
 * @return {number[][]}
 */
var combine = function(n, k) {
    // Final list holding every valid combination.
    const results = [];
    // Current path: one partial combination being built.
    const result = [];

    const backtracking = (startIndex) => {
        // Base case: the path already has exactly k numbers, so it is complete.
        if (result.length === k) {
            // Store a shallow COPY of the path, because result is mutated afterwards.
            results.push([...result]);
            return;
        }

        // Try every candidate number from startIndex up to n (inclusive).
        for (let i = startIndex; i <= n; i++) {
            result.push(i);        // Choose i.
            backtracking(i + 1);   // Explore: next number must be larger.
            result.pop();          // Un-choose: undo the choice (backtrack).
        }
    };

    // Start the search from the smallest candidate number 1.
    backtracking(1);
    return results;
};
```

## C++

```cpp
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        this->n = n;
        this->k = k;
        // Reset the state so this method is safe to call again on the same instance.
        results.clear();
        result.clear();
        // Start the search from the smallest candidate number 1.
        backtracking(1);
        return results;
    }

private:
    // Final list holding every valid combination.
    vector<vector<int>> results;
    // Current path: one partial combination being built.
    vector<int> result;
    int n;
    int k;

    void backtracking(int startIndex) {
        // Base case: the path already has exactly k numbers, so it is complete.
        if ((int)result.size() == k) {
            results.push_back(result);   // push_back copies the vector.
            return;
        }

        // Try every candidate number from startIndex up to n (inclusive).
        for (int i = startIndex; i <= n; i++) {
            result.push_back(i);   // Choose i.
            backtracking(i + 1);   // Explore: next number must be larger.
            result.pop_back();     // Un-choose: undo the choice (backtrack).
        }
    }
};
```

## C#

```csharp
public class Solution {
    // Final list holding every valid combination.
    private IList<IList<int>> results = new List<IList<int>>();
    // Current path: one partial combination being built.
    private List<int> result = new List<int>();
    private int n;
    private int k;

    public IList<IList<int>> Combine(int n, int k) {
        this.n = n;
        this.k = k;
        // Reset the state so this method is safe to call again on the same instance.
        results = new List<IList<int>>();
        result = new List<int>();
        // Start the search from the smallest candidate number 1.
        Backtracking(1);
        return results;
    }

    private void Backtracking(int startIndex) {
        // Base case: the path already has exactly k numbers, so it is complete.
        if (result.Count == k) {
            // Store a COPY, because result is mutated afterwards.
            results.Add(new List<int>(result));
            return;
        }

        // Try every candidate number from startIndex up to n (inclusive).
        for (int i = startIndex; i <= n; i++) {
            result.Add(i);                       // Choose i.
            Backtracking(i + 1);                 // Explore: next number must be larger.
            result.RemoveAt(result.Count - 1);   // Un-choose: undo the choice (backtrack).
        }
    }
}
```

## Go

```go
func combine(n int, k int) [][]int {
    // Final list holding every valid combination.
    results := [][]int{}
    // Current path: one partial combination being built.
    result := []int{}

    // Recursive helper defined as a closure so it can capture result and results.
    var backtracking func(startIndex int)
    backtracking = func(startIndex int) {
        // Base case: the path already has exactly k numbers, so it is complete.
        if len(result) == k {
            // Copy the current path, because the slice is reused afterwards.
            snapshot := make([]int, len(result))
            copy(snapshot, result)
            results = append(results, snapshot)
            return
        }

        // Try every candidate number from startIndex up to n (inclusive).
        for i := startIndex; i <= n; i++ {
            result = append(result, i)        // Choose i.
            backtracking(i + 1)               // Explore: next number must be larger.
            result = result[:len(result)-1]   // Un-choose: undo the choice (backtrack).
        }
    }

    // Start the search from the smallest candidate number 1.
    backtracking(1)
    return results
}
```

## Ruby

```ruby
# @param {Integer} n
# @param {Integer} k
# @return {Integer[][]}
def combine(n, k)
  # Instance variables so the helper method can read and mutate them.
  @results = []   # Final list holding every valid combination.
  @result = []    # Current path: one partial combination being built.
  @k = k
  @n = n

  # Start the search from the smallest candidate number 1.
  backtracking(1)

  @results
end

def backtracking(start_index)
  # Base case: the path already has exactly k numbers, so it is complete.
  if @result.length == @k
    # Store a COPY (dup), because @result is mutated afterwards.
    @results << @result.dup
    return
  end

  # Try every candidate number from start_index up to n (inclusive).
  (start_index..@n).each do |i|
    @result << i          # Choose i.
    backtracking(i + 1)   # Explore: next number must be larger.
    @result.pop           # Un-choose: undo the choice (backtrack).
  end
end
```

## Rust

```rust
impl Solution {
    pub fn combine(n: i32, k: i32) -> Vec<Vec<i32>> {
        // Final list holding every valid combination.
        let mut results: Vec<Vec<i32>> = Vec::new();
        // Current path: one partial combination being built.
        let mut result: Vec<i32> = Vec::new();

        // Recursive helper that builds combinations in strictly increasing order.
        fn backtracking(
            start_index: i32,
            n: i32,
            k: i32,
            result: &mut Vec<i32>,
            results: &mut Vec<Vec<i32>>,
        ) {
            // Base case: the path already has exactly k numbers, so it is complete.
            if result.len() == k as usize {
                // Clone the path to store a snapshot.
                results.push(result.clone());
                return;
            }

            // Try every candidate number from start_index up to n (inclusive).
            for i in start_index..=n {
                result.push(i);                                  // Choose i.
                backtracking(i + 1, n, k, result, results);      // Explore.
                result.pop();                                    // Un-choose (backtrack).
            }
        }

        // Start the search from the smallest candidate number 1.
        backtracking(1, n, k, &mut result, &mut results);
        results
    }
}
```

## Kotlin

```kotlin
class Solution {
    // Final list holding every valid combination.
    private val results = mutableListOf<List<Int>>()
    // Current path: one partial combination being built.
    private val result = mutableListOf<Int>()

    fun combine(n: Int, k: Int): List<List<Int>> {
        // Reset the state so this method is safe to call again on the same instance.
        results.clear()
        result.clear()
        // Start the search from the smallest candidate number 1.
        backtracking(1, n, k)
        return results
    }

    private fun backtracking(startIndex: Int, n: Int, k: Int) {
        // Base case: the path already has exactly k numbers, so it is complete.
        if (result.size == k) {
            // Store a COPY (toList), because result is mutated afterwards.
            results.add(result.toList())
            return
        }

        // Try every candidate number from startIndex up to n (inclusive).
        for (i in startIndex..n) {
            result.add(i)                     // Choose i.
            backtracking(i + 1, n, k)         // Explore: next number must be larger.
            result.removeAt(result.size - 1)  // Un-choose: undo the choice (backtrack).
        }
    }
}
```

## Swift

```swift
class Solution {
    func combine(_ n: Int, _ k: Int) -> [[Int]] {
        // Final list holding every valid combination.
        var results = [[Int]]()
        // Current path: one partial combination being built.
        var result = [Int]()

        // Recursive helper defined as a nested function so it can capture state.
        func backtracking(_ startIndex: Int) {
            // Base case: the path already has exactly k numbers, so it is complete.
            if result.count == k {
                // Arrays are value types, so appending copies the current path.
                results.append(result)
                return
            }

            // Guard: if there are no candidate numbers left, stop.
            // This also prevents building an invalid range such as 5...4, which
            // would crash Swift at runtime.
            if startIndex > n {
                return
            }

            // Try every candidate number from startIndex up to n (inclusive).
            for i in startIndex...n {
                result.append(i)     // Choose i.
                backtracking(i + 1)  // Explore: next number must be larger.
                result.removeLast()  // Un-choose: undo the choice (backtrack).
            }
        }

        // Start the search from the smallest candidate number 1.
        backtracking(1)
        return results
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

Visit original link: [77. Combinations - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/77-combinations) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

