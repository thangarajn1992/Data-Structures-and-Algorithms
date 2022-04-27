# Rearrange characters such that there are no repeated characters

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/rearrange-characters4649/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given a string S with repeated characters. The task is to rearrange characters in a string such that no two adjacent characters are the same.The string has only lowercase English alphabets and it can have multiple solutions. Return any one of them. The function **rearrangeString()** which takes the string as input and returns the modified string. If the string cannot be modified return "-1".

**Example 1:**

```
Input : 
str = "geeksforgeeks"
Output: 1
Explanation:
All the repeated characters of the given string can be rearranged so 
that no adjacent characters in the string is equal. 
```

**Example 2:**

```
Input : 
str = "bbbbb"
Output: 0
Explanation : 
Repeated characters in the string cannot be rearranged such that there should not 
be any adjacent repeated character.
```

**Note:** The generated output is 1 if the string is successfully rearranged and is 0 if rearranging is not possible.

* **Expected Time Complexity :** O(NlogN), N = length of String
* **Expected Auxiliary Space :** O(number of English alphabets)
* **Constraints :** 1 <= length of string <= 10^4

### Solution

```cpp
auto comp = [&](const pair<int,char> &a, const pair<int,char> &b){
    return a.first < b.first;
};
class Solution
{
    public:
    string rearrangeString(string str)
    {
        string result = "";
        priority_queue<pair<int,char>, vector<pair<int,char>>, decltype(comp)> pq(comp);                      
        int freq[26] = {0};
        
        for(char &c: str)
            freq[c - 'a']++;
        
        for(int i = 0; i < 26; i++)
            if(freq[i])
                pq.push(make_pair(freq[i], 'a'+i));
        
        pair<int,char> prev = {-1, '#'}; // dummy prev
        while(!pq.empty())
        {
            pair<int,char> temp = pq.top(); pq.pop();
            result += temp.second;
            
            if(prev.first > 0)
                pq.push(prev);
            
            temp.first--;
            prev = temp;
        }
        return (str.size() == result.size()) ? result : "-1";
    }
};
```

****
