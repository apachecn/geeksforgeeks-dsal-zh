# 在 C/C++

中使用 BitWise 运算符对字符串进行大小写转换(下限到上限，反之亦然)

> 原文:[https://www . geesforgeks . org/case-conversion-lower-upper-反之亦然-string-using-bitwise-operators-cc/](https://www.geeksforgeeks.org/case-conversion-lower-upper-vice-versa-string-using-bitwise-operators-cc/)

给定一个字符串，编写一个函数，使用按位运算符&(AND)、|(OR)、~(NOT)将字符串从小写转换为大写或从大写转换为小写，然后返回字符串。

我们中的许多人都知道，位运算比编译器执行算术运算更快，因为数据以二进制形式 0 和 1 存储。

示例:

```
Input : "LowerToUpPer"
Output : "LOWERTOUPPER"
   Letters already in the uppercase remains the same. 
   while rest get converted to uppercase.

Input : "UPPerTOloweR"
Output : "uppertolower"
   Letters already in the lowercase remains the same.
   while rest get converted to lowercase.

```

**1。小写到大写**
这个方法只是通过按位“与”(&)从小写字母的 ASCII 值中减去一个值 32，并将该字母转换为大写字母的否定(~)为 32。

```
// C++ program to convert a string from
// lower to upper case.
#include<stdio.h>

const int x = 32;

// Converts a string to uppercase
char *toUpperCase(char *a)
{
    for (int i=0; a[i]!='\0'; i++)
        a[i] = a[i] & ~x;

    return a;
}

// Driver Code
int main()
{
    char str[] = "SanjaYKannA";

    //Here it's recommended to use character array
    //as it's stored in read-write area.
    //If a pointer is used it's stored
    //in read-only memory as a string literal.

    printf("%s", toUpperCase(str));

    return 0;
}
```

输出:

```
SANJAYKANNA

```

**2。大写到小写**
类似地，它通过按位“或”(|)将大写字母的 ASCII 值加上 32，32 将字母转换为小写。

```
// C++ program to convert a string from
// upper to lower case.
#include<stdio.h>
const int x = 32;

// Converts a string to lowercase
char * toLowerCase(char *a)
{
    for (int i=0; a[i]!='\0'; i++)
        a[i] = a[i] | x;

    return a;
}

// Driver Code
int main()
{
    char str[] = "SanjaYKannA";
    printf("%s", toLowerCase(str));
    return 0;
}
```

输出:

```
sanjaykanna

```

**说明:**
[ASCII 表](http://www.asciitable.com/)的构造方式是小写字母的二进制表示与大写字母的二进制表示几乎相同。

字符“A”是整数 65 = (0100 0001)2，而字符“A”是整数 97 = (0110 0001)2。
ASCII 值“A”和“A”的差值为 32。

因此，我们可以使用如上所示的按位运算符，通过增加或减少字母之间的差异，轻松地将字母的大小写从大写更改为小写或从小写更改为大写。

**练习:**
实现一个改变字符串大小写的函数，使得极客变成极客。

本文由海得拉巴 **[JNTUH 工程学院](http://jntuhceh.ac.in/)**Sanjay Kumar Ulsha 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。