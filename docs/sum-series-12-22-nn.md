# 系列 1*1 之和！+ 2*2!+ ……..+ n*n！

> 原文:[https://www.geeksforgeeks.org/sum-series-12-22-nn/](https://www.geeksforgeeks.org/sum-series-12-22-nn/)

给定 n，我们需要求 1*1 的和！+ 2*2!+ ……..+ n*n！
**例:**

> 输入:1
> 输出:1
> 输入:3
> 输出:23
> 1 * 1！+ 2 * 2!+ 3 * 3!= 1 + 4 + 18 = 23

我们可以假设溢出不会发生。

一个**简单的解决方案**是一个一个地计算术语，并添加到结果中。
一个**高效解决方案**是基于直接公式 **(n + 1)！–1**
**这个公式是如何工作的？**

> 我们基本上需要计算低于总和。
> ∑(我*我！)其中 I 从 1 到 n 不等
> =∑((I+1–1)* I！)
> = ∑((i+1) * i！)–∑我！
> = ∑(i + 1)！–∑(I！)
> ∑(i + 1)！= 2!+ 3!+……(n+1)！其中 1<= I<= n –( 1)
> ∑(I！) = 1!+ 2!+ 3!+ … (n)！其中 1<= I<= n –( 2)
> 从第一个减去第二个，我们得到(n+1)！–1

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
    return factorial(n + 1) - 1;
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
// Java program to find sum of
// the series.
import java.io.*;

class GFG {

    static int factorial(int n)
    {
        int res = 1;
        for (int i = 2; i <= n; i++)
            res = res * i;
        return res;
    }

    // Function to calculate required
    // series
    static int calculateSeries(int n)
    {
        return factorial(n + 1) - 1;
    }

    // Drivers code
    public static void main (String[] args)
    {
        int n = 3;
        System.out.println(
                       calculateSeries(n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python program to find sum of
# the series.

def factorial(n):
    res = 1
    for i in range(2, n+1):
        res = res * i
    return res

# Function to calculate required
# series
def calculateSeries(n):
    return factorial(n + 1) - 1

# Drivers code
n = 3
print(calculateSeries(n))

# This code is contributed by
# Ansu Kumari.
```

## C#

```
// C# program to find
// sum of the series.
using System;

class GFG
{
    static int factorial(int n)
    {
        int res = 1;
        for (int i = 2; i <= n; i++)
            res = res * i;
        return res;
    }

    // Function to calculate
    // required series
    static int calculateSeries(int n)
    {
        return factorial(n + 1) - 1;
    }

    // Driver code
    static public void Main ()
    {
        int n = 3;
        Console.WriteLine(
                calculateSeries(n));
    }
}

// This code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// sum of the series.

function factorial($n)
{
    $res = 1;
    for ($i = 2; $i <= $n; $i++)
        $res = $res * $i;
    return $res;
}

// Function to calculate
// required series
function calculateSeries($n)
{
    return factorial($n + 1) - 1;
}

// Driver code
$n = 3;
echo calculateSeries($n);

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
<script>
// java script program to find
// sum of the series.

function factorial(n)
{
    let res = 1;
    for (let i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Function to calculate
// required series
function calculateSeries(n)
{
    return factorial(n + 1) - 1;
}

// Driver code
let n = 3;
document.write( calculateSeries(n));

// This code is contributed
// by sravan kumar
</script>
```

**Output:** 

```
23
```