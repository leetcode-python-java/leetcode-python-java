# 42. Trapping Rain Water (Monotonic Stack Solution 2)
LeetCode problem link: [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)

## LeetCode problem description
Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

### Example 1
![](../images/examples/0042_1.png)
```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6

Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1].
In this case, 6 units of rain water (blue section) are being trapped.
```

### Example 2
```
Input: height = [4,2,0,3,2,5]
Output: 9
```

### Constraints
- `n == height.length`
- `1 <= n <= 2 * 10000`
- `0 <= height[i] <= 100000`

## Thoughts
This problem can be solved using **Monotonic Stack**.

### Solution 2
This solution will follow **Monotonic Stack**'s common rule: **only calculating when `pop()` is happening**.

This common rule can be applied to calculating result for **most** of the **Monotonic Stack** problems.

![](../images/0042.png)

### Solution 1
Please click [42. Trapping Rain Water (solution 1)](./0042-trapping-rain-water.md) to see it.

### Complexity
* Time: `O(n)`.
* Space: `O(n)`.

## Java
```java
class Solution {
    public int trap(int[] heights) {
        var result = 0;
        var indexStack = new Stack<Integer>();

        for (var i = 0; i < heights.length; i++) {
            while (!indexStack.empty() && heights[indexStack.peek()] <= heights[i]) {
                var poppedIndex = indexStack.pop();

                if (indexStack.empty()) {
                    break;
                }

                var leftHeight = heights[indexStack.peek()];
                var rightHeight = heights[i];
                var heightGap = Math.min(leftHeight, rightHeight) - heights[poppedIndex];
                var width = i - indexStack.peek() - 1;
                result += heightGap * width;
            }

            indexStack.push(i);
        }

        return result;
    }
}
```

## Python
```python
class Solution:
    def trap(self, heights: List[int]) -> int:
        result = 0
        index_stack = []

        for i, height in enumerate(heights):
            while index_stack and heights[index_stack[-1]] <= height:
                popped_index = index_stack.pop()

                if not index_stack:
                    break

                left_height = heights[index_stack[-1]]
                right_height = height
                height_gap = min(left_height, right_height) - heights[popped_index]
                width = i - index_stack[-1] - 1
                result += height_gap * width

            index_stack.append(i)

        return result
```

![](../images/0042.png)

## C++
```cpp
class Solution {
public:
    int trap(vector<int>& heights) {
        auto result = 0;
        stack<int> index_stack;

        for (auto i = 0; i < heights.size(); i++) {
            auto previous_height = 0;

            while (!index_stack.empty() && heights[index_stack.top()] <= heights[i]) {
                auto popped_index = index_stack.top();
                index_stack.pop();

                if (index_stack.empty()) {
                    break;
                }

                auto left_height = heights[index_stack.top()];
                auto right_height = heights[i];
                auto height_gap = min(left_height, right_height) - heights[popped_index];
                auto width = i - index_stack.top() - 1;
                result += height_gap * width;
            }

            index_stack.push(i);
        }

        return result;
    }
};
```

## JavaScript
```javascript
var trap = function (heights) {
  let result = 0
  const indexStack = []

  heights.forEach((height, i) => {
    while (indexStack.length > 0 && heights[indexStack.at(-1)] <= height) {
      const poppedIndex = indexStack.pop()

      if (indexStack.length === 0) {
        break
      }

      const leftHeight = heights[indexStack.at(-1)]
      const rightHeight = heights[i]
      const heightGap = Math.min(leftHeight, rightHeight) - heights[poppedIndex]
      const width = i - indexStack.at(-1) - 1
      result += heightGap * width
    }

    indexStack.push(i)
  })

  return result
};
```

![](../images/0042.png)

## C#
```c#
public class Solution
{
    public int Trap(int[] heights)
    {
        int result = 0;
        var indexStack = new Stack<int>();

        for (var i = 0; i < heights.Length; i++)
        {
            while (indexStack.Count > 0 && heights[indexStack.Peek()] <= heights[i])
            {
                int poppedIndex = indexStack.Pop();

                if (indexStack.Count == 0)
                {
                    break;
                }

                int leftHeight = heights[indexStack.Peek()];
                int rightHeight = heights[i];
                int heightGap = Math.Min(leftHeight, rightHeight) - heights[poppedIndex];
                int width = i - indexStack.Peek() - 1;
                result += heightGap * width;
            }

            indexStack.Push(i);
        }

        return result;
    }
}
```

## Go
```go
func trap(heights []int) int {
    result := 0
    indexStack := []int{}

    for i, height := range heights {
        for len(indexStack) > 0 && heights[indexStack[len(indexStack) - 1]] <= height {
            poppedIndex := indexStack[len(indexStack) - 1]
            indexStack = indexStack[:len(indexStack) - 1]

            if len(indexStack) == 0 {
                break
            }

            leftIndex := indexStack[len(indexStack) - 1]
            leftHeight := heights[leftIndex]
            rightHeight := heights[i]
            heightGap := min(leftHeight, rightHeight) - heights[poppedIndex]
            width := i - leftIndex - 1
            result += heightGap * width
        }

        indexStack = append(indexStack, i)
    }

    return result
}
```

![](../images/0042.png)

## Ruby
```ruby
def trap(heights = [])
  result = 0
  index_stack = []

  heights.each_with_index do |height, i|
    while !index_stack.empty? && heights[index_stack.last] <= height
      popped_index = index_stack.pop

      break if index_stack.empty?

      left_height = heights[index_stack.last]
      right_height = heights[i]
      height_gap = [ left_height, right_height ].min - heights[popped_index]
      width = i - index_stack.last - 1
      result += height_gap * width
    end

    index_stack << i
  end

  result
end
```

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
