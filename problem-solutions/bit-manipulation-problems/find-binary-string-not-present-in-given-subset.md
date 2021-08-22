# Find Binary String not present in given subset

### Sources

* [Leetcode 1980](https://leetcode.com/problems/find-unique-binary-string/)

### Companies

### Problem Statement

Given an array of strings `nums` containing `n` **unique** binary strings each of length `n`, return _a binary string of length_ `n` _that **does not appear** in `nums`. If there are multiple answers, you may return **any** of them_.

**Example 1:**

```text
Input: nums = ["01","10"]
Output: "11"
Explanation: 
"11" does not appear in nums. "00" would also be correct.
```

**Example 2:**

```text
Input: nums = ["00","01"]
Output: "11"
Explanation: 
"11" does not appear in nums. "10" would also be correct.
```

**Example 3:**

```text
Input: nums = ["111","011","001"]
Output: "101"
Explanation: 
"101" does not appear in nums. "000", "010", "100", and "110" would also be correct.
```

**Constraints:**

* `n == nums.length`
* `1 <= n <= 16`
* `nums[i].length == n`
* `nums[i]` is either `'0'` or `'1'`.

### Solution

### [Cantor's diagonalization](https://en.wikipedia.org/wiki/Cantor%27s_diagonal_argument)

A sequence s is constructed by choosing the 1st digit as complementary to the 1st digit of s1 \(swapping **0**s for **1**s and vice versa\), the 2nd digit as complementary to the 2nd digit of s2, the 3rd digit as complementary to the 3rd digit of s3, and generally for every n, the nth digit as complementary to the nth digit of sn.

| s1 | = | \(**0**, | 0, | 0, | 0, | 0, | 0, | 0, | ...\) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| s2 | = | \(1, | **1**, | 1, | 1, | 1, | 1, | 1, | ...\) |
| s3 | = | \(0, | 1, | **0**, | 1, | 0, | 1, | 0, | ...\) |
| s4 | = | \(1, | 0, | 1, | **0**, | 1, | 0, | 1, | ...\) |
| s5 | = | \(1, | 1, | 0, | 1, | **0**, | 1, | 1, | ...\) |
| s6 | = | \(0, | 0, | 1, | 1, | 0, | **1**, | 1, | ...\) |
| s7 | = | \(1, | 0, | 0, | 0, | 1, | 0, | **0**, | ...\) |
| s | = | \(**1**, | **0**, | **1**, | **1**, | **1**, | **0**, | **1**, | ...\) |

By construction, s differs from each sn, since their nth digits differ \(highlighted in the example\). Hence, s cannot occur in the enumeration.

```cpp
class Solution {
public:
    string findDifferentBinaryString(vector<string>& nums) {
        int n = nums[0].size();
        string result = "";
        for(int i = 0; i < n; i++)
            result += nums[i][i] == '0' ? '1' : '0';
        return result;   
    }
};
```

