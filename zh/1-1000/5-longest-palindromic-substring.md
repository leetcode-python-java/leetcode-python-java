# 5. 最长回文子串 - 力扣Python/Java/C++等题解

访问原文链接：[5. 最长回文子串 - 力扣Python/Java/C++等题解](https://leetcodepython.com/zh/leetcode/5-longest-palindromic-substring)，体验更佳！

力扣链接：[5. 最长回文子串](https://leetcode.cn/problems/longest-palindromic-substring), 难度：**中等**。

## 力扣“5. 最长回文子串”问题描述

给你一个字符串 `s`，找到 `s` 中最长的 **回文子串**。

- **回文性**：如果字符串向前和向后读都相同，则它满足 **回文性**。
- **子字符串** 是字符串中连续的 **非空** 字符序列。

### [示例 1]

**输入**: `s = "babad"`

**输出**: `"bab"`

**解释**: `"aba" 同样是符合题意的答案。`

### [示例 2]

**输入**: `s = "cbbd"`

**输出**: `"bb"`

### [约束]

- `1 <= s.length <= 1000`
- `s` 仅由数字和英文字母组成

### [Hints]

<details>
  <summary>提示 1</summary>
  How can we reuse a previously computed palindrome to compute a larger palindrome?

  
</details>

<details>
  <summary>提示 2</summary>
  If “aba” is a palindrome, is “xabax” a palindrome? Similarly is “xabay” a palindrome?

  
</details>

<details>
  <summary>提示 3</summary>
  Complexity based hint:
If we use brute-force and check whether for every start and end position a substring is a palindrome we have O(n^2) start - end pairs and O(n) palindromic checks. Can we reduce the time for palindromic checks to O(1) by reusing some previous computation.

  
</details>

## 思路



## “动态规划”的模式

“动态规划”，需要用`dp`数组来保存结果。`dp[i][j]`的值可以由它的前一个（或多个）值通过公式转化出来。因此，`dp[i][j]`值是一步一步推导出来的，它和先前的`dp`记录值都有联系。

#### “动态规划”分为五步

1. 确定数组`dp`的每个值代表的含义。
2. 初始化数组`dp`的值。
3. 根据一个示例，“按顺序”填入`dp`网格数据。
4. 根据`dp`网格数据，推导出“递推公式”。
5. 写出程序，并打印`dp`数组，不合预期就调整。

#### 细说这五步

1. 确定数组`dp`的每个值代表的含义。
    - 先确定`dp`是一维数组还是二维数组。“一维滚动数组”意味着每次迭代时都会覆盖数组的值。大多时候，用“一维滚动数组”代替“二维数组”可以简化代码；但有些题目，比如要操作“两个对等数组”，为了理解方便，还是使用“二维数组”。
    - 尝试使用问题所求的`返回值`的含义作为 `dp[i]`（一维）或`dp[i][j]`（二维）的含义，约60%的概率能行。如果不行，再尝试其他含义。
    - 设计上尽量考虑保存更丰富的信息，重复信息只在某个`dp[i]`中保存一次就够了。
    - 使用简化的含义。如果用`布尔值`可以解决问题，就不要用`数值`。
2. 初始化数组`dp`的值。`dp`的值涉及两个层面：
    1. `dp`的长度。通常是：`条件数组长度加1`或`条件数组长度`。
    2. `dp[i]`或`dp[i][j]`的值。`dp[0]`或`dp[0][0]`有时需要特殊处理。
3. 根据一个示例，“按顺序”填入`dp`网格数据。
    - “递推公式”是“动态规划”算法的核心。但“递推公式”是隐晦的，想得到它，就需要制表，用数据启发自己。
    - 如果原示例不够好，需要自己重新设计一个。
    - 根据示例，填入`dp`网格数据，需要“按顺序”填，这是很重要的，因为它决定了代码的遍历顺序。
    - 大多时候，从左到右，从上到下。但有时需要从右向左、由下而上、从中间向右（或左），如“回文串”问题。有时，还需要一行遍历两次，先正向，再反向。
    - 当顺序决定对了，起点就决定好了，从起点出发，“按顺序”填写`dp`网格数据，这也是在模拟程序处理的过程。
    - 在此过程中，您将获得写出“递推公式”的灵感。如果您已经能推导出公式，不需要填完网格。
4. 根据`dp`网格数据，推导出“递推公式”。
    - 有三个特别的位置需要注意： `dp[i - 1][j - 1]`、`dp[i - 1][j]`和`dp[i][j - 1]`，当前的 `dp[i][j]`往往取决于它们。
    - 操作“两个对等数组”时，因为对称性，我们可能需要同时使用`dp[i - 1][j]`和`dp[i][j - 1]`。
5. 写出程序，并打印`dp`数组，不合预期就调整。
    - 重点分析那些不合预期的数值。

读完了上面的内容，是不是感觉“动态规划”也没有那么难了？试着解出这道题吧。🤗

## 复杂度

- 时间复杂度: ``.
- 空间复杂度: ``.

## Ruby

```ruby
# @param {String} s
# @return {String}
def longest_palindrome(s)
  longest = s[0]
  s = s.chars.join("#")

  s.size.times do |i|
    j = 1

    while j <= i and i + j < s.size
      break if s[i - j] != s[i + j]

      if s[i - j] == '#'
        j += 1
        next
      end
      
      length = j * 2 + 1

      if length > longest.size
        longest = s[i - j..i + j]
      end
      
      j += 1
    end
  end
  
  longest.gsub('#', '')
end
```

## Other languages

```java
// Welcome to create a PR to complete the code of this language, thanks!
```

亲爱的力扣人，为了您更好的刷题体验，请访问 [LeetCodePython.com](https://leetcodepython.com/zh)。
本站敢称力扣题解最佳实践，终将省你大量刷题时间！

原文链接：[5. 最长回文子串 - 力扣Python/Java/C++等题解](https://leetcodepython.com/zh/leetcode/5-longest-palindromic-substring).

GitHub 仓库: [f*ck-leetcode](https://github.com/fuck-leetcode/fuck-leetcode).

