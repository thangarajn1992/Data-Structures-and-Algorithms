# Infix to postfix

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/infix-to-postfix-1587115620/1)

### Companies

* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given an infix expression in the form of string **str**. Convert this infix expression to postfix expression.

* **Infix expression:** The expression of the form a **op** b. When an operator is in-between every pair of operands.
* **Postfix expression:** The expression of the form a b **op**. When an operator is followed for every pair of operands.\
  **Note:** The order of precedence is: ^ **greater than** \* **equals to** / **greater than** + **equals to** -.&#x20;

**Example 1:**

```
Input: str = "a+b*(c^d-e)^(f+g*h)-i"
Output: abcd^e-fgh*+^*+i-
Explanation:
After converting the infix expression 
into postfix expression, the resultant 
expression will be abcd^e-fgh*+^*+i-
```

**Example 2:**

```
Input: str = "A*(B+C)/D"
Output: ABC+*D/
Explanation:
After converting the infix expression 
into postfix expression, the resultant 
expression will be ABC+*D/
```

**Your Task:**\
&#x20;This is a **function** problem. You only need to complete the function **infixToPostfix()** that takes a **string**(Infix Expression) as a **parameter** and **returns** a **string(**postfix expression**)**. The **printing** is done **automatically** by the **driver code**.

**Expected Time Complexity:** O(|str|).\
&#x20;**Expected Auxiliary Space:** O(|str|).

**Constraints:**\
&#x20;1 ≤ |str| ≤ 10^5

### Solution

```cpp
class Solution
{
public:
    string infixToPostfix(string s)
    {
        stack<char> st;
        string result = "";
        for(char &c : s)
        {
            // if operand or '(', push to stack
            if((c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z') || 
               (c >= '0' && c <= '9')) 
                result += c;
            else if(c == '(')
                st.push(c);
            else if(c == ')') // pop till we see '('
            {
                while(!st.empty() && st.top() != '(')
                {
                    result += st.top();
                    st.pop();
                }
                st.pop(); // dont need to include parenthesis in postfix
            }
            else // operators
            {
                while(!st.empty() && prec(c) <= prec(st.top()))
                {
                    result += st.top();
                    st.pop();
                }
                st.push(c);
            }
        }
        // pop all remaining elements from the stack
        while(!st.empty())
        {
            result += st.top();
            st.pop();
        }
        return result;
    }
    
    int prec(char c) {
        if(c == '^')
            return 3;
        else if(c == '*' || c == '/')
            return 2;
        else if(c == '+' || c == '-')
            return 1;
        else
            return -1;
    }
};
```
