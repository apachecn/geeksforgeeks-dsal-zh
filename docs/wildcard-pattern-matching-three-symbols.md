# 通配符模式匹配有三个符号(*、+、？)

> 原文:[https://www . geesforgeks . org/通配符-模式匹配-三个符号/](https://www.geeksforgeeks.org/wildcard-pattern-matching-three-symbols/)

给定文本和通配符模式，实现通配符模式匹配算法，以发现通配符模式是否与文本匹配。匹配应该覆盖整个文本(而不是部分文本)。

通配符模式可以包括字符“？”、“*”和“+”。

```
‘?’ – matches any single character
‘*’ – Matches any sequence of characters
      (including the empty sequence)
'+' – Matches previous single character
      of pattern 
```

示例:

```
Input :Text = "baaabaaa",
Pattern = “****+ba*****a+", output : true
Pattern = "baaa?ab", output : false 
Pattern = "ba*a?", output : true
Pattern = "+a*ab", output : false 

Input : Text = "aab"
Pattern = "*+"  output : false 
Pattern = "*+b" output : true    

```

**情况 1:字符为' ***
这里出现两种情况:我们可以忽略' * '字符，移到模式中的下一个字符。* "字符与文本中的一个或多个字符匹配。这里我们将移动到字符串中的下一个字符。

**案例二:人物是“？”**我们可以忽略文本中的当前字符，转到模式和文本中的下一个字符。

**情况 3:字符为“+”**
这里出现两种情况:我们将文本的当前字符与模式的前一个字符进行匹配。如果没有前面的字符，这意味着“+”是模式的第一个字符，因此我们将结果打印为“文本不匹配”。如果前一个字符是“+”、“？”或者‘*’我们用他们使用的最后一个字符替换它。

**情况 4:字符不是通配符**
如果文本中的当前字符与模式中的当前字符匹配，我们将移动到模式和文本中的下一个字符。如果它们不匹配，则通配符模式和文本不匹配。

“*”、“？”的过程类似于两个字符的[通配符模式匹配](https://www.geeksforgeeks.org/wildcard-pattern-matching/):

```
Here we use a dp table that will contain 
two fields 
Struct DP
{
   // value is true if match possible
   // for current indexes, else false.
   bool value; 

   // Stores the character used 
   // by the symbol that we used 
   // later for symbol '+'
   char ch; 
}  

```

下面 c++实现上面的想法。

```
// C++ program to implement wildcard
// pattern matching algorithm
#include <bits/stdc++.h>
using namespace std;

struct DP {
    bool value;
    char ch;
};

// Function that matches input str with
// given wildcard pattern
bool strmatch(string str, string pattern,
              int n, int m)
{
    // empty pattern can only match with
    // empty string
    if (m == 0)
        return (n == 0);

    // If first character of pattern is '+'
    if (pattern[0] == '+')
        return false;

    // lookup table for storing results of
    // subproblems
    struct DP lookup[m + 1][n + 1];

    // initialize lookup table to false
    for (int i = 0; i <= m; i++)
        for (int j = 0; j <= n; j++) {
            lookup[i][j].value = false; 
            lookup[i][j].ch = ' '; 
        }  

    // empty pattern can match with
    // empty string
    lookup[0][0].value = true;

    // Only '*' can match with empty string
    for (int j = 1; j <= n; j++)
        if (pattern[j - 1] == '*')
            lookup[j][0].value = 
                   lookup[j - 1][0].value;

    // fill the table in bottom-up fashion
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {

            // Two cases if we see a '*'
            // a) We ignore ‘*’ character and move
            // to next character in the pattern,
            // i.e., ‘*’ indicates an empty sequence.
            // b) '*' character matches with ith
            // character in input
            if (pattern[i - 1] == '*') {
                lookup[i][j].value =
                       lookup[i][j - 1].value || 
                       lookup[i - 1][j].value;
                lookup[i][j].ch = str[j - 1];
            }

            // Current characters are considered as
            // matching in two cases
            // (a) current character of pattern is '?'
            else if (pattern[i - 1] == '?') {
                lookup[i][j].value = 
                          lookup[i - 1][j - 1].value;
                lookup[i][j].ch = str[j - 1];
            }

            // (b) characters actually match
            else if (str[j - 1] == pattern[i - 1])
                lookup[i][j].value =
                       lookup[i - 1][j - 1].value;

            // Current character match
            else if (pattern[i - 1] == '+')

                // case 1: if previous character is 
                // not symbol
                if (pattern[i - 2] != '+' ||
                    pattern[i - 2] != '*' ||
                    pattern[i - 2] != '?')
                    if (pattern[i - 2] == str[j - 1]) {
                        lookup[i][j].value = 
                           lookup[i - 1][j - 1].value;
                        lookup[i][j].ch = str[j - 1];
                    }

                    // case 2 : if previous character 
                    // is symbol (+, *, ? ) then we 
                    // compare current text character 
                    // with the character that is used by
                    // the symbol  at that point. we 
                    // access it by lookup[i-1][j-1]
                    else if (str[j-1] == lookup[i-1][j-1].ch) {
                        lookup[i][j].value =
                              lookup[i - 1][j - 1].value;
                        lookup[i][j].ch =
                              lookup[i - 1][j - 1].ch;
                    }

                    // If characters don't match
                    else
                        lookup[i][j].value = false;
        }
    }

    return lookup[m][n].value;
}

// Driver code
int main()
{
    string str = "baaabaaa";
    string pattern = "*****+ba***+";

    if (strmatch(str, pattern, str.length(),
                       pattern.length()))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}
```

输出:

```
Yes

```

时间复杂度:0(n * m)