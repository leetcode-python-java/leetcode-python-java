# 1431. 拥有最多糖果的孩子 - LeetCode Python/Java/C++ 题解

访问原文链接：[1431. 拥有最多糖果的孩子 - LeetCode Python/Java/C++ 题解](https://leetcode.blog/zh/leetcode/1431-kids-with-the-greatest-number-of-candies)，体验更佳！

力扣链接：[1431. 拥有最多糖果的孩子](https://leetcode.cn/problems/kids-with-the-greatest-number-of-candies), 难度等级：**简单**。

## LeetCode “1431. 拥有最多糖果的孩子”问题描述

有 `n` 个有糖果的孩子。给你一个数组 `candies`，其中 `candies[i]` 代表第 `i` 个孩子拥有的糖果数目，和一个整数 `extraCandies` 表示你所有的额外糖果的数量。

返回一个长度为 `n` 的布尔数组 `result`，如果把所有的 `extraCandies` 给第 `i` 个孩子之后，他会拥有所有孩子中 **最多** 的糖果，那么 `result[i]` 为 `true`，否则为 `false`。

注意，允许有多个孩子同时拥有 **最多** 的糖果数目。

### [示例 1]

**输入**: `candies = [2,3,5,1,3], extraCandies = 3`

**输出**: `[true,true,true,false,true]`

**解释**: 

<p>如果你把额外的糖果全部给：<br>
孩子 1，将有 2 + 3 = 5 个糖果，是孩子中最多的。<br>
孩子 2，将有 3 + 3 = 6 个糖果，是孩子中最多的。<br>
孩子 3，将有 5 + 3 = 8 个糖果，是孩子中最多的。<br>
孩子 4，将有 1 + 3 = 4 个糖果，不是孩子中最多的。<br>
孩子 5，将有 3 + 3 = 6 个糖果，是孩子中最多的。</p>


### [示例 2]

**输入**: `candies = [4,2,1,1,2], extraCandies = 1`

**输出**: `[true,false,false,false,false]`

**解释**: `只有 1 个额外糖果，所以不管额外糖果给谁，只有孩子 1 可以成为拥有糖果最多的孩子。`

### [示例 3]

**输入**: `candies = [12,1,12], extraCandies = 10`

**输出**: `[true,false,true]`

### [约束]

- `n == candies.length`
- `2 <= n <= 100`
- `1 <= candies[i] <= 100`
- `1 <= extraCandies <= 50`

### [Hints]

<details>
  <summary>提示 1</summary>
  For each kid check if candies[i] + extraCandies ≥ maximum in Candies[i].

  
</details>

## 思路

1. 找出所有孩子中最多的糖果数
2. 检查每个孩子拿到额外糖果后能否达到或超过这个数

## 步骤

1. `max_candy = candies.max` → 直接取数组最大值
2. `candies.map { |candy| candy + extra_candy >= max_candy }` → 用map遍历，计算每个孩子是否能达到最多

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(N)`.

## Python

```python
class Solution:
    def kidsWithCandies(self, candies: List[int], extra_candy: int) -> List[bool]:
        max_candy = max(candies)
        result = []

        for candy in candies:
            result.append(candy + extra_candy >= max_candy)

        return result
```

## Java

```java
class Solution {
    public List<Boolean> kidsWithCandies(int[] candies, int extraCandy) {
        int maxCandy = Arrays.stream(candies).max().getAsInt();
        List<Boolean> result = new ArrayList<>();

        for (int candy : candies) {
            result.add(candy + extraCandy >= maxCandy);
        }

        return result;
    }
}
```

## C++

```cpp
class Solution {
public:
    vector<bool> kidsWithCandies(vector<int>& candies, int extraCandy) {
        int max_candy = *max_element(candies.begin(), candies.end());
        vector<bool> result;

        for (int candy : candies) {
            result.push_back(candy + extraCandy >= max_candy);
        }

        return result;
    }
};
```

## JavaScript

```javascript
var kidsWithCandies = function(candies, extraCandy) {
  const maxCandy = Math.max(...candies)
  return candies.map((candy) => candy + extraCandy >= maxCandy)
};

```

## Go

```go
func kidsWithCandies(candies []int, extraCandy int) []bool {
    maxCandy := candies[0]
    for _, candy := range candies {
        if candy > maxCandy {
            maxCandy = candy
        }
    }

    result := make([]bool, len(candies))
    for i, candy := range candies {
        result[i] = candy+extraCandy >= maxCandy
    }

    return result
}
```

## C#

```csharp
public class Solution
{
    public IList<bool> KidsWithCandies(int[] candies, int extraCandy)
    {
        int maxCandy = candies.Max();
        return candies.Select(candy => candy + extraCandy >= maxCandy).ToList();
    }
}
```

## Ruby

```ruby
def kids_with_candies(candies, extra_candy)
  max_candy = candies.max
  candies.map { |candy| candy + extra_candy >= max_candy }
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCode.blog](https://leetcode.blog/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[1431. 拥有最多糖果的孩子 - LeetCode Python/Java/C++ 题解](https://leetcode.blog/zh/leetcode/1431-kids-with-the-greatest-number-of-candies).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

