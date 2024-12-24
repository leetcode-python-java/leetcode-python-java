# 207. Course Schedule - LeetCode Solution
LeetCode problem link: [207. Course Schedule](https://leetcode.com/problems/course-schedule)

## LeetCode problem description
There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

* For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

### Example 1
```ruby
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
```

### Example 2
```ruby
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
```

### Constraints
- `1 <= numCourses <= 2000`
- `0 <= prerequisites.length <= 5000`
- `prerequisites[i].length == 2`
- `0 <= ai, bi < numCourses`
- All the pairs `prerequisites[i]` are **unique**.

## Intuition
- Each course can be abstracted as a vertex in the graph.
- The existence of a dependency relationship indicates that it is a directed graph.

## Approach
- Course A depends on course B, which can be abstracted as course A needs course B to unlock, and the in-degree of course A needs to be increased by 1.
- So an `in_degrees` array is needed to save the in-degree of each course.
- Courses with an in-degree of 0 can be studied first, so courses with an in-degree of 0 can be put into a **queue** and processed one by one.
- After each course is completed, the in-degree of other courses that depend on it is reduced by 1. If it is found that the in-degree of the course is 0 after deducting 1, the course is added to the queue.
- Courses with an in-degree of 0 unlock other courses. This is the direction of the directed graph. Don't get it wrong.
- Which courses can be unlocked by a course need to be saved with a `course_map`.
- If the in-degree of all courses is 0 at the end, return `true`, otherwise it means that there is a **cycle** in the directed graph, and return `false`.
- The above algorithm is a _breadth-first algorithm_.
- You can also use a _depth-first algorithm_. Please think about it yourself. The answer will be given below.

## Complexity
`V` is `vertices.length`.

`E` is `edges.length`.

* Time: `O(V + E)`.
* Space: `O(V + E)`.

## Java
```java
// Solution is from Coding5DotCom
```

## Python
### Solution 1: Breadth-First Search
```pyhton
class Solution:
    def canFinish(self, num_courses: int, prerequisites: List[List[int]]) -> bool:
        in_degrees = [0] * num_courses
        course_map = collections.defaultdict(set) # {key: course, value: courses depending on key}

        for prerequisite in prerequisites:
            in_degrees[prerequisite[0]] += 1
            course_map[prerequisite[1]].add(prerequisite[0])

        free_courses = collections.deque()

        for course, in_degree in enumerate(in_degrees):
            if in_degree == 0:
                free_courses.append(course)

        while free_courses:
            free_course = free_courses.popleft()

            for course in course_map[free_course]:
                in_degrees[course] -= 1
                
                if in_degrees[course] == 0:
                    free_courses.append(course)

        return sum(in_degrees) == 0
```

### Solution 2: Depth-First Search
```python
class Solution:
    def canFinish(self, num_courses: int, prerequisites: List[List[int]]) -> bool:
        in_degrees = [0] * num_courses
        course_map = collections.defaultdict(set) # {key: course, value: courses depending on key}

        for prerequisite in prerequisites:
            in_degrees[prerequisite[0]] += 1
            course_map[prerequisite[1]].add(prerequisite[0])
        
        free_courses = []

        for course, in_degree in enumerate(in_degrees):
            if in_degree == 0:
                free_courses.append(course)

        while free_courses:
            free_course = free_courses.pop()

            for course in course_map[free_course]:
                in_degrees[course] -= 1
                
                if in_degrees[course] == 0:
                    free_courses.append(course)

        return sum(in_degrees) == 0
```

## C++
```cpp
// Welcome to create a PR to complete the code of this language, thanks!
```

## JavaScript
```javascript
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

## C
```c
// Welcome to create a PR to complete the code of this language, thanks!
```

## Kotlin
```kotlin
// Welcome to create a PR to complete the code of this language, thanks!
```

## Swift
```swift
// Welcome to create a PR to complete the code of this language, thanks!
```

## Rust
```rust
// Welcome to create a PR to complete the code of this language, thanks!
```

## Other languages
```
// Welcome to create a PR to complete the code of this language, thanks!
```
