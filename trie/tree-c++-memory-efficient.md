# Tree - C++ Memory Efficient

Compared to general list-based [C++ implementation](trie-c++-implementation.md), we can use maps to keep track of child nodes. This is memory efficient when compared to list-based child tracking.

```cpp
#include <iostream>
#include <unordered_map>
using namespace std;
 
// Data structure to store a Trie node
struct Trie
{
    // true when the node is a leaf node
    int index;

    // each node stores a map to its child nodes
    unordered_map<char, Trie*> map;
};
 
// Function that returns a new Trie node
Trie* getNewTrieNode()
{
    Trie* node = new Trie;
    node->index = -1;
    return node;
}
 
// Iterative function to insert a string into a Trie
void insert(Trie*& head, char* str, int index)
{
    if (head == nullptr) {
        head = getNewTrieNode();
    }
 
    // start from the root node
    Trie* curr = head;
    while (*str)
    {
        // create a new node if the path doesn't exist
        if (curr->map.find(*str) == curr->map.end()) {
            curr->map[*str] = getNewTrieNode();
        }
 
        // go to the next node
        curr = curr->map[*str];
 
        // move to the next character
        str++;
    }
 
    // mark the current node as a leaf
    curr->index = index;
}
 
// Returns true if the given node has any children
bool haveChildren(Trie const* curr)
{
    // don't use `(curr->map).size()` to check for children
 
    for (auto it: curr->map)
    {
        if (it.second != nullptr) {
            return true;
        }
    }
 
    return false;
}
 
// Recursive function to delete a string from a Trie
bool deletion(Trie*& curr, char* str)
{
    // return if Trie is empty
    if (curr == nullptr) {
        return false;
    }
 
    // if the end of the string is not reached
    if (*str)
    {
        // recur for the node corresponding to the next character in
        // the string and if it returns true, delete the current node
        // (if it is non-leaf)
        if (curr != nullptr && curr->map.find(*str) != curr->map.end() &&
            deletion(curr->map[*str], str + 1) && curr->index == -1)
        {
            if (!haveChildren(curr))
            {
                delete curr;
                curr = nullptr;
                return true;
            }
            else {
                return false;
            }
        }
    }
 
    // if the end of the string is reached
    if (*str == '\0' && curr->index != -1)
    {
        // if the current node is a leaf node and doesn't have any children
        if (!haveChildren(curr))
        {
            delete curr;    // delete the current node
            curr = nullptr;
            return true;    // delete the non-leaf parent nodes
        }
 
        // if the current node is a leaf node and has children
        else {
            // mark the current node as a non-leaf node (DON'T DELETE IT)
            curr->index = -1;
            return false;   // don't delete its parent nodes
        }
    }
 
    return false;
}
 
// Iterative function to search a string in a Trie. It returns true
// if the string is found in the Trie; otherwise, it returns false.
bool search(Trie* head, char* str)
{
    // return false if Trie is empty
    if (head == nullptr) {
        return false;
    }
 
    Trie* curr = head;
    while (*str)
    {
        // go to the next node
        curr = curr->map[*str];
 
        // if the string is invalid (reached end of a path in the Trie)
        if (curr == nullptr) {
            return false;
        }
 
        // move to the next character
        str++;
    }
 
    // return true if the current node is a leaf and the
    // end of the string is reached
    return curr->index != -1;
}

```

