# 编写自己的忽略案例的 strcmp

> 原文:[https://www . geeksforgeeks . org/write-your-your-strcmp-哪些-忽略-cases/](https://www.geeksforgeeks.org/write-your-own-strcmp-which-ignores-cases/)

编写一个修改后的 strcmp 函数，该函数忽略大小写，如果 s1 < s2, 0 if s1 = s2, else returns 1\. For example, your strcmp should consider “GeeksforGeeks” and “geeksforgeeks” as same string.
返回-1 来源:[微软面试集 5](https://www.geeksforgeeks.org/microsoft-interview-set-5/)
以下解决方案假设字符使用 ASCII 表示法表示，即‘a’、‘b’、‘c’、‘z’的代码分别为 97、98、99、… 122。而‘A’、‘B’、‘C’、‘Z’的代码分别为 65、66、……90。
具体步骤如下。
**1)** 遍历两个字符串的每个字符，并对每个字符执行以下操作。
……**a)**如果 str1[i]与 str2[i]相同，则继续。
… **b)** 如果将 str1[i]的第 6 个最低有效位反相，使其与 str2[i]相同，则继续。例如，如果 str1[i]是 65，那么反转第 6 位将使其为 97。如果 str1[i]为 97，则第 6 位反相后为 65。
……**c)**如果以上两个条件中有一个不成立，那么就破。
**2)** 比较最后一个(或不相同时第一个不匹配)字符。

## C++

```
#include <bits/stdc++.h>
using namespace std;
/* implementation of strcmp that ignores cases */
int ic_strcmp(string s1, string s2)
{
    int i;
    for (i = 0; s1[i] && s2[i]; ++i)
    {
        /* If characters are same or inverting the
        6th bit makes them same */
        if (s1[i] == s2[i] || (s1[i] ^ 32) == s2[i])
        continue;
        else
        break;
    }

    /* Compare the last (or first mismatching in
    case of not same) characters */
    if (s1[i] == s2[i])
        return 0;

    // Set the 6th bit in both, then compare
    if ((s1[i] | 32) < (s2[i] | 32))
        return -1;
    return 1;
}

// Driver program to test above function
int main()
{
    cout<<"ret: "<<ic_strcmp("Geeks", "apple") <<endl;
    cout<<"ret: "<<ic_strcmp("", "ABCD")<<endl;
    cout<<"ret: "<<ic_strcmp("ABCD", "z")<<endl;
    cout<<"ret: "<<ic_strcmp("ABCD", "abcdEghe")<<endl;
    cout<<"ret: "<<ic_strcmp("GeeksForGeeks", "gEEksFORGeEKs")<<endl;
    cout<<"ret: "<<ic_strcmp("GeeksForGeeks", "geeksForGeeks")<<endl;
    return 0;
}

//This code is contributed by rathbhupendra
```

## C

```
#include <stdio.h>

/* implementation of strcmp that ignores cases */
int ic_strcmp(char *s1, char *s2)
{
    int i;
    for (i = 0; s1[i] && s2[i]; ++i)
    {
        /* If characters are same or inverting the
           6th bit makes them same */
        if (s1[i] == s2[i] || (s1[i] ^ 32) == s2[i])
           continue;
        else
           break;
    }

    /* Compare the last (or first mismatching in
       case of not same) characters */
    if (s1[i] == s2[i])
        return 0;

    // Set the 6th bit in both, then compare
    if ((s1[i] | 32) < (s2[i] | 32))
        return -1;
    return 1;
}

// Driver program to test above function
int main(void)
{
    printf("ret: %d\n", ic_strcmp("Geeks", "apple"));
    printf("ret: %d\n", ic_strcmp("", "ABCD"));
    printf("ret: %d\n", ic_strcmp("ABCD", "z"));
    printf("ret: %d\n", ic_strcmp("ABCD", "abcdEghe"));
    printf("ret: %d\n", ic_strcmp("GeeksForGeeks", "gEEksFORGeEKs"));
    printf("ret: %d\n", ic_strcmp("GeeksForGeeks", "geeksForGeeks"));
    return 0;
}
```

输出:

```
ret: 1
ret: -1
ret: -1
ret: -1
ret: 0
ret: 0
```

***时间复杂度:** O(min(|s1|，| S2 |)*

***辅助空间:** O(1)*

本文由**纳伦德拉·康拉尔卡尔**整理。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。