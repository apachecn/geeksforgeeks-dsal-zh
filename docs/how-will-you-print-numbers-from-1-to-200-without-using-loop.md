# 不使用循环，如何打印 1 到 100 的数字？

> 原文:[https://www . geeksforgeeks . org/不使用循环将如何打印从 1 到 200 的数字/](https://www.geeksforgeeks.org/how-will-you-print-numbers-from-1-to-200-without-using-loop/)

如果我们仔细看看这个问题，我们可以看到“循环”的想法是跟踪一些计数器值，例如“i=0”直到“i <= 100”. So if we aren’t allowed to use loop, how else can be track something in C language! 
好吧，一种可能性是使用‘递归’，前提是我们仔细使用终止条件。这里有一个使用递归打印数字的解决方案。

**<u>法-1:</u>**

## C++

```
// C++ program to How will you print
//  numbers from 1 to 100 without using loop?
#include <iostream>
using namespace std;

class gfg
{

// Prints numbers from 1 to n
public:
void printNos(unsigned int n)
{
    if(n > 0)
    {
        printNos(n - 1);
        cout << n << " ";
    }
    return;
}
};

// Driver code
int main()
{
    gfg g;
    g.printNos(100);
    return 0;
}

// This code is contributed by SoM15242
```

## C

```
#include <stdio.h>

// Prints numbers from 1 to n
void printNos(unsigned int n)
{
    if(n > 0)
    {
        printNos(n - 1);
        printf("%d ", n);
    }
    return;
}

// Driver code
int main()
{
    printNos(100);
    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

class GFG
{
    // Prints numbers from 1 to n
    static void printNos(int n)
    {
        if(n > 0)
        {
            printNos(n - 1);
            System.out.print(n + " ");
        }
        return;
    }

    // Driver Code
    public static void main(String[] args)
    {
        printNos(100);
    }
}

// This code is contributed by Manish_100
```

## 蟒蛇 3

```
# Python3 program to Print
# numbers from 1 to n

def printNos(n):
    if n > 0:
        printNos(n - 1)
        print(n, end = ' ')

# Driver code
printNos(100)

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# code for print numbers from
// 1 to 100 without using loop
using System;

class GFG
{

    // Prints numbers from 1 to n
    static void printNos(int n)
    {
        if(n > 0)
        {
            printNos(n - 1);
            Console.Write(n + " ");
        }
        return;
    }

// Driver Code
public static void Main()
{
        printNos(100);
}
}

// This code is contributed by Ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program print numbers
// from 1 to 100 without
// using loop   

// Prints numbers from 1 to n
function printNos($n)
{
    if($n > 0)
    {
        printNos($n - 1);
        echo $n, " ";
    }
    return;
}

// Driver code
printNos(100);

// This code is contributed by vt_m
?>
```

## java 描述语言

```
<script>
    // Javascript code for print numbers from
    // 1 to 100 without using loop

    // Prints numbers from 1 to n
    function printNos(n)
    {
        if(n > 0)
        {
            printNos(n - 1);
            document.write(n + " ");
        }
        return;
    }

    printNos(100);

// This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 
16 17 18 19 20 21 22 23 24 25 26 27 
28 29 30 31 32 33 34 35 36 37 38 39
40 41 42 43 44 45 46 47 48 49 50 51
52 53 54 55 56 57 58 59 60 61 62 63
64 65 66 67 68 69 70 71 72 73 74 75
76 77 78 79 80 81 82 83 84 85 86 87
88 89 90 91 92 93 94 95 96 97 98 99 
100 
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

**<u>方法二:</u>**

## C++

```
// C++ program
#include <bits/stdc++.h>
using namespace std;

void printNos(int initial, int last)
{
    if (initial <= last) {
        cout << initial << " ";
        printNos(initial + 1, last);
    }
}

int main()
{
    printNos(1, 100);
    return 0;
}

// This code is contributed by ukasp.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
    public static void main(String[] args)
    {
        printNos(1, 100);
    }
    public static void printNos(int initial, int last)
    {
        if (initial <= last) {
            System.out.print(initial + " ");
            printNos(initial + 1, last);
        }
    }
}
```

## 蟒蛇 3

```
def printNos(initial, last):
    if(initial<=last):
        print(initial)
        printNos(initial+1,last)
printNos(1,10)
```

## C#

```
/*package whatever //do not write package name here */

using System;
public class GFG {
    public static void Main(String[] args)
    {
        printNos(1, 100);
    }
    public static void printNos(int initial, int last)
    {
        if (initial <= last) {
            Console.Write(initial + " ");
            printNos(initial + 1, last);
        }
    }
}

// This code contributed by gauravrajput1
```

## java 描述语言

```
/*package whatever //do not write package name here */

    printNos(1, 100);

    function printNos(initial, last)
    {
        if (initial <= last) {
            document.write(initial + " ");
            printNos(initial + 1, last);
        }
    }

// This code is contributed by shivanisinghss2110
```

**Output**

```
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 91 92 93 94 95 96 97 98 99 100 
```

**时间复杂度:** O(n)

***辅助空间:** O(n)*
现在试着写一个程序，做同样的事情，但是没有任何“如果”的构造。
提示—使用一些可以用来代替“如果”的运算符。
请注意，递归技术很好，但是每次调用函数都会在程序堆栈中创建一个“堆栈帧”。因此，如果有限的内存有限制，我们需要打印大量的数字，“递归”可能不是一个好主意。那么，还有什么其他选择呢？
另一种选择是“goto”语句。虽然“goto”的使用不像一般的编程实践那样受影响，因为“goto”语句改变了正常的程序执行顺序，但是在某些情况下，使用“goto”是最好的解决方案。
所以请试着用“goto”语句打印 1 到 100 的数字。可以使用 [GfG IDE！](https://ide.geeksforgeeks.org/)
[用 C++打印 1 到 100，没有循环和递归](https://www.geeksforgeeks.org/output-of-c-program-set-18-3/)