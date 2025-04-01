# 349. Intersection of Two Arrays - LeetCode Best Practices

Visit original link: [349. Intersection of Two Arrays - LeetCode Best Practices](https://leetcoder.net/en/leetcode/349-intersection-of-two-arrays) for a better experience!

LeetCode link: [349. Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays), difficulty: **Easy**.

## LeetCode description of "349. Intersection of Two Arrays"

Given two integer arrays `nums1` and `nums2`, return _an array of their **intersection**_.
Each element in the result must be **unique** and you may return the result in **any order**.

> Array Intersection: The intersection of two arrays is defined as the set of elements that are present in both arrays.


### [Example 1]

**Input**: `nums1 = [1,2,2,1], nums2 = [2,2]`

**Output**: `[2]`

### [Example 2]

**Input**: `nums1 = [4,9,5], nums2 = [9,4,9,8,4]`

**Output**: `[9,4]`

**Explanation**: `[4,9] is also accepted.`

### [Constraints]

- `1 <= nums1.length, nums2.length <= 1000`
- `0 <= nums1[i], nums2[i] <= 1000`

## Intuition

1. Convert one of the arrays to a `set`. The elements are unique in a `set`.
2. When traversing the other array, if an element is found to already exist in the `set`, it means that the element belongs to the intersection, and the element should be added to the `results`.
3. The `results` is also of `set` type because duplicate removal is required.

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(N)`.

## Java

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        var results = new HashSet<Integer>();
        var num1Set = new HashSet<Integer>();

        for (var num : nums1) {
            num1Set.add(num);
        }

        for (var num : nums2) {
            if (num1Set.contains(num)) {
                results.add(num);
            }
        }

        return results.stream().mapToInt(num -> num).toArray();
    }
}
```

## Python

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        set_of_nums1 = set(nums1)
        results = set()

        for num in nums2:
            if num in set_of_nums1:
                results.add(num)

        return list(results)
```

## C++

```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> results;
        unordered_set<int> set_of_nums1(nums1.begin(), nums1.end());

        for (auto num : nums2) {
            if (set_of_nums1.contains(num)) {
                results.insert(num);
            }
        }

        return vector<int>(results.begin(), results.end());
    }
};
```

## JavaScript

```javascript
var intersection = function (nums1, nums2) {
  let results = new Set()
  let num1Set = new Set(nums1)

  for (const num of nums2) {
    if (num1Set.has(num)) {
      results.add(num)
    }
  }

  return Array.from(results)
};
```

## C#

```csharp
public class Solution
{
    public int[] Intersection(int[] nums1, int[] nums2)
    {
        var results = new HashSet<int>();
        var num1Set = new HashSet<int>();

        foreach (int num in nums1)
            num1Set.Add(num);

        foreach (int num in nums2)
        {
            if (num1Set.Contains(num))
            {
                results.Add(num);
            }
        }

        return results.ToArray();
    }
}
```

## Go

```go
func intersection(nums1 []int, nums2 []int) []int {
    results := map[int]bool{}
    num1Set := map[int]bool{}

    for _, num := range nums1 {
        num1Set[num] = true
    }

    for _, num := range nums2 {
        if _, ok := num1Set[num]; ok {
            results[num] = true
        }
    }

    return slices.Collect(maps.Keys(results))
}
```

## Ruby

```ruby
def intersection(nums1, nums2)
  nums1_set = Set.new(nums1)
  results = Set.new

  nums2.each do |num|
    if nums1_set.include?(num)
      results << num
    end
  end

  results.to_a
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [leetcoder.net](https://leetcoder.net): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [349. Intersection of Two Arrays - LeetCode Best Practices](https://leetcoder.net/en/leetcode/349-intersection-of-two-arrays).

GitHub repository: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

