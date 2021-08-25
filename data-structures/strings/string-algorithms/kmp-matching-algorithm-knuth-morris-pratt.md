# KMP Matching Algorithm \(Knuth Morris Pratt\)

For Naive Pattern Searching approach, refer this [link](naive-pattern-searching.md). The worst case scenario for naive pattern searching is `O(m(n-m+1))`. The time complexity of KMP algorithm is `O(n)` in the worst case.

The KMP matching algorithm uses degenerating property \(pattern having same sub-patterns appearing more than once in the pattern\) of the pattern and improves the worst case complexity to O\(n\). The basic idea behind KMP’s algorithm is: **whenever we detect a mismatch \(after some matches\), we already know some of the characters in the text of the next window. We take advantage of this information to avoid matching the characters that we know will anyway match**. Let us consider below example to understand this.

```text
Matching Overview
txt = "AAAAABAAABA" 
pat = "AAAA"

We compare first window of txt with pat
txt = "AAAAABAAABA" 
pat = "AAAA"  [Initial position]
We find a match. This is same as Naive String Matching.

In the next step, we compare next window of txt with pat.
txt = "AAAAABAAABA" 
pat =  "AAAA" [Pattern shifted one position]
This is where KMP does optimization over Naive. In this second window, we only compare 
fourth A of pattern with fourth character of current window of text to decide whether 
current window matches or not. Since we know first three characters will anyway match, 
we skipped matching first three characters. 

Need of Preprocessing?
An important question arises from the above explanation, how to know how many characters 
to be skipped. To know this, we pre-process pattern and prepare an integer array 
lps[] that tells us the count of characters to be skipped. 
```

**Preprocessing Overview:**

* KMP algorithm preprocesses pat\[\] and constructs an auxiliary **lps\[\]** of size m \(same as size of pattern\) which is used to skip characters while matching.
* **name lps indicates longest proper prefix which is also suffix**. A proper prefix is prefix with whole string **not** allowed. For example, prefixes of “ABC” are “”, “A”, “AB” and “ABC”. Proper prefixes are “”, “A” and “AB”. Suffixes of the string are “”, “C”, “BC” and “ABC”.
* We search for lps in sub-patterns. More clearly we focus on sub-strings of patterns that are either prefix and suffix.
* _**For each sub-pattern pat\[0..i\] where i = 0 to m-1, lps\[i\] stores length of the maximum matching proper prefix which is also a suffix of the sub-pattern pat\[0..i\].**_

  ```text
     lps[i] = the longest proper prefix of pat[0..i] 
                which is also a suffix of pat[0..i]. 
  ```

  **Note :** lps\[i\] could also be defined as longest prefix which is also proper suffix. **We need to use properly at one place to make sure that the whole substring is not considered.**

  ```text
  Examples of lps[] construction:
  For the pattern “AAAA”, 
  lps[] is [0, 1, 2, 3]

  For the pattern “ABCDE”, 
  lps[] is [0, 0, 0, 0, 0]

  For the pattern “AABAACAABAA”, 
  lps[] is [0, 1, 0, 1, 2, 0, 1, 2, 3, 4, 5]

  For the pattern “AAACAAAAAC”, 
  lps[] is [0, 1, 2, 0, 1, 2, 3, 3, 3, 4] 

  For the pattern “AAABAAA”, 
  lps[] is [0, 1, 2, 0, 1, 2, 3]
  ```

  **Searching Algorithm:**  
  Unlike [Naive algorithm,](naive-pattern-searching.md) where we slide the pattern by one and compare all characters at each shift, we use a value from lps\[\] to decide the next characters to be matched. The idea is to not match a character that we know will anyway match.

  How to use lps\[\] to decide next positions \(or to know a number of characters to be skipped\)?

  * We start comparison of pat\[j\] with j = 0 with characters of current window of text.
  * We keep matching characters txt\[i\] and pat\[j\] and keep incrementing i and j while pat\[j\] and txt\[i\] keep **matching**.
  * When we see a **mismatch**
    * We know that characters pat\[0..j-1\] match with txt\[i-j…i-1\] \(Note that j starts with 0 and increment it only when there is a match\).
    * We also know \(from above definition\) that lps\[j-1\] is count of characters of pat\[0…j-1\] that are both proper prefix and suffix.
    * From above two points, **we can conclude that we do not need to match these lps\[j-1\] characters with txt\[i-j…i-1\] because we know that these characters will anyway match.** Let us consider above example to understand this.

  ```text
  txt[] = "AAAAABAAABA" 
  pat[] = "AAAA"
  lps[] = {0, 1, 2, 3} 

  i = 0, j = 0
  txt[] = "AAAAABAAABA" 
  pat[] = "AAAA"
  txt[i] and pat[j] match, do i++, j++

  i = 1, j = 1
  txt[] = "AAAAABAAABA" 
  pat[] = "AAAA"
  txt[i] and pat[j] match, do i++, j++

  i = 2, j = 2
  txt[] = "AAAAABAAABA" 
  pat[] = "AAAA"
  pat[i] and pat[j] match, do i++, j++

  i = 3, j = 3
  txt[] = "AAAAABAAABA" 
  pat[] = "AAAA"
  txt[i] and pat[j] match, do i++, j++

  i = 4, j = 4
  Since j == M, print pattern found and reset j,
  j = lps[j-1] = lps[3] = 3

  Here unlike Naive algorithm, we do not match first three 
  characters of this window. Value of lps[j-1] (in above 
  step) gave us index of next character to match.
  i = 4, j = 3
  txt[] = "AAAAABAAABA" 
  pat[] =  "AAAA"
  txt[i] and pat[j] match, do i++, j++

  i = 5, j = 4
  Since j == M, print pattern found and reset j,
  j = lps[j-1] = lps[3] = 3

  Again unlike Naive algorithm, we do not match first three 
  characters of this window. Value of lps[j-1] (in above 
  step) gave us index of next character to match.
  i = 5, j = 3
  txt[] = "AAAAABAAABA" 
  pat[] =   "AAAA"
  txt[i] and pat[j] do NOT match and j > 0, change only j
  j = lps[j-1] = lps[2] = 2

  i = 5, j = 2
  txt[] = "AAAAABAAABA" 
  pat[] =    "AAAA"
  txt[i] and pat[j] do NOT match and j > 0, change only j
  j = lps[j-1] = lps[1] = 1 

  i = 5, j = 1
  txt[] = "AAAAABAAABA" 
  pat[] =     "AAAA"
  txt[i] and pat[j] do NOT match and j > 0, change only j
  j = lps[j-1] = lps[0] = 0

  i = 5, j = 0
  txt[] = "AAAAABAAABA" 
  pat[] =      "AAAA"
  txt[i] and pat[j] do NOT match and j is 0, we do i++.

  i = 6, j = 0
  txt[] = "AAAAABAAABA" 
  pat[] =       "AAAA"
  txt[i] and pat[j] match, do i++ and j++

  i = 7, j = 1
  txt[] = "AAAAABAAABA" 
  pat[] =       "AAAA"
  txt[i] and pat[j] match, do i++ and j++

  We continue this way...
  ```

### Implementation

```cpp
void computeLPSArray(char* pattern, int patternLen, int* lps);
  
// Prints occurrences of text[] in pattern[]
void KMPSearch(char* pattern, char* text)
{
    int patternLen = strlen(pattern);
    int textLen = strlen(text);
  
    // create lps[] that will hold the longest prefix suffix
    // values for pattern
    int lps[patternLen];
  
    // Preprocess the pattern (calculate lps[] array)
    computeLPSArray(pattern, patternLen, lps);
  
    int textIndex = 0; // index for text[]
    int patternIndex = 0; // index for pattern[]
    while (textIndex < textLen) {
        if (pattern[patternIndex] == text[textIndex]) {
            patternIndex++;
            textIndex++;
        }
  
        if (patternIndex == patternLen) {
            printf("Found pattern at index %d ", textIndex - patternIndex);
            patternIndex = lps[patternIndex - 1];
        }
  
        // mismatch after j matches
        else if (textIndex < textLen && pattern[patternIndex] != text[textIndex]) {
            // Do not match lps[0..lps[patternIndex-1]] characters,
            // they will match anyway
            if (patternIndex != 0)
                patternIndex = lps[patternIndex - 1];
            else
                textIndex = textIndex + 1;
        }
    }
}
  
// Fills lps[] for given patttern pattern[0..patternLen-1]
void computeLPSArray(char* pattern, int patternLen, int* lps)
{
    // length of the previous longest prefix suffix
    int lpsLen = 0;
  
    lps[0] = 0; // lps[0] is always 0
  
    // the loop calculates lps[i] for i = 1 to M-1
    int patternIndex = 1;
    while (patternIndex < patternLen) {
        if (pattern[patternIndex] == pattern[lpsLen]) {
            lpsLen++;
            lps[patternIndex] = lpsLen;
            patternIndex++;
        }
        else
        {
            // This is tricky. Consider the example.
            // AAACAAAA and i = 7. The idea is similar
            // to search step.
            if (lpsLen != 0) {
                lpsLen = lps[lpsLen - 1];
  
                // Also, note that we do not increment
                // i here
            }
            else // if (len == 0)
            {
                lps[patternIndex] = 0;
                patternIndex++;
            }
        }
    }
}
  
// Driver program to test above function
int main()
{
    char txt[] = "ABABDABACDABABCABAB";
    char pat[] = "ABABCABAB";
    KMPSearch(pat, txt);
    return 0;
}
```

