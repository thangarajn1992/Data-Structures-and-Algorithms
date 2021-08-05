# Stone Game

### Sources

* [Leetcode 877](https://leetcode.com/problems/stone-game/)

### Problem Statement

Alex and Lee play a game with piles of stones.  There are an even number of piles **arranged in a row**, and each pile has a positive integer number of stones `piles[i]`.

The objective of the game is to end with the most stones.  The total number of stones is odd, so there are no ties.

Alex and Lee take turns, with Alex starting first.  Each turn, a player takes the entire pile of stones from either the beginning or the end of the row.  This continues until there are no more piles left, at which point the person with the most stones wins.

Assuming Alex and Lee play optimally, return `True` if and only if Alex wins the game.

**Example 1:**

```text
Input: piles = [5,3,4,5]
Output: true
Explanation: 
Alex starts first, and can only take the first 5 or the last 5.
Say he takes the first 5, so that the row becomes [3, 4, 5].
If Lee takes 3, then the board is [4, 5], and Alex takes 5 to win with 10 points.
If Lee takes the last 5, then the board is [3, 4], and Alex takes 4 to win with 9 points.
This demonstrated that taking the first 5 was a winning move for Alex, so we return true.
```

**Constraints:**

* `2 <= piles.length <= 500`
* `piles.length` is even.
* `1 <= piles[i] <= 500`
* `sum(piles)` is odd.

### Solution

#### Mathematical Approach

Alex clearly always wins the 2 pile game by taking the max of the available two piles.

 With some effort, we can see that she always wins the 4 pile game. If Alex takes the first pile initially, she can always take the third pile. If she takes the fourth pile initially, she can always take the second pile. At least one of `first + third, second + fourth` is larger, so she can always win.

We can extend this idea to `N` piles. Say the first, third, fifth, seventh, etc. piles are white, and the second, fourth, sixth, eighth, etc. piles are black. Alex can always take either all white piles or all black piles, and one of the colors must have a sum number of stones larger than the other color.

Hence, Alex can always wins the game in atleast one of the scenario. So for this problem, it is always true.

```cpp
class Solution {
public:
    bool stoneGame(vector<int>& piles) {
        return true;
    }
};
```

#### Dynamic Programming Approach



```cpp
class Solution {
    vector<vector<int>> dp;
    //dp[i][j] is the maximum stone Alex can collect when we have piles i to piles j
public:
	bool stoneGame(vector<int>& piles) {
		int n = piles.size();

		dp.resize(n, vector<int>(n, INT_MIN));
		int sum = accumulate(piles.begin(), piles.end(), 0);

    //since the sum is always odd so their can't be a tie,
    //so just return true if the collected stones are greater than half of the stones
		return solve(piles, 0, n-1) >= sum/2;
	}

	
	int solve(vector<int> &piles, int i, int j){
        
    // If precalculated, return that value
		if(dp[i][j] != INT_MIN) return dp[i][j];
		
		//if only one pile left then return the pile value
		if(i == j)  return dp[i][j] = piles[i];
		
		//if only two piles left then return the greater one
		if(j == i+1) return dp[i][j] = max(piles[i], piles[j]);
	
		//case 1: 
    // If we pick the left most pile then the opponent will choose the optimal pile after our move 
    // either the opponent will pick from the left pile or the right pile and 
    // we'll take the minumum of that because the opponent is playing optimal too
    // so he will want us to pick the minimum pile after his move.
		
		//case 2: same approach as case 1 just pick the right most pile
		
		return dp[i][j] = max(piles[i] + min(solve(piles, i+2, j), solve(piles, i+1, j-1)),                                       
													piles[j] + min(solve(piles, i, j-2), solve(piles, i+1, j-1)));
	}
};
```

