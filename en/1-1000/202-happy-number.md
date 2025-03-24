Original link: [leetcoder.net - LeetCoder: Fucking Good LeetCode Solutions](https://leetcoder.net/en/leetcode/202-happy-number)

# 202. Happy Number - LeetCoder: Fucking Good LeetCode Solutions

LeetCode link: [202. Happy Number](https://leetcode.com/problems/happy-number), Difficulty: **Easy**.

## LeetCode description of "202. Happy Number"

Write an algorithm to determine if a number `n` is happy.

A **happy number** is a number defined by the following process:

- Starting with any positive integer, replace the number by the sum of the squares of its digits.
- Repeat the process until the number equals 1 (where it will stay), or it **loops endlessly in a cycle** which does not include 1.
- Those numbers for which this process **ends in 1** are happy.

Return `true` if `n` is *a happy number*, and `false` if not.

### [Example 1]

**Input**: `n = 19`

**Output**: `true`

**Explanation**: 

1^2 + 9^2 = 82
8^2 + 2^2 = 68
6^2 + 8^2 = 100
1^2 + 0^2 + 0^2 = 1

### [Example 2]

**Input**: `n = 2`

**Output**: `false`

### [Constraints]

- `1 <= n <= 2^31 - 1`

## Intuition

1. It is more convenient to call `isHappy(n)` recursively. You only need to generate a new `n` as a parameter each time.
2. If `n` has already appeared, it means that the loop has been entered, and `return false`. You can use `Set` to save the `n` that has appeared.

## Steps

1. Generate a new `n` as the `isHappy(n)` parameter.

	```javascript
	let sum = 0
	
	for (const digit of n.toString()) {
	  sum += Math.pow(Number(digit), 2)
	}
	
	// omitted code
	
	return isHappy(sum)
	```

2. If `n` has already appeared, it means that the loop has been entered, and `return false`. You can use `Set` to save the `n` that has appeared.

	```javascript
	var isHappy = function (n, appearedNums) { // 0
	  appearedNums ||= new Set() // 1
	  let sum = 0
	
	  for (const digit of n.toString()) {
	    sum += Math.pow(Number(digit), 2)
	  }
	
	  if (sum == 1) {
	    return true
	  }
	
	  if (appearedNums.has(sum)) { // 2
	    return false
	  }
	
	  appearedNums.add(sum) // 3
	
	  return isHappy(sum, appearedNums)
	};
	```

## Complexity

- Time complexity: `O(log N)`.
- Space complexity: `O(log N)`.

## Java

```java
class Solution {
    private HashSet<Integer> appearedNums = new HashSet<>();

    public boolean isHappy(int n) {
        appearedNums.add(n);

        var sum = 0;

        for (var digit : String.valueOf(n).toCharArray()) {
            sum += Math.pow(digit - '0', 2);
        }

        if (sum == 1) {
            return true;
        }
        
        if (appearedNums.contains(sum)) {
            return false;
        }

        return isHappy(sum);
    }
}
```

## Python

```python
class Solution:
    def __init__(self):
        self.appeared_nums = set()

    def isHappy(self, n: int) -> bool:
        self.appeared_nums.add(n)

        number = sum([int(digit) ** 2 for digit in str(n)])

        if number == 1:
            return True
        
        if number in self.appeared_nums:
            return False

        return self.isHappy(number)
```

## JavaScript

```javascript
```javascript
var isHappy = function (n, appearedNums) {
  appearedNums ||= new Set()
  let sum = 0

  for (const digit of n.toString()) {
    sum += Math.pow(Number(digit), 2)
  }

  if (sum == 1) {
    return true
  }

  if (appearedNums.has(sum)) {
    return false
  }

  appearedNums.add(sum)

  return isHappy(sum, appearedNums)
};
```
```

## C#

```c#
public class Solution
{
    HashSet<int> appearedNums = new HashSet<int>();

    public bool IsHappy(int n)
    {
        appearedNums.Add(n);

        int sum = 0;

        foreach (char digit in n.ToString().ToCharArray())
            sum += (int)Math.Pow(digit - '0', 2);

        if (sum == 1)
            return true;
        
        if (appearedNums.Contains(sum))
            return false;

        return IsHappy(sum);
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

