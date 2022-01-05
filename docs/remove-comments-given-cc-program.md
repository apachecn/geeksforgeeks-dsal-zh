# 从给定的 C/C++程序中删除注释

> 原文:[https://www . geesforgeks . org/remove-comments-given-cc-program/](https://www.geeksforgeeks.org/remove-comments-given-cc-program/)

给定一个 C/C++程序，删除其中的注释。
**我们强烈建议尽量减少你的浏览器，先自己试试这个。**
这个想法是维护两个标志变量，一个表示单行注释开始，另一个表示多行注释开始。当一个标志被设置时，我们寻找注释的结尾，忽略开始和结束之间的所有字符。
下面是上述思想的 C++实现。

## C

```
// C++ program to remove comments from a C/C++ program
#include <iostream>
using namespace std;

string removeComments(string prgm)
{
    int n = prgm.length();
    string res;

    // Flags to indicate that single line and multiple line comments
    // have started or not.
    bool s_cmt = false;
    bool m_cmt = false;

    // Traverse the given program
    for (int i=0; i<n; i++)
    {
        // If single line comment flag is on, then check for end of it
        if (s_cmt == true && prgm[i] == '\n')
            s_cmt = false;

        // If multiple line comment is on, then check for end of it
        else if  (m_cmt == true && prgm[i] == '*' && prgm[i+1] == '/')
            m_cmt = false,  i++;

        // If this character is in a comment, ignore it
        else if (s_cmt || m_cmt)
            continue;

        // Check for beginning of comments and set the approproate flags
        else if (prgm[i] == '/' && prgm[i+1] == '/')
            s_cmt = true, i++;
        else if (prgm[i] == '/' && prgm[i+1] == '*')
            m_cmt = true,  i++;

        // If current character is a non-comment character, append it to res
        else  res += prgm[i];
    }
    return res;
}

// Driver program to test above functions
int main()
{
    string prgm = "   /* Test program */ \n"
                  "   int main()  \n"
                  "   {           \n"
                  "      // variable declaration \n"
                  "      int a, b, c;    \n"
                  "      /* This is a test  \n"
                  "          multiline     \n"
                  "          comment for   \n"
                  "          testing */      \n"
                  "      a = b + c;       \n"
                  "   }           \n";
    cout << "Given Program \n";
    cout << prgm << endl;
    cout << " Modified Program ";
    cout << removeComments(prgm);
    return 0;
}
```

输出

```
Given Program
   /* Test program */
   int main()
   {
      // variable declaration
      int a, b, c;
      /* This is a test
          multiline
          comment for
          testing */
      a = b + c;
   }

 Modified Program
   int main()
   {
             int a, b, c;

          a = b + c;
   }
```

本文由萨钦·古普塔供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息