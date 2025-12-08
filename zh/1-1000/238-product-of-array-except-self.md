# 238. 除自身以外数组的乘积 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解

> 🚀 **进阶你的开发者身份**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **专业简历 (Resume)：** 告别平庸，生成一份令猎头和面试官眼前一亮的动态技术简历。
> - 🎨 **作品集 (Portfolio)：** 自动聚合 GitHub 贡献与项目经历，将枯燥的代码转化为极具冲击力的视觉作品集。
> - ✍️ **技术博客 (Blog)：** 在纯净、专注的写作空间分享技术见解，树立你的行业影响力。
>
> [**立即前往 Show.dev 打造你的专属品牌 →**](https://www.show.dev)

---

访问原文链接：[238. 除自身以外数组的乘积 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/238-product-of-array-except-self)，体验更佳！

力扣链接：[238. 除自身以外数组的乘积](https://leetcode.cn/problems/product-of-array-except-self), 难度等级：**中等**。

## LeetCode “238. 除自身以外数组的乘积”问题描述

给你一个整数数组 `nums`，返回 数组 `answer` ，其中 `answer[i]` 等于 `nums` 中除 `nums[i]` 之外其余各元素的乘积 。

题目数据 **保证** 数组 `nums` 之中任意元素的全部前缀元素和后缀的乘积都在  **32 位** 整数范围内。

请 **不要使用除法**，且在 `O(n)` 时间复杂度内完成此题。

### [示例 1]

**输入**: `nums = [1,2,3,4]`

**输出**: `[24,12,8,6]`

### [示例 2]

**输入**: `nums = [-1,1,0,-3,3]`

**输出**: `[0,0,9,0,0]`

### [约束]

- `2 <= nums.length <= 10^5`
- `-30 <= nums[i] <= 30`
- 输入 **保证** 数组 `answer[i]` 在  **32 位** 整数范围内


**进阶**：你可以在 `O(1)` 的额外空间复杂度内完成这个题目吗？（ 出于对空间复杂度分析的目的，输出数组 **不被视为** 额外空间。）

### [Hints]

<details>
  <summary>提示 1</summary>
  Think how you can efficiently utilize prefix and suffix products to calculate the product of all elements except self for each index. Can you pre-compute the prefix and suffix products in linear time to avoid redundant calculations?


  
</details>

<details>
  <summary>提示 2</summary>
  Can you minimize additional space usage by reusing memory or modifying the input array to store intermediate results?

  
</details>

## 思路 1

1. **分解问题**：将"除自身外的乘积"分解为"左侧乘积 × 右侧乘积"
2. **两次遍历**：先计算每个元素的左侧乘积，再计算右侧乘积
3. **合并结果**：将左右乘积相乘得到最终结果

## “预计算技术”的模式

**预计算技术（Pre-Computation Techniques）** 是一种通过提前计算并存储中间结果或常用数据，以减少实时计算开销的优化方法。其核心思想是**“用空间换时间”**。

#### 主要应用场景

- **数组的前缀/后缀**计算问题。
- **高频计算问题**：如斐波那契数列、阶乘、素数表等，通过预先生成查找表（Lookup Table）避免重复计算。
- **动态规划（DP）**：预先计算子问题的解并存储，如背包问题、最短路径问题。

## 步骤

1. **初始化数组**：
    - 创建`leftProducts`数组，存储每个元素左侧所有元素的乘积
    - 创建`rightProducts`数组，存储每个元素右侧所有元素的乘积

2. **计算左侧乘积**（从左到右遍历）：
    - 第一个元素左侧乘积初始化为1
    - 后续元素：`leftProducts[i] = nums[i-1] * leftProducts[i-1]`

3. **计算右侧乘积**（从右到左遍历）：
    - 最后一个元素右侧乘积初始化为1
    - 前序元素：`rightProducts[i] = nums[i+1] * rightProducts[i+1]`

4. **合并结果**：
    - 遍历每个位置，将左右乘积相乘：`answer[i] = leftProducts[i] * rightProducts[i]`

5. **返回结果数组**

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(N)`.

## Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer[]}
def product_except_self(nums)
  #           nums: [1,  2, 3, 4]
  #  left_products: [1,  1, 2, 6]
  # right_products: [24,12, 4, 1]
  #         answer: [24,12, 8, 6]
  size = nums.size

  left_products = Array.new(size, 1)
  (1...size).each do |i|
    left_products[i] = nums[i - 1] * left_products[i - 1]
  end

  right_products = Array.new(size, 1)
  (size - 2).downto(0) do |i|
    right_products[i] = nums[i + 1] * right_products[i + 1]
  end

  answer = []
  (0...size).each do |i|
    answer << left_products[i] * right_products[i]
  end

  answer
end
```

## Python

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        size = len(nums)

        #           nums: [1,  2, 3, 4]
        #  left_products: [1,  1, 2, 6]
        # right_products: [24,12, 4, 1]
        #         answer: [24,12, 8, 6]
        left_products = [1] * size
        for i in range(1, size):
            left_products[i] = nums[i - 1] * left_products[i - 1]
        
        right_products = [1] * size
        for i in range(size - 2, -1, -1):
            right_products[i] = nums[i + 1] * right_products[i + 1]
        
        answer = []
        for i in range(size):
            answer.append(left_products[i] * right_products[i])
        
        return answer
```

## Java

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int size = nums.length;
        //           nums: [1,  2, 3, 4]
        //  left_products: [1,  1, 2, 6]
        // right_products: [24,12, 4, 1]
        //         answer: [24,12, 8, 6]
        int[] leftProducts = new int[size];
        leftProducts[0] = 1;
        for (int i = 1; i < size; i++) {
            leftProducts[i] = nums[i - 1] * leftProducts[i - 1];
        }

        int[] rightProducts = new int[size];
        rightProducts[size - 1] = 1;
        for (int i = size - 2; i >= 0; i--) {
            rightProducts[i] = nums[i + 1] * rightProducts[i + 1];
        }

        int[] answer = new int[size];
        for (int i = 0; i < size; i++) {
            answer[i] = leftProducts[i] * rightProducts[i];
        }

        return answer;
    }
}
```

## C++

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int size = nums.size();
        //           nums: [1,  2, 3, 4]
        //  left_products: [1,  1, 2, 6]
        // right_products: [24,12, 4, 1]
        //         answer: [24,12, 8, 6]
        vector<int> left_products(size, 1);
        for (int i = 1; i < size; i++) {
            left_products[i] = nums[i - 1] * left_products[i - 1];
        }

        vector<int> right_products(size, 1);
        for (int i = size - 2; i >= 0; i--) {
            right_products[i] = nums[i + 1] * right_products[i + 1];
        }

        vector<int> answer(size);
        for (int i = 0; i < size; i++) {
            answer[i] = left_products[i] * right_products[i];
        }

        return answer;
    }
};
```

## JavaScript

```javascript
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var productExceptSelf = function(nums) {
  const size = nums.length

  const leftProducts = new Array(size).fill(1)
  for (let i = 1; i < size; i++) {
    leftProducts[i] = nums[i - 1] * leftProducts[i - 1]
  }

  const rightProducts = new Array(size).fill(1)
  for (let i = size - 2; i >= 0; i--) {
    rightProducts[i] = nums[i + 1] * rightProducts[i + 1]
  }

  const answer = []
  for (let i = 0; i < size; i++) {
    answer.push(leftProducts[i] * rightProducts[i])
  }

  return answer
};

```

## C#

```csharp
public class Solution
{
    public int[] ProductExceptSelf(int[] nums)
    {
        int size = nums.Length;
        //           nums: [1,  2, 3, 4]
        //  left_products: [1,  1, 2, 6]
        // right_products: [24,12, 4, 1]
        //         answer: [24,12, 8, 6]
        int[] leftProducts = new int[size];
        leftProducts[0] = 1;

        for (int i = 1; i < size; i++)
            leftProducts[i] = nums[i - 1] * leftProducts[i - 1];

        int[] rightProducts = new int[size];
        rightProducts[size - 1] = 1;

        for (int i = size - 2; i >= 0; i--)
            rightProducts[i] = nums[i + 1] * rightProducts[i + 1];

        int[] answer = new int[size];

        for (int i = 0; i < size; i++)
            answer[i] = leftProducts[i] * rightProducts[i];

        return answer;
    }
}
```

## Go

```go
func productExceptSelf(nums []int) []int {
    size := len(nums)

    leftProducts := make([]int, size)
    leftProducts[0] = 1
    for i := 1; i < size; i++ {
        leftProducts[i] = nums[i - 1] * leftProducts[i - 1]
    }

    rightProducts := make([]int, size)
    rightProducts[size - 1] = 1
    for i := size - 2; i >= 0; i-- {
        rightProducts[i] = nums[i + 1] * rightProducts[i + 1]
    }

    answer := make([]int, size)
    for i := 0; i < size; i++ {
        answer[i] = leftProducts[i] * rightProducts[i]
    }

    return answer
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## 思路 2

1. **空间优化**：利用输出数组存储中间结果，避免额外空间
2. **两阶段计算**：先计算左侧乘积存入结果，再动态计算右侧乘积并直接合并
3. **原地操作**：仅使用一个变量动态维护右侧乘积

## 步骤

1. **初始化结果数组**：
    - 创建大小相同的`answer`数组，初始值全1

2. **计算左侧乘积**（左→右遍历）：
    - 初始化`left_product = 1`
    - 遍历时：`answer[i] = left_product`，然后`left_product *= nums[i]`

3. **计算右侧乘积并合并**（右→左遍历）：
    - 初始化`right_product = 1`
    - 遍历时：`answer[i] *= right_product`，然后`right_product *= nums[i]`

4. **返回结果数组**
    - 空间复杂度：O(1)（输出数组不计入空间复杂度）

## 复杂度

- 时间复杂度: `O(N)`.
- 空间复杂度: `O(1)`.

## Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer[]}
def product_except_self(nums)
  size = nums.size
  answer = Array.new(size, 1)

  left_product = 1
  (0...size).each do |i|
    answer[i] = left_product
    left_product *= nums[i]
  end

  #    nums: [1,  2, 3, 4]
  #  answer: [1,  1, 2, 6]  left_product done 
  #  answer: [24,12, 8, 6] right_product done

  right_product = 1
  (size - 1).downto(0) do |i|
    answer[i] *= right_product
    right_product *= nums[i]
  end

  answer
end
```

## Python

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        size = len(nums)
        answer = [1] * size

        left_product = 1
        for i in range(size):
            answer[i] = left_product
            left_product *= nums[i]

        #    nums: [1,  2, 3, 4]
        #  answer: [1,  1, 2, 6]  left_product done 
        #  answer: [24,12, 8, 6] right_product done

        right_product = 1
        for i in range(size-1, -1, -1):
            answer[i] *= right_product
            right_product *= nums[i]

        return answer
```

## Java

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int size = nums.length;
        int[] answer = new int[size];
        Arrays.fill(answer, 1);

        int leftProduct = 1;
        for (int i = 0; i < size; i++) {
            answer[i] = leftProduct;
            leftProduct *= nums[i];
        }

        //    nums: [1,  2, 3, 4]
        //  answer: [1,  1, 2, 6]  leftProduct done 
        //  answer: [24,12, 8, 6] rightProduct done

        int rightProduct = 1;
        for (int i = size - 1; i >= 0; i--) {
            answer[i] *= rightProduct;
            rightProduct *= nums[i];
        }

        return answer;
    }
}
```

## C++

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int size = nums.size();
        vector<int> answer(size, 1);

        int left_product = 1;
        for (int i = 0; i < size; ++i) {
            answer[i] = left_product;
            left_product *= nums[i];
        }

        //    nums: [1,  2, 3, 4]
        //  answer: [1,  1, 2, 6]  left_product done 
        //  answer: [24,12, 8, 6] right_product done

        int right_product = 1;
        for (int i = size - 1; i >= 0; --i) {
            answer[i] *= right_product;
            right_product *= nums[i];
        }

        return answer;
    }
};
```

## JavaScript

```javascript
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var productExceptSelf = function(nums) {
  const answer = [];
  let left_product = 1;

  for (let i = 0; i < nums.length; i++) {
    answer[i] = left_product;
    left_product *= nums[i];
  }

  //  nums: [1,  2, 3, 4]
  //  answer: [1,  1, 2, 6]  left_product done 
  //  answer: [24,12, 8, 6] right_product done
  
  right_product = 1;

  for (let i = nums.length - 1; i >= 0; i--) {
    answer[i] *= right_product;
    right_product *= nums[i];
  }

  return answer;
};
```

## C#

```csharp
public class Solution
{
    public int[] ProductExceptSelf(int[] nums)
    {
        int size = nums.Length;
        int[] answer = new int[size];
        Array.Fill(answer, 1);

        int leftProduct = 1;
        for (int i = 0; i < size; i++)
        {
            answer[i] = leftProduct;
            leftProduct *= nums[i];
        }

        //    nums: [1,  2, 3, 4]
        //  answer: [1,  1, 2, 6]  leftProduct done 
        //  answer: [24,12, 8, 6] rightProduct done

        int rightProduct = 1;
        for (int i = size - 1; i >= 0; i--)
        {
            answer[i] *= rightProduct;
            rightProduct *= nums[i];
        }

        return answer;
    }
}
```

## Go

```go
func productExceptSelf(nums []int) []int {
    n := len(nums)
    answer := make([]int, n)

    answer[0] = 1
    for i := 1; i < n; i++ {
        answer[i] = answer[i-1] * nums[i-1]
    }

    right := 1
    for i := n - 1; i >= 0; i-- {
        answer[i] *= right
        right *= nums[i]
    }

    return answer
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **进阶你的开发者身份**
>
> 掌握算法是成功的基石，而全方位展示你的才华则是获得垂青的关键。我们向你推荐 [**Show.dev**](https://www.show.dev) —— 专为程序员打造的“全能型”个人品牌展示平台。
>
> **三位一体（All-In-One）的职场利器：**
> - 📄 **专业简历 (Resume)：** 告别平庸，生成一份令猎头和面试官眼前一亮的动态技术简历。
> - 🎨 **作品集 (Portfolio)：** 自动聚合 GitHub 贡献与项目经历，将枯燥的代码转化为极具冲击力的视觉作品集。
> - ✍️ **技术博客 (Blog)：** 在纯净、专注的写作空间分享技术见解，树立你的行业影响力。
>
> [**立即前往 Show.dev 打造你的专属品牌 →**](https://www.show.dev)

---

访问原文链接：[238. 除自身以外数组的乘积 - LeetCode Python/Java/C++/JS/C#/Go/Ruby 题解](https://leetcode.blog/zh/leetcode/238-product-of-array-except-self)，体验更佳！

GitHub 仓库: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

