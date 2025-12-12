# 88. Merge Sorted Array - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**Like.dev**](https://www.like.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Like.dev →**](https://www.like.dev)

---

Visit original link: [88. Merge Sorted Array - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/88-merge-sorted-array) for a better experience!

LeetCode link: [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array), difficulty: **Easy**.

## LeetCode description of "88. Merge Sorted Array"

You are given two integer arrays `nums1` and `nums2`, sorted in **non-decreasing** order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

**Merge** `nums1` and `nums2` into a single array sorted in **non-decreasing** order.

The final sorted array should not be returned by the function, but instead be stored inside the array `nums1`. To accommodate this, `nums1` has a length of `m + n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to `0` and should be ignored. `nums2` has a length of `n`.

### [Example 1]

**Input**: `nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3`

**Output**: `[1,2,2,3,5,6]`

**Explanation**: 

<p>The arrays we are merging are [1,2,3] and [2,5,6].<br>
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.</p>


### [Example 2]

**Input**: `nums1 = [1], m = 1, nums2 = [], n = 0`

**Output**: `[1]`

**Explanation**: 

<p>The arrays we are merging are [1] and [].<br>
The result of the merge is [1].</p>


### [Example 3]

**Input**: `nums1 = [0], m = 0, nums2 = [1], n = 1`

**Output**: `[1]`

**Explanation**: 

<p>The arrays we are merging are [] and [1].<br>
The result of the merge is [1].<br>
Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.</p>


### [Constraints]

- `nums1.length == m + n`
- `nums2.length == n`
- `0 <= m, n <= 200`
- `1 <= m + n <= 200`
- `-10^9 <= nums1[i], nums2[j] <= 10^9`

Follow up: Can you come up with an algorithm that runs in `O(m + n)` time?



## Intuition

- This problem can be solved by using the built-in `sort()` method of a programming language to sort the array, which is very simple to implement. However, the time complexity of this approach is `O(n log n)`.
- That’s why this problem usually restricts the time complexity to `O(n)`. How can we achieve `O(n)`?
- We need to consider the given conditions. Both arrays are already sorted, and this condition must be leveraged.
- When reorganizing the arrays, we can either place the numbers in order from left to right, or from right to left. Which direction should we choose?
- If you don’t ask yourself this question, you’d normally just go left to right. But in that case, a problem arises: if the current number in `nums1` is not the smallest, it can’t be directly replaced and needs to be stored somewhere temporarily. A simple workaround is to create a new empty array to hold the final result, and then copy that array back into `nums1`. But this increases the amount of code you need to write.
- Therefore, it’s better to place the numbers in order from right to left.

## Complexity

- Time complexity: `m + n`.
- Space complexity: `m + n`.

## Python

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        # Make a good example first.
        # nums1: [1, 5, 7, 0, 0, 0, 0]
        # nums2: [2, 3, 4, 8]
        # result:[1, 2, 3, 4, 5, 7, 8]
        i = m - 1
        j = n - 1

        for k in range(len(nums1) - 1, -1, -1):
            if i < 0 or (j >= 0 and nums2[j] > nums1[i]):
                nums1[k] = nums2[j]
                j -= 1
            else:
                nums1[k] = nums1[i]
                i -= 1
```

## Ruby

```ruby
# @param {Integer[]} nums1
# @param {Integer} m
# @param {Integer[]} nums2
# @param {Integer} n
# @return {Void} Do not return anything, modify nums1 in-place instead.
def merge(nums1, m, nums2, n)
  # Make a good example first.
  # nums1: [1, 5, 7, 0, 0, 0, 0]
  # nums2: [2, 3, 4, 8]
  # result:[1, 2, 3, 4, 5, 7, 8]
  i = m - 1
  j = n - 1

  (nums1.size - 1).downto(0) do |k|
    if i < 0 || (j >= 0 and nums2[j] > nums1[i])
      nums1[k] = nums2[j]
      j -= 1
    else
      nums1[k] = nums1[i]
      i -= 1
    end
  end
end

```

## Java

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        // Make a good example first.
        // nums1: [1, 5, 7, 0, 0, 0, 0]
        // nums2: [2, 3, 4, 8]
        // result:[1, 2, 3, 4, 5, 7, 8]

        var i = m - 1;
        var j = n - 1;

        for (var k = nums1.length - 1; k >= 0; k--) {
            if (i < 0 || (j >= 0 && nums2[j] > nums1[i])) {
                nums1[k] = nums2[j];
                j--;
            } else {
                nums1[k] = nums1[i];
                i--;
            }
        }
    }
}
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**Like.dev**](https://www.like.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Like.dev →**](https://www.like.dev)

---

Visit original link: [88. Merge Sorted Array - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/88-merge-sorted-array) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

