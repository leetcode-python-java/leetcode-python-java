# 42. Trapping Rain Water
LeetCode problem: [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)

## LeetCode problem description
Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

```
-----------------------------------------------------------------------------------------------------------
[Example 1]

Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6

Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1].
In this case, 6 units of rain water (blue section) are being trapped.
-----------------------------------------------------------------------------------------------------------
[Example 2]

Input: height = [4,2,0,3,2,5]
Output: 9
-----------------------------------------------------------------------------------------------------------
[Constraints]

n == height.length
1 <= n <= 2 * 10000
0 <= height[i] <= 100000
-----------------------------------------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Monotonic Stack**.

### Solution 1
#### Rules
* Whenever there are area (rain) can be added, add it immediately.
* The shorter side's height will be used to calculate the area.
* There would be two situations:
    1. The left side (the top of stack) is taller than the right side (current item).
    2. The left side (the top of stack) is not taller than the right side (current item).

![](../images/0042.png)

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Solution 2
The `solution 2` will follow **Monotonic Stack**'s common rule: **only calculating when `pop()` is happening**.

Please click [42. Trapping Rain Water (solution 2)](./0042-trapping-rain-water-2.md) to see it.

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
            var previousHeight = 0;

            while (!indexStack.empty() && heights[indexStack.peek()] < heights[i]) { // situation 2
                var index = indexStack.pop();
                var heightGap = heights[index] - previousHeight;
                var width = i - index - 1;
                result += heightGap * width;
                previousHeight = heights[index];
            }

            if (!indexStack.empty()) { // situation 1
                var heightGap = heights[i] - previousHeight;
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
            previous_height = 0

            while index_stack and heights[index_stack[-1]] <= height: # situation 2
                index = index_stack.pop()
                height_gap = heights[index] - previous_height
                width = i - index - 1
                result += height_gap * width
                previous_height = heights[index]

            if index_stack: # situation 1
                height_gap = height - previous_height
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

            while (!index_stack.empty() && heights[index_stack.top()] < heights[i]) { // situation 2
                auto index = index_stack.top();
                auto height_gap = heights[index] - previous_height;
                auto width = i - index - 1;
                result += height_gap * width;
                previous_height = heights[index];
                index_stack.pop();
            }

            if (!index_stack.empty()) { // situation 1
                auto height_gap = heights[i] - previous_height;
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
    let previousHeight = 0

    while (indexStack.length > 0 && heights[indexStack.at(-1)] < height) { // situation 2
      const index = indexStack.pop()
      const heightGap = heights[index] - previousHeight
      const width = i - index - 1
      result += heightGap * width
      previousHeight = heights[index]
    }

    if (indexStack.length > 0) { // situation 1
      const heightGap = height - previousHeight
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
public class Solution {
    public int Trap(int[] heights) {
        var result = 0;
        var indexStack = new Stack<int>();

        for (var i = 0; i < heights.Length; i++) {
            var previousHeight = 0;

            while (indexStack.Count > 0 && heights[indexStack.Peek()] < heights[i]) { // situation 2
                var index = indexStack.Pop();
                var heightGap = heights[index] - previousHeight;
                var width = i - index - 1;
                result += heightGap * width;
                previousHeight = heights[index];
            }

            if (indexStack.Count > 0) { // situation 1
                var heightGap = heights[i] - previousHeight;
                var width = i - indexStack.Peek() - 1;
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
        previousHeight := 0

        for len(indexStack) > 0 && heights[indexStack[len(indexStack) - 1]] < height { // situation 2
            index := indexStack[len(indexStack) - 1]
            heightGap := heights[index] - previousHeight
            width := i - index - 1
            result += heightGap * width
            previousHeight = heights[index]
            indexStack = indexStack[:len(indexStack) - 1]
        }

        if len(indexStack) > 0 { // situation 1
            heightGap := height - previousHeight
            width := i - indexStack[len(indexStack) - 1] - 1
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
    previous_height = 0

    while !index_stack.empty? && heights[index_stack[-1]] <= height # situation 2
      index = index_stack.pop
      height_gap = heights[index] - previous_height
      width = i - index - 1
      result += height_gap * width
      previous_height = heights[index]
    end

    if !index_stack.empty? # situation 1
      height_gap = height - previous_height
      width = i - index_stack[-1] - 1
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
