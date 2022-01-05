# 三角形数

> 原文:[https://www.geeksforgeeks.org/triacontagon-number/](https://www.geeksforgeeks.org/triacontagon-number/)

给定一个编号 **N** ，任务是找到**N<sup>th</sup>T5[三十烷编号](https://en.wikipedia.org/wiki/Triacontagon)。** 

> 一个[三十烷数](https://en.wikipedia.org/wiki/Triacontagon)是一类数字。它有 30 边的多边形，叫做三十边形。第 N 个三十进制数是 30 个数的点，所有其他的点被一个公共的共享角包围并形成一个图案。前几个三十烷醇的数字是 **1、30、87、172……**

**例:**

> **输入:** N = 2
> **输出:** 30
> **说明:**
> 第二个三十烷数为 30。
> **输入:** N = 3
> **输出:** 87

**方法:**第 N 个三十烷数由公式给出:

*   s 边多边形的第 n 项= ![\frac{((s-2)n^2 - (s-4)n)}{2}   ](img/e1b7be7ec1f82453b47cd0c23edff33f.png "Rendered by QuickLaTeX.com")

*   因此 30 边多边形的第 n 项是

> ![Tn =\frac{((30-2)n^2 - (30-4)n)}{2} =\frac{(28n^2 - 26n)}{2} ](img/dbdd1150b4720cb4c6ca1bcbe9ba61e8.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Finding the nth triacontagonal number
int triacontagonalNum(int n)
{
    return (28 * n * n - 26 * n) / 2;
}

// Driver code
int main()
{
    int n = 3;

    cout << "3rd triacontagonal Number is = "
         << triacontagonalNum(n);

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program for above approach
#include <stdio.h>
#include <stdlib.h>

// Finding the nth triacontagonal Number
int triacontagonalNum(int n)
{
    return (28 * n * n - 26 * n) / 2;
}

// Driver program to test above function
int main()
{
    int n = 3;
    printf("3rd triacontagonal Number is = %d",
           triacontagonalNum(n));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;
import java.util.*;

class GFG {

// Finding the nth triacontagonal number
static int triacontagonalNum(int n)
{
    return (28 * n * n - 26 * n) / 2;
}

// Driver code
public static void main(String[] args)
{
    int n = 3;

    System.out.println("3rd triacontagonal Number is = " +
                                    triacontagonalNum(n));
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 program for above approach

# Finding the nth triacontagonal Number
def triacontagonalNum(n):

    return (28 * n * n - 26 * n) // 2

# Driver Code
n = 3
print("3rd triacontagonal Number is = ",
                   triacontagonalNum(n))

# This code is contributed by divyamohan123
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Finding the nth triacontagonal number
static int triacontagonalNum(int n)
{
    return (28 * n * n - 26 * n) / 2;
}

// Driver code
public static void Main()
{
    int n = 3;

    Console.Write("3rd triacontagonal Number is = " +
                               triacontagonalNum(n));
}
}

// This code is contributed by Akanksha_Rai
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Finding the nth triacontagonal number
function triacontagonalNum(n)
{
    return (28 * n * n - 26 * n) / 2;
}

// Driver code
var n = 3;
document.write("3rd triacontagonal Number is = " + triacontagonalNum(n));

</script>
```

**Output:** 

```
3rd triacontagonal Number is = 87
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

**参考资料:**[https://en . Wikipedia . org/wiki/tricontgon](https://en.wikipedia.org/wiki/Triacontagon)