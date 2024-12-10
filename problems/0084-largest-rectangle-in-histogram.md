# 84. Largest Rectangle in Histogram
LeetCode problem: [84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)

## LeetCode problem description
Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return the area of the largest rectangle in the histogram.

```
------------------------------------------------------------------------
[Example 1]

Input: heights = [2,1,5,6,2,3]
Output: 10

Explanation: The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.
------------------------------------------------------------------------
[Example 2]

Input: heights = [2,4]
Output: 4
------------------------------------------------------------------------
[Constraints]

1 <= heights.length <= 100000
0 <= heights[i] <= 10000
------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Monotonic Stack**.

* The `heights` in the stack from bottom to top are in ascending order.
* While `current_height < stack_top_height`, pop `stack_top_height`.
* Follow **Monotonic Stack**'s common rule: **only calculating when `pop()` is happening**. This common rule can be applied to calculating result for **most** of the `Monotonic Stack` problems.
* Disappeared heights (popped by `current_height` or popped by `stack_top_height`) are all taller than `stack_top_height`. This logic will be used to calculate the `width`.

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Complexity
* Time: `O(n)`.
* Space: `O(n)`.

## Python
```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        heights = [0] + heights + [0]
        max_area = 0
        index_stack = []

        for i, height in enumerate(heights):
            while index_stack and height < heights[index_stack[-1]]:
                popped_index = index_stack.pop()

                popped_height = heights[popped_index]
                
                left_index = index_stack[-1] # popped_height's remaining left heights are all shorter than 'popped_height', because when 'popped_height' itself was pushed into stack, it must have caused some (could be none) taller heights been popped out of the stack.
                right_index = i # popped_height's right heights (which are all taller than 'popped_height') have been popped out of the stack (disappeared) when current `i` height is being pushed into stack.
                width = right_index - left_index - 1 # So in the range of 'width', they are all no shorter than `popped_height`, although they have been popped out of the stack (disappeared).

                area = popped_height * width
                if area > max_area:
                    max_area = area

            index_stack.append(i)

        return max_area
```

## Java
```java
class Solution {
    public int largestRectangleArea(int[] heightArray) {
        var heights = new int[heightArray.length + 2];
        System.arraycopy(heightArray, 0, heights, 1, heightArray.length);

        var maxArea = 0;
        var indexStack = new Stack<Integer>();

        for (var i = 0; i < heights.length; i++) {
            while (!indexStack.empty() && heights[i] < heights[indexStack.peek()]) {
                var poppedIndex = indexStack.pop();

                var poppedHeight = heights[poppedIndex];
                var leftIndex = indexStack.peek(); // poppedHeight's remaining left heights are all shorter than it, because when 'poppedHeight' itself was pushed into stack, it must have caused some (could be none) taller heights been popped out of the stack.
                var rightIndex = i; // poppedHeight's right heights (which are all taller than 'poppedHeight') have been popped out of the stack (disappeared) when current `i` height is being pushed into stack.
                var width = rightIndex - leftIndex - 1; // So in the range of 'width', they are all no shorter than `poppedHeight`, although they have been popped out of the stack (disappeared).

                var area = poppedHeight * width;
                if (area > maxArea) {
                    maxArea = area;
                }
            }

            indexStack.push(i);
        }

        return maxArea;
    }
}
```

## C++
```cpp
class Solution {
public:
    int largestRectangleArea(vector<int> heights) {
        heights.insert(heights.begin(), 0);
        heights.emplace_back(0);
        auto max_area = 0;
        stack<int> index_stack;

        for (auto i = 0; i < heights.size(); i++) {
            while (!index_stack.empty() && heights[i] < heights[index_stack.top()]) {
                auto popped_height = heights[index_stack.top()];

                index_stack.pop();

                auto left_index = index_stack.top(); // popped_height's remaining left heights are all shorter than it, because when 'popped_height' itself was pushed into stack, it must have caused some (could be none) taller heights been popped out of the stack.
                auto right_index = i; // popped_height's right heights (which are all taller than 'popped_height') have been popped out of the stack (disappeared) when current `i` height is being pushed into stack.
                auto width = right_index - left_index - 1; // So in the range of 'width', they are all no shorter than `popped_height`, although they have been popped out of the stack (disappeared).
                
                auto area = popped_height * width;
                if (area > max_area) {
                    max_area = area;
                }
            }

            index_stack.push(i);
        }

        return max_area;
    }
};
```

## JavaScript
```javascript
var largestRectangleArea = function(heights) {
  let maxArea = 0
  const indexStack = []
  heights = [0, ...heights, 0]

  heights.forEach((height, i) => {
    while (indexStack.length > 0 && height < heights[indexStack.at(-1)]) {
      const poppedIndex = indexStack.pop()

      const poppedHeight = heights[poppedIndex]
      const leftIndex = indexStack.at(-1) // poppedHeight's remaining left heights are all shorter than it, because when 'poppedHeight' itself was pushed into stack, it must have caused some (could be none) taller heights been popped out of the stack.
      const rightIndex = i // poppedHeight's right heights (which are all taller than 'poppedHeight') have been popped out of the stack (disappeared) when current `i` height is being pushed into stack.
      const width = rightIndex - leftIndex - 1 // So in the range of 'width', they are all no shorter than `poppedHeight`, although they have been popped out of the stack (disappeared).

      const area = poppedHeight * width
      if (area > maxArea) {
        maxArea = area
      }
    }

    indexStack.push(i)
  })

  return maxArea
};
```

## C#
```c#
public class Solution {
    public int LargestRectangleArea(int[] heights) {
        var maxArea = 0;
        var indexStack = new Stack<int>();
        heights = [0, ..heights, 0];

        for (var i = 0; i < heights.Length; i++) {
            while (indexStack.Count > 0 && heights[i] < heights[indexStack.Peek()]) {
                var poppedIndex = indexStack.Pop();

                var poppedHeight = heights[poppedIndex];
                var leftIndex = indexStack.Peek(); // poppedHeight's remaining left heights are all shorter than it, because when 'poppedHeight' itself was pushed into stack, it must have caused some (could be none) taller heights been popped out of the stack.
                var rightIndex = i; // poppedHeight's right heights (which are all taller than 'poppedHeight') have been popped out of the stack (disappeared) when current `i` height is being pushed into stack.
                var width = rightIndex - leftIndex - 1; // So in the range of 'width', they are all no shorter than `poppedHeight`, although they have been popped out of the stack (disappeared).

                var area = poppedHeight * width;
                if (area > maxArea) {
                    maxArea = area;
                }
            }

            indexStack.Push(i);
        }

        return maxArea;
    }
}
```

## Go
```go
func largestRectangleArea(heightSlice []int) int {
    maxArea := 0
    indexStack := []int{}
    heights := append([]int{0}, append(heightSlice, 0)...)

    for i, height := range heights {
        for len(indexStack) > 0 && height < heights[indexStack[len(indexStack) - 1]] {
            poppedIndex := indexStack[len(indexStack) - 1]
            indexStack = indexStack[:len(indexStack) - 1]

            poppedHeight := heights[poppedIndex]
            leftIndex := indexStack[len(indexStack) - 1] // poppedHeight's remaining left heights are all shorter than it, because when 'poppedHeight' itself was pushed into stack, it must have caused some (could be none) taller heights been popped out of the stack.
            rightIndex := i // poppedHeight's right heights (which are all taller than 'poppedHeight') have been popped out of the stack (disappeared) when current `i` height is being pushed into stack.
            width := rightIndex - leftIndex - 1 // So in the range of 'width', they are all no shorter than `poppedHeight`, although they have been popped out of the stack (disappeared).

            area := poppedHeight * width
            if (area > maxArea) {
                maxArea = area
            }
        }

        indexStack = append(indexStack, i)
    }

    return maxArea
}
```

## Ruby
```ruby
def largest_rectangle_area(heights)
  heights = [0] + heights + [0]
  max_area = 0
  index_stack = []

  heights.each_with_index do |height, i|
    while !index_stack.empty? && height < heights[index_stack.last]
      popped_index = index_stack.pop

      popped_height = heights[popped_index]
        
      left_index = index_stack[-1] # popped_height's remaining left heights are all shorter than 'popped_height', because when 'popped_height' itself was pushed into stack, it must have caused some (could be none) taller heights been popped out of the stack.
      right_index = i # popped_height's right heights (which are all taller than 'popped_height') have been popped out of the stack (disappeared) when current `i` height is being pushed into stack.
      width = right_index - left_index - 1 # So in the range of 'width', they are all no shorter than `popped_height`, although they have been popped out of the stack (disappeared).

      area = popped_height * width
      max_area = area if area > max_area
    end

    index_stack << i
  end

  max_area
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
