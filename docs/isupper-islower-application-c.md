# isupper()和 islower()及其在 C++中的应用

> 原文:[https://www . geeksforgeeks . org/I upper-islower-application-c/](https://www.geeksforgeeks.org/isupper-islower-application-c/)

在 C++中，isupper()和 islower()是用于字符串和字符处理的预定义函数。cstring.h 是字符串函数所需的头文件，cctype.h 是字符函数所需的头文件。

**isupper()函数**
此函数用于检查参数是否包含任何大写字母，如 A、B、C、D、…、z。

```
Syntax
int isupper(int x)
```

## C++

```
// Program to check if a character is in
// uppercase using isupper()
#include <iostream>
#include <cctype>
using namespace std;
int main()
{
    char x;
    cin >> x;
    if (isupper(x))
        cout << "Uppercase";
    else
        cout << "Not uppercase.";   
    return 0;
}
```

```
Input : A
Output : Uppercase
```

```
Input : a
Output : Not uppercase
```

**islower()函数**
该函数用于检查参数是否包含小写字母，如 a、b、c、d、…、z。

```
Syntax
int islower(int x)

```

## C++

```
// Program to check if a character is in
// lowercase using islower()
#include <iostream>
#include <cctype>
using namespace std;
int main()
{
    char x;
    cin >> x;
    if (islower(x))
        cout << "Lowercase";
    else
        cout << "Not Lowercase.";   

    return 0;
}
```

```
Input:A
Output : Not Lowercase
```

```
Input : a
Output : Lowercase
```

**is lower()，isupper()，tolower()，toupper()函数的应用。**
给定一个字符串，任务是将字符串中的字符转换成相反的大小写，即如果一个字符是小写的，我们需要将其转换成大写，反之亦然。

```
Syntax of tolower():

int tolower(int ch);
```

```
Syntax of toupper():

int toupper(int ch);
```

**示例:**

```
Input : GeekS
Output :gEEKs

Input :Test Case
Output :tEST cASE
```

1.逐个字符遍历给定的字符串直到其长度，使用预定义的函数检查字符是小写还是大写。
3。如果小写，使用 toupper()函数将其转换为大写，如果大写，使用 tolower()函数将其转换为小写。
4。打印最后一个字符串。

## C++

```
// C++ program to toggle cases of a given
// string.
#include <iostream>
#include <cstring>
using namespace std;

// function to toggle cases of a string
void toggle(string& str)
{
    int length = str.length();
    for (int i = 0; i < length; i++) {
        int c = str[i];
        if (islower(c))
            str[i] = toupper(c);
        else if (isupper(c))
            str[i] = tolower(c);       
    }
}

// Driver Code
int main()
{
    string str = "GeekS";
    toggle(str);
    cout << str;
    return 0;
}
```

**输出:**

```
gEEKs
```

本文由 **Ayush Saxena** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。