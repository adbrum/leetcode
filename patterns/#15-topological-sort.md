# 15) Topological Sort

**When to use:**
* Problems involving dependencies between items.
* Scheduling tasks with prerequisites.
* Detecting cycles in a directed graph.

## Example Problem: [Course Schedule](https://leetcode.com/problems/course-schedule/)

* **Input:** `numCourses = 2, prerequisites = [[1,0]]`
* **Output:** `true`

## Solution (O(V + E) / O(V + E))

```python
from collections import deque

def canFinish(numCourses, prerequisites):
    adj = [[] for _ in range(numCourses)]
    indegree = [0] * numCourses
    
    for course, prereq in prerequisites:
        adj[prereq].append(course)
        indegree[course] += 1
        
    queue = deque([i for i, deg in enumerate(indegree) if deg == 0])
    count = 0
    
    while queue:
        course = queue.popleft()
        count += 1
        for neighbor in adj[course]:
            indegree[neighbor] -= 1
            if indegree[neighbor] == 0:
                queue.append(neighbor)
                
    return count == numCourses
```

## Complexity:

* **Time:** `O(V + E)` where V is the number of vertices and E is the number of edges.
* **Space:** `O(V + E)` for the adjacency list and the queue.

---

## Step-by-step:

1.  Build an adjacency list and an in-degree array from the prerequisites.
2.  Initialize a queue with all courses that have an in-degree of 0.
3.  Initialize a counter for the number of courses taken.
4.  While the queue is not empty:
    *   Dequeue a course.
    *   Increment the counter.
    *   For each of its neighbors, decrement their in-degree.
    *   If a neighbor's in-degree becomes 0, enqueue it.
5.  If the counter is equal to the number of courses, it means all courses can be taken. Otherwise, there is a cycle.

---

## 🎯 Other Typical Problems

| Problem | Difficulty | Link |
|---|---|---|
| [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/) | Medium | [Link](https://leetcode.com/problems/course-schedule-ii/) |
| [Alien Dictionary](https://leetcode.com/problems/alien-dictionary/) | Hard | [Link](https://leetcode.com/problems/alien-dictionary/) |
| [Minimum Height Trees](https://leetcode.com/problems/minimum-height-trees/) | Medium | [Link](https://leetcode.com/problems/minimum-height-trees/) |
