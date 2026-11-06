# 3753. 范围内的数字总波度 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 coder.id 打造你的开发者个人IP →**](https://www.coder.id)

访问原文链接：[3753. 范围内的数字总波度 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/3753-total-waviness-of-numbers-in-range-ii)，体验更佳！

力扣链接：[3753. 范围内的数字总波度 II](https://leetcode.cn/problems/total-waviness-of-numbers-in-range-ii), 难度等级：**Difficulty/**。

## LeetCode “3753. 范围内的数字总波度 II”问题描述

给你两个整数 `num1` 和 `num2`，表示一个 **闭** 区间 `[num1, num2]`。

一个数字的 **波度**（waviness）定义为其 **峰**（peaks）和 **谷**（valleys）的总数：

- 如果一个数字 **严格大于** 其两个相邻数字，则该数字是一个 **峰**。
- 如果一个数字 **严格小于** 其两个相邻数字，则该数字是一个 **谷**。
- 一个数字的第一个和最后一个数字 **不能** 是峰或谷。
- 任何少于 3 位的数字的波度为 0。

返回区间 `[num1, num2]` 内所有数字的波度总和。

### [示例 1]

**输入**: `num1 = 120, num2 = 130`

**输出**: `3`

**解释**: 

<p>在区间 <code>[120, 130]</code> 中：<br>
- <code>120</code>：中间的数字 2 是一个峰，波度 = 1。<br>
- <code>121</code>：中间的数字 2 是一个峰，波度 = 1。<br>
- <code>130</code>：中间的数字 3 是一个峰，波度 = 1。<br>
- 区间内的所有其他数字的波度为 0。<br>
因此，总波度为 <code>1 + 1 + 1 = 3</code>。</p>


### [示例 2]

**输入**: `num1 = 198, num2 = 202`

**输出**: `3`

**解释**: 

<p>在区间 <code>[198, 202]</code> 中：<br>
- <code>198</code>：中间的数字 9 是一个峰，波度 = 1。<br>
- <code>201</code>：中间的数字 0 是一个谷，波度 = 1。<br>
- <code>202</code>：中间的数字 0 是一个谷，波度 = 1。<br>
- 区间内的所有其他数字的波度为 0。<br>
因此，总波度为 <code>1 + 1 + 1 = 3</code>。</p>


### [示例 3]

**输入**: `num1 = 4848, num2 = 4848`

**输出**: `2`

**解释**: 

<p>数字 <code>4848</code>：第二个数字 8 是一个峰，第三个数字 4 是一个谷，得出波度为 2。</p>


### [约束]

- `1 <= num1 <= num2 <= 10^15`

### [Hints]

<details>
  <summary>提示 1</summary>
  Use digit dynamic programming

  
</details>

<details>
  <summary>提示 2</summary>
  Build a digit-DP state `(position, tight, lastDigit, secondLastDigit)`

  
</details>

## 思路

问题要求我们求出范围 `[num1, num2]` 内所有数字的波度总和。由于范围可以大到 `10^15`，遍历所有数字的暴力解法太慢了。相反，我们可以使用数位动态规划（Digit DP）。核心思想是逐位计算符合条件的贡献。我们定义一个函数 `calc(x)`，它计算范围 `[1, x]` 内所有数字的总波度。那么最终答案将是 `calc(num2) - calc(num1 - 1)`。在 DP 状态中，我们需要跟踪当前位置（`pos`）、前缀是否受限于上限（`tight`）、数字是否已经开始（用于处理前导零，`started`），以及最后两个数字（`prev2` 和 `prev1`）。DP 函数将返回一对值：从当前状态形成的有效数字的计数，以及这些数字贡献的总波度。

## 步骤

1. **定义 `calc(x)` 函数：** 将数字 `x` 转换为字符串或字符数组，以便轻松遍历其每一位。如果 `x <= 0`，则返回 `0`。
2. **定义 DP 状态：** 创建一个备忘录表（或在某些语言中使用字典）来存储由 `(pos, prev2, prev1, started)` 定义的状态结果。我们不记忆 `tight == true` 的状态，因为它们对于特定的上限 `x` 是唯一的。
3. **DP 状态转移：** 在 `dfs` 函数中，遍历从 `0` 到 `limit` 的所有可能数字 `d`（如果 `tight` 为真，则 `limit` 是 `x` 在 `pos` 处的数字，否则为 `9`）。
4. **更新 `count` 和 `waviness`：** 对于每一个选择的 `d`，递归调用 `dfs`。如果数字已经开始并且我们至少有两个前面的数字，检查 `prev1` 是否与 `prev2` 和 `d` 形成一个峰或谷（`(prev1 > prev2 && prev1 > d) || (prev1 < prev2 && prev1 < d)`）。如果是，每一个形成的有效后缀都会给波度加 `1`，所以我们将 `1 * next_count` 加到总波度中。
5. **返回结果：** 一个状态的结果是所有选择 `d` 的 `count` 和 `waviness` 的总和。最终答案是 `dfs(0, true, false, 10, 10)` 结果中的波度部分。

## 复杂度

> - **时间复杂度：** `O(D * 10 * 10 * 10)`，其中 `D` 是 `num2` 的位数（最大为 16，因为上限是 `10^15`）。状态由 `pos`（最大 16）、`prev2`（11 种可能：0-9 以及 10 表示无）、`prev1`（11 种可能）和 `started`（2 种可能）组成。对于每个状态，我们最多遍历 10 个数字。状态总数很小（大约 `16 * 11 * 11 * 2 = 3872`），使得时间复杂度实际上是 `O(1)`，严格来说是 `O(log(num2))`。
- **空间复杂度：** `O(D * 10 * 10 * 2)`，用于存储备忘录表。递归栈也需要 `O(D)` 的空间。这只需要微不足道的空间，使得空间复杂度实际上是 `O(1)`，严格来说是 `O(log(num2))`。

- 时间复杂度: ``.
- 空间复杂度: ``.

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

访问原文链接：[3753. 范围内的数字总波度 II - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.coder.id/leetcode/zh/solutions/3753-total-waviness-of-numbers-in-range-ii)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

