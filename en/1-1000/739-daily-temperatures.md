# 739. Daily Temperatures
LeetCode link: [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)

## LeetCode problem description
Given an array of integers `temperatures` represents the daily temperatures, return an array `answer` such that `answer[i]` is the number of days you have to wait after the `i-th` day to get a warmer temperature. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

```
------------------------------------------------------------------------
[Example 1]

Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
------------------------------------------------------------------------
[Example 2]

Input: temperatures = [30,40,50,60]
Output: [1,1,1,0]
------------------------------------------------------------------------
[Example 3]

Input: temperatures = [30,60,90]
Output: [1,1,0]
------------------------------------------------------------------------
[Constraints]

1 <= temperatures.length <= 100000
30 <= temperatures[i] <= 100
------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Monotonic Stack**.

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Complexity
* Time: `O(n)`.
* Space: `O(n)`.

## Java
```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        var results = new int[temperatures.length];
        var indexStack = new Stack<Integer>();

        for (var i = 0; i < temperatures.length; i++) {
            while (!indexStack.empty() && temperatures[indexStack.peek()] < temperatures[i]) {
                var index = indexStack.pop();
                results[index] = i - index;
            }

            indexStack.push(i);
        }

        return results;
    }
}
```

## Python
```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        results = [0] * len(temperatures)
        index_stack = []

        for i, temperature in enumerate(temperatures):
            while index_stack and temperature > temperatures[index_stack[-1]]:
                index = index_stack.pop()
                results[index] = i - index

            index_stack.append(i)

        return results
```

## C++
```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        vector<int> results(temperatures.size());
        stack<int> index_stack;

        for (auto i = 0; i < temperatures.size(); i++) {
            while (!index_stack.empty() && temperatures[i] > temperatures[index_stack.top()]) {
                results[index_stack.top()] = i - index_stack.top();
                index_stack.pop();
            }

            index_stack.push(i);
        }

        return results;
    }
};
```

## JavaScript
```javascript
var dailyTemperatures = function (temperatures) {
  const results = Array(temperatures.length).fill(0)
  const indexStack = []

  temperatures.forEach((temperature, i) => {
    while (indexStack.length > 0 && temperatures[indexStack.at(-1)] < temperature) {
      results[indexStack.at(-1)] = i - indexStack.at(-1)
      indexStack.pop()
    }

    indexStack.push(i)
  })

  return results
};
```

## C#
```c#
public class Solution
{
    public int[] DailyTemperatures(int[] temperatures)
    {
        var results = new int[temperatures.Length];
        var indexStack = new Stack<int>();

        for (var i = 0; i < temperatures.Length; i++)
        {
            while (indexStack.Count > 0 && temperatures[indexStack.Peek()] < temperatures[i])
            {
                int index = indexStack.Pop();
                results[index] = i - index;
            }

            indexStack.Push(i);
        }

        return results;
    }
}
```

## Go
### Solution 1: Using a 'slice' as stack
```go
func dailyTemperatures(temperatures []int) []int {
    results := make([]int, len(temperatures))
    indexStack := []int{}

    for i, temperature := range temperatures {
        for len(indexStack) > 0 && temperature > temperatures[indexStack[len(indexStack) - 1]] {
            index := indexStack[len(indexStack) - 1]
            results[index] = i - index
            indexStack = indexStack[:len(indexStack) - 1]
        }

        indexStack = append(indexStack, i)
    }

    return results
}
```

### Solution 2: Using `GoDS` stack
```go
func dailyTemperatures(temperatures []int) []int {
    results := make([]int, len(temperatures))
    indexStack := arraystack.New()

    for i, temperature := range temperatures {
        for !indexStack.Empty() {
            index, _ := indexStack.Peek();

            if temperature <= temperatures[index.(int)] {
                break
            }

            indexStack.Pop()
            results[index.(int)] = i - index.(int)
        }

        indexStack.Push(i)
    }

    return results
}
```

## Ruby
```ruby
def daily_temperatures(temperatures)
  results = Array.new(temperatures.size, 0)
  index_stack = []

  temperatures.each_with_index do |temperature, i|
    while !index_stack.empty? && temperatures[index_stack.last] < temperature
      results[index_stack.last] = i - index_stack.last
      index_stack.pop
    end

    index_stack << i
  end

  results
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
