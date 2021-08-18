# Decode ways

### Source

* [Leetcode 91](https://leetcode.com/problems/decode-ways/)

### Problem Statement

A message containing letters from `A-Z` can be **encoded** into numbers using the following mapping:

```text
'A' -> "1"
'B' -> "2"
...
'Z' -> "26"
```

To **decode** an encoded message, all the digits must be grouped then mapped back into letters using the reverse of the mapping above \(there may be multiple ways\). For example, `"11106"` can be mapped into:

* `"AAJF"` with the grouping `(1 1 10 6)`
* `"KJF"` with the grouping `(11 10 6)`

Note that the grouping `(1 11 06)` is invalid because `"06"` cannot be mapped into `'F'` since `"6"` is different from `"06"`.

Given a string `s` containing only digits, return _the **number** of ways to **decode** it_.

The answer is guaranteed to fit in a **32-bit** integer.

**Example 1:**

```text
Input: s = "12"
Output: 2
Explanation: 
"12" could be decoded as "AB" (1 2) or "L" (12).
```

**Example 2:**

```text
Input: s = "226"
Output: 3
Explanation: 
"226" could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

**Example 3:**

```text
Input: s = "0"
Output: 0
Explanation: 
There is no character that is mapped to a number starting with 0.
The only valid mappings with 0 are 'J' -> "10" and 'T' -> "20", neither of which start with 0.
Hence, there are no valid ways to decode this since all digits need to be mapped.
```

**Example 4:**

```text
Input: s = "06"
Output: 0
Explanation: 
"06" cannot be mapped to "F" because of the leading zero ("6" is different from "06").
```

**Constraints:**

* `1 <= s.length <= 100`
* `s` contains only digits and may contain leading zero\(s\).

### Solution

```cpp
class Solution {
public:
    int numDecodings(string s) {
        int combo_n_plus_2 = 0, combo_n_plus_1 = 1, combo_n = 0;
        
        for(int i = s.size() - 1; i >= 0; i--)
        {
            if(s[i] != '0') // single digit 
                combo_n += combo_n_plus_1;
            if(i+1 < s.size() && s[i] == '1' || s[i] == '2' && s[i+1] <= '6') // double digit
                combo_n += combo_n_plus_2;
            
            combo_n_plus_2 = combo_n_plus_1;
            combo_n_plus_1 = combo_n;
            combo_n = 0;
        }
        return combo_n_plus_1;
    }
};
```

