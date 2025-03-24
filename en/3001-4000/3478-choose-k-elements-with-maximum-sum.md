Original link: [leetcoder.net - LeetCoder: Fucking Good LeetCode Solutions](https://leetcoder.net/en/leetcode/3478-choose-k-elements-with-maximum-sum)

# 3478. Choose K Elements With Maximum Sum - LeetCoder: Fucking Good LeetCode Solutions

LeetCode link: [3478. Choose K Elements With Maximum Sum](https://leetcode.com/problems/choose-k-elements-with-maximum-sum), Difficulty: **Medium**.

## LeetCode description of "3478. Choose K Elements With Maximum Sum"

You are given two integer arrays, `nums1` and `nums2`, both of length `n`, along with a positive integer `k`.

For each index `i` from `0` to `n - 1`, perform the following:

- Find all indices `j` where `nums1[j]` is less than `nums1[i]`.
- Choose at most `k` values of `nums2[j]` at these indices to maximize the total sum.

Return an array `answer` of size `n`, where `answer[i]` represents the result for the corresponding index `i`.

### [Example 1]

**Input**: `nums1 = [4,2,1,5,3], nums2 = [10,20,30,40,50], k = 2`

**Output**: `[80,30,0,80,50]`

**Explanation**: 

```
- For `i = 0`: Select the 2 largest values from `nums2` at indices `[1, 2, 4]` where `nums1[j] < nums1[0]`, resulting in `50 + 30 = 80`.
- For `i = 1`: Select the 2 largest values from `nums2` at index `[2]` where `nums1[j] < nums1[1]`, resulting in `30`.
- For `i = 2`: No indices satisfy `nums1[j] < nums1[2]`, resulting in `0`.
- For `i = 3`: Select the 2 largest values from `nums2` at indices `[0, 1, 2, 4]` where `nums1[j] < nums1[3]`, resulting in `50 + 30 = 80`.
- For `i = 4`: Select the 2 largest values from `nums2` at indices `[1, 2]` where `nums1[j] < nums1[4]`, resulting in `30 + 20 = 50`.
```

### [Example 2]

**Input**: `nums1 = [2,2,2,2], nums2 = [3,1,2,3], k = 1`

**Output**: `[0,0,0,0]`

**Explanation**: 

```
Since all elements in `nums1` are equal, no indices satisfy the condition `nums1[j] < nums1[i]` for any `i`, resulting in `0` for all positions.
```

### [Constraints]

- `n == nums1.length == nums2.length`
- `1 <= n <= 10^5`
- `1 <= nums1[i], nums2[i] <= 10^6`
- `1 <= k <= n`

### [Hints]

<details>
  <summary>Hint 1</summary>
  Sort `nums1` and its corresponding `nums2` values together based on `nums1`.

  
</details>

<details>
  <summary>Hint 2</summary>
  Use a max heap to track the top `k` values of `nums2` as you process each element in the sorted order.

  
</details>

## Intuition

* Seeing this, everyone will definitely think of sorting `nums1` from small to large, so that the front is less than or equal to the back, but the indexes will be **messy** when sorting. If there is no good way to solve this problem, the whole question cannot be solved. Please think about it first.

    <details><summary>Click to view the answer</summary><p> Bring the `index` when sorting, that is, the object to be sorted is an array of tuples of `(num, index)`. This technique **must be mastered**, as it will be used in many questions.</p></details>

    After solving the above problems, the indexes are all there, let's continue reading:

* Requirement 2: Choose at most `k` values of `nums2[j]` at these indices to **maximize** the total sum.

    After seeing this, have you thought of any good method?

    <details><summary>Click to view the answer</summary><p> Heap sort, maintain a large root heap of size `k`. This is also a knowledge point that is often tested, **must be mastered**. </p></details>

    Seeing this, please implement the code according to the above prompts.

* Finally, it is found that the repeated `num` that appear continuously should be specially processed, that is, the values ​​in `answer` corresponding to the same `num` should be the same. There are many ways to deal with it. What is the simplest way to deal with it?

    <details><summary>Click to view the answer</summary><p> Use a `Map`, `key` is `num`, and the same `key` directly uses the `value` corresponding to `key`. </p></details>

## Complexity

- Time complexity: `O(N * logN)`.
- Space complexity: `O(N)`.

## Python

```python
class Solution:
    def findMaxSum(self, nums1: List[int], nums2: List[int], k: int) -> List[int]:
        num_index_list = [(num, index) for index, num in enumerate(nums1)] # key 1
        num_index_list.sort()

        answer = [None] * len(nums1)
        k_max_nums = []
        sum_ = 0
        num_to_sum = defaultdict(int) # key 2

        for i, num_index in enumerate(num_index_list):
            num, index = num_index

            if num in num_to_sum:
                answer[index] = num_to_sum[num]
            else:
                answer[index] = sum_
                num_to_sum[num] = sum_

            heapq.heappush(k_max_nums, nums2[index])
            sum_ += nums2[index]

            if len(k_max_nums) > k:
                num = heapq.heappop(k_max_nums) # key 3
                sum_ -= num

        return answer
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

