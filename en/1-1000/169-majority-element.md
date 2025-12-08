# 169. Majority Element - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions

> 🚀 **Level Up Your Developer Identity**
>
> While mastering algorithms is key, showcasing your talent is what gets you hired.
> We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [169. Majority Element - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/169-majority-element) for a better experience!

LeetCode link: [169. Majority Element](https://leetcode.com/problems/majority-element), difficulty: **Easy**.

## LeetCode description of "169. Majority Element"

Given an array `nums` of size `n`, return _the majority element_.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

### [Example 1]

**Input**: `nums = [3,2,3]`

**Output**: `3`

### [Example 2]

**Input**: `nums = [2,2,1,1,1,2,2]`

**Output**: `2`

### [Constraints]

- `n == nums.length`
- `1 <= n <= 5 * 10^4`
- `-10^9 <= nums[i] <= 10^9`

**Follow-up**: Could you solve the problem in linear time and in `O(1)` space?

### [Hints]

<details>
  <summary>Hint 1</summary>
  How to solve the problem in `O(1)` space?

Please search `Boyer-Moore majority vote algorithm`.

  
</details>

## Intuition

The key to solving this problem is to use a hash table to store the occurrence count of each `num`. The `key` is the `num`, and the `value` is the number of times it appears.

## Complexity

- Time complexity: `O(N)`.
- Space complexity: `O(N)`.

## Python

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        num_to_count = defaultdict(int)

        for num in nums:
            num_to_count[num] += 1
            if num_to_count[num] >= len(nums) / 2:
                return num

```

## Ruby

```ruby
# @param {Integer[]} nums
# @return {Integer}
def majority_element(nums)
  num_to_count = Hash.new(0)

  nums.each do |num|
    num_to_count[num] += 1

    if num_to_count[num] > nums.size / 2
      return num
    end
  end
end
```

## Java

```java
class Solution {
    public int majorityElement(int[] nums) {
        Map<Integer, Integer> numToCount = new HashMap<>();

        for (int num : nums) {
            numToCount.put(num, numToCount.getOrDefault(num, 0) + 1);

            if (numToCount.get(num) > nums.length / 2) {
                return num;
            }
        }

        return -1; // This line won't be reached due to problem constraints
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
> We recommend [**Show.dev**](https://www.show.dev) — the ultimate all-in-one personal branding platform for programmers.
>
> **The All-In-One Career Powerhouse:**
> - 📄 **Resume, Portfolio & Blog:** Integrate your skills, GitHub projects, and writing into one stunning site.
> - 🌐 **Free Custom Domain:** Bind your own personal domain for free—forever.
> - ✨ **Premium Subdomains:** Stand out with elite tech handles like `name.cto.page` or `name.engineer.dev`.
> - 🔗 **Cool Short Links:** Get sleek, memorable bio-links like `is.bio/yourname` and `an.dev/yourname`.
>
> [**Build Your Programmer Brand at Show.dev →**](https://www.show.dev)

---

Visit original link: [169. Majority Element - LeetCode Python/Java/C++/JS/C#/Go/Ruby Solutions](https://leetcode.blog/en/leetcode/169-majority-element) for a better experience!

GitHub repository: [leetcode-python-java](https://github.com/leetcode-python-java/leetcode-python-java).

