# 程序打印系列 1、3、4、8、15、27、50…直到 N 个术语

> 原文:[https://www . geesforgeks . org/program-to-print-the-series-1-3-4-8-15-27-50-till-n-terms/](https://www.geeksforgeeks.org/program-to-print-the-series-1-3-4-8-15-27-50-till-n-terms/)

给定一个数字 **N** ，任务是打印以下系列的第一个 **N** 术语:

```
1, 3, 4, 8, 15, 27, 50…
```

**示例:**

> **输入:** N = 7
> **输出:** 1、3、4、8、15、27、50
> **输入:** N = 3
> **输出:** 1、3、4

**方法:**从给定的级数中，我们可以找到第 n 项的公式:

> 第一学期= 1，第二学期= 3，第三学期= 4
> 第四学期=第一学期+第二学期+第三学期
> 第五学期=第二学期+第三学期+第四学期
> 第六学期=第三学期+第四学期+第五学期
> 。
> 。
> 依此类推

因此，想法是跟踪系列的最后三个术语，并找到系列的连续术语。

下面是上述方法的实现:

## C++

```
// C++ implementation to print the
// N terms of the series whose three
// terms are given

#include "bits/stdc++.h"
using namespace std;

// Function to print the series
void printSeries(int n, int a,
                 int b, int c)
{

    int d;

    // Generate the ith term and
    // print it
    if (n == 1) {
        cout << a << " ";
        return;
    }
    if (n == 2) {
        cout << a << " " << b << " ";
        return;
    }

    cout << a << " " << b
         << " " << c << " ";

    for (int i = 4; i <= n; i++) {
        d = a + b + c;
        cout << d << " ";
        a = b;
        b = c;
        c = d;
    }
}

// Driver Code
int main()
{
    int N = 7, a = 1, b = 3;
    int c = 4;

    // Function Call
    printSeries(N, a, b, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print the
// N terms of the series whose three
// terms are given

//include "bits/stdJava.h"
import java.util.*;
class GFG{

// Function to print the series
static void printSeries(int n, int a,
                         int b, int c)
{
    int d;

    // Generate the ith term and
    // print it
    if (n == 1)
    {
        System.out.print(a + " ");
        return;
    }
    if (n == 2)
    {
        System.out.print(a + " " +  b + " ");
        return;
    }

    System.out.print(a + " " +
                     b + " " + 
                     c + " ");

    for (int i = 4; i <= n; i++)
    {
        d = a + b + c;
        System.out.print(d + " ");
        a = b;
        b = c;
        c = d;
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 7, a = 1, b = 3;
    int c = 4;

    // Function Call
    printSeries(N, a, b, c);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to print the
# N terms of the series whose three
# terms are given

# Function to print the series
def printSeries(n, a, b, c):

    # Generate the ith term and
    # print it
    if (n == 1):
        print(a, end = " ");
        return;

    if (n == 2):
        print(a, b, end = " ");
        return;

    print(a, b, c, end = " ");

    for i in range (4, n + 1):
        d = a + b + c;
        print(d, end = " ");
        a = b;
        b = c;
        c = d;

# Driver Code
N = 7; a = 1; b = 3;
c = 4;

# Function Call
printSeries(N, a, b, c);

# This code is contributed by Code_Mech
```

## C#

```
// C# implementation to print the
// N terms of the series whose three
// terms are given
using System;
class GFG{

// Function to print the series
static void printSeries(int n, int a,
                        int b, int c)
{
    int d;

    // Generate the ith term and
    // print it
    if (n == 1)
    {
        Console.Write(a + " ");
        return;
    }
    if (n == 2)
    {
        Console.Write(a + " " +
                      b + " ");
        return;
    }

    Console.Write(a + " " +
                  b + " " +
                  c + " ");

    for(int i = 4; i <= n; i++)
    {
       d = a + b + c;
       Console.Write(d + " ");

       a = b;
       b = c;
       c = d;
    }
}

// Driver Code
public static void Main()
{
    int N = 7, a = 1, b = 3;
    int c = 4;

    // Function call
    printSeries(N, a, b, c);
}
}

// This code is contributed by rock cool
```

## java 描述语言

```
<script>
// javascript implementation to print the
// N terms of the series whose three
// terms are given

// Function to print the series
function printSeries( n,  a,
                  b,  c)
{

    let d;

    // Generate the ith term and
    // print it
    if (n == 1) {
        document.write( a + " ");
        return;
    }
    if (n == 2) {
        document.write( a + " " + b + " ");
        return;
    }

    document.write( a + " " + b
         + " " + c + " ");

    for (let i = 4; i <= n; i++) {
        d = a + b + c;
        document.write( d + " ");
        a = b;
        b = c;
        c = d;
    }
}

// Driver Code

    let N = 7, a = 1, b = 3;
    let c = 4;

    // Function Call
    printSeries(N, a, b, c);

// This code is contributed by gauravrajput1

</script>
```

**Output:** 

```
1 3 4 8 15 27 50
```