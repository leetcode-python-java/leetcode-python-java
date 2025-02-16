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

## Intuition 1
We can think of this problem as a shortest path problem on a graph: there are `4^8` vertices (strings `'AAAAAAAA'` to `'TTTTTTTT'`), and there is an edge between two vertices if they differ in one character, and if *both* vertices are in `bank`.

So this issue can be solved by **Breadth-First Search** on a undirected graph.

![](../../images/binary_tree_BFS_1.gif)

* As shown in the figure above, **Breadth-First Search** can be thought of as visiting vertices in rounds and rounds. Actually, whenever you see a question is about
  getting `minimum number` of something of a graph, `Breadth-First Search` would probably help.

* `Breadth-First Search` emphasizes first-in-first-out, so a **queue** is needed.

### Approach 1: Breadth-First Search Algorithm
1. `Breadth-First Search` a graph means traversing **from near to far**, from `circle 1` to `circle N`. Each `circle` is a round of iteration.
1. So through `Breadth-First Search`, when a word matches `endGene`, the game is over, and we can return the number of **circle** as a result.

### Complexity
> **N** is the length of `bank`.

* Time: `O((8 * 4) * N)`.
* Space: `O(N)`.

## Approach 2: A* (A-Star) Search Algorithm

**A-Star Search Algorithm** can be used to greatly improve the performance of **Breadth-First Search Algorithm**.

Please view detailed **A-Star Algorithm** at [752. Open the Lock](./752-open-the-lock.md).

Bellow has code using _A-Star Search Algorithm_ in Python.

## Python
### Approach 1: Breadth-First Search (way 1)
```python
class Solution:
    def minMutation(self, start_gene: str, end_gene: str, bank: List[str]) -> int:
        if not end_gene in bank:
            return -1

        self.end_gene = end_gene
        self.bank = set(bank)
        self.queue = deque([start_gene]) # difference 1
        result = 0

        while self.queue:
            result += 1 # difference 2
            queue_size = len(self.queue)

            for i in range(queue_size): # difference 3
                gene = self.queue.popleft()

                if self.mutate_one(gene):
                    return result

        return -1

    def mutate_one(self, gene): # difference 4
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

### Approach 1: Breadth-First Search (way 2 by adding `mutated_count` in queue's item)
```python
class Solution:
    def minMutation(self, start_gene: str, end_gene: str, bank: List[str]) -> int:
        if not end_gene in bank:
            return -1

        self.bank = set(bank)
        self.end_gene = end_gene
        self.queue = deque([(start_gene, 0)]) # difference 1

        while self.queue:
            gene, mutated_count = self.queue.popleft() # difference 2

            if self.mutate_one(gene, mutated_count):
                return mutated_count + 1

        return -1

    def mutate_one(self, gene, mutated_count): # difference 3
        for i in range(len(gene)):
            for char in ['A', 'C', 'G', 'T']:
                if gene[i] == char:
                    continue

                mutation = f'{gene[:i]}{char}{gene[i + 1:]}'

                if mutation == self.end_gene:
                    return True

                if mutation in self.bank:
                    self.queue.append((mutation, mutated_count + 1))
                    self.bank.remove(mutation)
```

### Approach 2: A* (A-Star) Search Algorithm
```python
import heapq


class Solution:
    def minMutation(self, start_gene: str, end_gene: str, bank: List[str]) -> int:
        if not end_gene in bank:
            return -1

        self.end_gene = end_gene
        bank = set(bank)
        priority_queue = [(self.distance(start_gene), start_gene, 0)] # difference 1

        while priority_queue:
            _, gene, mutated_count = heapq.heappop(priority_queue) # difference 2

            for i in range(len(gene)):
                for char in ['A', 'C', 'G', 'T']:
                    if gene[i] == char:
                        continue

                    mutation = f'{gene[:i]}{char}{gene[i + 1:]}'

                    if mutation == end_gene:
                        return mutated_count + 1

                    if mutation in bank:
                        heapq.heappush(
                            priority_queue,
                            (self.distance(mutation), mutation, mutated_count + 1)
                        ) # difference 3
                        bank.remove(mutation)

        return -1

    def distance(self, gene): # difference 4
        result = 0
        
        for i in range(8):
            if gene[i] != self.end_gene[i]:
                result += 1

        return result
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
