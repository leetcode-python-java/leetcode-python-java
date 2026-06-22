# 1732. Find the Highest Altitude - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

Visit original link: [1732. Find the Highest Altitude - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/1732-find-the-highest-altitude) for a better experience!

LeetCode link: [1732. Find the Highest Altitude](https://leetcode.com/problems/find-the-highest-altitude), difficulty: **Easy**.

## LeetCode description of "1732. Find the Highest Altitude"

There is a biker going on a road trip. The road trip consists of `n + 1` points at different altitudes. The biker starts his trip on point `0` with altitude equal `0`.

You are given an integer array `gain` of length `n` where `gain[i]` is the **net gain in altitude** between points `i` and `i + 1` for all (`0 <= i < n)`. Return *the **highest altitude** of a point.*

### [Example 1]

**Input**: `gain = [-5,1,5,0,-7]`

**Output**: `1`

**Explanation**: 

<p>The altitudes are [0,-5,-4,1,1,-6]. The highest is 1.</p>


### [Example 2]

**Input**: `gain = [-4,-3,-2,-1,4,3,2]`

**Output**: `0`

**Explanation**: 

<p>The altitudes are [0,-4,-7,-9,-10,-6,-3,-1]. The highest is 0.</p>


### [Constraints]

- `n == gain.length`
- `1 <= n <= 100`
- `-100 <= gain[i] <= 100`

### [Hints]

<details>
  <summary>Hint 1</summary>
  Let's note that the altitude of an element is the sum of gains of all the elements behind it

  
</details>

<details>
  <summary>Hint 2</summary>
  Getting the altitudes can be done by getting the prefix sum array of the given array

  
</details>

## Intuition

The problem requires finding the highest altitude reached during a road trip. The biker starts at altitude `0`. The `gain` array represents the change in altitude between consecutive points. 

This implies that the altitude at point `i` is the sum of all gains up to point `i-1`. 

We can maintain a running sum (prefix sum) to represent the current altitude and continuously update the maximum altitude encountered so far.

## Step-by-Step Solution

1. Initialize two variables: `current_altitude` to `0` and `max_altitude` to `0`.
2. Iterate through each value `g` in the `gain` array.
3. Add `g` to `current_altitude` to calculate the altitude of the next point.
4. Update `max_altitude` with the maximum of `max_altitude` and `current_altitude`.
5. After the loop finishes, return `max_altitude`.

## Complexity

> - **Time Complexity**: `O(N)`, where `N` is the length of the array `gain`. We only need to traverse the array once.
- **Space Complexity**: `O(1)`. We only use a few integer variables to store the current and maximum altitudes, so the extra space required is constant.

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Python

```python
class Solution:
    def largestAltitude(self, gain: List[int]) -> int:
        current_altitude = 0
        max_altitude = 0
        
        for g in gain:
            current_altitude += g
            if current_altitude > max_altitude:
                max_altitude = current_altitude
                
        return max_altitude
```

## Java

```java
class Solution {
    public int largestAltitude(int[] gain) {
        int currentAltitude = 0;
        int maxAltitude = 0;
        
        for (int g : gain) {
            currentAltitude += g;
            if (currentAltitude > maxAltitude) {
                maxAltitude = currentAltitude;
            }
        }
        
        return maxAltitude;
    }
}
```

## JavaScript

```javascript
/**
 * @param {number[]} gain
 * @return {number}
 */
var largestAltitude = function(gain) {
    let currentAltitude = 0;
    let maxAltitude = 0;
    
    for (const g of gain) {
        currentAltitude += g;
        if (currentAltitude > maxAltitude) {
            maxAltitude = currentAltitude;
        }
    }
    
    return maxAltitude;
};
```

## Cpp

```cpp
class Solution {
public:
    int largestAltitude(vector<int>& gain) {
        int currentAltitude = 0;
        int maxAltitude = 0;
        
        for (int g : gain) {
            currentAltitude += g;
            if (currentAltitude > maxAltitude) {
                maxAltitude = currentAltitude;
            }
        }
        
        return maxAltitude;
    }
};
```

## Csharp

```csharp
public class Solution {
    public int LargestAltitude(int[] gain) {
        int currentAltitude = 0;
        int maxAltitude = 0;
        
        foreach (int g in gain) {
            currentAltitude += g;
            if (currentAltitude > maxAltitude) {
                maxAltitude = currentAltitude;
            }
        }
        
        return maxAltitude;
    }
}
```

## Go

```go
func largestAltitude(gain []int) int {
    currentAltitude := 0
    maxAltitude := 0
    
    for _, g := range gain {
        currentAltitude += g
        if currentAltitude > maxAltitude {
            maxAltitude = currentAltitude
        }
    }
    
    return maxAltitude
}
```

## Ruby

```ruby
# @param {Integer[]} gain
# @return {Integer}
def largest_altitude(gain)
    current_altitude = 0
    max_altitude = 0
    
    gain.each do |g|
        current_altitude += g
        max_altitude = current_altitude if current_altitude > max_altitude
    end
    
    max_altitude
end
```

## Rust

```rust
impl Solution {
    pub fn largest_altitude(gain: Vec<i32>) -> i32 {
        let mut current_altitude = 0;
        let mut max_altitude = 0;
        
        for g in gain {
            current_altitude += g;
            if current_altitude > max_altitude {
                max_altitude = current_altitude;
            }
        }
        
        max_altitude
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun largestAltitude(gain: IntArray): Int {
        var currentAltitude = 0
        var maxAltitude = 0
        
        for (g in gain) {
            currentAltitude += g
            if (currentAltitude > maxAltitude) {
                maxAltitude = currentAltitude
            }
        }
        
        return maxAltitude
    }
}
```

## Swift

```swift
class Solution {
    func largestAltitude(_ gain: [Int]) -> Int {
        var currentAltitude = 0
        var maxAltitude = 0
        
        for g in gain {
            currentAltitude += g
            if currentAltitude > maxAltitude {
                maxAltitude = currentAltitude
            }
        }
        
        return maxAltitude
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

Visit original link: [1732. Find the Highest Altitude - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/1732-find-the-highest-altitude) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

