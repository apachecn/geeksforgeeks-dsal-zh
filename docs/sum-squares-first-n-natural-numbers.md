# 前 n 个自然数的平方和

> 原文:[https://www . geesforgeks . org/sum-squares-first-n-natural-numbers/](https://www.geeksforgeeks.org/sum-squares-first-n-natural-numbers/)

给定正整数 **N** 。任务是找到 1<sup>2</sup>+2<sup>2</sup>+3<sup>2</sup>+…..+ N <sup>2</sup> 。

**示例:**

```
Input : N = 4
Output : 30
12 + 22 + 32 + 42
= 1 + 4 + 9 + 16
= 30

Input : N = 5
Output : 55
```

**方法 1: O(N)** 思路是运行一个从 1 到 N 的循环，对于每个 I，1 < = i < = n，找 i <sup>2</sup> 求和。

下面是这种方法的实现

## C++

```
// CPP Program to find sum of square of first n natural numbers
#include <bits/stdc++.h>
using namespace std;

// Return the sum of square of first n natural numbers
int squaresum(int n)
{
    // Iterate i from 1 and n
    // finding square of i and add to sum.
    int sum = 0;
    for (int i = 1; i <= n; i++)
        sum += (i * i);
    return sum;
}

// Driven Program
int main()
{
    int n = 4;
    cout << squaresum(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum of
// square of first n natural numbers
import java.io.*;

class GFG {

    // Return the sum of square of first n natural numbers
    static int squaresum(int n)
    {
        // Iterate i from 1 and n
        // finding square of i and add to sum.
        int sum = 0;
        for (int i = 1; i <= n; i++)
            sum += (i * i);
        return sum;
    }

    // Driven Program
    public static void main(String args[])throws IOException
    {
        int n = 4;
        System.out.println(squaresum(n));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python3 Program to
# find sum of square
# of first n natural
# numbers

# Return the sum of
# square of first n
# natural numbers
def squaresum(n) :

    # Iterate i from 1
    # and n finding
    # square of i and
    # add to sum.
    sm = 0
    for i in range(1, n+1) :
        sm = sm + (i * i)

    return sm

# Driven Program
n = 4
print(squaresum(n))

# This code is contributed by Nikita Tiwari.*/
```

## C#

```
// C# Program to find sum of
// square of first n natural numbers
using System;

class GFG {

    // Return the sum of square of first
    // n natural numbers
    static int squaresum(int n)
    {

        // Iterate i from 1 and n
        // finding square of i and add to sum.
        int sum = 0;

        for (int i = 1; i <= n; i++)
            sum += (i * i);

        return sum;
    }

    // Driven Program
    public static void Main()
    {
        int n = 4;

        Console.WriteLine(squaresum(n));
    }
}

/* This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum of
// square of first n natural numbers

// Return the sum of square of
// first n natural numbers
function squaresum($n)
{
    // Iterate i from 1 and n
    // finding square of i and
    // add to sum.
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum += ($i * $i);
    return $sum;
}

// Driven Code
$n = 4;
echo(squaresum($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript Program to find sum of square of first n natural numbers

// Return the sum of square of first n natural numbers
function squaresum(n)
{
    // Iterate i from 1 and n
    // finding square of i and add to sum.
    let sum = 0;
    for (let i = 1; i <= n; i++)
        sum += (i * i);
    return sum;
}

// Driven Program

    let n = 4;
    document.write(squaresum(n) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
30
```

**方法二:O(1)**

> 前 N 个自然数的平方和= (N*(N+1)*(2*N+1))/6

例如
对于 N=4，Sum =(4 *(4+1)*(2 * 4+1))/6
= 180/6
= 30
对于 N=5，Sum = ( 5 * ( 5 + 1 ) * ( 2 * 5 + 1 ) ) / 6
= 55

证据:

```
We know,
(k + 1)3 = k3 + 3 * k2 + 3 * k + 1
We can write the above identity for k from 1 to n:
23 = 13 + 3 * 12 + 3 * 1 + 1 ......... (1)
33 = 23 + 3 * 22 + 3 * 2 + 1 ......... (2)
43 = 33 + 3 * 32 + 3 * 3 + 1 ......... (3)
53 = 43 + 3 * 42 + 3 * 4 + 1 ......... (4)
...
n3 = (n - 1)3 + 3 * (n - 1)2 + 3 * (n - 1) + 1 ......... (n - 1)
(n + 1)3 = n3 + 3 * n2 + 3 * n + 1 ......... (n)

Putting equation (n - 1) in equation n,
(n + 1)3 = (n - 1)3 + 3 * (n - 1)2 + 3 * (n - 1) + 1 + 3 * n2 + 3 * n + 1
         = (n - 1)3 + 3 * (n2 + (n - 1)2) + 3 * ( n + (n - 1) ) + 1 + 1

By putting all equation, we get
(n + 1)3 = 13 + 3 * Σ k2 + 3 * Σ k + Σ 1
n3 + 3 * n2 + 3 * n + 1 = 1 + 3 * Σ k2 + 3 * (n * (n + 1))/2 + n
n3 + 3 * n2 + 3 * n = 3 * Σ k2 + 3 * (n * (n + 1))/2 + n
n3 + 3 * n2 + 2 * n - 3 * (n * (n + 1))/2 = 3 * Σ k2
n * (n2 + 3 * n + 2) - 3 * (n * (n + 1))/2 = 3 * Σ k2
n * (n + 1) * (n + 2) - 3 * (n * (n + 1))/2 = 3 * Σ k2
n * (n + 1) * (n + 2 - 3/2) = 3 * Σ k2
n * (n + 1) * (2 * n + 1)/2  = 3 * Σ k2
n * (n + 1) * (2 * n + 1)/6  = Σ k2
```

下面是该方法的实现:

## C++

```
// CPP Program to find sum
// of square of first n
// natural numbers
#include <bits/stdc++.h>
using namespace std;

// Return the sum of square of
// first n natural numbers
int squaresum(int n)
{
    return (n * (n + 1) * (2 * n + 1)) / 6;
}

// Driven Program
int main()
{
    int n = 4;
    cout << squaresum(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum
// of square of first n
// natural numbers
import java.io.*;

class GFG {

    // Return the sum of square
    // of first n natural numbers
    static int squaresum(int n)
    {
        return (n * (n + 1) * (2 * n + 1)) / 6;
    }

    // Driven Program
    public static void main(String args[])
                            throws IOException
    {
        int n = 4;
        System.out.println(squaresum(n));
    }
}

/*This code si contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python3 Program to
# find sum of square
# of first n natural
# numbers

# Return the sum of
# square of first n
# natural numbers
def squaresum(n) :
    return (n * (n + 1) * (2 * n + 1)) // 6

# Driven Program
n = 4
print(squaresum(n))

#This code is contributed by Nikita Tiwari.                                                              
```

## C#

```
// C# Program to find sum
// of square of first n
// natural numbers
using System;

class GFG {

    // Return the sum of square
    // of first n natural numbers
    static int squaresum(int n)
    {
        return (n * (n + 1) * (2 * n + 1)) / 6;
    }

    // Driven Program
    public static void Main()

    {
        int n = 4;

        Console.WriteLine(squaresum(n));
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum
// of square of first n
// natural numbers

// Return the sum of square of
// first n natural numbers
function squaresum($n)
{
    return ($n * ($n + 1) *
           (2 * $n + 1)) / 6;
}

// Driven Code
$n = 4;
echo(squaresum($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum
// of square of first n
// natural numbers

// Return the sum of square of
// first n natural numbers
function squaresum(n)
{
    return parseInt((n * (n + 1) *
                     (2 * n + 1)) / 6);
}

// Driver code
let n = 4;

document.write(squaresum(n));

// This code is contributed by rishavmahato348

</script>
```

**输出:**

```
30
```

**避免过早溢出:**
对于大 n，值(n * (n + 1) * (2 * n + 1))会溢出。利用 n*(n+1)必须能被 2 整除的事实，我们可以在一定程度上避免溢出。

## C++

```
// CPP Program to find sum of square of first
// n natural numbers. This program avoids
// overflow upto some extent for large value
// of n.
#include <bits/stdc++.h>
using namespace std;

// Return the sum of square of first n natural
// numbers
int squaresum(int n)
{
    return (n * (n + 1) / 2) * (2 * n + 1) / 3;
}

// Driven Program
int main()
{
    int n = 4;
    cout << squaresum(n) << endl;
    return 0;
}
```

## 蟒蛇 3

```
# Python Program to find sum of square of first
# n natural numbers. This program avoids
# overflow upto some extent for large value
# of n.y

def squaresum(n):
    return (n * (n + 1) / 2) * (2 * n + 1) / 3

# main()
n = 4
print(squaresum(n));

# Code Contributed by Mohit Gupta_OMG <(0_o)>
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum of square of first
// n natural numbers. This program avoids
// overflow upto some extent for large value
// of n.

import java.io.*;
import java.util.*;

class GFG
{
    // Return the sum of square of first n natural
    // numbers
public static int squaresum(int n)
{
    return (n * (n + 1) / 2) * (2 * n + 1) / 3;
}

    public static void main (String[] args)
    {
        int n = 4;
    System.out.println(squaresum(n));
    }
}

// Code Contributed by Mohit Gupta_OMG <(0_o)>
```

## C#

```
// C# Program to find sum of square of first
// n natural numbers. This program avoids
// overflow upto some extent for large value
// of n.

using System;

class GFG {

    // Return the sum of square of
    // first n natural numbers
    public static int squaresum(int n)
    {
        return (n * (n + 1) / 2) * (2 * n + 1) / 3;
    }

    // Driver Code
    public static void Main()
    {
        int n = 4;

        Console.WriteLine(squaresum(n));
    }
}

// This Code is Contributed by vt_m.>
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find
// sum of square of first
// n natural numbers.
// This program avoids
// overflow upto some
// extent for large value
// of n.

// Return the sum of square
// of first n natural numbers
function squaresum($n)
{
    return ($n * ($n + 1) / 2) *
           (2 * $n + 1) / 3;
}

    // Driver Code
    $n = 4;
    echo squaresum($n) ;

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// javascript Program to find sum of square of first
// n natural numbers. This program avoids
// overflow upto some extent for large value
// of n.

// Return the sum of square of first n natural
// numbers
function squaresum( n)
{
    return (n * (n + 1) / 2) * (2 * n + 1) / 3;
}

// Driven Program

    let n = 4;
     document.write(squaresum(n));

// This code contributed by aashish1995

</script>
```

**输出:**

```
30
```