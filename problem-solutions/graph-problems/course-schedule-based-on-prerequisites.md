# Course Schedule based on Prerequisites

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/prerequisite-tasks/1#)
* [Leetcode 207](https://leetcode.com/problems/course-schedule/)

### Companies

* [Google](../../company-based-lists/google.md)
* [Facebook](../../company-based-lists/facebook.md)
* [Apple](../../company-based-lists/apple.md)
* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

* For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

**Example 1:**

```text
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: 
There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
```

**Example 2:**

```text
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: 
There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should 
also have finished course 1. So it is impossible.
```

**Constraints:**

* `1 <= numCourses <= 10^5`
* `0 <= prerequisites.length <= 5000`
* `prerequisites[i].length == 2`
* `0 <= ai, bi < numCourses`
* All the pairs prerequisites\[i\] are **unique**.

## Solution

### My Approach

```cpp
class Solution {
public:
    vector<vector<int>> dependents;   // courses that depends on this course to be completed
    vector<int> depended_on; // No. of courses this course depends on
    
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        dependents.resize(numCourses, vector<int>());
        depended_on.resize(numCourses,0);
        
        for(vector<int>& prerequisite : prerequisites)
        {
            dependents[prerequisite[1]].push_back(prerequisite[0]);
            depended_on[prerequisite[0]]++;
        }
        
        // Find a nodes with no pre-requisite and complete as many courses as possible
        int courses_completed = 0;
        vector<bool> visited(numCourses, false);
        bool valid_loop = true; // To avoid infinite loop when we can't complete any more course
        
        while(courses_completed < numCourses && valid_loop)
        {
            int old_courses_completed = courses_completed;
            
            for(int course = 0; course < numCourses; course++)
                if(depended_on[course] == 0 && visited[course] == false)
                    DFS(course, visited, courses_completed);

            valid_loop = (old_courses_completed != courses_completed);
        }
        return courses_completed == numCourses;
    }

    void DFS(int course, vector<bool>&visited, int &courses_completed)
    {   
        visited[course] = true;
        courses_completed++;
        
        // Reduce dependency count for all dependents of this course
        for(int &dependent :dependents[course])
            if(visited[dependent] == false)
                depended_on[dependent]--;
    
        // If any course dependency became 0, schedule it
        for(int &dependent :dependents[course])
        {
            if(depended_on[dependent] == 0 && visited[dependent] == false)    
                DFS(dependent, visited, courses_completed);
        }   
    }
};
```

