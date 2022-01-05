# 系列 1*1*2 之和！+ 2*2*3!+ ……..+ n*n*(n+1)！

> 原文:[https://www . geesforgeks . org/program-find-s-given-series-112-223-nnn 1/](https://www.geeksforgeeks.org/program-find-s-given-series-112-223-nnn1/)

给定 n，我们需要求 1*1*2 的和！+ 2*2*3!+ ……..+ n*n*(n+1)！
示例:

> 输入:1
> 输出:2
> 输入:3
> 输出:242

我们可以假设溢出不会发生。

一个**简单的解决方案**是一个一个地计算术语，并添加到结果中。
一个**高效的解决方案**是基于直接公式 2+(n * n+n–2)*(n+1)！
配方的工作基于[这个](https://www.geeksforgeeks.org/sum-series-12-22-nn/)岗位。

## C++

```
// CPP program to find sum of the series.
#include <bits/stdc++.h>
using namespace std;

int factorial(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Function to calculate required series
int calculateSeries(int n)
{
    return 2 + (n * n + n - 2) * factorial(n + 1);
}

// Drivers code
int main()
{
    int n = 3;
    cout << calculateSeries(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find sum of the series.
import java.io.*;

class GFG {

    static int factorial(int n)
    {
        int res = 1;
        for (int i = 2; i <= n; i++)
            res = res * i;
        return res;
    }

    // Function to calculate required series
    static int calculateSeries(int n)
    {
        return 2 + (n * n + n - 2)
                      * factorial(n + 1);
    }

    // Drivers code
    public static void main (String[] args)
    {
        int n = 3;
        System.out.println(calculateSeries(n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python program to find sum of
# the series.
import math

def factorial(n):
    res = 1
    i = 2
    for i in (n+1):
        res = res * i
    return res

# Function to calculate required
# series
def calculateSeries(n):
    return (2 + (n * n + n - 2)
        * math.factorial(n + 1))

# Driver code
n = 3
print(calculateSeries(n))

# This code is contributed by
# Prateek bajaj
```

## C#

```
// C# program to find sum of the series.
using System;
class GFG {

    static int factorial(int n)
    {
        int res = 1;
        for (int i = 2; i <= n; i++)
            res = res * i;
        return res;
    }

    // Function to calculate required series
    static int calculateSeries(int n)
    {
        return 2 + (n * n + n - 2)
                 * factorial(n + 1);
    }

    // Driver code
    public static void Main ()
    {
        int n = 3;
        Console.WriteLine(calculateSeries(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of the series.

function factorial( $n)
{
    $res = 1;
    for ( $i = 2; $i <= $n; $i++)
        $res = $res * $i;
    return $res;
}

// Function to calculate required series
function calculateSeries( $n)
{
    return 2 + ($n * $n + $n - 2) *
                 factorial($n + 1);
}

    // Driver code
    $n = 3;
    echo calculateSeries($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// java script  program to find sum of the series.
function factorial( n)
    {
        let res = 1;
        for (let i = 2; i <= n; i++)
            res = res * i;
        return res;
    }

    // Function to calculate required series
    function calculateSeries( n)
    {
        return 2 + (n * n + n - 2)
                      * factorial(n + 1);
    }

    // Drivers code
        let n = 3;
        document.write(calculateSeries(n));

// This code is contributed by mohan pavan
</script>
```

**Output:** 

```
242
```