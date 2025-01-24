# 496. Next Greater Element I
LeetCode link: [496. Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/)

## LeetCode problem description
The next greater element of some element `x` in an array is the first greater element that is to the right of `x` in the same array.

You are given two distinct 0-indexed integer arrays `nums1` and `nums2`, where `nums1` is a subset of `nums2`.

For each `0 <= i < nums1.length`, find the index `j` such that `nums1[i] == nums2[j]` and determine the next greater element of `nums2[j]` in `nums2`. If there is no next greater element, then the answer for this query is `-1`.

Return an array `ans` of length `nums1.length` such that `ans[i]` is the next greater element as described above.

```
-----------------------------------------------------------------------------------------------
[Example 1]

Input: nums1 = [4,1,2], nums2 = [1,3,4,2]
Output: [-1,3,-1]

Explanation: The next greater element for each value of nums1 is as follows:
- 4 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
- 1 is underlined in nums2 = [1,3,4,2]. The next greater element is 3.
- 2 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
-----------------------------------------------------------------------------------------------
[Example 2]

Input: nums1 = [2,4], nums2 = [1,2,3,4]
Output: [3,-1]

Explanation: The next greater element for each value of nums1 is as follows:
- 2 is underlined in nums2 = [1,2,3,4]. The next greater element is 3.
- 4 is underlined in nums2 = [1,2,3,4]. There is no next greater element, so the answer is -1.
-----------------------------------------------------------------------------------------------
[Constraints]

1 <= nums1.length <= nums2.length <= 1000
0 <= nums1[i], nums2[i] <= 10000
All integers in 'nums1' and 'nums2' are unique.
All the integers of 'nums1' also appear in 'nums2'.
-----------------------------------------------------------------------------------------------
```

## Thoughts
This problem can be solved using **Monotonic Stack**.

Detailed solutions will be given later, and now only the best practices in 7 languages are given.

### Complexity
#### Brute force solution
* Time: `O(n * m)`.
* Space: `O(n)`.

#### Monotonic stack solution
* Time: `O(n + m)`.
* Space: `O(n)`.

## Java
### Brute force solution
```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        var results = new int[nums1.length];
        Arrays.fill(results, -1);

        for (var i = 0; i < nums1.length; i++) {
            var found = false;

            for (var num2 : nums2) {
                if (found && num2 > nums1[i]) {
                    results[i] = num2;
                    break;
                }    

                if (nums1[i] == num2) {
                    found = true;
                }
            }
        }

        return results;
    }
}
```

### Monotonic stack solution
```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        var numToGreater = new HashMap<Integer, Integer>();
        var indexStack = new Stack<Integer>();

        for (var i = 0; i < nums2.length; i++) {
            while (!indexStack.empty() && nums2[indexStack.peek()] < nums2[i]) {
                var index = indexStack.pop();
                numToGreater.put(nums2[index], nums2[i]);
            }

            indexStack.push(i);
        }

        var results = new int[nums1.length];

        for (var i = 0; i < nums1.length; i++) {
            results[i] = numToGreater.getOrDefault(nums1[i], -1);
        }

        return results;
    }
}
```

## Python
### Brute force solution
```python
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        results = [-1] * len(nums1)

        for i, num1 in enumerate(nums1):
            found = False

            for num2 in nums2:
                if found and num2 > num1:
                    results[i] = num2
                    break

                if num1 == num2:
                    found = True

        return results
```

### Monotonic stack solution
```python
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        num_to_greater = defaultdict(int)
        index_stack = []

        for i, num in enumerate(nums2):
            while index_stack and nums2[index_stack[-1]] < num:
                index = index_stack.pop()
                num_to_greater[nums2[index]] = num

            index_stack.append(i)

        return [num_to_greater.get(num, -1) for num in nums1]
```

## C++
### Brute force solution
```cpp
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        vector<int> results(nums1.size(), -1);

        for (auto i = 0; i < nums1.size(); i++) {
            auto found = false;

            for (auto num2 : nums2) {
                if (found && num2 > nums1[i]) {
                    results[i] = num2;
                    break;
                }    

                if (nums1[i] == num2) {
                    found = true;
                }
            }
        }

        return results;
    }
};
```

### Monotonic stack solution
```cpp
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        unordered_map<int, int> num_to_greater;
        stack<int> index_stack;

        for (auto i = 0; i < nums2.size(); i++) {
            while (!index_stack.empty() && nums2[index_stack.top()] < nums2[i]) {
                num_to_greater[nums2[index_stack.top()]] = nums2[i];
                index_stack.pop();
            }

            index_stack.push(i);
        }

        vector<int> results(nums1.size(), -1);

        for (auto i = 0; i < nums1.size(); i++) {
            if (num_to_greater.contains(nums1[i])) {
                results[i] = num_to_greater[nums1[i]];
            }
        }

        return results;
    }
};
```

## JavaScript
### Brute force solution
```javascript
var nextGreaterElement = function (nums1, nums2) {
  const results = Array(nums1.length).fill(-1)

  nums1.forEach((num1, i) => {
    let found = false

    for (const num2 of nums2) {
      if (found && num2 > num1) {
        results[i] = num2
        break
      }    

      if (num1 == num2) {
        found = true
      }
    }
  })

  return results
};
```

### Monotonic stack solution
```javascript
var nextGreaterElement = function (nums1, nums2) {
  const numToGreater = {}
  const indexStack = []

  nums2.forEach((num, i) => {
    while (indexStack.length > 0 && nums2[indexStack.at(-1)] < num) {
      const index = indexStack.pop()
      numToGreater[nums2[index]] = num
    }

    indexStack.push(i)
  })

  return nums1.map((num) => numToGreater[num] || -1)
};
```

## C#
### Brute force solution
```c#
public class Solution
{
    public int[] NextGreaterElement(int[] nums1, int[] nums2)
    {
        var results = new int[nums1.Length];
        Array.Fill(results, -1);

        for (var i = 0; i < nums1.Length; i++)
        {
            bool found = false;

            foreach (var num2 in nums2)
            {
                if (found && num2 > nums1[i])
                {
                    results[i] = num2;
                    break;
                }    

                if (nums1[i] == num2)
                {
                    found = true;
                }
            }
        }

        return results;
    }
}
```

### Monotonic stack solution
```c#
public class Solution {
    public int[] NextGreaterElement(int[] nums1, int[] nums2) {
        var numToGreater = new Dictionary<int, int>();
        var indexStack = new Stack<int>();

        for (var i = 0; i < nums2.Length; i++) {
            while (indexStack.Count > 0 && nums2[indexStack.Peek()] < nums2[i]) {
                var index = indexStack.Pop();
                numToGreater[nums2[index]] = nums2[i];
            }

            indexStack.Push(i);
        }

        var results = new int[nums1.Length];

        for (var i = 0; i < nums1.Length; i++) {
            results[i] = numToGreater.GetValueOrDefault(nums1[i], -1);
        }

        return results;
    }
}
```

## Go
### Brute force solution
```go
func nextGreaterElement(nums1 []int, nums2 []int) []int {
    results := slices.Repeat([]int{-1}, len(nums1))

    for i, num1 := range nums1 {
        found := false

        for _, num2 := range nums2 {
            if found && num2 > num1 {
                results[i] = num2
                break
            }

            if num1 == num2 {
                found = true
            }
        }
    }

    return results
}
```

### Monotonic stack solution
```go
func nextGreaterElement(nums1 []int, nums2 []int) []int {
    numToGreater := map[int]int{}
    indexStack := []int{}

    for i, num2 := range nums2 {
        for (len(indexStack) > 0 && nums2[indexStack[len(indexStack) - 1]] < num2) {
            index := indexStack[len(indexStack) - 1]
            numToGreater[nums2[index]] = num2
            indexStack = indexStack[:len(indexStack) - 1]
        }

        indexStack = append(indexStack, i)
    }

    results := make([]int, len(nums1))

    for i, num1 := range nums1 {
        if value, ok := numToGreater[num1]; ok {
            results[i] = value
            continue
        }
        results[i] = -1
    }

    return results
}
```

## Ruby
### Brute force solution
```ruby
def next_greater_element(nums1, nums2)
  results = Array.new(nums1.size, -1)

  nums1.each_with_index do |num1, i|
    found = false

    nums2.each do |num2|
      if found and num2 > num1
        results[i] = num2
        break
      end

      found = true if num1 == num2
    end
  end

  results
end
```

### Monotonic stack solution
```ruby
def next_greater_element(nums1, nums2)
  num_to_greater = {}
  index_stack = []

  nums2.each_with_index do |num, i|
    while !index_stack.empty? && nums2[index_stack.last] < num
      index = index_stack.pop
      num_to_greater[nums2[index]] = num
    end

    index_stack << i
  end

  nums1.map { |num| num_to_greater[num] || -1 }
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
