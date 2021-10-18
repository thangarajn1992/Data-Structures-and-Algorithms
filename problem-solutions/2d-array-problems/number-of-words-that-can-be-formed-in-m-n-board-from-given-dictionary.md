# Number of words that can be formed in M\*N Board from given dictionary

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/72cf44eabd18006810efad06fbb623a0682acee2/1#)

### Companies

* [Google](../../company-based-lists/google.md)
* [Facebook](../../company-based-lists/facebook.md)
* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given a dictionary of words and an M x N board where every cell has one character. Find all possible different words from the dictionary that can be formed by a sequence of adjacent characters on the board. We can move to any of 8 adjacent characters, but a word should not have multiple instances of the same cell. (**NOTE**: All words returned must be different even it occurs multiple times in the dictionary).

\
 **Example 1:**

```
Input: 
N = 1
dictionary = {"CAT"}
R = 3, C = 3
board = {{C,A,P},{A,N,D},{T,I,E}}
Output:
CAT
Explanation: 
C A P
A N D
T I E
Words we got is denoted using same color.
```

**Example 2:**

```
Input:
N = 4
dictionary = {"GEEKS","FOR","QUIZ","GO"}
R = 3, C = 3 
board = {{G,I,Z},{U,E,K},{Q,S,E}}
Output:
GEEKS QUIZ
Explanation: 
G I Z
U E K
Q S E 
Words we got is denoted using same color.
```

**Expected Time Complexity:** O(4^(N^2))\
**Expected Auxiliary Space: **O(N^2)\
**Constraints:**\
 1 ≤ N ≤ 15\
 1 ≤ R, C ≤ 50\
 1 ≤ length of Word ≤ 60

All words of Dictionary and all characters of board are in uppercase letters from **'A'** to **'Z'**

### **Solution**

```cpp
class Solution {
public:
    vector<vector<int>> dir = {{0, 1}, {0, -1}, 
    							             {1, 0}, {-1, 0}, 
    							             {1, 1}, {-1, -1}, 
    							             {1, -1}, {-1, 1}};
	vector<string> wordBoggle(vector<vector<char>>& board, vector<string>& dictionary) {
	    // Since dictionary can contain duplicates and result shouldnt have duplicate,
	    // we can remove the duplicates in dictonary to save no.of words being searched.
        sort(dictionary.begin(), dictionary.end());
        dictionary.erase(unique(dictionary.begin(), dictionary.end()), dictionary.end());
	    vector<string> result;  // result string vector
	    
	    // Map to hold the character to locations mapping.
        map<int, vector<pair<int,int>>> my_map;

	    for(int i = 0; i < board.size(); i++)
	        for(int j = 0; j < board[0].size(); j++)
	            my_map[board[i][j] - 'A'].push_back(make_pair(i,j));
	  
	    for(int i = 0; i < dictionary.size(); i++)
	    {
	        // visited array to keep track of visited characters in this word search
	        vector<vector<bool>> visited(board.size(), vector<bool>(board[0].size(), 0));
	        
	        // Locations we can pick for our first character in the word
	        vector<pair<int,int>> choices = my_map[dictionary[i][0] - 'A'];
	        
	        for(int j = 0; j < choices.size(); j++)
	        {
              visited[choices[j].first][choices[j].second] = true;
	            if(search(board, dictionary[i], 1, choices[j].first, choices[j].second, visited))
	            {
	                result.push_back(dictionary[i]);
	                break;
	            }
	            visited[choices[j].first][choices[j].second] = false;
	        }
	    }
	    return result;
	}
	
	bool search(vector<vector<char>>& board, string key, int index, int row, int col, vector<vector<bool>>&visited)
	{
	    // Base case
        if(index == key.size())
            return true;
        
        for(int k = 0; k < 8; k++)
        {
            int r = row + dir[k][0];
            int c = col + dir[k][1];
            if(r >= 0 && r < board.size() &&
               c >= 0 && c < board[0].size() &&
               visited[r][c] == false &&
               board[r][c] == key[index])
               {
                   visited[r][c] = true;
                   if(search(board, key, index+1, r, c, visited))
                        return true;
                   visited[r][c] = false;
               }
        }
        return false;
	}
};
```
