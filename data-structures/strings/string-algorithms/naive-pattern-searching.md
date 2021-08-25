# Naive Pattern Searching

Slide the pattern over text one by one and check for a match. If a match is found, then slides by 1 again to check for subsequent matches.

```cpp
void search(char* pattern, char* text)
{
    int patternLen = strlen(pattern);
    int textLen = strlen(text);
 
    /* A loop to slide pat[] one by one */
    for (int textIndex = 0; textIndex <= textLen - patternLen; textIndex++) {
        int pattern_index;
 
        /* For current textIndex, check for pattern match */
        for (patternIndex = 0; patternIndex < patternLen; patternIndex++)
            if (text[textIndex + patternIndex] != pattern[patternIndex])
                break;
 
        if (patternIndex == patternLen)
            cout << "Pattern found at index " << textIndex << endl;
    }
}
```

Worst case also occurs when only the last character is different. 

```text
txt[] = "AAAAAAAAAAAAAAAAAB";
pat[] = "AAAAB";
```

The number of comparisons in the worst case is O\(m\*\(n-m+1\)\). Although strings which have repeated characters are not likely to appear in English text, they may well occur in other applications \(for example, in binary texts\). The [KMP matching algorithm](kmp-matching-algorithm-knuth-morris-pratt.md) improves the worst case to O\(n\). 

