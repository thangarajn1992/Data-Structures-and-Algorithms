# Maximum Profit in Job Scheduling

### Source

* [Leetcode 1235](https://leetcode.com/problems/maximum-profit-in-job-scheduling/)

### Companies



### Problem Statement

We have `n` jobs, where every job is scheduled to be done from `startTime[i]` to `endTime[i]`, obtaining a profit of `profit[i]`.

You're given the `startTime`, `endTime` and `profit` arrays, return the maximum profit you can take such that there are no two jobs in the subset with overlapping time range.

If you choose a job that ends at time `X` you will be able to start another job that starts at time `X`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/10/10/sample1_1584.png)

```text
Input: startTime = [1,2,3,3], endTime = [3,4,5,6], profit = [50,10,40,70]
Output: 120
Explanation: The subset chosen is the first and fourth job. 
Time range [1-3]+[3-6] , we get profit of 120 = 50 + 70.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/10/10/sample22_1584.png)

```text
Input: startTime = [1,2,3,4,6], endTime = [3,5,10,6,9], profit = [20,20,100,70,60]
Output: 150
Explanation: The subset chosen is the first, fourth and fifth job. 
Profit obtained 150 = 20 + 70 + 60.
```

**Example 3:**

![](https://assets.leetcode.com/uploads/2019/10/10/sample3_1584.png)

```text
Input: startTime = [1,1,1], endTime = [2,3,4], profit = [5,6,4]
Output: 6
```

**Constraints:**

* `1 <= startTime.length == endTime.length == profit.length <= 5 * 10^4`
* `1 <= startTime[i] < endTime[i] <= 10^9`
* `1 <= profit[i] <= 10^4`

### Solution

#### Dynamic Programming + Binary Search

```cpp
class Solution {
public:
    vector<int> preCalc;
    int jobScheduling(vector<int>& startTime, vector<int>& endTime, vector<int>& profit) {
        int totalJobs = startTime.size();
        preCalc.resize(totalJobs, -1);
        vector<vector<int>> jobs(totalJobs, vector<int>(3,0));
        
        for(int job = 0; job < totalJobs; job++)
        {
            jobs[job][0] = startTime[job];
            jobs[job][1] = endTime[job];
            jobs[job][2] = profit[job];
        }
        sort(jobs.begin(), jobs.end());
        return solve(jobs, 0);
    }
    
    int solve(vector<vector<int>>&jobs, int index)
    {
        if(index >= jobs.size())
            return 0;
        
        if(preCalc[index] != -1)
            return preCalc[index];
        
        // Max profit with including this job
        int nextIndex = findNextIndex(jobs, index);
        int curProfit = jobs[index][2] + ((nextIndex != -1) ? solve(jobs, nextIndex) : 0);
        
        // without this job
        curProfit = max(curProfit, solve(jobs, index+1));

        return preCalc[index] = curProfit;
    }
    
    int findNextIndex(vector<vector<int>>&jobs, int index)
    {
        int left = index + 1, right = jobs.size() - 1;
        int result = -1;
        while(left <= right)
        {
            int mid = left + (right - left)/2;
            
            if(jobs[mid][0] >= jobs[index][1])
            {
                result = mid;
                right = mid - 1;
            }
            else
            {
                left = mid + 1;
            }
        }
        return result;
    }
};
```

