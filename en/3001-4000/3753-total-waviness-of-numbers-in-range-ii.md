# 3753. Total Waviness of Numbers in Range II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at coder.id →**](https://www.coder.id)

Visit original link: [3753. Total Waviness of Numbers in Range II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/3753-total-waviness-of-numbers-in-range-ii) for a better experience!

LeetCode link: [3753. Total Waviness of Numbers in Range II](https://leetcode.com/problems/total-waviness-of-numbers-in-range-ii), difficulty: **Hard**.

## LeetCode description of "3753. Total Waviness of Numbers in Range II"

You are given two integers `num1` and `num2` representing an **inclusive** range `[num1, num2]`.

The **waviness** of a number is defined as the total count of its **peaks** and **valleys**:

- A digit is a **peak** if it is **strictly greater** than both of its immediate neighbors.
- A digit is a **valley** if it is **strictly less** than both of its immediate neighbors.
- The first and last digits of a number **cannot** be peaks or valleys.
- Any number with fewer than 3 digits has a waviness of 0.

Return the total sum of waviness for all numbers in the range `[num1, num2]`.

### [Example 1]

**Input**: `num1 = 120, num2 = 130`

**Output**: `3`

**Explanation**: 

<p>In the range <code>[120, 130]</code>:<br>
- <code>120</code>: middle digit 2 is a peak, waviness = 1.<br>
- <code>121</code>: middle digit 2 is a peak, waviness = 1.<br>
- <code>130</code>: middle digit 3 is a peak, waviness = 1.<br>
- All other numbers in the range have a waviness of 0.<br>
Thus, total waviness is <code>1 + 1 + 1 = 3</code>.</p>


### [Example 2]

**Input**: `num1 = 198, num2 = 202`

**Output**: `3`

**Explanation**: 

<p>In the range <code>[198, 202]</code>:<br>
- <code>198</code>: middle digit 9 is a peak, waviness = 1.<br>
- <code>201</code>: middle digit 0 is a valley, waviness = 1.<br>
- <code>202</code>: middle digit 0 is a valley, waviness = 1.<br>
- All other numbers in the range have a waviness of 0.<br>
Thus, total waviness is <code>1 + 1 + 1 = 3</code>.</p>


### [Example 3]

**Input**: `num1 = 4848, num2 = 4848`

**Output**: `2`

**Explanation**: 

<p>Number <code>4848</code>: the second digit 8 is a peak, and the third digit 4 is a valley, giving a waviness of 2.</p>


### [Constraints]

- `1 <= num1 <= num2 <= 10^15`

### [Hints]

<details>
  <summary>Hint 1</summary>
  Use digit dynamic programming

  
</details>

<details>
  <summary>Hint 2</summary>
  Build a digit-DP state `(position, tight, lastDigit, secondLastDigit)`

  
</details>

## Intuition

The problem asks us to find the total sum of waviness for all numbers in a range `[num1, num2]`. Since the range can be up to `10^15`, a brute-force approach iterating through all numbers is too slow.

Instead, we can use Digit Dynamic Programming (Digit DP). The core idea is to count the valid contributions digit by digit. We define a function `calc(x)` that calculates the total waviness for all numbers in the range `[1, x]`. 

The answer will then be `calc(num2) - calc(num1 - 1)`. In the DP state, we need to track the current position (`pos`), whether the prefix is tight to the upper bound (`tight`), whether the number has started (to handle leading zeros, `started`), and the last two digits (`prev2` and `prev1`). 

The DP function will return a pair of values: the count of valid numbers formed from the current state, and the total waviness contributed by those numbers.

## Step-by-Step Solution

1. **Define the `calc(x)` function:** Convert the number `x` to a string or character array to easily iterate through its digits. If `x <= 0`, return `0`.
2. **Define the DP State:** Create a memoization table (or use a dictionary in some languages) to store results for states defined by `(pos, prev2, prev1, started)`. We do not memoize states where `tight == true` because they are unique to the specific upper bound `x`.
3. **DP Transitions:** In the `dfs` function, iterate through all possible digits `d` from `0` up to `limit` (which is the digit at `pos` in `x` if `tight` is true, otherwise `9`).
4. **Update `count` and `waviness`:** For each choice of `d`, recursively call `dfs`. If the number has started and we have at least two previous digits, check if `prev1` forms a peak or valley with `prev2` and `d` (`(prev1 > prev2 && prev1 > d) || (prev1 < prev2 && prev1 < d)`). If it does, each valid suffix formed will add `1` to the waviness, so we add `1 * next_count` to the total waviness.
5. **Return Result:** The result for a state is the sum of `count` and `waviness` over all choices of `d`. The final answer is the waviness part of the result from `dfs(0, true, false, 10, 10)`.

## Complexity

> - **Time Complexity:** `O(D * 10 * 10 * 10)`, where `D` is the number of digits in `num2` (at most 16 since `10^15`). The state consists of `pos` (up to 16), `prev2` (11 possibilities: 0-9 and 10 for none), `prev1` (11 possibilities), and `started` (2 possibilities). For each state, we iterate through at most 10 digits. The total number of states is small (around `16 * 11 * 11 * 2 = 3872`), making the time complexity `O(1)` effectively or `O(log(num2))` strictly.
- **Space Complexity:** `O(D * 10 * 10 * 2)`, to store the memoization table. The recursion stack also takes `O(D)` space. This requires negligible space, making the space complexity `O(1)` effectively or `O(log(num2))` strictly.

- Time complexity: `O(D * 10 * 10 * 10)`.
- Space complexity: `O(D * 10 * 10 * 2)`.

## Python

```python
class Solution:
    def totalWaviness(self, num1: int, num2: int) -> int:
        def calc(x: int) -> int:
            if x <= 0:
                return 0
            
            s = str(x)
            n = len(s)
            
            # memo[pos][prev2][prev1][started]
            # stores a tuple: (count, waviness)
            memo = {}
            
            def dfs(pos: int, tight: bool, started: bool, prev2: int, prev1: int) -> tuple[int, int]:
                # Base case: we've processed all digits
                if pos == n:
                    return (1 if started else 0, 0)
                
                # Use a state tuple for memoization
                state = (pos, prev2, prev1, started)
                if not tight and state in memo:
                    return memo[state]
                    
                limit = int(s[pos]) if tight else 9
                total_cnt = 0
                total_wav = 0
                
                # Iterate through all possible digits at current position
                for d in range(limit + 1):
                    nt = tight and (d == limit)
                    
                    if not started and d == 0:
                        # Skip leading zeros
                        cnt, wav = dfs(pos + 1, nt, False, 10, 10)
                        total_cnt += cnt
                        total_wav += wav
                    elif not started:
                        # First non-zero digit
                        cnt, wav = dfs(pos + 1, nt, True, 10, d)
                        total_cnt += cnt
                        total_wav += wav
                    elif prev2 == 10:
                        # Second digit of the number
                        cnt, wav = dfs(pos + 1, nt, True, prev1, d)
                        total_cnt += cnt
                        total_wav += wav
                    else:
                        # We have at least 3 digits, so we can check for peak or valley
                        is_peak_or_valley = (prev1 > prev2 and prev1 > d) or (prev1 < prev2 and prev1 < d)
                        add = 1 if is_peak_or_valley else 0
                        
                        cnt, wav = dfs(pos + 1, nt, True, prev1, d)
                        total_cnt += cnt
                        # Every valid number suffix formed adds `add` to the waviness
                        total_wav += wav + cnt * add
                        
                ans = (total_cnt, total_wav)
                
                # Memoize the result if we are not constrained by the upper bound
                if not tight:
                    memo[state] = ans
                return ans
                
            return dfs(0, True, False, 10, 10)[1]
            
        return calc(num2) - calc(num1 - 1)
```

## Ruby

```ruby
# @param {Integer} num1
# @param {Integer} num2
# @return {Integer}
def total_waviness(num1, num2)
  calc = ->(x) do
    return 0 if x <= 0
    
    s = x.to_s
    n = s.length
    memo = {}
    
    # Recursive DFS function for Digit DP
    dfs = ->(pos, tight, started, prev2, prev1) do
      # Base case: reached the end of the number
      return [started ? 1 : 0, 0] if pos == n
      
      state = [pos, prev2, prev1, started]
      return memo[state] if !tight && memo.key?(state)
      
      limit = tight ? s[pos].to_i : 9
      total_cnt = 0
      total_wav = 0
      
      (0..limit).each do |d|
        nt = tight && (d == limit)
        
        if !started && d == 0
          # Handling leading zeros
          cnt, wav = dfs.call(pos + 1, nt, false, 10, 10)
          total_cnt += cnt
          total_wav += wav
        elsif !started
          # The first non-zero digit
          cnt, wav = dfs.call(pos + 1, nt, true, 10, d)
          total_cnt += cnt
          total_wav += wav
        elsif prev2 == 10
          # The second digit
          cnt, wav = dfs.call(pos + 1, nt, true, prev1, d)
          total_cnt += cnt
          total_wav += wav
        else
          # Check if the middle digit `prev1` forms a peak or a valley
          is_peak_or_valley = (prev1 > prev2 && prev1 > d) || (prev1 < prev2 && prev1 < d)
          add = is_peak_or_valley ? 1 : 0
          
          cnt, wav = dfs.call(pos + 1, nt, true, prev1, d)
          total_cnt += cnt
          total_wav += wav + cnt * add
        end
      end
      
      ans = [total_cnt, total_wav]
      memo[state] = ans unless tight
      ans
    end
    
    dfs.call(0, true, false, 10, 10)[1]
  end
  
  calc.call(num2) - calc.call(num1 - 1)
end
```

## JavaScript

```javascript
/**
 * @param {number} num1
 * @param {number} num2
 * @return {number}
 */
var totalWaviness = function(num1, num2) {
    // JavaScript uses Double precision float for numbers, which is safe up to 2^53 - 1 (approx 9 * 10^15).
    // The constraints are up to 10^15, so regular JS numbers are fine.
    
    const calc = (x) => {
        if (x <= 0) return 0;
        
        const s = x.toString();
        const n = s.length;
        
        // memo[pos][prev2][prev1][started]
        const memo = new Map();
        
        const dfs = (pos, tight, started, prev2, prev1) => {
            if (pos === n) {
                return [started ? 1 : 0, 0];
            }
            
            const state = `${pos}-${prev2}-${prev1}-${started}`;
            if (!tight && memo.has(state)) {
                return memo.get(state);
            }
            
            const limit = tight ? parseInt(s[pos]) : 9;
            let totalCnt = 0;
            let totalWav = 0;
            
            for (let d = 0; d <= limit; d++) {
                const nt = tight && (d === limit);
                
                if (!started && d === 0) {
                    const [cnt, wav] = dfs(pos + 1, nt, false, 10, 10);
                    totalCnt += cnt;
                    totalWav += wav;
                } else if (!started) {
                    const [cnt, wav] = dfs(pos + 1, nt, true, 10, d);
                    totalCnt += cnt;
                    totalWav += wav;
                } else if (prev2 === 10) {
                    const [cnt, wav] = dfs(pos + 1, nt, true, prev1, d);
                    totalCnt += cnt;
                    totalWav += wav;
                } else {
                    const isPeakOrValley = (prev1 > prev2 && prev1 > d) || (prev1 < prev2 && prev1 < d);
                    const add = isPeakOrValley ? 1 : 0;
                    
                    const [cnt, wav] = dfs(pos + 1, nt, true, prev1, d);
                    totalCnt += cnt;
                    totalWav += wav + cnt * add;
                }
            }
            
            const ans = [totalCnt, totalWav];
            if (!tight) {
                memo.set(state, ans);
            }
            return ans;
        };
        
        return dfs(0, true, false, 10, 10)[1];
    };
    
    return calc(num2) - calc(num1 - 1);
};
```

## Rust

```rust
impl Solution {
    pub fn total_waviness(num1: i64, num2: i64) -> i64 {
        fn calc(x: i64) -> i64 {
            if x <= 0 {
                return 0;
            }
            
            let s: Vec<char> = x.to_string().chars().collect();
            let n = s.len();
            
            let mut memo = vec![vec![vec![vec![None; 2]; 11]; 11]; n];
            
            fn dfs(
                pos: usize, 
                tight: bool, 
                started: bool, 
                prev2: usize, 
                prev1: usize,
                s: &Vec<char>,
                memo: &mut Vec<Vec<Vec<Vec<Option<(i64, i64)>>>>>
            ) -> (i64, i64) {
                if pos == s.len() {
                    return (if started { 1 } else { 0 }, 0);
                }
                
                let started_idx = if started { 1 } else { 0 };
                if !tight && memo[pos][prev2][prev1][started_idx].is_some() {
                    return memo[pos][prev2][prev1][started_idx].unwrap();
                }
                
                let limit = if tight { s[pos] as usize - '0' as usize } else { 9 };
                let mut total_cnt = 0;
                let mut total_wav = 0;
                
                for d in 0..=limit {
                    let nt = tight && (d == limit);
                    
                    if !started && d == 0 {
                        let (cnt, wav) = dfs(pos + 1, nt, false, 10, 10, s, memo);
                        total_cnt += cnt;
                        total_wav += wav;
                    } else if !started {
                        let (cnt, wav) = dfs(pos + 1, nt, true, 10, d, s, memo);
                        total_cnt += cnt;
                        total_wav += wav;
                    } else if prev2 == 10 {
                        let (cnt, wav) = dfs(pos + 1, nt, true, prev1, d, s, memo);
                        total_cnt += cnt;
                        total_wav += wav;
                    } else {
                        let add = if (prev1 > prev2 && prev1 > d) || (prev1 < prev2 && prev1 < d) { 1 } else { 0 };
                        let (cnt, wav) = dfs(pos + 1, nt, true, prev1, d, s, memo);
                        total_cnt += cnt;
                        total_wav += wav + cnt * add;
                    }
                }
                
                let ans = (total_cnt, total_wav);
                if !tight {
                    memo[pos][prev2][prev1][started_idx] = Some(ans);
                }
                ans
            }
            
            dfs(0, true, false, 10, 10, &s, &mut memo).1
        }
        
        calc(num2) - calc(num1 - 1)
    }
}
```

## Kotlin

```kotlin
class Solution {
    private data class Pair(val cnt: Long, val wav: Long)

    fun totalWaviness(num1: Long, num2: Long): Long {
        return calc(num2) - calc(num1 - 1)
    }

    private fun calc(x: Long): Long {
        if (x <= 0) return 0
        
        val s = x.toString().toCharArray()
        val n = s.size
        
        val memo = Array(n) { Array(11) { Array(11) { arrayOfNulls<Pair>(2) } } }
        
        fun dfs(pos: Int, tight: Boolean, started: Boolean, prev2: Int, prev1: Int): Pair {
            if (pos == n) {
                return Pair(if (started) 1L else 0L, 0L)
            }
            
            val startedIdx = if (started) 1 else 0
            if (!tight) {
                val cached = memo[pos][prev2][prev1][startedIdx]
                if (cached != null) return cached
            }
            
            val limit = if (tight) s[pos] - '0' else 9
            var totalCnt = 0L
            var totalWav = 0L
            
            for (d in 0..limit) {
                val nt = tight && (d == s[pos] - '0')
                
                if (!started && d == 0) {
                    val nxt = dfs(pos + 1, nt, false, 10, 10)
                    totalCnt += nxt.cnt
                    totalWav += nxt.wav
                } else if (!started) {
                    val nxt = dfs(pos + 1, nt, true, 10, d)
                    totalCnt += nxt.cnt
                    totalWav += nxt.wav
                } else if (prev2 == 10) {
                    val nxt = dfs(pos + 1, nt, true, prev1, d)
                    totalCnt += nxt.cnt
                    totalWav += nxt.wav
                } else {
                    val add = if ((prev1 > prev2 && prev1 > d) || (prev1 < prev2 && prev1 < d)) 1L else 0L
                    val nxt = dfs(pos + 1, nt, true, prev1, d)
                    totalCnt += nxt.cnt
                    totalWav += nxt.wav + nxt.cnt * add
                }
            }
            
            val ans = Pair(totalCnt, totalWav)
            if (!tight) {
                memo[pos][prev2][prev1][startedIdx] = ans
            }
            return ans
        }
        
        return dfs(0, true, false, 10, 10).wav
    }
}
```

## Swift

```swift
class Solution {
    struct Pair {
        let cnt: Int64
        let wav: Int64
    }

    func totalWaviness(_ num1: Int, _ num2: Int) -> Int {
        func calc(_ x: Int64) -> Int64 {
            if x <= 0 { return 0 }
            
            let s = Array(String(x))
            let n = s.count
            
            // Using a flat array for 4D memoization to avoid nested array overhead
            // Dimensions: [20][11][11][2]
            var memo = [Pair?](repeating: nil, count: 20 * 11 * 11 * 2)
            
            func getIndex(pos: Int, prev2: Int, prev1: Int, startedIdx: Int) -> Int {
                return ((pos * 11 + prev2) * 11 + prev1) * 2 + startedIdx
            }
            
            func dfs(pos: Int, tight: Bool, started: Bool, prev2: Int, prev1: Int) -> Pair {
                if pos == n {
                    return Pair(cnt: started ? 1 : 0, wav: 0)
                }
                
                let startedIdx = started ? 1 : 0
                let memoIdx = getIndex(pos: pos, prev2: prev2, prev1: prev1, startedIdx: startedIdx)
                
                if !tight, let cached = memo[memoIdx] {
                    return cached
                }
                
                let limit = tight ? Int(s[pos].asciiValue! - Character("0").asciiValue!) : 9
                var totalCnt: Int64 = 0
                var totalWav: Int64 = 0
                
                for d in 0...limit {
                    let nt = tight && (d == limit)
                    
                    if !started && d == 0 {
                        let nxt = dfs(pos: pos + 1, tight: nt, started: false, prev2: 10, prev1: 10)
                        totalCnt += nxt.cnt
                        totalWav += nxt.wav
                    } else if !started {
                        let nxt = dfs(pos: pos + 1, tight: nt, started: true, prev2: 10, prev1: d)
                        totalCnt += nxt.cnt
                        totalWav += nxt.wav
                    } else if prev2 == 10 {
                        let nxt = dfs(pos: pos + 1, tight: nt, started: true, prev2: prev1, prev1: d)
                        totalCnt += nxt.cnt
                        totalWav += nxt.wav
                    } else {
                        let isPeakOrValley = (prev1 > prev2 && prev1 > d) || (prev1 < prev2 && prev1 < d)
                        let add: Int64 = isPeakOrValley ? 1 : 0
                        let nxt = dfs(pos: pos + 1, tight: nt, started: true, prev2: prev1, prev1: d)
                        totalCnt += nxt.cnt
                        totalWav += nxt.wav + nxt.cnt * add
                    }
                }
                
                let ans = Pair(cnt: totalCnt, wav: totalWav)
                if !tight {
                    memo[memoIdx] = ans
                }
                return ans
            }
            
            return dfs(pos: 0, tight: true, started: false, prev2: 10, prev1: 10).wav
        }
        
        return Int(calc(Int64(num2)) - calc(Int64(num1 - 1)))
    }
}
```

## Java

```java
class Solution {
    private char[] s;
    private Pair[][][][] memo;

    // Helper class to store multiple return values
    static class Pair {
        long cnt;
        long wav;
        Pair(long cnt, long wav) {
            this.cnt = cnt;
            this.wav = wav;
        }
    }

    public long totalWaviness(long num1, long num2) {
        return calc(num2) - calc(num1 - 1);
    }

    private long calc(long x) {
        if (x <= 0) return 0;
        
        s = Long.toString(x).toCharArray();
        int n = s.length;
        
        // Initialize memoization table with 10 for "no digit" state
        memo = new Pair[n][11][11][2];
        
        return dfs(0, true, false, 10, 10).wav;
    }

    private Pair dfs(int pos, boolean tight, boolean started, int prev2, int prev1) {
        // Base case: processed all digits
        if (pos == s.length) {
            return new Pair(started ? 1 : 0, 0);
        }
        
        // Return cached result if prefix is not tight
        if (!tight) {
            Pair cached = memo[pos][prev2][prev1][started ? 1 : 0];
            if (cached != null) return cached;
        }
        
        int limit = tight ? s[pos] - '0' : 9;
        long totalCnt = 0;
        long totalWav = 0;
        
        // Try placing all possible digits
        for (int d = 0; d <= limit; d++) {
            boolean nt = tight && (d == (s[pos] - '0'));
            
            if (!started && d == 0) {
                // Leading zero
                Pair nxt = dfs(pos + 1, nt, false, 10, 10);
                totalCnt += nxt.cnt;
                totalWav += nxt.wav;
            } else if (!started) {
                // First actual digit
                Pair nxt = dfs(pos + 1, nt, true, 10, d);
                totalCnt += nxt.cnt;
                totalWav += nxt.wav;
            } else if (prev2 == 10) {
                // Second actual digit
                Pair nxt = dfs(pos + 1, nt, true, prev1, d);
                totalCnt += nxt.cnt;
                totalWav += nxt.wav;
            } else {
                // Three or more digits, we can check for peaks and valleys
                int add = ((prev1 > prev2 && prev1 > d) || (prev1 < prev2 && prev1 < d)) ? 1 : 0;
                Pair nxt = dfs(pos + 1, nt, true, prev1, d);
                totalCnt += nxt.cnt;
                totalWav += nxt.wav + nxt.cnt * add;
            }
        }
        
        Pair ans = new Pair(totalCnt, totalWav);
        if (!tight) {
            memo[pos][prev2][prev1][started ? 1 : 0] = ans;
        }
        return ans;
    }
}
```

## Cpp

```cpp
#include <string>
#include <vector>
#include <cstring>

using namespace std;

class Solution {
    struct Pair {
        long long cnt;
        long long wav;
    };

    string s;
    Pair memo[20][11][11][2];
    bool visited[20][11][11][2];

    Pair dfs(int pos, bool tight, bool started, int prev2, int prev1) {
        if (pos == s.length()) {
            return {started ? 1LL : 0LL, 0LL};
        }

        if (!tight && visited[pos][prev2][prev1][started ? 1 : 0]) {
            return memo[pos][prev2][prev1][started ? 1 : 0];
        }

        int limit = tight ? s[pos] - '0' : 9;
        long long totalCnt = 0;
        long long totalWav = 0;

        for (int d = 0; d <= limit; d++) {
            bool nt = tight && (d == (s[pos] - '0'));

            if (!started && d == 0) {
                Pair nxt = dfs(pos + 1, nt, false, 10, 10);
                totalCnt += nxt.cnt;
                totalWav += nxt.wav;
            } else if (!started) {
                Pair nxt = dfs(pos + 1, nt, true, 10, d);
                totalCnt += nxt.cnt;
                totalWav += nxt.wav;
            } else if (prev2 == 10) {
                Pair nxt = dfs(pos + 1, nt, true, prev1, d);
                totalCnt += nxt.cnt;
                totalWav += nxt.wav;
            } else {
                int add = ((prev1 > prev2 && prev1 > d) || (prev1 < prev2 && prev1 < d)) ? 1 : 0;
                Pair nxt = dfs(pos + 1, nt, true, prev1, d);
                totalCnt += nxt.cnt;
                totalWav += nxt.wav + nxt.cnt * add;
            }
        }

        Pair ans = {totalCnt, totalWav};
        if (!tight) {
            visited[pos][prev2][prev1][started ? 1 : 0] = true;
            memo[pos][prev2][prev1][started ? 1 : 0] = ans;
        }
        return ans;
    }

    long long calc(long long x) {
        if (x <= 0) return 0;
        s = to_string(x);
        memset(visited, 0, sizeof(visited));
        return dfs(0, true, false, 10, 10).wav;
    }

public:
    long long totalWaviness(long long num1, long long num2) {
        return calc(num2) - calc(num1 - 1);
    }
};
```

## Csharp

```csharp
using System;

public class Solution {
    private struct Pair {
        public long Cnt;
        public long Wav;
        public Pair(long cnt, long wav) {
            Cnt = cnt;
            Wav = wav;
        }
    }

    private string s;
    private Pair[,,,] memo;
    private bool[,,,] visited;

    public long TotalWaviness(long num1, long num2) {
        return Calc(num2) - Calc(num1 - 1);
    }

    private long Calc(long x) {
        if (x <= 0) return 0;
        s = x.ToString();
        int n = s.Length;
        memo = new Pair[n, 11, 11, 2];
        visited = new bool[n, 11, 11, 2];
        
        return Dfs(0, true, false, 10, 10).Wav;
    }

    private Pair Dfs(int pos, bool tight, bool started, int prev2, int prev1) {
        if (pos == s.Length) {
            return new Pair(started ? 1 : 0, 0);
        }

        int startedIdx = started ? 1 : 0;
        if (!tight && visited[pos, prev2, prev1, startedIdx]) {
            return memo[pos, prev2, prev1, startedIdx];
        }

        int limit = tight ? s[pos] - '0' : 9;
        long totalCnt = 0;
        long totalWav = 0;

        for (int d = 0; d <= limit; d++) {
            bool nt = tight && (d == (s[pos] - '0'));

            if (!started && d == 0) {
                Pair nxt = Dfs(pos + 1, nt, false, 10, 10);
                totalCnt += nxt.Cnt;
                totalWav += nxt.Wav;
            } else if (!started) {
                Pair nxt = Dfs(pos + 1, nt, true, 10, d);
                totalCnt += nxt.Cnt;
                totalWav += nxt.Wav;
            } else if (prev2 == 10) {
                Pair nxt = Dfs(pos + 1, nt, true, prev1, d);
                totalCnt += nxt.Cnt;
                totalWav += nxt.Wav;
            } else {
                int add = ((prev1 > prev2 && prev1 > d) || (prev1 < prev2 && prev1 < d)) ? 1 : 0;
                Pair nxt = Dfs(pos + 1, nt, true, prev1, d);
                totalCnt += nxt.Cnt;
                totalWav += nxt.Wav + nxt.Cnt * add;
            }
        }

        Pair ans = new Pair(totalCnt, totalWav);
        if (!tight) {
            visited[pos, prev2, prev1, startedIdx] = true;
            memo[pos, prev2, prev1, startedIdx] = ans;
        }
        return ans;
    }
}
```

## Go

```go
package main

import (
	"strconv"
)

type Pair struct {
	cnt int64
	wav int64
}

func totalWaviness(num1 int64, num2 int64) int64 {
	calc := func(x int64) int64 {
		if x <= 0 {
			return 0
		}
		
		s := strconv.FormatInt(x, 10)
		n := len(s)
		
		// 16 is enough since 10^15 has 16 digits
		var memo [20][11][11][2]Pair
		var visited [20][11][11][2]bool
		
		var dfs func(pos int, tight bool, started bool, prev2 int, prev1 int) Pair
		dfs = func(pos int, tight bool, started bool, prev2 int, prev1 int) Pair {
			if pos == n {
				var startedInt int64 = 0
				if started {
					startedInt = 1
				}
				return Pair{startedInt, 0}
			}
			
			startedIdx := 0
			if started {
				startedIdx = 1
			}
			
			if !tight && visited[pos][prev2][prev1][startedIdx] {
				return memo[pos][prev2][prev1][startedIdx]
			}
			
			limit := 9
			if tight {
				limit = int(s[pos] - '0')
			}
			
			var totalCnt int64 = 0
			var totalWav int64 = 0
			
			for d := 0; d <= limit; d++ {
				nt := tight && (d == limit)
				
				if !started && d == 0 {
					nxt := dfs(pos+1, nt, false, 10, 10)
					totalCnt += nxt.cnt
					totalWav += nxt.wav
				} else if !started {
					nxt := dfs(pos+1, nt, true, 10, d)
					totalCnt += nxt.cnt
					totalWav += nxt.wav
				} else if prev2 == 10 {
					nxt := dfs(pos+1, nt, true, prev1, d)
					totalCnt += nxt.cnt
					totalWav += nxt.wav
				} else {
					var add int64 = 0
					if (prev1 > prev2 && prev1 > d) || (prev1 < prev2 && prev1 < d) {
						add = 1
					}
					nxt := dfs(pos+1, nt, true, prev1, d)
					totalCnt += nxt.cnt
					totalWav += nxt.wav + nxt.cnt*add
				}
			}
			
			ans := Pair{totalCnt, totalWav}
			if !tight {
				visited[pos][prev2][prev1][startedIdx] = true
				memo[pos][prev2][prev1][startedIdx] = ans
			}
			return ans
		}
		
		return dfs(0, true, false, 10, 10).wav
	}
	
	return calc(num2) - calc(num1-1)
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

Visit original link: [3753. Total Waviness of Numbers in Range II - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.coder.id/leetcode/en/solutions/3753-total-waviness-of-numbers-in-range-ii) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

