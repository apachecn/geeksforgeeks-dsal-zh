# 不使用循环，如何打印 1 到 100 的数字？| Set-2

> 原文:[https://www . geesforgeks . org/program-print-up-100-不使用循环/](https://www.geeksforgeeks.org/program-print-upto-100-without-using-loops/)

如果我们仔细看一下这个问题，我们可以看到“循环”的思想是跟踪某个计数器值，例如“i=0”直到“i <= 100″. So if we aren’t allowed to use loop, how else can be track something in C language!
可以通过多种方式完成，使用任何循环条件打印数字，例如 for()，while()，do-while()。但是同样可以在不使用循环的情况下完成(使用递归函数，goto 语句)。

使用递归函数打印从 1 到 100 的数字已经在 [Set-1](https://www.geeksforgeeks.org/how-will-you-print-numbers-from-1-to-200-without-using-loop/) 中讨论过。在这篇文章中，我们讨论了另外两种方法:

**1。使用 goto 语句:**

## C++

```
#include <iostream>
using namespace std;

int main()
{
    int i = 0;

begin:
    i = i + 1;
    cout << i << " ";

    if (i < 100)
    {
        goto begin;
    }
    return 0;
}

// This code is contributed by ShubhamCoder
```

## C

```
#include <stdio.h>

int main()
{
    int i = 0;
begin:
    i = i + 1;
    printf("%d ", i);

    if (i < 100)
        goto begin;
    return 0;
}
```

## C#

```
using System;

class GFG{

static public void Main ()
{
    int i = 0;
    begin:
        i = i + 1;
        Console.Write(" " + i + " ");

        if (i < 100)
        {
            goto begin;
        }
}
}

// This code is contributed by ShubhamCoder
```

**Output:** 

```
1 2 3 4 . . . 97 98 99 100
```