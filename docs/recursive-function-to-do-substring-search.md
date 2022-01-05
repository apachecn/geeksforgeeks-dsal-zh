# 递归函数做子串搜索

> 原文:[https://www . geesforgeks . org/recursive-function-to-do-substring-search/](https://www.geeksforgeeks.org/recursive-function-to-do-substring-search/)

给定一个文本 txt[]和一个模式 pat[]，编写一个递归函数“contains(char pat[]，char txt[])”，如果 pat[]存在于 txt[]，则返回 true，否则返回 false。

示例:

```
1) Input:   txt[] =  "THIS IS A TEST TEXT"
            pat[] = "TEST"
  Output:  true

2) Input:  txt[] =  "geeksforgeeks"
           pat[] = "quiz"
  Output:  false;
```

**强烈建议尽量减少浏览器，先自己试试这个。**

下面是递归算法。

```
contains(tex[], pat[])
    1) If the current character is the last character of the text, but pat
       has more characters, return false.

    2) Else If the current character is the last character of the pattern,
       then return true

    3) Else If current characters of pat and text match, then
        return contains(text + 1, pat + 1);

    4) Else If current characters of pat and text don't match
        return contains(text + 1, pat);

```

下面是上述算法的实现。

## C++

```
// Recursive C++ program to find if a given pattern is 
// present in a text
#include<iostream>
using namespace std;

bool exactMatch(char *text, char *pat)
{
    if (*text == '\0' && *pat != '\0')
        return false;

    // Else If last character of pattern reaches
    if (*pat == '\0')
        return true;

    if (*text == *pat)
        return exactMatch(text + 1, pat + 1);

    return false;
}

// This function returns true if 'text' contain 'pat'
bool contains(char *text, char *pat)
{
    // If last character of text reaches
    if (*text == '\0')
        return false;

    // If current characters of pat and text match
    if (*text == *pat)
        if(exactMatch(text, pat))
            return 1;
        else
          return contains(text + 1, pat);

    // If current characters of pat and tex don't match
    return contains(text + 1, pat);
}

// Driver program to test above function
int main()
{
    cout << contains("geeksforgeeks", "geeks") << endl;
    cout << contains("geeksforgeeks", "geeksquiz") << endl;
    cout << contains("geeksquizgeeks", "quiz") << endl;
    return 0;
}
```

## 蟒蛇 3

```
# Recursive Python3 program to find if a given pattern is 
# present in a text

def exactMatch(text, pat, text_index, pat_index):
    if text_index == len(text) and pat_index != len(pat):
        return 0

    # Else If last character of pattern reaches
    if pat_index == len(pat):
        return 1

    if text[text_index] == pat[pat_index]:
        return exactMatch(text, pat, text_index+1, pat_index+1)

    return 0

# This function returns true if 'text' contain 'pat'
def contains(text, pat, text_index, pat_index):
    # If last character of text reaches
    if text_index == len(text):
        return 0

    # If current characters of pat and text match
    if text[text_index] == pat[pat_index]:
        if exactMatch(text, pat, text_index, pat_index):
            return 1
        else:
            return contains(text, pat, text_index+1, pat_index)

    # If current characters of pat and tex don't match
    return contains(text , pat, text_index+1, pat_index)

# Driver program to test the above function

print(contains("geeksforgeeks", "geeks", 0, 0))
print(contains("geeksforgeeks", "geeksquiz", 0, 0))
print(contains("geeksquizgeeks", "quiz", 0, 0))

# This code is contributed by ankush_953.
```

**Output:**

```
1
0
1
```

本文由布平德供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论