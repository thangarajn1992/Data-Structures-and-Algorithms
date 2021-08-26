# Verify Preorder Serialization of a Binary Tree

### Sources

* [Leetcode 331](https://leetcode.com/problems/verify-preorder-serialization-of-a-binary-tree/)

### Companies

### Problem Statement

One way to serialize a binary tree is to use **preorder traversal**. When we encounter a non-null node, we record the node's value. If it is a null node, we record using a sentinel value such as `'#'`. ![](https://assets.leetcode.com/uploads/2021/03/12/pre-tree.jpg)

For example, the above binary tree can be serialized to the string `"9,3,4,#,#,1,#,#,2,#,6,#,#"`, where `'#'` represents a null node.

Given a string of comma-separated values `preorder`, return `true` if it is a correct preorder traversal serialization of a binary tree.

It is **guaranteed** that each comma-separated value in the string must be either an integer or a character `'#'` representing null pointer.

You may assume that the input format is always valid.

* For example, it could never contain two consecutive commas, such as `"1,,3"`.

**Note:** You are not allowed to reconstruct the tree.

**Example 1:**

```text
Input: preorder = "9,3,4,#,#,1,#,#,2,#,6,#,#"
Output: true
```

**Example 2:**

```text
Input: preorder = "1,#"
Output: false
```

**Example 3:**

```text
Input: preorder = "9,#,#,1"
Output: false
```

**Constraints:**

* `1 <= preorder.length <= 10^4`
* `preoder` consist of integers in the range `[0, 100]` and `'#'` separated by commas `','`.

### Solution

#### Iterative Approach

```cpp
class Solution {
public:
    bool isValidSerialization(string preorder) {
        // If first node is NULL, then that must be the only node
        if(preorder[0] == '#')
            return preorder.size() == 1;
        
        
        int index = 0;
        // Non-null first node, process and move to next node
        while(index < preorder.size() && preorder[index] != ',')
           index++;
        index++;
        
        int needed_nodes = 2;

        while(index < preorder.size())
        {
            // If there are extra nodes, when we dont need them, return false
            if(needed_nodes == 0)
                return false;
            
            // We have visited new node, reduce needed_nodes by 1
            needed_nodes--;
            
            if(preorder[index] != '#')
                needed_nodes += 2;
            
            // Move to next node in serialization
            while(index < preorder.size() && preorder[index] != ',')
                    index++;
            index++;
        }
        return needed_nodes == 0;
    }
};
```

#### Recursive Approach

```cpp
class Solution {
public:
    bool isValidSerialization(string preorder) {
        int index = 0;
        return isValidSerializationUtil(preorder, index) && index >= preorder.size() - 1;  
    }
    bool isValidSerializationUtil(string& preorder, int &index)
    {
        // We need a node here, but it is not present, return FALSE
        if(index >= preorder.size())
            return false;
        
        // If it is Null, return TRUE
        if(preorder[index] == '#')
            return true;
        
        // This is not NULL node, Validate left and right Sub-tree
        // Move to next entry which is supposed to be its left child
        while(index < preorder.size() && preorder[index] != ',')
            index++;
        index++; 
        
        // validate left sub-tree
        if(isValidSerializationUtil(preorder, index) == false)
            return false;
        
        // Move to next entry which is supposed to be its right child
        while(index < preorder.size() && preorder[index] != ',')
            index++;
        index++;  
        
        // Right Child is present, validate right sub-tree
        return isValidSerializationUtil(preorder, index);
    }
};
```

