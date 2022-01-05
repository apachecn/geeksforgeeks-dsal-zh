# 在 C/C++中反转字符串的不同方法

> 原文:[https://www . geesforgeks . org/reverse-a-string-in-c-CPP-differential-methods/](https://www.geeksforgeeks.org/reverse-a-string-in-c-cpp-different-methods/)

给定一个字符串，编写一个 C/C++程序来反转它。

![string-reverse](img/cae5a93160f0bfede3e4c4695e484c6f.png)

1.  **通过交换字符来编写自己的反函数:**一个简单的解决方法是编写自己的反函数，在 C++ 中反转一个[字符串。](https://www.geeksforgeeks.org/c-string-class-and-its-applications/) 

## 卡片打印处理机（Card Print Processor 的缩写）

```
// A Simple C++ program to reverse a string
#include <bits/stdc++.h>
using namespace std;

// Function to reverse a string
void reverseStr(string& str)
{
    int n = str.length();

    // Swap character starting from two
    // corners
    for (int i = 0; i < n / 2; i++)
        swap(str[i], str[n - i - 1]);
}

// Driver program
int main()
{
    string str = "geeksforgeeks";
    reverseStr(str);
    cout << str;
    return 0;
}
```

1.  输出:

```
skeegrofskeeg
```

2.  **使用内置的“反向”功能:**在“算法”头文件中有一个直接做反向的功能，可以节省我们编程时的时间。

```
// Reverses elements in [begin, end]
void reverse (BidirectionalIterator begin, 
BidirectionalIterator end);
```

## 卡片打印处理机（Card Print Processor 的缩写）

```
// A quickly written program for reversing a string
// using reverse()
#include <bits/stdc++.h>
using namespace std;
int main()
{
    string str = "geeksforgeeks";

    // Reverse str[begin..end]
    reverse(str.begin(), str.end());

    cout << str;
    return 0;
}
```

1.  输出:

```
skeegrofskeeg
```

2.  **只打印反转** :

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to print reverse of a string
#include <bits/stdc++.h>
using namespace std;

// Function to reverse a string
void reverse(string str)
{
   for (int i=str.length()-1; i>=0; i--)
      cout << str[i];
}

// Driver code
int main(void)
{
    string s = "GeeksforGeeks";
    reverse(s);
    return (0);
}
```

1.  输出:

```
skeegrofskeeG
```

1.  **反转一个常量字符串:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to get reverse of a const string
#include <bits/stdc++.h>
using namespace std;

// Function to reverse string and return
// reverse string pointer of that
char* reverseConstString(char const* str)
{
    // find length of string
    int n = strlen(str);

    // create a dynamic pointer char array
    char *rev = new char[n+1];

    // copy of string to ptr array
    strcpy(rev, str);

    // Swap character starting from two
    // corners
    for (int i=0, j=n-1; i<j; i++,j--)
        swap(rev[i], rev[j]);      

    // return pointer of the reversed string
    return rev;
}

// Driver code
int main(void)
{
    const char *s = "GeeksforGeeks";
    printf("%s", reverseConstString(s));
    return (0);
}
```

1.  输出:

```
skeeGrofskeeG
```

1.  **使用构造函数反向字符串:**将反向迭代器传递给构造函数会返回一个反向字符串。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// A simple C++ program to reverse string using constructor
#include <bits/stdc++.h>
using namespace std;
int main(){

    string str = "GeeksforGeeks";

    //Use of reverse iterators
    string rev = string(str.rbegin(),str.rend());

    cout<<rev<<endl;
    return 0;
}
```

1.  输出:

```
skeeGrofskeeG
```

5.**使用临时绳子**

## C++

```
// A simple C++ program to reverse string using constructor
#include <bits/stdc++.h>
using namespace std;
int main(){

    string str = "GeeksforGeeks";
    int n=str.length();
    //Temporary string to store the reverse
    string rev;
    for(int i=n-1;i>=0;i--)
      rev.push_back(str[i]);

    cout<<rev<<endl;
    return 0;
}
```

输出:

> 斯基格罗夫斯基格

？list = plqm7 alhxfysg6 gsrme 2 ni4k 8 fph5 qvb
本文由 **Priyam kakati、巨然活女神、Somesh Awasthi** 供稿，经 **Supratik Mitra、Lakshay Bansal** 改进。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息