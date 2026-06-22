# 202. 快乐数 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> [**前往 leader.me 打造你的开发者个人IP →**](https://www.leader.me)

访问原文链接：[202. 快乐数 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/202-happy-number)，体验更佳！

力扣链接：[202. 快乐数](https://leetcode.cn/problems/happy-number), 难度等级：**简单**。

## LeetCode “202. 快乐数”问题描述

编写一个算法来判断一个数 `n` 是不是快乐数。

「**快乐数**」 定义为：

- 对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和。
- 然后重复这个过程直到这个数变为 `1`，也可能是 **无限循环** 但始终变不到 `1`。
- 如果这个过程 **结果为** `1`，那么这个数就是快乐数。
- 如果 `n` 是 *快乐数* 就返回 `true` ；不是，则返回 `false` 。

### [示例 1]

**输入**: `n = 19`

**输出**: `true`

**解释**: 

<p>1<sup>2</sup> + 9<sup>2</sup> = 82<br>
8<sup>2</sup> + 2<sup>2</sup> = 68<br>
6<sup>2</sup> + 8<sup>2</sup> = 100<br>
1<sup>2</sup> + 0<sup>2</sup> + 0<sup>2</sup> = 1</p>


### [示例 2]

**输入**: `n = 2`

**输出**: `false`

### [约束]

- `1 <= n <= 2^31 - 1`

## 思路

1. 递归调用`isHappy(n)`比较方便，每次只需要生成新的`n`作为参数。
2. 如果`n`已经出现过了，说明进入了循环，`return false`。可以用`Set`保存已经出现过的`n`。
3. Go是迭代解法，其他语言都是递归解法。

## 步骤

1. 生成新的`n`作为`isHappy()`的参数。

	```javascript
	let sum = 0
	
	for (const digit of n.toString()) {
	  sum += Math.pow(Number(digit), 2)
	}
	
	// omitted code
	
	return isHappy(sum)
	```

2. 如果`n`已经出现过了，说明进入了循环，`return false`。可以用`Set`保存已经出现过的`n`。

	```javascript
	var isHappy = function (n, appearedNums) {
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

## 复杂度

- 时间复杂度: `O(log N)`.
- 空间复杂度: `O(log N)`.

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

> 🚀 **打造你的开发者个人IP**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。
>
> 我的另一个项目 [**leader.me**](https://www.leader.me) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **简历 + 作品集 + 博客：** 将你的 GitHub 项目、技术心得与职场经历完美融合。
> - 🌐 **永久免费自定义域名：** 支持绑定你自己的独立域名，且该功能永久免费。
> - ✨ **顶级行业子域名：** 提供 `name.leader.me`，极具职业含金量的专属域名。

>
> [**立即前往 leader.me 打造你的个人品牌 →**](https://www.leader.me)

---

访问原文链接：[202. 快乐数 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://www.leader.me/leetcode/zh/solutions/202-happy-number)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

