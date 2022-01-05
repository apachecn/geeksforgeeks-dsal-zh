# 求数列 1 + 1/2^2 + 1/3^3 +的和的程序…..+ 1/n^n

> 原文:[https://www . geesforgeks . org/program-find-sum-series-1-122-133-1nn/](https://www.geeksforgeeks.org/program-find-sum-series-1-122-133-1nn/)

你得到了一个系列 1 + 1/2^2 + 1/3^3 + …..+ 1/n^n，求第 n 项前级数的和。

示例:

> 输入:n = 3
> 
> 产出:1.28704
> 
> 解说:1 + 1/2^2 + 1/3^3
> 
> 输入:n = 5
> 
> 输出:1.29126
> 
> 解说:1 + 1/2^2 + 1/3^3 + 1/4^4 + 1/5^5

我们用幂函数来计算功率。

## C++

```
// C++ program to calculate the following series
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the following series
double Series(int n)
{
    int i;
    double sums = 0.0, ser;
    for(i = 1; i <= n; ++i)
    {
        ser = 1 / pow(i, i);
        sums += ser;
    }
    return sums;
}

// Driver Code
int main()
{
    int n = 3;
    double res = Series(n);

    cout << res;
    return 0;
}

// This code is contributed by Ankita saini
```

## C

```
// C program to calculate the following series
#include <math.h>
#include <stdio.h>

// Function to calculate the following series
double Series(int n)
{
    int i;
    double sums = 0.0, ser;
    for (i = 1; i <= n; ++i) {
        ser = 1 / pow(i, i);
        sums += ser;
    }
    return sums;
}

// Driver Code
int main()
{
    int n = 3;
    double res = Series(n);
    printf("%.5f", res);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the following series
import java.io.*;

class Maths {

    // Function to calculate the following series
    static double Series(int n)
    {
        int i;
        double sums = 0.0, ser;
        for (i = 1; i <= n; ++i) {
            ser = 1 / Math.pow(i, i);
            sums += ser;
        }
        return sums;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 3;
        double res = Series(n);
        res = Math.round(res * 100000.0) / 100000.0;
        System.out.println(res);
    }
}
```

## 蟒蛇 3

```
# Python program to calculate the following series
def Series(n):
    sums = 0.0
    for i in range(1, n + 1):
        ser = 1 / (i**i)
        sums += ser
    return sums

# Driver Code
n = 3
res = round(Series(n), 5)
print(res)
```

## C#

```
// C# program to calculate the following series
using System;

class Maths {

    // Function to calculate the following series
    static double Series(int n)
    {
        int i;
        double sums = 0.0, ser;
        for (i = 1; i <= n; ++i) {
            ser = 1 / Math.Pow(i, i);
            sums += ser;
        }
        return sums;
    }

    // Driver Code
    public static void Main()
    {
        int n = 3;
        double res = Series(n);
        res = Math.Round(res * 100000.0) / 100000.0;
        Console.Write(res);
    }
}
/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// the following series

// Function to calculate
// the following series
function Series($n)
{
    $i;
    $sums = 0.0;
    $ser;
    for ($i = 1; $i <= $n; ++$i)
    {
        $ser = 1 / pow($i, $i);
        $sums += $ser;
    }
    return $sums;
}

    // Driver Code
    $n = 3;
    $res = Series($n);
    echo $res;

// This code is contributed by Vishal Tripathi.
?>
```

## java 描述语言

```
<script>

// Javascript program to calculate
// the following series
function Series(n)
{
    let sums = 0.0;

    for(let i = 1; i < n + 1; i++)
    {
        ser = 1 / Math.pow(i, i);
        sums += ser;
    }
    return sums;
}

// Driver Code
let n = 3;
let res = Math.round(Series(n) * 100000) / 100000;

document.write(res);

// This code is contributed by rohitsingh07052

</script>
```

**输出:**

```
1.28704
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*