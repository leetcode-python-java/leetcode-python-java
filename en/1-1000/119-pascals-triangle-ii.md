# 119. Pascal's Triangle II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

Visit original link: [119. Pascal's Triangle II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/119-pascals-triangle-ii) for a better experience!

LeetCode link: [119. Pascal's Triangle II](https://leetcode.com/problems/pascals-triangle-ii), difficulty: **Easy**.

## LeetCode description of "119. Pascal's Triangle II"

Given an integer `rowIndex`, return the `rowIndex`<sup>th</sup> (**0-indexed**) row of the **Pascal's triangle**.

In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:

![](https://raw.githubusercontent.com/leetcode-python-java/leetcode-python-java/main/images/problems/119_1.gif)

### [Example 1]

**Input**: `rowIndex = 3`

**Output**: `[1,3,3,1]`

### [Example 2]

**Input**: `rowIndex = 0`

**Output**: `[1]`

### [Example 3]

**Input**: `rowIndex = 1`

**Output**: `[1,1]`

### [Constraints]

* `0 <= rowIndex <= 33`

## Intuition

Each element in a row of Pascal's triangle can be calculated from the previous element in the same row using combinatorics. 

The k-th element of the n-th row is given by the combination formula C(n, k).

We can compute C(n, k) based on C(n, k-1) by multiplying it by `(n - k + 1)` and then dividing by `k`.

This allows us to generate the entire row in a single pass without needing to compute previous rows.

## Step-by-Step Solution

1. Initialize an array `res` of size `rowIndex + 1` filled with 1s. The first and last elements are always 1.
2. Initialize a variable `prev` to 1, representing the previous element C(n, 0).
3. Loop variable `k` from 1 up to `rowIndex - 1`.
4. In each iteration, compute the current element: `curr = prev * (rowIndex - k + 1) / k`. It's crucial to multiply before dividing to avoid fractional loss, and use a 64-bit integer type during calculation to prevent overflow.
5. Store `curr` in `res[k]` and update `prev = curr` for the next iteration.
6. Return the `res` array.

## Complexity

> - **Time Complexity**: `O(rowIndex)`. We only iterate `rowIndex` times to compute each element of the required row.
- **Space Complexity**: `O(1)` auxiliary space. The problem requires returning an array of size `rowIndex + 1`, which is considered `O(rowIndex)` space for the output. However, we only use a few extra variables (`prev`, `curr`), so the auxiliary space complexity is `O(1)`.

- Time complexity: `O(rowIndex)`.
- Space complexity: `O(1)`.

## Python

```python
class Solution:
    def getRow(self, rowIndex: int) -> List[int]:
        # Initialize the result array with 1s.
        # This handles the boundary 1s automatically.
        res = [1] * (rowIndex + 1)
        
        # Calculate intermediate values using the combination formula
        for k in range(1, rowIndex):
            # res[k] = res[k-1] * (rowIndex - k + 1) / k
            # Use integer division // to ensure we keep integers
            res[k] = res[k - 1] * (rowIndex - k + 1) // k
            
        return res
```

## Java

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> res = new ArrayList<>();
        // The first element is always 1
        res.add(1);
        
        // Use long to prevent integer overflow during multiplication
        long prev = 1;
        for (int k = 1; k <= rowIndex; k++) {
            // Calculate next combination value: C(n, k) = C(n, k-1) * (n - k + 1) / k
            long curr = prev * (rowIndex - k + 1) / k;
            res.add((int) curr);
            prev = curr;
        }
        
        return res;
    }
}
```

## JavaScript

```javascript
/**
 * @param {number} rowIndex
 * @return {number[]}
 */
var getRow = function(rowIndex) {
    // Initialize array of size rowIndex + 1 with 1s
    const res = new Array(rowIndex + 1).fill(1);
    let prev = 1;
    
    // Calculate the values between the boundary 1s
    for (let k = 1; k < rowIndex; k++) {
        // Numbers in JS are double precision floats, safe up to 2^53 - 1
        // The max value in Pascal's triangle for rowIndex 33 is ~1.16 * 10^9, so it's perfectly safe
        let curr = (prev * (rowIndex - k + 1)) / k;
        res[k] = curr;
        prev = curr;
    }
    
    return res;
};
```

## Cpp

```cpp
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        // Initialize vector with size rowIndex + 1 and default value 1
        vector<int> res(rowIndex + 1, 1);
        long long prev = 1;
        
        // Iterate through the inner elements
        for (int k = 1; k < rowIndex; ++k) {
            // Use long long to avoid overflow when multiplying large numbers
            long long curr = prev * (rowIndex - k + 1) / k;
            res[k] = curr;
            prev = curr;
        }
        
        return res;
    }
};
```

## Csharp

```csharp
public class Solution {
    public IList<int> GetRow(int rowIndex) {
        int[] res = new int[rowIndex + 1];
        // Set the first element
        res[0] = 1;
        
        long prev = 1;
        for (int k = 1; k <= rowIndex; k++) {
            // Compute the next element using the combination formula
            // We use 'long' to prevent multiplication overflow
            long curr = prev * (rowIndex - k + 1) / k;
            res[k] = (int)curr;
            prev = curr;
        }
        
        return res;
    }
}
```

## Go

```go
func getRow(rowIndex int) []int {
    // Initialize the slice with the required size
    res := make([]int, rowIndex + 1)
    res[0] = 1
    
    prev := int64(1)
    for k := 1; k <= rowIndex; k++ {
        // Calculate current element using int64 to prevent overflow
        curr := prev * int64(rowIndex - k + 1) / int64(k)
        res[k] = int(curr)
        prev = curr
    }
    
    return res
}
```

## Ruby

```ruby
# @param {Integer} row_index
# @return {Integer[]}
def get_row(row_index)
    # Create array initialized with 1s
    res = Array.new(row_index + 1, 1)
    prev = 1
    
    # Calculate the inner values
    (1...row_index).each do |k|
        # Ruby automatically handles arbitrarily large integers, so no overflow concerns
        curr = prev * (row_index - k + 1) / k
        res[k] = curr
        prev = curr
    end
    
    res
end
```

## Rust

```rust
impl Solution {
    pub fn get_row(row_index: i32) -> Vec<i32> {
        // Initialize vector with 1s
        let mut res = vec![1; (row_index + 1) as usize];
        let mut prev: i64 = 1;
        
        for k in 1..row_index {
            // Use i64 for calculation to avoid integer overflow
            let curr = prev * (row_index as i64 - k as i64 + 1) / k as i64;
            res[k as usize] = curr as i32;
            prev = curr;
        }
        
        res
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun getRow(rowIndex: Int): List<Int> {
        // Initialize array with 1s
        val res = IntArray(rowIndex + 1) { 1 }
        var prev: Long = 1L
        
        for (k in 1 until rowIndex) {
            // Use Long to prevent overflow during intermediate multiplication
            val curr = prev * (rowIndex - k + 1) / k
            res[k] = curr.toInt()
            prev = curr
        }
        
        return res.toList()
    }
}
```

## Swift

```swift
class Solution {
    func getRow(_ rowIndex: Int) -> [Int] {
        // Initialize array of given size with 1s
        var res = Array(repeating: 1, count: rowIndex + 1)
        var prev = 1
        
        if rowIndex > 1 {
            for k in 1..<rowIndex {
                // Compute using combination formula
                // Standard Int in Swift is 64-bit on modern Apple platforms, avoiding overflow for rowIndex <= 33
                let curr = prev * (rowIndex - k + 1) / k
                res[k] = curr
                prev = curr
            }
        }
        
        return res
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
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.leader.me`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [119. Pascal's Triangle II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/119-pascals-triangle-ii) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

