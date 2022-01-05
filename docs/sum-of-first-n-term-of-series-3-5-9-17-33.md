# 数列 3、5、9、17、33 的前 n 项之和。

> 原文:[https://www . geesforgeks . org/系列第一个 n 项之和-3-5-9-17-33/](https://www.geeksforgeeks.org/sum-of-first-n-term-of-series-3-5-9-17-33/)

给定 n，我们需要求出表示为 Sn = 3 + 5 + 9 + 17 + 33 的级数的前 n 项之和…直到 n
**例:**

```
Input : 2
Output : 8
3 + 5 = 8

Input : 5
Output : 67
3 + 5 + 9 + 17 + 33 = 67
```

让第 n 项用 tn 表示。
这个问题可以很容易地通过将每个术语拆分如下来解决:

> Sn = 3+5+9+17+33……
> Sn =(2+1)+(4+1)+(8+1)+(16+1)+……
> Sn =(2+1)+(2 * 2+1)+(2 * 2 * 2+1)+(2 * 2 * 2 * 2+1)+……+((2 * 2 * 2..直到 n 倍)+ 1)

我们观察到第 n 项可以用 2 和 1 的幂来写。
因此，前 n 项之和如下所示:

> Sn =(2+1)+(4+1)+(8+1)+(16+1)+……+至 n 项
> Sn =(1+1+1+1+……至 n 项)+(2+4+8+16+……至 2 的 n 次方)
> 在上述公式中，
> 2 + 4 + 8 + 16。是 G.P.
> 它的前 n 项之和由 2*(2^n-1)/(2-1)= 2^(n+1)–2(使用 G.P .公式)
> sn = n+2*(2^n–1)
> sn = 2^(n+1)+n-2 给出

## C++

```
// C++ program to find sum of first n terms
#include <bits/stdc++.h>
using namespace std;

int calculateSum(int n)
{
    // Sn = n*(4*n*n + 6*n - 1)/3
    return (pow(2, n + 1) + n - 2);
}

// Driver code
int main()
{
    // number of terms to be included in sum
    int n = 4;

    // find the Sn
    cout << "Sum = " << calculateSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// sum of first n terms
import java.util.*;

class GFG
{
static int calculateSum(int n)
{
    // Sn = n*(4*n*n + 6*n - 1)/3
    return ((int)Math.pow(2, n + 1) +
                             n - 2);
}

// Driver Code
public static void main(String args[])
{
    // number of terms to
    // be included in sum
    int n = 4;

    // find the Sn
    System.out.println("Sum = " +
                calculateSum(n));
}
}

// This code is contributed
// by Kirti_Mangal
```

## 计算机编程语言

```
# Python program to find sum
# of n terms of the series
def calculateSum(n):

    return (2**(n + 1) + n - 2)

# Driver Code

# number of terms for the sum
n = 4

# find the Sn
print("Sum =", calculateSum(n))

# This code is contributed
# by Surendra_Gangwar
```

## C#

```
//C# program to find
// sum of first n terms
using System;

class GFG
{
static int calculateSum(int n)
{
    // Sn = n*(4*n*n + 6*n - 1)/3
    return ((int)Math.Pow(2, n + 1) +
                            n - 2);
}

// Driver Code
public static void Main()
{
    // number of terms to
    // be included in sum
    int n = 4;

    // find the Sn
    Console.WriteLine("Sum = " +
                calculateSum(n));
}
}

// This code is contributed
// by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum
// of first n terms
function calculateSum( $n)
{
    // Sn = n*(4*n*n + 6*n - 1)/3
    return (pow(2, $n + 1) + $n - 2);
}

// Driver code

// number of terms to be
// included in sum
$n = 4;

// find the Sn
echo "Sum = " , calculateSum($n);

// This code is contributed
// by inder_verma..
?>
```

## java 描述语言

```
<script>
// Java script program to find
// sum of first n terms

function calculateSum( n)
{
    // Sn = n*(4*n*n + 6*n - 1)/3
    return (Math.pow(2, n + 1) +
                             n - 2);
}

// Driver Code

    // number of terms to
    // be included in sum
    let n = 4;

    // find the Sn
    document.write("Sum = " +
                calculateSum(n));

// This code is contributed by mohan pavan

</script>
```

**Output:** 

```
Sum = 34
```