# 非直角数字

> 原文:[https://www.geeksforgeeks.org/nonagonal-number/](https://www.geeksforgeeks.org/nonagonal-number/)

一个 [**非直角数**](https://en.wikipedia.org/wiki/Nonagonal_number) 是一个将三角形和正方形的概念扩展到非直角的图形数。具体来说，第 n 个非正交数计算 n 个嵌套非正多边形(9 边多边形)图案中的点数，所有非正多边形共享一个公共角，其中图案中的第 I 个非正多边形的边由相互间隔一个单位的 I 个点组成。

**例:**

```
Input : n = 10
       n (7n - 5) / 2
       10 * (7 * 10 - 5) / 2
       10 * 65 / 2 = 325
Output :325

Input : 15
Output :750
```

**n <sup>第</sup>个非正交数**由公式给出:**n(7n–5)/2**。

## c++

```
// CPP Program to find
// nth nonagonal number.
#include <bits/stdc++.h>
using namespace std;

// Function to find nth
// nonagonal number.
int Nonagonal(int n)
{
    // Formula to find nth
    // nonagonal number.
    return n * (7 * n - 5) / 2;
}

// Driver function.
int main()
{
    int n = 10;   
    cout << Nonagonal(n);   
    return 0;
}
```

## Java

```
// Java Program to find
// nth nonagonal number.
import java.io.*;

class GFG {

    // Function to find nth
    // nonagonal number.
    static int Nonagonal(int n)
    {
        // Formula to find nth
        // nonagonal number.
        return n * (7 * n - 5) / 2;
    }

    // Driver function.
    public static void main(String args[])
    {
        int n = 10;
        System.out.println(Nonagonal(n));
    }
}

// This code is contributed by Nikita Tiwari.
```

T21【python 3】T2

## c#

```
// C# Program to find
// nth nonagonal number.
using System;

class GFG {

    // Function to find nth
    // nonagonal number.
    static int Nonagonal(int n)
    {
        // Formula to find nth
        // nonagonal number.
        return n * (7 * n - 5) / 2;
    }

    // Driver function.
    public static void Main()
    {
        int n = 10;
        Console.Write(Nonagonal(n));
    }
}

// This code is contributed by vt_m.
```

## PHP

```
<?php
// PHP Program to find
// nth nonagonal number.

// Function to find nth
// nonagonal number.
function Nonagonal($n)
{
    // Formula to find nth
    // nonagonal number.
    return $n * (7 * $n - 5) / 2;
}

// Driver Code
$n = 10;
echo Nonagonal($n);

// This code is contributed by vt_m.
?>
```

## Javascript

**输出:**

```
325
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

**给定一个数字 n，找到非正交的数字系列，直到 n 项**。

## c++

```
// CPP Program find first
// n nonagonal number.
#include <bits/stdc++.h>
using namespace std;

// Function to find nonagonal
// number series.
int Nonagonal(int n)
{
    for (int i = 1; i <= n; i++)
    {
        cout << i * (7 * i - 5) / 2;
        cout << " ";
    }
}

// Driver Code
int main()
{
    int n = 10;

    Nonagonal(n);

    return 0;
}
```

## Java

```
// Java Program find first
// n nonagonal number.
import java.io.*;

class GFG
{

    // Function to find nonagonal
    // number series.
    static void Nonagonal(int n)
    {
        for (int i = 1; i <= n; i++)
        {
            System.out.print(i * (7 *
                             i - 5) / 2);
            System.out.print(" ");
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 10;
        Nonagonal(n);
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## python 3

```
# Python 3 Program find first
# n nonagonal number.

# Function to find nonagonal
# number series.
def Nonagonal(n):

    for i in range(1, n+1): 
        print(int(i * (7 * i - 5) / 2),end=" ")

# driver Function    
n = 10
Nonagonal(n)

# This code is contributed by
# Smitha Dinesh Semwal
```

## c#

```
// C# Program find first
// n nonagonal number.
using System;

class GFG
{

    // Function to find nonagonal
    // number series.
    static void Nonagonal(int n)
    {
        for (int i = 1; i <= n; i++)
        {
            Console.Write(i * (7 *
                          i - 5) / 2);
            Console.Write(" ");
        }
    }

    // Driver Code
    public static void Main()
    {
        int n = 10;
        Nonagonal(n);
    }
}

// This code is contributed by vt_m.
```

## PHP

```
<?php
// PHP Program find first
// n nonagonal number.

// Function to find nonagonal
// number series.
function Nonagonal($n)
{
    for ( $i = 1; $i <= $n; $i++)
    {
        echo $i * (7 * $i - 5) / 2;
        echo " ";
    }
}

// Driver Code
$n = 10;

Nonagonal($n);

// This code is contributed by ajit
?>
```

## Javascript

T33】

**输出:**

```
1 9 24 46 75 111 154 204 261 325 
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

**参考资料:**[https://en . Wikipedia . org/wiki/nonagonale _ number】](https://en.wikipedia.org/wiki/Nonagonal_number)