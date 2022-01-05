# 在 C++中标记字符串

> 原文:[https://www.geeksforgeeks.org/tokenizing-a-string-cpp/](https://www.geeksforgeeks.org/tokenizing-a-string-cpp/)

将字符串标记化表示相对于某些分隔符拆分字符串。有许多方法可以标记字符串。本文解释了其中的四个:

### 使用 stringstream

一个**字符串流**将一个字符串对象与一个流相关联，允许您像读取一个流一样读取该字符串。

下面是 C++实现:

## c++

```
// Tokenizing a string using stringstream
#include <bits/stdc++.h>

using namespace std;

int main()
{

    string line = "GeeksForGeeks is a must try";

    // Vector of string to save tokens
    vector <string> tokens;

    // stringstream class check1
    stringstream check1(line);

    string intermediate;

    // Tokenizing w.r.t. space ' '
    while(getline(check1, intermediate, ' '))
    {
        tokens.push_back(intermediate);
    }

    // Printing the token vector
    for(int i = 0; i < tokens.size(); i++)
        cout << tokens[i] << '\n';
}
```

输出

```
GeeksForGeeks
is
a
must
try
```