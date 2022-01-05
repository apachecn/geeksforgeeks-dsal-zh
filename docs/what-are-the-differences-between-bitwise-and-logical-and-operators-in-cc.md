# C/c++中按位与逻辑 and 运算符有什么区别？

> 原文:[https://www . geeksforgeeks . org/cc 中按位和逻辑与运算符的区别是什么/](https://www.geeksforgeeks.org/what-are-the-differences-between-bitwise-and-logical-and-operators-in-cc/)

按位“与”运算符用“&”表示，逻辑运算符用“&&”表示。以下是这两种运算符之间的一些基本区别。

**a)** 逻辑 and 运算符“& &”要求其操作数为布尔表达式(1 或 0)，并返回一个布尔值。
按位“与”运算符“&”处理整型(短整型、整型、无符号型、char 型、bool 型、无符号型、长整型)值并返回整型值。

## C++

```
#include<iostream>
using namespace std;
int main()
{
    int x = 3;  //...0011
    int y = 7;  //...0111

    // A typical use of '&&'
    if (y > 1 && y > x)
      cout<<"y is greater than 1 AND x\n";

    // A typical use of '&'
    int z = x & y;   // 0011

    cout<<"z = "<< z;

    return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
#include<stdio.h>
int main()
{
    int x = 3;  //...0011
    int y = 7;  //...0111

    // A typical use of '&&'
    if (y > 1 && y > x)
      printf("y is greater than 1 AND x\n");

    // A typical use of '&'
    int z = x & y;   // 0011

    printf ("z = %d", z);

    return 0;
}
```

**Output**

```
y is greater than 1 AND x
z = 3
```

***时间复杂度:** O(1)*

辅助空间:0(1)

**b)** 如果一个整数值被用作“& &”的操作数，该操作数应该对布尔值起作用，则在 C.
中使用以下规则…..零被认为是假的，非零被认为是真的。

例如，在下面的程序中，x 和 y 被认为是 1。

## C++

```
#include<iostream>
using namespace std;

// Example that uses non-boolean expression as
// operand for '&&'
int main()
{
   int x = 2, y = 5;
   cout<<" "<< x&&y;
   return 0;
}

//this code is contributed by shivanisinghss2110
```

## C

```
#include<stdio.h>
// Example that uses non-boolean expression as
// operand for '&&'
int main()
{
   int x = 2, y = 5;
   printf("%d", x&&y);
   return 0;
}
```

**Output**

```
1
```

时间复杂度:0(1)

辅助空间:0(1)

将非整数表达式用作按位&的操作数是编译器错误。例如，以下程序显示编译器错误。

## C

```
#include<stdio.h>
// Example that uses non-integral expression as
// operator for '&'
int main()
{
   float x = 2.0, y = 5.0;
   printf("%d", x&y);
   return 0;
}
```

**输出:**

```
error: invalid operands to binary & (have 'float' and 'float')
```

时间复杂度:0(1)

辅助空间:0(1)

**c)** 如果第一个操作数变为假，则“& &”运算符不会计算第二个操作数。同样，当第一个操作数为真时，“||”不会计算第二个操作数。按位“&”和“|”运算符总是计算它们的操作数。

## C

```
#include<stdio.h>
int main()
{
    int x = 0;

    // 'Geeks in &&' is NOT
    // printed because x is 0
    printf("%d\n", (x && printf("Geeks in && ")));

    // 'Geeks in &' is  printed
    printf("%d\n", (x & printf("Geeks in & ")));

    return 0;
}
```

**Output**

```
0
Geeks in & 0
```

时间复杂度:0(1)

辅助空间:0(1)

逻辑 OR“| |”和按位 OR“|”之间有相同的区别。

本文由 **Ujjwal Jain** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。