# Best Time to Buy and Sell Stock with Cooldown

### Sources

* [Leetcode 309](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

### Companies



### Problem Statement

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

Find the maximum profit you can achieve. You may complete as many transactions as you like \(i.e., buy one and sell one share of the stock multiple times\) with the following restrictions:

* After you sell your stock, you cannot buy stock on the next day \(i.e., cooldown one day\).

**Note:** You may not engage in multiple transactions simultaneously \(i.e., you must sell the stock before you buy again\).

**Example 1:**

```text
Input: prices = [1,2,3,0,2]
Output: 3
Explanation: transactions = [buy, sell, cooldown, buy, sell]
```

**Example 2:**

```text
Input: prices = [1]
Output: 0
```

**Constraints:**

* `1 <= prices.length <= 5000`
* `0 <= prices[i] <= 1000`

### Solution

[Good Explanation on Youtube](https://www.youtube.com/watch?v=4wNXkhAky3s)

![](../../.gitbook/assets/image%20%2841%29.png)

![](../../.gitbook/assets/image%20%2840%29.png)

```cpp
/*
Three States: NOSTOCK, INHAND, SOLD
We start from NOSTOCK state.
State Transitions:
1. To Reach NOSTOCK:   Previous day state must be NOSTOCK or SOLD
2. To Reach INHAND:    Previous day state must be NOSTOCK - prices[day] or INHAND.. 
                       By Ensuring that we cannot move from SOLD To INHAND immediately , 
                       the cooldown is taken care of.
3. To Reach SOLD:      Previous day INHAND + prices[day] i.e selling, the stock we already
                       have, on this day 
*/
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int days = prices.size();
        
        if(days <= 1)
            return 0;
        
        int prevnoStock, previnHand, prevSold;
        int noStock = 0, sold = 0;
        int inHand = -prices[0]; // We are buying on day1.
        
        for(int i = 1; i < days; i++)
        { 
            prevnoStock = noStock;
            previnHand = inHand;
            prevSold = sold;
            
            noStock = max(prevnoStock, prevSold);
            inHand = max(previnHand, prevnoStock - prices[i]);
            sold = previnHand + prices[i];
        }
        return max(noStock, sold);
    }
};
```

