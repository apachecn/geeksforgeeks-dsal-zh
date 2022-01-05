# 系列之和 1^1 + 2^2 + 3^3 + …..+ n^n 使用递归

> 原文:[https://www . geesforgeks . org/series-11-22-33-nn-使用递归/](https://www.geeksforgeeks.org/sum-of-the-series-11-22-33-nn-using-recursion/)

给定一个整数 **n** ，任务是求数列**1<sup>1</sup>+2<sup>2</sup>+3<sup>3</sup>+…..+ n <sup>n</sup>** 使用递归。
**示例:**

> **输入:** n = 2
> **输出:**5
> 1<sup>1</sup>+2<sup>2</sup>= 1+4 = 5
> **输入:** n = 3
> **输出:**32
> 1<sup>1</sup>+2<sup>2</sup>+3<sup>3</sup>= 1+4+27 = 32

**方法:**从 **n** 开始，开始将系列的所有术语逐一相加，每次递归调用中 **n** 的值递减 **1** ，直到 **n = 1** 的值，对此返回 **1** 为 **1 <sup>1</sup> = 1** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Recursive function to return
// the sum of the given series
ll sum(int n)
{

    // 1^1 = 1
    if (n == 1)
        return 1;
    else

        // Recursive call
        return ((ll)pow(n, n) + sum(n - 1));
}

// Driver code
int main()
{
    int n = 2;
    cout << sum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Recursive function to return
    // the sum of the given series
    static long sum(int n)
    {

        // 1^1 = 1
        if (n == 1)
            return 1;
        else

            // Recursive call
            return ((long)Math.pow(n, n) + sum(n - 1));
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 2;
        System.out.println(sum(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Recursive function to return
# the sum of the given series
def sum(n):
    if n == 1:
        return 1
    else:

        # Recursive call
        return pow(n, n) + sum(n - 1)

# Driver code
n = 2
print(sum(n))

# This code is contributed
# by Shrikant13
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Recursive function to return
    // the sum of the given series
    static long sum(int n)
    {
        // 1^1 = 1
        if (n == 1)
            return 1;
        else

            // Recursive call
            return ((long)Math.Pow(n, n) + sum(n - 1));
    }

    // Driver code
    public static void Main()
    {
        int n = 2;
        Console.Write(sum(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Recursive function to return
// the sum of the given series
function sum($n)
{

    // 1^1 = 1
    if ($n == 1)
        return 1;
    else

        // Recursive call
        return (pow($n, $n) + sum($n - 1));
}

// Driver code
$n = 2;
echo(sum($n));

// This code is contributed
// by Code_Mech
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Recursive function to return
// the sum of the given series
function sum(n)
{

    // 1^1 = 1
    if (n == 1)
        return 1;
    else

        // Recursive call
        return (Math.pow(n, n) + sum(n - 1));
}

// Driver code
var n = 2;
document.write(sum(n));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
5
```