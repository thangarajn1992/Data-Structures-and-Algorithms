# Add & Merge Interval

### Source

* [Leetcode 57](https://leetcode.com/problems/insert-interval/)
* [Interviewbit](https://www.interviewbit.com/problems/merge-intervals/)

### Problem Statement

Given a set of non-overlapping intervals, insert a new interval into the intervals \(merge if necessary\).

_You may assume that the intervals were initially sorted according to their start times_.

**Example 1:**

Given intervals `[1,3],[6,9]` insert and merge `[2,5]` would result in `[1,5],[6,9]`.

**Example 2:**

Given `[1,2],[3,5],[6,7],[8,10],[12,16]`, insert and merge `[4,9]` would result in `[1,2],[3,10],[12,16]`.

This is because the new interval `[4,9]` overlaps with `[3,5],[6,7],[8,10]`.

Make sure the returned intervals are also sorted.

### Solution

### Approach

1. Mark 's' as the start of new interval and 'e' as the end of new interval
2. Run a loop for each element in the interval
   1. If current interval is non-overlapping and less than new interval, insert the interval into result
   2. If current interval is non-overlapping and more than new interval, insert new interval into result and update 's' and 'e' with current interval start and end respectively
   3. If there is overlap, update 's' and 'e' with minimum start and maximum end of current and new interval. i.e. we combine these two interval into one interval. But we wont insert anything right now.
3. At the end of loop, insert the current 's' and 'e' as last interval in the result.

```cpp
Leetcode Solution:
==================
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        vector<vector<int>> final_intervals;
        int i = 0;
        int start = newInterval[0], end = newInterval[1];
        for(; i < intervals.size(); i++)
        {
            if(intervals[i][1] < start) // No Overlap
                final_intervals.push_back(intervals[i]);
            else if(end >= intervals[i][0]) // Overlap with new Interval
            {
                start = min(intervals[i][0], start);
                end = max(intervals[i][1], end);
            }
            else if(intervals[i][0] > end) // Merging done
                break;
        }
        final_intervals.push_back({start, end});
        final_intervals.insert(final_intervals.end(), intervals.begin()+i, intervals.end());
        return final_intervals; 
    }
};

InterviewBit Solution: [ When Interval is User-Defined Data Structure ]
======================
vector<Interval> Solution::insert(vector<Interval> &it, Interval newinterval) 
    int s = min(newinterval.start,newinterval.end);
    int e = max(newinterval.start,newinterval.end);

    int n = it.size();
    vector<Interval> v;

    for(int i = 0; i < n; i++)
    {
        if(s < it[i].start && e < it[i].start)
        {
            v.push_back(Interval(s,e));
            s = it[i].start;
            e = it[i].end;
        }
        else if(it[i].end < s)
        {
            v.push_back(it[i]);
        }
        else if(it[i].start <= e && s <= it[i].end) // overlap
        {
            s = min(s, it[i].start);
            e = max(e, it[i].end);
        }
    }
    v.push_back(Interval(s,e));
    return v;
}
```

