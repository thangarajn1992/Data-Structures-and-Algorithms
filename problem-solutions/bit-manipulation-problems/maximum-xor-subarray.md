# Maximum XOR subarray

### Source

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/a512e4b2e812b6df2159b19cc7090ffc1ab056dd/1#)

### Companies

* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given an array **arr\[] **of size, **N.** Find the subarray with maximum XOR. A subarray is a contiguous part of the array.

\
 **Example 1:**

```
Input:
N = 4
arr[] = {1,2,3,4}
Output: 7
Explanation: 
The subarray {3,4} has maximum xor 
value equal to 7.

```

\
**Expected Time Complexity:** O(N)\
**Expected Auxiliary Space:** O(N

**Constraints:**\
 1 <= N <= 10^5\
 1 <= arr\[i] <= 10^5

### Solution

#### Trie Based Approach

An **Efficient Solution** can solve the above problem in O(n) time under the assumption that integers take fixed number of bits to store. The idea is to use Trie Data Structure. Below is algorithm.  

```
1) Create an empty Trie.  Every node of Trie is going to 
   contain two children, for 0 and 1 value of bit.
2) Initialize pre_xor = 0 and insert into the Trie.
3) Initialize result = minus infinite
4) Traverse the given array and do following for every 
   array element arr[i].
       a) pre_xor  = pre_xor  ^ arr[i]
          pre_xor now contains xor of elements from 
          arr[0] to arr[i].
       b) Query the maximum xor value ending with arr[i] 
          from Trie.
       c) Update result if the value obtained in step 
          4.b is more than current value of result.
```

**How does 4.b work?** \
We can observe from above algorithm that we build a Trie that contains XOR of all prefixes of given array. To find the maximum XOR subarray ending with arr\[i], there may be two cases. \
i) The prefix itself has the maximum XOR value ending with arr\[i]. For example if i=2 in {8, 2, 1, 12}, then the maximum subarray xor ending with arr\[2] is the whole prefix. \
ii) We need to remove some prefix (ending at index from 0 to i-1). For example if i=3 in {8, 2, 1, 12}, then the maximum subarray xor ending with arr\[3] starts with arr\[1] and we need to remove arr\[0].\
To find the prefix to be removed, we find the entry in Trie that has maximum XOR value with current prefix. If we do XOR of such previous prefix with current prefix, we get the maximum XOR value ending with arr\[i]. \
If there is no prefix to be removed (case i), then we return 0 (that’s why we inserted 0 in Trie). 

```cpp
class TrieNode {
public:
    int val;
    TrieNode *next[2];
};

TrieNode *newNode()
{
    TrieNode *temp = new TrieNode;
    temp->val = 0;
    temp->next[0] = temp->next[1] = NULL;
    return temp;
}

void insert_node(TrieNode *root, int cur_xor)
{
    TrieNode* cur = root;
    for(int i = 31; i >= 0; i--)
    {
        bool val = cur_xor & (1 << i);
        
        if(cur->next[val] == nullptr)
            cur->next[val] = newNode();
        
        cur = cur->next[val];
    }
    cur->val = cur_xor;
}

int get_value(TrieNode *root, int cur_xor)
{
    TrieNode *cur = root;
    int this_xor = root->val;
    for(int i = 31; i >= 0; i--)
    {
        bool val = cur_xor & (1 << i);
        
        if(cur->next[1 - val] != nullptr)
            cur = cur->next[1 - val];
        else if(cur->next[val] != nullptr)
            cur = cur->next[val];
        else
            break;
    }
    return cur_xor ^ (cur->val);
}

class Solution{   
public:
    int maxSubarrayXOR(int N, int arr[]){    
        TrieNode *root = newNode();
        insert_node(root, 0);
        int cur_xor = 0, maxXor = INT_MIN;
        for(int i = 0; i < N; i++)
        {
            cur_xor = cur_xor ^ arr[i];
            insert_node(root, cur_xor);
            
            maxXor = max(maxXor, get_value(root, cur_xor));
        }
        return maxXor;
    }
};

```
