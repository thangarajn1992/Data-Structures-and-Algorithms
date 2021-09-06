# Best Time to Buy and Sell Stock - Should buy and/or sell each day

### Sources

* [Leetcode 122](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

### Companies

### Problem Statement

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

On each day, you may decide to buy and/or sell the stock. You can only hold **at most one** share of the stock at any time. However, you can buy it then immediately sell it on the **same day**.

Find and return _the **maximum** profit you can achieve_.

**Example 1:**

```text
Input: prices = [7,1,5,3,6,4]
Output: 7
Explanation: 
Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Total profit is 4 + 3 = 7.
```

**Example 2:**

```text
Input: prices = [1,2,3,4,5]
Output: 4
Explanation: 
Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Total profit is 4.
```

**Example 3:**

```text
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: 
There is no way to make a positive profit, so we never buy the stock to achieve the maximum profit of 0.
```

**Constraints:**

* `1 <= prices.length <= 3 * 10^4`
* `0 <= prices[i] <= 10^4`

### Solution

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int profit = 0;
        int days = prices.size();
        
        for(int day = 0; day < days-1; day++)
            if(prices[day+1] > prices[day])
                profit += prices[day+1] - prices[day];
        
        return profit;
    }
};
```

