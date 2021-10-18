# Trie - C++ Implementation

As we learned about [Trie](./), in our previous page, Now lets see its implementation in C++, which is way cleaner than the [C Implementation.](trie-c-implementation.md)

For memory efficient implementation of Trie in C++ using maps to track child nodes, use this link

### Code

```cpp
#include <iostream>
using namespace std;
 
// Define the character size
#define CHAR_SIZE 26
 
// A class to store a Trie node
class Trie
{
public:
    bool isLeaf;
    Trie* character[CHAR_SIZE];
 
    // Constructor
    Trie()
    {
        this->index = -1;
 
        for (int i = 0; i < CHAR_SIZE; i++) {
            this->character[i] = nullptr;
        }
    }
 
    void insert(string);
    bool deletion(Trie*&, string);
    bool search(string);
    bool haveChildren(Trie const*);
    bool preorder(vector<string>&);
};
 
// Iterative function to insert a key into a Trie
void Trie::insert(string key, int index)
{
    // start from the root node
    Trie* curr = this;
    for (int i = 0; i < key.length(); i++)
    {
        // create a new node if the path doesn't exist
        if (curr->character[key[i] - 'a'] == nullptr) {
            curr->character[key[i] - 'a'] = new Trie();
        }
 
        // go to the next node
        curr = curr->character[key[i] - 'a'];
    }
 
    // mark the current node as a leaf
    curr->isLeaf = index;
}
 
// Iterative function to search a key in a Trie. It returns true
// if the key is found in the Trie; otherwise, it returns false
bool Trie::search(string key)
{
    // return false if Trie is empty
    if (this == nullptr) {
        return false;
    }
 
    Trie* curr = this;
    for (int i = 0; i < key.length(); i++)
    {
        // go to the next node
        curr = curr->character[key[i] - 'a'];
 
        // if the string is invalid (reached end of a path in the Trie)
        if (curr == nullptr) {
            return false;
        }
    }
 
    // return true if the current node is a leaf and the
    // end of the string is reached
    return curr->index != -1;
}
 
// Returns true if a given node has any children
bool Trie::haveChildren(Trie const* curr)
{
    for (int i = 0; i < CHAR_SIZE; i++)
    {
        if (curr->character[i]) {
            return true;    // child found
        }
    }
    return false;
}
 
// Recursive function to delete a key in the Trie
bool Trie::deletion(Trie*& curr, string key)
{
    // return if Trie is empty
    if (curr == nullptr) {
        return false;
    }
 
    // if the end of the key is not reached
    if (key.length())
    {
        // recur for the node corresponding to the next character in the key
        // and if it returns true, delete the current node (if it is non-leaf)
 
        if (curr != nullptr &&
            curr->character[key[0] - 'a'] != nullptr &&
            deletion(curr->character[key[0] - 'a'], key.substr(1)) &&
            curr->index == -1)
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
 
    // if the end of the key is reached
    if (key.length() == 0 && curr->isLeaf)
    {
        // if the current node is a leaf node and doesn't have any children
        if (!haveChildren(curr))
        {
            // delete the current node
            delete curr;
            curr = nullptr;
 
            // delete the non-leaf parent nodes
            return true;
        }
 
        // if the current node is a leaf node and has children
        else {
            // mark the current node as a non-leaf node (DON'T DELETE IT)
            curr->index = -1;
 
            // don't delete its parent nodes
            return false;
        }
    }
 
    return false;
}
 
/* function for preorder traversal */
/* products is the string vector contains all the keys in the trie with their index */
/* Preorder Traversal results is Lexicographical order */
bool Trie::preorder(vector<string>& products)
{
    if (this == nullptr)
        return false;
        
    Trie* curr = this;
    for (int i = 0; i < CHAR_SIZE; i++) {
        if (curr->character[i] != NULL) {
    
            /* if leaf node then print key*/
            if (curr->character[i]->index != -1)
                cout << products[curr->character[i]->index] << endl;
  
            curr->character[i]->preorder(products);
        }
    }
    return true;
}

// C++ implementation of Trie data structure
int main()
{
    Trie* head = new Trie();
 
    head->insert("hello");
    cout << head->search("hello") << " ";      // print 1
 
    head->insert("helloworld");
    cout << head->search("helloworld") << " "; // print 1
 
    cout << head->search("helll") << " ";      // print 0 (Not found)
 
    head->insert("hell");
    cout << head->search("hell") << " ";       // print 1
 
    head->insert("h");
    cout << head->search("h");                 // print 1
 
    cout << endl;
 
    head->deletion(head, "hello");
    cout << head->search("hello") << " ";      // print 0
 
    cout << head->search("helloworld") << " "; // print 1
    cout << head->search("hell");              // print 1
 
    cout << endl;
 
    head->deletion(head, "h");
    cout << head->search("h") << " ";          // print 0
    cout << head->search("hell") << " ";       // print 1
    cout << head->search("helloworld");        // print 1
 
    cout << endl;
 
    head->deletion(head, "helloworld");
    cout << head->search("helloworld") << " "; // print 0
    cout << head->search("hell") << " ";       // print 1
 
    head->deletion(head, "hell");
    cout << head->search("hell");              // print 0
 
    cout << endl;
 
    if (head == nullptr) {
        cout << "Trie empty!!\n";              // Trie is empty now
    }
 
    cout << head->search("hell");              // print 0
 
    return 0;
}
```

### Output

```cpp
1 1 0 1 1
0 1 1
0 1 1
0 1 0
Trie empty!!
0
```

### Complexity

**Time Complexity:  **

Insert  O(n) ;  Delete O(n) ; Search O(n), where n is the key length

**Space Complexity: **O(N \* M \* C)  

N - Total number of Strings

M - Maximum length of String

C - Alphabet's Size

