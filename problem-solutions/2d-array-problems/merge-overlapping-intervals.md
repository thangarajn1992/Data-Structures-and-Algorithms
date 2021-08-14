# Merge Overlapping Intervals

[InterviewBit](https://www.interviewbit.com/problems/merge-overlapping-intervals/)

[Leetcode 56](https://leetcode.com/problems/merge-intervals/)

### Problem Statement

Given a collection of intervals, merge all overlapping intervals.

**For example:**

Given `[1,3],[2,6],[8,10],[15,18]`,

return `[1,6],[8,10],[15,18]`.

Make sure the returned intervals are sorted.

### Solution

#### Sorting Approach

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> merged_intervals;
        merged_intervals.push_back(intervals[0]);
        for(int i = 1; i < intervals.size(); i++)
        {
            // No overlap
            if(merged_intervals.back()[1] < intervals[i][0]) 
                merged_intervals.push_back(intervals[i]);
            else if(merged_intervals.back()[1] < intervals[i][1])
                merged_intervals.back()[1] = intervals[i][1];
        }
        return merged_intervals;
    }
};
```

#### Map Based Approach

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        map<int,int> inter;
        for(vector<int> & interval : intervals)
        {
            inter[interval[0]]++;
            inter[interval[1]]--;
        }
        
        vector<vector<int>> merged_intervals;
        vector<int> cur_interval(2);
        bool interval_started = false;
        int interval_count = 0;
        for(auto &[time, value] : inter)
        {
            interval_count += value;
            if(interval_started == false)
            {
                cur_interval[0] = time;
                interval_started = true;
            }
            if(interval_count == 0)
            {
                cur_interval[1] = time;
                merged_intervals.push_back(cur_interval);
                interval_started = false;
            }
        }
        if(interval_started)
        {
            cur_interval[1] = inter.end()->second;
            merged_intervals.push_back(cur_interval);
        }
        return merged_intervals;
    }
};
```

