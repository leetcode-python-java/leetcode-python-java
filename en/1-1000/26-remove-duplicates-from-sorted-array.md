# 26. Remove Duplicates from Sorted Array - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
>
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.leader.me`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [26. Remove Duplicates from Sorted Array - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/26-remove-duplicates-from-sorted-array) for a better experience!

LeetCode link: [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array), difficulty: **Easy**.

## LeetCode description of "26. Remove Duplicates from Sorted Array"

Given an integer array `nums` sorted in **non-decreasing** order, remove the duplicates [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) such that each unique element appears only **once**. The **relative order** of the elements should be kept the **same**. Then return _the number of unique elements in `nums`_.

Consider the number of unique elements of `nums` to be `k`, to get accepted, you need to do the following things:

- Change the array `nums` such that the first `k` elements of `nums` contain the unique elements in the order they were present in `nums` initially. The remaining elements of `nums` are not important as well as the size of `nums`.
- Return `k`.

### [Example 1]

**Input**: `nums = [1,1,2]`

**Output**: `2, nums = [1,2,_]`

**Explanation**: 

<p>Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.</p>

<p>It does not matter what you leave beyond the returned k (hence they are underscores).</p>


### [Example 2]

**Input**: `nums = [0,0,1,1,1,2,2,3,3,4]`

**Output**: `5, nums = [0,1,2,3,4,_,_,_,_,_]`

**Explanation**: 

<p>Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.</p>

<p>It does not matter what you leave beyond the returned k (hence they are underscores).</p>


### [Constraints]

- `1 <= nums.length <= 3 * 10^4`
- `-10^4 <= nums[i] <= 10^4`
- `nums` is sorted in **non-decreasing** order.

### [Hints]

<details>
  <summary>Hint 1</summary>
  In this problem, the key point to focus on is the input array being sorted. As far as duplicate elements are concerned, what is their positioning in the array when the given array is sorted? Look at the image below for the answer. If we know the position of one of the elements, do we also know the positioning of all the duplicate elements?

  
</details>

<details>
  <summary>Hint 2</summary>
  We need to modify the array in-place and the size of the final array would potentially be smaller than the size of the input array. So, we ought to use a two-pointer approach here. One, that would keep track of the current element in the original array and another one for just the unique elements.

  
</details>

<details>
  <summary>Hint 3</summary>
  Essentially, once an element is encountered, you simply need to **bypass** its duplicates and move on to the next unique element.


  
</details>

## Intuition

The numbers in the array are already sorted, so any duplicate values must appear consecutively.

To remove duplicates, we need to keep every number that is different from the previous one, and discard the rest.

Since the array needs to be modified in place, two pointers are required: one moves fast and the other moves slow.

the fast pointer increases its position by 1 each time, while the slow pointer marks the current position to be modified.

## Pattern of "Fast & Slow Pointers Technique"

```java
int slow = 0; // slow pointer
// ...

for (int fast = 1; fast < array_length; fast++) { // This line is the key!
    if (condition_1) {
        // ...
        continue; // 'continue' is better than 'else' because 'else' will introduce more indents
    }

    if (condition_2) {
        // ...
        continue; // 'continue' is better than 'else'
    }

    // condition_3
    // ...
    slow++;
    // ...
}

return something;
```

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(1)`.

## Python

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        slow = 1

        # nums = [0,0,1,1,1,2,2,3,3,4]
        for fast in range(1, len(nums)):
            if nums[fast] == nums[slow - 1]:
                continue

            nums[slow] = nums[fast]
            slow += 1

        return slow

```

## Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer}
def remove_duplicates(nums)
  slow = 1

  # nums = [0,0,1,1,1,2,2,3,3,4]
  (1...nums.size).each do |fast|
    if nums[fast] == nums[slow - 1]
      next
    end

    nums[slow] = nums[fast]
    slow += 1
  end

  slow
end
```

## Java

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        var slow = 1;

        // nums = [0,0,1,1,1,2,2,3,3,4]
        for (var fast = 1; fast < nums.length; fast++) {
            if (nums[fast] != nums[slow - 1]) {
                nums[slow] = nums[fast];
                slow++;
            }
        }

        return slow;
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
> We recommend [**leader.me**](https://www.leader.me) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handle like `name.leader.me`.
>
> [**Build Your Programmer Brand at leader.me →**](https://www.leader.me)

---

Visit original link: [26. Remove Duplicates from Sorted Array - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/26-remove-duplicates-from-sorted-array) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

