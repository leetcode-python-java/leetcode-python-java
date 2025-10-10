# 238. Product of Array Except Self - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

Visit original link: [238. Product of Array Except Self - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/238-product-of-array-except-self) for a better experience!

LeetCode link: [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self), difficulty: **Medium**.

## LeetCode description of "238. Product of Array Except Self"

Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and **without using the division operation**.

### [Example 1]

**Input**: `nums = [1,2,3,4]`

**Output**: `[24,12,8,6]`

### [Example 2]

**Input**: `nums = [-1,1,0,-3,3]`

**Output**: `[0,0,9,0,0]`

### [Constraints]

- `2 <= nums.length <= 10^5`
- `-30 <= nums[i] <= 30`
- The input is generated such that `answer[i]` is **guaranteed** to fit in a **32-bit** integer.


**Follow up**: Can you solve the problem in `O(1)` extra space complexity? (The output array **does not** count as extra space for space complexity analysis.)

### [Hints]

<details>
  <summary>Hint 1</summary>
  Think how you can efficiently utilize prefix and suffix products to calculate the product of all elements except self for each index. Can you pre-compute the prefix and suffix products in linear time to avoid redundant calculations?


  
</details>

<details>
  <summary>Hint 2</summary>
  Can you minimize additional space usage by reusing memory or modifying the input array to store intermediate results?

  
</details>

## Intuition 1

1. **Decompose the Problem**: Break down the `product except self` into `left product × right product`
2. **Two Passes**:
    - First pass: Calculate the left product for each element
    - Second pass: Calculate the right product for each element
3. **Combine Results**: Multiply left and right products to get the final result

## Pattern of "Pre-Computation Techniques"

**Pre-Computation Techniques** are an optimization method that reduces real-time computational overhead by calculating and storing intermediate or frequently used data in advance. The core idea is **"trade space for time."**

#### Key Application Scenarios

- **Prefix/Suffix computation problems** for arrays.
- **High-frequency computation problems**: Such as Fibonacci sequences, factorials, prime number tables, etc., which avoid repetitive calculations by pre-generating lookup tables.
- **Dynamic Programming (DP)**: Pre-computing and storing solutions to sub-problems, e.g., the `knapsack problem` or `shortest path problems`.

## Step-by-Step Solution

1. **Initialize Arrays**:
    - Create a `leftProducts` array to store the product of all elements to the left of each element
    - Create a `rightProducts` array to store the product of all elements to the right of each element

2. **Compute Left Products** (Left to Right Pass):
    - The left product of the first element is initialized to `1`
    - For subsequent elements: `leftProducts[i] = nums[i-1] * leftProducts[i-1]`

3. **Compute Right Products** (Right to Left Pass):
    - The right product of the last element is initialized to `1`
    - For previous elements: `rightProducts[i] = nums[i+1] * rightProducts[i+1]`

4. **Combine Results**:
    - For each position, multiply left and right products: `answer[i] = leftProducts[i] * rightProducts[i]`

5. **Return the Result Array**

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(N)`.

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

## Intuition 2

1. **Space Optimization**: Utilize the output array to store intermediate results, avoiding extra space
2. **Two-Phase Calculation**: First compute left products and store in the result, then dynamically compute right products and merge directly
3. **In-Place Operation**: Use only a single variable to dynamically maintain the right product

## Step-by-Step Solution

1. **Initialize Result Array**:
    - Create an `answer` array of the same size, initialized with all 1s

2. **Compute Left Products** (Left → Right Pass):
    - Initialize `left_product = 1`
    - During traversal: `answer[i] = left_product`, then `left_product *= nums[i]`

3. **Compute Right Products and Merge** (Right → Left Pass):
    - Initialize `right_product = 1`
    - During traversal: `answer[i] *= right_product`, then `right_product *= nums[i]`

4. **Return Result Array**
    - Space Complexity: O(1) (Output array not counted in space complexity)

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

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

Dear LeetCoders! For a better LeetCode problem-solving experience, please visit website [LeetCode.blog](https://leetcode.blog): Dare to claim the best practices of LeetCode solutions! Will save you a lot of time!

Original link: [238. Product of Array Except Self - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/238-product-of-array-except-self).

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).
