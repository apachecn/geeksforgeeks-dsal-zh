# 程序获取级数之和:1–x^2/2！+ x^4/4！-….第 n 个学期

> 原文:[https://www . geesforgeks . org/program-get-sum-series-1-x22-x44-up-n-term/](https://www.geeksforgeeks.org/program-get-sum-series-1-x22-x44-upto-nth-term/)

这是一个数学级数程序，用户必须输入级数求和的项数。接下来，我们还需要 x 的值，它构成了级数的基础。

示例:

```
Input : x = 9, n = 10
Output : -5.1463

Input : x = 5, n = 15
Output : 0.2837
```

**简单方法:**
我们使用两个嵌套循环来计算阶乘，并使用幂函数来计算幂。

## C

```
// C program to get the sum of the series
#include <math.h>
#include <stdio.h>

// Function to get the series
double Series(double x, int n)
{
    double sum = 1, term = 1, fct, j, y = 2, m;

    // Sum of n-1 terms starting from 2nd term
    int i;
    for (i = 1; i < n; i++) {
        fct = 1;
        for (j = 1; j <= y; j++) {
            fct = fct * j;
        }
        term = term * (-1);
        m = term * pow(x, y) / fct;
        sum = sum + m;
        y += 2;
    }
    return sum;
}

// Driver Code
int main()
{
    double x = 9;
    int n = 10;
    printf("%.4f", Series(x, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get the sum of the series
import java.io.*;

class MathSeries {

    // Function to get the series
    static double Series(double x, int n)
    {
        double sum = 1, term = 1, fct, j, y = 2, m;

       // Sum of n-1 terms starting from 2nd term
        int i;
        for (i = 1; i < n; i++) {
            fct = 1;
            for (j = 1; j <= y; j++) {
                fct = fct * j;
            }
            term = term * (-1);
            m = Math.pow(x, y) / fct;
            m = m * term;
            sum = sum + m;
            y += 2;
        }
        return sum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        double x = 3;
        int n = 4;
        System.out.println(Math.round(Series(x, n) *
                                10000.0) / 10000.0);
    }
}
```

## 蟒蛇 3

```
# Python3 code to get the sum of the series
import math

# Function to get the series
def Series( x , n ):
    sum = 1
    term = 1
    y = 2

    # Sum of n-1 terms starting from 2nd term
    for i in range(1,n):
        fct = 1
        for j in range(1,y+1):
            fct = fct * j

        term = term * (-1)
        m = term * math.pow(x, y) / fct
        sum = sum + m
        y += 2

    return sum

# Driver Code
x = 9
n = 10
print('%.4f'% Series(x, n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to get the sum of the series
using System;

class GFG {

    // Function to get the series
    static double Series(double x, int n)
    {
        double sum = 1, term = 1, fct, j, y = 2, m;

    // Sum of n-1 terms starting from 2nd term
        int i;
        for (i = 1; i < n; i++) {
            fct = 1;
            for (j = 1; j <= y; j++) {
                fct = fct * j;
            }
            term = term * (-1);
            m = Math.Pow(x, y) / fct;
            m = m * term;
            sum = sum + m;
            y += 2;
        }
        return sum;
    }

    // Driver Code
    public static void Main()
    {
        double x = 9;
        int n = 10;
        Console.Write(Series(x, n) *
                            10000.0 / 10000.0);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get the
// sum of the series

// Function to get the series
function Series($x, $n)
{
    $sum = 1; $term = 1;
    $fct; $j; $y = 2; $m;

    // Sum of n-1 terms starting
    // from 2nd term
    for ($i = 1; $i < $n; $i++)
    {
        $fct = 1;
        for ($j = 1; $j <= $y; $j++)
        {
            $fct = $fct * $j;
        }
        $term = $term * (-1);
        $m = $term * pow($x, $y) / $fct;
        $sum = $sum + $m;
        $y += 2;
    }
    return $sum;
}

// Driver Code
$x = 9;
$n = 10;
$precision = 4;
echo substr(number_format(Series($x, $n),
            $precision + 1, '.', ''), 0, -1);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to get the sum of the series

// Function to get the series
function Series(x, n)
{
    let sum = 1, term = 1, fct, j, y = 2, m;

    // Sum of n-1 terms starting from 2nd term
    let i;
    for(i = 1; i < n; i++)
    {
        fct = 1;
        for(j = 1; j <= y; j++)
        {
            fct = fct * j;
        }
        term = term * (-1);
        m = term * Math.pow(x, y) / fct;
        sum = sum + m;
        y += 2;
    }
    return sum;
}

// Driver Code
let x = 9;
let n = 10;

document.write(Series(x, n).toFixed(4));

// This code is contributed by Surbhi Tyagi.

</script>
```

## C++

```
// C++ program to get the sum of the series
#include <bits/stdc++.h>
using namespace std;

// Function to get the series
double Series(double x, int n)
{
    double sum = 1, term = 1, fct, j, y = 2, m;

    // Sum of n-1 terms starting from 2nd term
    int i;
    for (i = 1; i < n; i++) {
        fct = 1;
        for (j = 1; j <= y; j++) {
            fct = fct * j;
        }
        term = term * (-1);
        m = term * pow(x, y) / fct;
        sum = sum + m;
        y += 2;
    }
    return sum;
}

// Driver Code
int main()
{
    double x = 9;
    int n = 10;
    cout << Series(x, n);
    return 0;
}
// This code is contributed by Samim Hossain Mondal.
```

**Output**

```
-5.1463
```