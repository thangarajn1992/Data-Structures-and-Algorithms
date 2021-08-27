# Utility Functions

* [Is s1 sub-sequence of s2](utility-functions.md#is-s1-sub-sequence-of-s2)
* 
### Is s1 sub-sequence of s2

```cpp
// s2.size() >= s1.size()
bool isSubsequence(string s1 ,string s2){
    int s1Iindex = 0;
    for(int s2Index = 0;  s2Index < s2.size(); s2Index++){
        if(s2[s2Index] == s1[s1Index])
            s2Index++;
        if(s1Index == s1.size())
        return true;
    }
    return s1Index == s1.size();
}
```

