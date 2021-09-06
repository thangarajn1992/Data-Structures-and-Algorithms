# Best Time to Buy and Sell Stock Atmost k transactions

### Sources

* [Leetcode 188](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)

### Companies

### Problem Statement

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day, and an integer `k`.

Find the maximum profit you can achieve. You may complete at most `k` transactions.

**Note:** You may not engage in multiple transactions simultaneously \(i.e., you must sell the stock before you buy again\).

**Example 1:**

```text
Input: k = 2, prices = [2,4,1]
Output: 2
Explanation: 
Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.
```

**Example 2:**

```text
Input: k = 2, prices = [3,2,6,5,0,3]
Output: 7
Explanation: 
Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4. 
Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
```

**Constraints:**

* `0 <= k <= 100`
* `0 <= prices.length <= 1000`
* `0 <= prices[i] <= 1000`

### Solution

[Good Explanation on Youtube](https://www.youtube.com/watch?v=6928FkPhGUA)

```cpp
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        int days = prices.size();
        
        //case 1: No transaction or number of days less than 2
        // When k = 0 or days <= 1, we wont have any profit
        if(k == 0 || days <= 1)
            return 0;
        
        int totalTransactionStates = 2*k;

        // case 2: Total Buy + Sell > days, then we can make theortically INFINITE transaction
        // In this case, we can just consider all the upstream curve for transactions
        // i.e Valley-Peak Approach, Buy at valley and Sell at Peak.
        if(totalTransactionStates > days)
        {
            int profit = 0;
            for(int day = 1; day < days; day++)
                if(prices[day] > prices[day - 1])
                    profit += prices[day] - prices[day - 1];
            return profit;
        }
        
        // case 3: Where we can make atmost k transactions (normal case)
        // States: 
        //  BUY, SELL, SKIP
        // State Machine: 
        //  From BUY => SELL, SKIP
        //  From SELL => BUY, SKIP
        // So we will have Buy -> Sell -> Buy -> Sell alternatively. 
        // We must always end with Sell state.
        // For this problem, we will have Atmost k Buys + k Sells
        // Dynamic Programming Approach:
        // For k transactions, we may have maximum of 2*k States. B1 S1 B2 S2....B2k S2k
        // All even states are BUY State and its default value will be MIN and 
        // All odd states are SELL and its default value will be 0 because our profit should atleast be 0.
        
        // Implementation:
        // For each day, we will go through all the states
        // BUY STATE:   State_index == 0, dp = max(INTMIN, -price[day]);   
        // BUY STATE:   State_index % 2 == 0, dp = max(dp[state_index], dp[state_index-1] - price[day]) SKIP or BUY
        // SELL STATE:  State_index % 2 == 1, dp = max(dp[state_index], dp[state_index-1] + price[day]) SKIP or SELL
        
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

