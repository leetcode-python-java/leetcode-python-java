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
- Each course can be abstracted as a vertex in a graph.
- The existence of a dependency relationship indicates that it is a directed graph.

## Approach 1
- Course A depends on course B, which can be abstracted as course A needs course B to unlock, and the in-degree of course A needs to be increased by 1.
- So an `in_degrees` array is needed to save the in-degree of each course.
- Courses with an in-degree of 0 can be studied first, so they can be put into a **queue** and processed one by one.
- Courses with an in-degree of 0 unlock other courses. This is the direction of the directed graph. Don't get it wrong.
- After each course is completed, the in-degree of other courses that depend on it is reduced by 1. If it is found that the in-degree of the course is 0 after deducting 1, the course is added to the queue.
- Which courses can be unlocked by a course need to be saved with a map or an array `courses_list`.
- If the in-degree of all courses is 0 at the end, return `true`, otherwise it means that there is a **cycle** in the directed graph, and return `false`.
- The above algorithm is a _breadth-first algorithm_.

## Approach 2
- Can you use a _depth-first algorithm_ to solve it?
- Simply replacing the queue used in the _breadth-first_ algorithm with a **stack** will create a _depth-first_ algorithm.

## Complexity
`V` is `vertices.length`.

`E` is `edges.length`.

* Time: `O(V + E)`.
* Space: `O(V + E)`.

## Python
### Solution 1: Breadth-First Search
```python
class Solution:
    def canFinish(self, num_courses: int, prerequisites: List[List[int]]) -> bool:
        in_degrees = [0] * num_courses
        courses_list = [set() for _ in range(num_courses)] # index: course, value: courses depending on course

        for prerequisite in prerequisites:
            in_degrees[prerequisite[0]] += 1
            courses_list[prerequisite[1]].add(prerequisite[0])

        ok_courses = collections.deque()

        for course, in_degree in enumerate(in_degrees):
            if in_degree == 0:
                ok_courses.append(course)

        while ok_courses:
            ok_course = ok_courses.popleft()

            for course in courses_list[ok_course]:
                in_degrees[course] -= 1
                
                if in_degrees[course] == 0:
                    ok_courses.append(course)

        return sum(in_degrees) == 0
```

### Solution 2: Depth-First Search
```python
class Solution:
    def canFinish(self, num_courses: int, prerequisites: List[List[int]]) -> bool:
        in_degrees = [0] * num_courses
        courses_list = [set() for _ in range(num_courses)] # index: course, value: courses depending on course

        for prerequisite in prerequisites:
            in_degrees[prerequisite[0]] += 1
            courses_list[prerequisite[1]].add(prerequisite[0])

        ok_courses = []

        for course, in_degree in enumerate(in_degrees):
            if in_degree == 0:
                ok_courses.append(course)

        while ok_courses:
            ok_course = ok_courses.pop()

            for course in courses_list[ok_course]:
                in_degrees[course] -= 1

                if in_degrees[course] == 0:
                    ok_courses.append(course)

        return sum(in_degrees) == 0
```

## Java
### Solution 1: Breadth-First Search
```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        var inDegrees = new int[numCourses];
        var coursesList = new ArrayList<HashSet<Integer>>(); // index: course, value: courses depending on course
        for (var i = 0; i < numCourses; i++) {
            coursesList.add(new HashSet<Integer>());
        }

        for (var prerequisite : prerequisites) {
            inDegrees[prerequisite[0]]++;

            var courses = coursesList.get(prerequisite[1]);
            courses.add(prerequisite[0]);
        }

        var okCourses = new ArrayDeque<Integer>();
        var studiedCourseCount = 0;

        for (var course = 0; course < inDegrees.length; course++) {
            if (inDegrees[course] == 0) {
                okCourses.add(course);
            }
        }

        while (!okCourses.isEmpty()) {
            var okCourse = okCourses.poll();
            studiedCourseCount++;

            for (var course : coursesList.get(okCourse)) {
                inDegrees[course]--;
                
                if (inDegrees[course] == 0) {
                    okCourses.add(course);
                }
            }
        }

        return studiedCourseCount == numCourses;
    }
}
```

### Solution 2: Depth-First Search
```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        var inDegrees = new int[numCourses];
        var coursesList = new ArrayList<HashSet<Integer>>(); // index: course, value: courses depending on course
        for (var i = 0; i < numCourses; i++) {
            coursesList.add(new HashSet<Integer>());
        }

        for (var prerequisite : prerequisites) {
            inDegrees[prerequisite[0]]++;

            var courses = coursesList.get(prerequisite[1]);
            courses.add(prerequisite[0]);
        }

        var okCourses = new Stack<Integer>();
        var studiedCourseCount = 0;

        for (var course = 0; course < inDegrees.length; course++) {
            if (inDegrees[course] == 0) {
                okCourses.push(course);
            }
        }

        while (!okCourses.isEmpty()) {
            var okCourse = okCourses.pop();
            studiedCourseCount++;

            for (var course : coursesList.get(okCourse)) {
                inDegrees[course]--;
                
                if (inDegrees[course] == 0) {
                    okCourses.push(course);
                }
            }
        }

        return studiedCourseCount == numCourses;
    }
}
```

## C++
### Solution 1: Breadth-First Search
```cpp
class Solution {
public:
    bool canFinish(int num_courses, vector<vector<int>>& prerequisites) {
        auto in_degrees = vector<int>(num_courses);
        auto courses_vector = vector<set<int>>(num_courses); // index: course, value: courses depending on course

        for (auto& prerequisite : prerequisites) {
            in_degrees[prerequisite[0]]++;

            courses_vector[prerequisite[1]].insert(prerequisite[0]);
        }

        queue<int> ok_courses;
        auto studied_course_count = 0;

        for (auto course = 0; course < in_degrees.size(); course++) {
            if (in_degrees[course] == 0) {
                ok_courses.push(course);
            }
        }

        while (!ok_courses.empty()) {
            auto okCourse = ok_courses.front();
            ok_courses.pop();
            studied_course_count++;

            for (auto course : courses_vector[okCourse]) {
                in_degrees[course]--;
                
                if (in_degrees[course] == 0) {
                    ok_courses.push(course);
                }
            }
        }

        return studied_course_count == num_courses;
    }
};
```

### Solution 2: Depth-First Search
```cpp
class Solution {
public:
    bool canFinish(int num_courses, vector<vector<int>>& prerequisites) {
        auto in_degrees = vector<int>(num_courses);
        auto courses_vector = vector<set<int>>(num_courses); // index: course, value: courses depending on course

        for (auto& prerequisite : prerequisites) {
            in_degrees[prerequisite[0]]++;

            courses_vector[prerequisite[1]].insert(prerequisite[0]);
        }

        stack<int> ok_courses;
        auto studied_course_count = 0;

        for (auto course = 0; course < in_degrees.size(); course++) {
            if (in_degrees[course] == 0) {
                ok_courses.push(course);
            }
        }

        while (!ok_courses.empty()) {
            auto okCourse = ok_courses.top();
            ok_courses.pop();
            studied_course_count++;

            for (auto course : courses_vector[okCourse]) {
                in_degrees[course]--;
                
                if (in_degrees[course] == 0) {
                    ok_courses.push(course);
                }
            }
        }

        return studied_course_count == num_courses;
    }
};
```

## JavaScript
```javascript
// Welcome to create a PR to complete the code of this language, thanks!
```

## C#
### Solution 1: Breadth-First Search
```c#
public class Solution {
    public bool CanFinish(int numCourses, int[][] prerequisites)
    {
        var inDegrees = new int[numCourses];
        var coursesList = new List<HashSet<int>>(); // index: course, value: courses depending on course
        
        for (int i = 0; i < numCourses; i++)
            coursesList.Add(new HashSet<int>());

        foreach (int[] prerequisite in prerequisites)
        {
            inDegrees[prerequisite[0]]++;

            var courses = coursesList[prerequisite[1]];
            courses.Add(prerequisite[0]);
        }

        var okCourses = new Queue<int>();
        int studiedCourseCount = 0;

        for (int course = 0; course < inDegrees.Length; course++)
        {
            if (inDegrees[course] == 0)
            {
                okCourses.Enqueue(course);
            }
        }

        while (okCourses.Count > 0)
        {
            int okCourse = okCourses.Dequeue();
            studiedCourseCount++;

            foreach (int course in coursesList[okCourse])
            {
                inDegrees[course]--;
                
                if (inDegrees[course] == 0)
                {
                    okCourses.Enqueue(course);
                }
            }
        }

        return studiedCourseCount == numCourses;
    }
}
```

### Solution 2: Depth-First Search
```c#
public class Solution {
    public bool CanFinish(int numCourses, int[][] prerequisites)
    {
        var inDegrees = new int[numCourses];
        var coursesList = new List<HashSet<int>>(); // index: course, value: courses depending on course

        for (int i = 0; i < numCourses; i++)
            coursesList.Add(new HashSet<int>());

        foreach (int[] prerequisite in prerequisites)
        {
            inDegrees[prerequisite[0]]++;

            var courses = coursesList[prerequisite[1]];
            courses.Add(prerequisite[0]);
        }

        var okCourses = new Stack<int>();
        int studiedCourseCount = 0;

        for (int course = 0; course < inDegrees.Length; course++)
        {
            if (inDegrees[course] == 0)
            {
                okCourses.Push(course);
            }
        }

        while (okCourses.Count > 0)
        {
            int okCourse = okCourses.Pop();
            studiedCourseCount++;

            foreach (int course in coursesList[okCourse])
            {
                inDegrees[course]--;
                
                if (inDegrees[course] == 0)
                {
                    okCourses.Push(course);
                }
            }
        }

        return studiedCourseCount == numCourses;
    }
}
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
