# Best Time to Buy and Sell Stock once

### Sources

* [Leetcode 121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

### Companies

### Problem Statement

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day. You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock. Return _the maximum profit you can achieve from this transaction_. If you cannot achieve any profit, return `0`.

**Example 1:**

```text
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before
you sell.
```

**Example 2:**

```text
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
```

**Constraints:**

* `1 <= prices.length <= 10^5`
* `0 <= prices[i] <= 10^4`

### Solution

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int costPrice = INT_MAX;
        int profit = 0;
        for(int &price : prices)
        {
            if(price < costPrice)
                costPrice = price;
            int curProfit = price - costPrice;
            if(curProfit > profit)
                profit = curProfit;
        }
        return profit;
    }
};
```

