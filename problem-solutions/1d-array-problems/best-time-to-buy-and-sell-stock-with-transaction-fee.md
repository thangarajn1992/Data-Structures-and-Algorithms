# Best Time to Buy and Sell Stock with Transaction Fee

### Sources

* [Leetcode 714](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

### Companies

### Problem Statement

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day, and an integer `fee` representing a transaction fee.

Find the maximum profit you can achieve. You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction.

**Note:** You may not engage in multiple transactions simultaneously \(i.e., you must sell the stock before you buy again\).

**Example 1:**

```text
Input: prices = [1,3,2,8,4,9], fee = 2
Output: 8
Explanation: The maximum profit can be achieved by:
- Buying at prices[0] = 1
- Selling at prices[3] = 8
- Buying at prices[4] = 4
- Selling at prices[5] = 9
The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
```

**Example 2:**

```text
Input: prices = [1,3,7,5,10,3], fee = 3
Output: 6
```

**Constraints:**

* `1 <= prices.length <= 5 * 10^4`
* `1 <= prices[i] < 5 * 10^4`
* `0 <= fee < 5 * 10^4`

### Solution

```cpp
// Two States: INHAND and SOLD
// State Transitions:
// To INHAND =>  From holding stock prevInhand or Buying Stock ( PrevSold - price[day])
// TO SOLD => From not buying stock prevSold or Selling stock ( PrevinHand + price[day] - fee)

class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int days = prices.size();
        int sold = 0;
        int inHand = -prices[0];
        
        for(int day = 1; day < days; day++)
        {
            sold = max(sold, inHand + prices[day] - fee);
            
            // Ideally we would be using temporary variables to keep track of previous sold,inhand
            // But since in this problem, buying + selling on same day won't be better than holding the stock
            
            // More explanation:
            // Lets assume oldSold is less than curr Sell ( inhand + prices[day] - fee)
            // So our newSold = inhand + prices[day] - fee;
            // Now when we use this newSold in below equation, it becomes,
            // max(inhand, inhand + prices[day] - fee - prices[day])
            // max(inhand, inhand - fee) == inhand
            
            // So only when oldSold is better then newSold, our inhand may change
            // Hence no need for new variable to store prev values.
            inHand = max(inHand, sold - prices[day]);
        }
        return sold;
    }
};
```

