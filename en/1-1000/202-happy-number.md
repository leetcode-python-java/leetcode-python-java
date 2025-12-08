# 202. Happy Number - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired. We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform designed specifically for programmers.
>
> **The All-In-One Powerhouse for Your Career:**
> - 📄 **Professional Resume:** Create a dynamic, tech-focused resume that stands out to recruiters.
> - 🎨 **Visual Portfolio:** Automatically aggregate your GitHub contributions and projects into a stunning showcase.
> - ✍️ **Tech Blog:** Share your knowledge and build authority with a clean, distraction-free blogging space.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [202. Happy Number - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/202-happy-number) for a better experience!

LeetCode link: [202. Happy Number](https://leetcode.com/problems/happy-number), difficulty: **Easy**.

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

<p>1<sup>2</sup> + 9<sup>2</sup> = 82<br>
8<sup>2</sup> + 2<sup>2</sup> = 68<br>
6<sup>2</sup> + 8<sup>2</sup> = 100<br>
1<sup>2</sup> + 0<sup>2</sup> + 0<sup>2</sup> = 1</p>


### [Example 2]

**Input**: `n = 2`

**Output**: `false`

### [Constraints]

- `1 <= n <= 2^31 - 1`

## Intuition

1. It is more convenient to call `isHappy(n)` recursively. You only need to generate a new `n` as a parameter each time.
2. If `n` has already appeared, it means that the loop has been entered, and `return false`. You can use `Set` to save the `n` that has appeared.
3. Go is the iterative solution, other languages are the recursive solution.

## Step-by-Step Solution

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

## C#

```csharp
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

## Go

```go
func isHappy(n int) bool {
    // Use map to track seen numbers
    seen := make(map[int]bool)
    
    for n != 1 && !seen[n] {
        seen[n] = true
        n = sumOfSquaredDigits(n)
    }
    
    return n == 1
}

func sumOfSquaredDigits(n int) int {
    sum := 0
    nStr := strconv.Itoa(n)
    for i := 0; i < len(nStr); i++ {
        digit := int(nStr[i] - '0')
        sum += digit * digit
    }
    return sum
}
```

## C++

```cpp
class Solution {
public:
    bool isHappy(int n) {
        if (n == 1) {
            return true;
        }
        
        if (appeared_nums_.count(n)) {
            return false;
        }

        appeared_nums_.insert(n);
        
        return isHappy(getSum(n));
    }

private:
    unordered_set<int> appeared_nums_;
    
    int getSum(int n) {
        string n_str = to_string(n);
        int sum = 0;
        for (char digit : n_str) {
            sum += (digit - '0') * (digit - '0');
        }
        return sum;
    }
};
```

## Ruby

```ruby
def is_happy(n, appeared_nums = Set.new)
  return true if n == 1
  return false if appeared_nums.include?(n)

  appeared_nums.add(n)
  sum = n.to_s.chars.map { |digit| digit.to_i ** 2 }.sum

  is_happy(sum, appeared_nums)
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired. We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform designed specifically for programmers.
>
> **The All-In-One Powerhouse for Your Career:**
> - 📄 **Professional Resume:** Create a dynamic, tech-focused resume that stands out to recruiters.
> - 🎨 **Visual Portfolio:** Automatically aggregate your GitHub contributions and projects into a stunning showcase.
> - ✍️ **Tech Blog:** Share your knowledge and build authority with a clean, distraction-free blogging space.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [202. Happy Number - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/202-happy-number) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

