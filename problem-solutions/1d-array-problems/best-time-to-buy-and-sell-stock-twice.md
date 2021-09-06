# Best Time to Buy and Sell Stock Twice

### Sources

* [Leetcode 123](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)

### Companies

### Problem Statement

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

Find the maximum profit you can achieve. You may complete **at most two transactions**.

**Note:** You may not engage in multiple transactions simultaneously \(i.e., you must sell the stock before you buy again\).

**Example 1:**

```text
Input: prices = [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
```

**Example 2:**

```text
Input: prices = [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.
```

**Example 3:**

```text
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

**Example 4:**

```text
Input: prices = [1]
Output: 0
```

**Constraints:**

* `1 <= prices.length <= 10^5`
* `0 <= prices[i] <= 10^5`

### Solution

[Good Explanation on Youtube](https://www.youtube.com/watch?v=6928FkPhGUA)

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int days = prices.size();
        // States: 
        //  BUY, SELL, SKIP
        // State Machine: 
        //  From BUY => SELL, SKIP
        //  From SELL => BUY, SKIP
        // So we will have Buy -> Sell -> Buy -> Sell alternatively. 
        // We must always end with Sell state.
        // For this problem, we will have Atmost 2 Buys + 2 Sells
        // Dynamic Programming Approach:
        // For 2 transactions, we may have maximum of 4 States. B S B S
        // Default Buy State value will be MIN and 
        // Default Sell State will be 0 because our profit should atleast be 0
        
        // Implementation:
        // For each day, we will go through all the states
        // BUY STATE:   State_index == 0, dp = max(INTMIN, -price[day]);   
        // BUY STATE:   State_index % 2 == 0, dp = max(dp[state_index], dp[state_index-1] - price[day]) SKIP or BUY
        // SELL STATE:  State_index % 2 == 1, dp = max(dp[state_index], dp[state_index-1] + price[day]) SKIP or SELL
        // Same concept can be extended upto K transactions.
        
        int totalTransactionStates = 4;
        vector<int> maxProfit(totalTransactionStates, 0); // max profit at given state
        
        // Initialize BUY state with INT_MIN and SELL state with 0
        for(int stateNum = 0; stateNum < totalTransactionStates; stateNum++)
            if(stateNum % 2 == 0)
                maxProfit[stateNum] = INT_MIN;
        
        for(int day = 0; day < days; day++)
        {
            maxProfit[0] = max(maxProfit[0], -prices[day]);
            for(int stateNum = 1; stateNum < totalTransactionStates; stateNum++)
            {
                if(stateNum % 2 == 0) // BUY or SKIP
                    maxProfit[stateNum] = max(maxProfit[stateNum], maxProfit[stateNum - 1] - prices[day]);
                else // SELL or SKIP
                    maxProfit[stateNum] = max(maxProfit[stateNum], maxProfit[stateNum -1] + prices[day]);       
            }
        }
        return maxProfit[totalTransactionStates - 1];
    }  
};
```

