# 程序求一个数列的和(1 * 1)+(2 * 2)+(3 * 3)+(4 * 4)+(5 * 5)+…+(n * n)

> 原文:[https://www . geesforgeks . org/program-find-sum-series-11-22-33-44-55-nn/](https://www.geeksforgeeks.org/program-find-sum-series-11-22-33-44-55-nn/)

给了你一个数列(1 * 1)+(2 * 2)+(3 * 3)+(4 * 4)+(5 * 5)+…+(n * n)，求到第 n 项为止的数列的和。
**例:**

```
Input : n = 3
Output : 14
Explanation : 1 + 1/2^2 + 1/3^3

Input : n = 5
Output : 55
Explanation : (1*1) + (2*2) + (3*3) + (4*4) + (5*5)
```

## C++

```
// CPP program to calculate the following series
#include<iostream>
using namespace std;

// Function to calculate the following series
int Series(int n)
{
    int i;
    int sums = 0;
    for (i = 1; i <= n; i++)
        sums += (i * i);
    return sums;
}

// Driver Code
int main()
{
    int n = 3;
    int res = Series(n);
    cout<<res<<endl;
}
```

## C

```
// C program to calculate the following series
#include <stdio.h>

// Function to calculate the following series
int Series(int n)
{
    int i;
    int sums = 0;
    for (i = 1; i <= n; i++)
        sums += (i * i);
    return sums;
}

// Driver Code
int main()
{
    int n = 3;
    int res = Series(n);
    printf("%d", res);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the following series
import java.io.*;
class GFG {

    // Function to calculate the following series
    static int Series(int n)
    {
        int i;
        int sums = 0;
        for (i = 1; i <= n; i++)
            sums += (i * i);
        return sums;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 3;
        int res = Series(n);
        System.out.println(res);
    }
}
```

## 计算机编程语言

```
# Python program to calculate the following series
def Series(n):
    sums = 0
    for i in range(1, n + 1):
        sums += (i * i);
    return sums

# Driver Code
n = 3
res = Series(n)
print(res)
```

## C#

```
// C# program to calculate the following series
using System;
class GFG {

    // Function to calculate the following series
    static int Series(int n)
    {
        int i;
        int sums = 0;
        for (i = 1; i <= n; i++)
            sums += (i * i);
        return sums;
    }

    // Driver Code
    public static void Main()
    {
        int n = 3;
        int res = Series(n);
        Console.Write(res);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// the following series

// Function to calculate the
// following series
function Series($n)
{
    $i;
    $sums = 0;
    for ($i = 1; $i <= $n; $i++)
        $sums += ($i * $i);
    return $sums;
}

// Driver Code
$n = 3;
$res = Series($n);
echo($res);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to calculate the following series

    // Function to calculate the following series
    function Series( n) {
        let i;
        let sums = 0;
        for (i = 1; i <= n; i++)
            sums += (i * i);
        return sums;
    }

    // Driver Code

        let n = 3;
        let res = Series(n);
        document.write(res);

// This code contributed by Princi Singh

</script>
```

**输出:**

```
14
```

**时间复杂度:O(n)**
O(1)解请参考下方帖子。
[前 n 个自然数的平方和](https://www.geeksforgeeks.org/sum-squares-first-n-natural-numbers/)