# 求数列 1+11+111+1111+的和…..最新条款

> 原文:[https://www . geesforgeks . org/find-sum-series-111111111-upto-n-terms/](https://www.geeksforgeeks.org/find-sum-series-1111111111-upto-n-terms/)

这里我们要求数列 1 + 11 + 111 + 1111 +的和…..最多 N 个术语(其中 N 是给定的)。
**例:**

```
Input : 3
Output : 1 + 11 + 111 +....
Total sum is : 123

Input : 4
Output : 1 + 11 + 111 + 1111 +..... 
Total sum is : 1234

Input : 7
Output : 1 + 11 + 111 + 1111 + 11111 + 
         111111 + 1111111 +..... 
Total sum is : 1234567
```

这里我们看到，当 N 的值为 3 时，级数持续到 1 + 11 + 111，即三项，其和为 123。
求上述级数和的程序:

## C++

```
// C++ program to find the sum of
// the series 1+11+111+1111+....
#include <bits/stdc++.h>
using namespace std;

// Function for finding summation
int summation(int n)
{
    int sum = 0, j = 1;
    for (int i = 1; i <= n; i++) {
        sum = sum + j;

        // Appending a 1 at the end
        j = (j * 10) + 1;
    }

    return sum;
}

// Driver Code
int main()
{
    int n = 5;
    cout << " " <<  summation(n);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program to find the sum of
// the series 1+11+111+1111+....
#include <stdio.h>

// Function for finding summation
int summation(int n)
{
    int sum = 0, j = 1;
    for (int i = 1; i <= n; i++) {
        sum = sum + j;

        // Appending a 1 at the end
        j = (j * 10) + 1;
    }

    return sum;
}

// Driver Code
int main()
{
    int n = 5;
    printf("%d", summation(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of
// the series 1+11+111+1111+....
import java.io.*;

class GFG
{

    // Function for finding summation
    static int summation(int n)
    {
        int sum = 0, j = 1;
        for (int i = 1; i <= n; i++)
        {
            sum = sum + j;
            j = (j * 10) + 1;
        }

        return sum;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 5;
        System.out.println(summation(n));
    }
}

// This code is contributed
// by Nikita Tiwari
```

## 计算机编程语言

```
# Python program to get the summation
# of following series
def summation(n):
    sum = 0
    j = 1

    for i in range(1, n + 1):
        sum = sum + j
        j = (j * 10) + 1

    return sum

# Driver Code
n = 5
print(summation(n))
```

## C#

```
// C# program to find the sum of
// the series 1+11+111+1111+....
using System;

class GFG
{

    // Function for finding summation
    static int summation(int n)
    {
        int sum = 0, j = 1;
        for (int i = 1; i <= n; i++)
        {
            sum = sum + j;
            j = (j * 10) + 1;
        }

        return sum;
    }

    // Driver Code
    public static void Main()
    {
        int n = 5;
        Console.WriteLine(summation(n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum of
// the series 1+11+111+1111+....

// Function for finding summation
function summation($n)
{
    $sum = 0; $j = 1;
    for ($i = 1; $i <= $n; $i++)
    {
        $sum = $sum + $j;

        // Appending a 1 at the end
        $j = ($j * 10) + 1;
    }

    return $sum;
}

// Driver Code
$n = 5;
echo summation($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find the sum of
// the series 1+11+111+1111+....

    // Function for finding summation
    function summation( n) {
        let sum = 0, j = 1;
        for ( let i = 1; i <= n; i++) {
            sum = sum + j;

            // Appending a 1 at the end
            j = (j * 10) + 1;
        }

        return sum;
    }

    // Driver Code

        let n = 5;
        document.write(summation(n));

// This code contributed by Princi Singh

</script>
```

**输出:**

```
12345
```

**另一种方法:**让给定的数列 S = 1 + 11 + 111 + 1111 +。。。+直到第 n 个学期。用公式求数列的和。

> ![\\ S = 1 + 11 + 111 + 1111 + . . . + upto \ n \ term \\ \\ S = \left ( \frac{1}{9} \right )*\left ( 9 + 99 + 999 + 9999 + . . . + upto \ n \ term \right ) \\ \\ S = \left ( \frac{1}{9} \right ) * \left ( \left (10 ^{1} - 1\right ) + \left (10 ^{2} -1 \right ) +\left (10 ^{3} -1 \right ) + \left (10 ^{4} -1 \right ) + . . . + \left (10 ^{n} -1 \right ) \right ) \\ \\ S = \left ( \frac{1}{9} \right ) *\left (10 ^{1} + 10 ^{2} + 10 ^{3} + 10 ^{4} + . . . + 10 ^{n} - n\right ) \\ \\ S = \left ( \frac{1}{9} \right ) * \left ( \frac{10 * (10^{n} - 1)}{10 - 1} - n \right ) \\ \\ S = \frac{10^{n+1} - 10 - 9n}{81}      ](img/2599b31f768e0455a482637d5252ccb8.png "Rendered by QuickLaTeX.com")

下面是上述方法的实现。

## C++

```
// C++ program to find the sum of
// the series 1+11+111+1111+....
#include <bits/stdc++.h>

// Function for finding summation
int summation(int n)
{
    int sum;

    sum = (pow(10, n + 1) -
               10 - (9 * n)) / 81;

    return sum;
}

// Driver Code
int main()
{
    int n = 5;
    printf("%d", summation(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find the sum of
// the series 1+11+111+1111+....
import java.io.*;

class GFG {

    // Function for finding summation
    static int summation(int n)
    {
        int sum;

        sum = (int)(Math.pow(10, n + 1) -
                10 - (9 * n)) / 81;

        return sum;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 5;
        System.out.println(summation(n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to
# find the sum of
# the series 1+11+111+1111+....
import math

# Function for
# finding summation
def summation(n):
    return int((pow(10, n + 1) -
                    10 - (9 * n)) / 81);

# Driver Code
print(summation(5));

# This code is contributed
# by mits.
```

## C#

```
// C# program to find the sum of
// the series 1+11+111+1111+....
using System;

class GFG {

    // Function for finding summation
    static int summation(int n)
    {
        int sum;

        sum = (int)(Math.Pow(10, n + 1) -
                10 - (9 * n)) / 81;

        return sum;
    }

    // Driver Code
    public static void Main ()
    {
        int n = 5;
        Console.WriteLine(summation(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to find the sum of
// the series 1+11+111+1111+....

// Function for finding summation
function summation($n)
{
    $sum;

    $sum = (pow(10, $n + 1) -
                10 - (9 * $n)) / 81;

    return $sum;
}

// Driver Code
$n = 5;
echo summation($n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
// javascript program to find the sum of
// the series 1+11+111+1111+....

// Function for finding summation
function summation( n)
{
    let sum;
    sum = (Math.pow(10, n + 1) -
               10 - (9 * n)) / 81;
    return sum;
}

// Driver Code
let n = 5;
    document.write(summation(n)) ;

// This code is contributed by aashish1995

</script>
```

**输出:**

```
12345
```