# 433. Minimum Genetic Mutation - Best Practices of LeetCode Solutions
LeetCode link: [433. Minimum Genetic Mutation](https://leetcode.com/problems/minimum-genetic-mutation), difficulty: **Medium**.

## LeetCode description of "433. Minimum Genetic Mutation"
A gene string can be represented by an 8-character long string, with choices from `A`, `C`, `G`, and `T`.

Suppose we need to investigate a mutation from a gene string `startGene` to a gene string `endGene` where one mutation is defined as one single character changed in the gene string.

* For example, `"AACCGGTT" --> "AACCGGTA"` is one mutation.

There is also a gene bank `bank` that records all the valid gene mutations. A gene must be in `bank` to make it a valid gene string.

Given the two gene strings `startGene` and `endGene` and the gene bank `bank`, return _the minimum number of mutations needed to mutate from `startGene` to `endGene`_. If there is no such a mutation, return `-1`.

Note that the starting point is assumed to be valid, so it might not be included in the bank.

### [Example 1]
**Input**: `startGene = "AACCGGTT", endGene = "AACCGGTA", bank = ["AACCGGTA"]`

**Output**: `1`

### [Example 2]
**Input**: `startGene = "AACCGGTT", endGene = "AAACGGTA", bank = ["AACCGGTA","AACCGCTA","AAACGGTA"]`

**Output**: `2`

### [Constraints]
- `0 <= bank.length <= 10`
- `startGene.length == endGene.length == bank[i].length == 8`
- `startGene`, `endGene`, and `bank[i]` consist of only the characters `['A', 'C', 'G', 'T']`.

## Intuition
This issue can be solved by **Breadth-First Search**.

### Breadth-First Search
![](../../images/binary_tree_BFS_1.gif)

* As shown in the figure above, **breadth-first search** can be thought of as visiting vertices in rounds and rounds. Actually, whenever you see a question is about
  getting `shortest` or `least` of something of a graph, `breadth-first search` would probably help.

* `breadth-first search` emphasizes first-in-first-out, so a **queue** is needed.

## Approach
1. `Breadth-First Search` a graph means traversing **from near to far**, from `circle 1` to `circle N`. Each `circle` is a round of iteration, but we can simplify it by using just 1 round.
1. So through `Breadth-First Search`, when a word matches `endWord`, the game is over, and we can return the number of **circle** as a result.

## Complexity
> **N** is the length of `bank`.

* Time: `O((8 * 4) * N)`.
* Space: `O(N)`.

## Python
```python
class Solution:
    def minMutation(self, start_gene: str, end_gene: str, bank: List[str]) -> int:
        if not end_gene in bank:
            return -1

        self.end_gene = end_gene
        self.bank = set(bank)
        self.queue = deque([start_gene])
        result = 0

        while self.queue:
            result += 1
            queue_size = len(self.queue)

            for i in range(queue_size):
                gene = self.queue.popleft()

                if self.mutate_one(gene):
                    return result

        return -1

    def mutate_one(self, gene):
        for i in range(len(gene)):
            for char in ['A', 'C', 'G', 'T']:
                if gene[i] == char:
                    continue

                mutation = f'{gene[:i]}{char}{gene[i + 1:]}'

                if mutation == self.end_gene:
                    return True

                if mutation in self.bank:
                    self.queue.append(mutation)
                    self.bank.remove(mutation)
```

## JavaScript
```javascript
// Welcome to create a PR to complete the code of this language, thanks!
```

## Java
```java
// Welcome to create a PR to complete the code of this language, thanks!
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## C#
```c#
// Welcome to create a PR to complete the code of this language, thanks!
```

## Go
```go
// Welcome to create a PR to complete the code of this language, thanks!
```

## Ruby
```ruby
# Welcome to create a PR to complete the code of this language, thanks!
```

## C, Kotlin, Swift, Rust or other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
