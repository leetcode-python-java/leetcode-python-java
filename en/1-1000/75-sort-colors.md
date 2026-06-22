# 75. Sort Colors - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

Visit original link: [75. Sort Colors - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/75-sort-colors) for a better experience!

LeetCode link: [75. Sort Colors](https://leetcode.com/problems/sort-colors), difficulty: **Medium**.

## LeetCode description of "75. Sort Colors"

Given an array `nums` with `n` objects colored red, white, or blue, sort them **in-place** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

### [Example 1]

**Input**: `nums = [2,0,2,1,1,0]`

**Output**: `[0,0,1,1,2,2]`

### [Example 2]

**Input**: `nums = [2,0,1]`

**Output**: `[0,1,2]`

### [Constraints]

- `n == nums.length`
- `1 <= n <= 300`
- `nums[i]` is either `0`, `1`, or `2`.
- **Follow up:** Could you come up with a one-pass algorithm using only constant extra space?

### [Hints]

<details>
  <summary>Hint 1</summary>
  A rather straight forward solution is a two-pass algorithm using counting sort.

  
</details>

<details>
  <summary>Hint 2</summary>
  Iterate the array counting number of 0's, 1's, and 2's.

  
</details>

<details>
  <summary>Hint 3</summary>
  Overwrite array with the total number of 0's, then 1's and followed by 2's.

  
</details>

## Intuition

The problem asks us to sort an array containing only `0`s, `1`s, and `2`s in-place. The follow-up challenge is to do it in a single pass using constant extra space.
This is exactly the "Dutch National Flag" problem proposed by Edsger W. Dijkstra. We can solve it using three pointers to divide the array into three main regions: a region of `0`s at the beginning, a region of `2`s at the end, and the region of elements currently being processed (which will naturally leave `1`s in the middle).

## Step-by-Step Solution

1. Initialize three pointers: `low = 0` (boundary for 0s), `high = nums.length - 1` (boundary for 2s), and `i = 0` (current element index).
2. Loop while `i <= high`:
   - If `nums[i] == 0`: Swap `nums[i]` and `nums[low]`. We know the swapped element from `low` is either `0` or `1` (since `i` has already passed or is at `low`), so it's safe to increment both `low` and `i`.
   - If `nums[i] == 1`: The element is already in the correct middle region, just increment `i`.
   - If `nums[i] == 2`: Swap `nums[i]` and `nums[high]`. We decrement `high`. However, we **do not** increment `i` here because the new element swapped from `high` into `i` hasn't been checked yet (it could be a `0`, `1`, or `2`).
3. Once `i` surpasses `high`, the array is sorted.

## Complexity

> - **Time Complexity**: `O(N)`, where `N` is the length of the array `nums`. We process each element at most twice (once by `i` and possibly once swapped from `high`), meaning we do a single pass through the array.
- **Space Complexity**: `O(1)`. The sorting is done completely in-place using only three integer variables for pointers, requiring constant extra space.

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Python

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        # low points to the next position for 0
        # high points to the next position for 2
        low, i, high = 0, 0, len(nums) - 1
        
        while i <= high:
            if nums[i] == 0:
                # Swap and advance both low and i
                nums[low], nums[i] = nums[i], nums[low]
                low += 1
                i += 1
            elif nums[i] == 2:
                # Swap and decrement high. Do NOT advance i yet
                # because the swapped element needs to be checked
                nums[high], nums[i] = nums[i], nums[high]
                high -= 1
            else:
                # nums[i] == 1, already in place
                i += 1
```

## Java

```java
class Solution {
    public void sortColors(int[] nums) {
        int low = 0;
        int i = 0;
        int high = nums.length - 1;
        
        while (i <= high) {
            if (nums[i] == 0) {
                swap(nums, low, i);
                low++;
                i++;
            } else if (nums[i] == 2) {
                swap(nums, i, high);
                high--;
                // Don't increment 'i' here, the new nums[i] needs to be evaluated
            } else {
                // nums[i] == 1
                i++;
            }
        }
    }
    
    private void swap(int[] nums, int a, int b) {
        int temp = nums[a];
        nums[a] = nums[b];
        nums[b] = temp;
    }
}
```

## JavaScript

```javascript
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var sortColors = function(nums) {
    let low = 0;
    let i = 0;
    let high = nums.length - 1;
    
    while (i <= high) {
        if (nums[i] === 0) {
            // Swap nums[low] and nums[i]
            [nums[low], nums[i]] = [nums[i], nums[low]];
            low++;
            i++;
        } else if (nums[i] === 2) {
            // Swap nums[i] and nums[high]
            [nums[high], nums[i]] = [nums[i], nums[high]];
            high--;
            // Do not increment i, evaluate the newly swapped element
        } else {
            // If it is 1, just move forward
            i++;
        }
    }
};
```

## Cpp

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int low = 0;
        int i = 0;
        int high = nums.size() - 1;
        
        while (i <= high) {
            if (nums[i] == 0) {
                swap(nums[low], nums[i]);
                low++;
                i++;
            } else if (nums[i] == 2) {
                swap(nums[i], nums[high]);
                high--;
                // Note: i is not incremented
            } else {
                // nums[i] == 1
                i++;
            }
        }
    }
};
```

## Csharp

```csharp
public class Solution {
    public void SortColors(int[] nums) {
        int low = 0;
        int i = 0;
        int high = nums.Length - 1;
        
        while (i <= high) {
            if (nums[i] == 0) {
                // Swap
                int temp = nums[low];
                nums[low] = nums[i];
                nums[i] = temp;
                
                low++;
                i++;
            } else if (nums[i] == 2) {
                // Swap
                int temp = nums[high];
                nums[high] = nums[i];
                nums[i] = temp;
                
                high--;
            } else {
                i++;
            }
        }
    }
}
```

## Go

```go
func sortColors(nums []int) {
    low := 0
    i := 0
    high := len(nums) - 1
    
    for i <= high {
        if nums[i] == 0 {
            nums[low], nums[i] = nums[i], nums[low]
            low++
            i++
        } else if nums[i] == 2 {
            nums[high], nums[i] = nums[i], nums[high]
            high--
        } else {
            // nums[i] == 1
            i++
        }
    }
}
```

## Ruby

```ruby
# @param {Integer[]} nums
# @return {Void} Do not return anything, modify nums in-place instead.
def sort_colors(nums)
    low = 0
    i = 0
    high = nums.length - 1
    
    while i <= high
        if nums[i] == 0
            nums[low], nums[i] = nums[i], nums[low]
            low += 1
            i += 1
        elsif nums[i] == 2
            nums[high], nums[i] = nums[i], nums[high]
            high -= 1
        else
            i += 1
        end
    end
end
```

## Rust

```rust
impl Solution {
    pub fn sort_colors(nums: &mut Vec<i32>) {
        let mut low = 0;
        let mut i = 0;
        let mut high = nums.len() as i32 - 1;
        
        while (i as i32) <= high {
            match nums[i] {
                0 => {
                    nums.swap(low, i);
                    low += 1;
                    i += 1;
                }
                2 => {
                    nums.swap(i, high as usize);
                    high -= 1;
                }
                _ => {
                    // It's 1
                    i += 1;
                }
            }
        }
    }
}
```

## Kotlin

```kotlin
class Solution {
    fun sortColors(nums: IntArray): Unit {
        var low = 0
        var i = 0
        var high = nums.size - 1
        
        while (i <= high) {
            when (nums[i]) {
                0 -> {
                    val temp = nums[low]
                    nums[low] = nums[i]
                    nums[i] = temp
                    low++
                    i++
                }
                2 -> {
                    val temp = nums[high]
                    nums[high] = nums[i]
                    nums[i] = temp
                    high--
                }
                else -> {
                    i++
                }
            }
        }
    }
}
```

## Swift

```swift
class Solution {
    func sortColors(_ nums: inout [Int]) {
        var low = 0
        var i = 0
        var high = nums.count - 1
        
        while i <= high {
            if nums[i] == 0 {
                nums.swapAt(low, i)
                low += 1
                i += 1
            } else if nums[i] == 2 {
                nums.swapAt(i, high)
                high -= 1
            } else {
                i += 1
            }
        }
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

Visit original link: [75. Sort Colors - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://www.leader.me/leetcode/en/solutions/75-sort-colors) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

