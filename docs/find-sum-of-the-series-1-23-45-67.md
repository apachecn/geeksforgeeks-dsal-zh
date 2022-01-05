# 求数列 1-2+3-4+5-6+7 的和……

> 原文:[https://www . geesforgeks . org/find-series-sum-1-23-45-67/](https://www.geeksforgeeks.org/find-sum-of-the-series-1-23-45-67/)

给定一个数字 n，任务是找到下面系列的和，直到第 n <sup>个</sup>项。

> **1-2+3–4+5–6+…。**

**示例** :

```
Input : N = 8
Output : -4

Input : N = 10001
Output : 5001
```

**逼近:**如果我们仔细观察，可以看到上述级数的和遵循从 1 到 N 的正负整数交替的模式，如下所示:

```
N   = 1, 2, 3, 4, 5, 6, 7 ......
Sum = 1, -1, 2, -2, 3, -3, 4 ......
```

因此，从上面的模式中，我们可以得出:

*   当 n 为奇数时=> sum = (n+1)/2
*   当 n 为偶数时=> sum = (-1)*n/2

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of
// series 1 - 2 + 3 - 4 +......

#include <iostream>
using namespace std;

// Function to calculate sum
int solve_sum(int n)
{
    // when n is odd
    if (n % 2 == 1)
        return (n + 1) / 2;

    // when n is not odd
    return -n / 2;
}

// Driver code
int main()
{
    int n = 8;

    cout << solve_sum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of
// first n terms of the given series
import java.util.*;

class GFG
{
static int calculateSum(int n)
{
    // when n is odd
    if (n % 2 == 1)
        return (n + 1) / 2;

    // when n is not odd
    return -n / 2;
}

// Driver code
public static void main(String ar[])
{

// no. of terms to find the sum
int n = 8;
System.out.println(calculateSum(n));
}
}
```

## 蟒蛇 3

```
# Python program to find the sum of
# series 1 - 2 + 3 - 4 +......

# Function to calculate sum
def solve_sum(n):
    # when n is odd
    if(n % 2 == 1):
        return (n + 1)/2

    # when n is not odd
    return -n / 2

# Driver code
n = 8

print(int(solve_sum(n)))
```

## C#

```
// C# program to find sum of
// first n terms of the given series
using System;

class GFG
{
static int calculateSum(int n)
{
    // when n is odd
    if (n % 2 == 1)
        return (n + 1) / 2;

    // when n is not odd
    return -n / 2;
}

// Driver code
public static void Main()
{

    // no. of terms to find the sum
    int n = 8;
    Console.WriteLine(calculateSum(n));
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum of
// series 1 - 2 + 3 - 4 +......

// Function to calculate sum
function solve_sum($n)
{
    // when n is odd
    if ($n % 2 == 1)
        return ($n + 1) / 2;

    // when n is not odd
    return -$n / 2;
}

// Driver code
$n = 8;

echo solve_sum($n);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// javascript program to find sum of
// first n terms of the given series

function calculateSum(n)
{
    // when n is odd
    if (n % 2 == 1)
        return (n + 1) / 2;

    // when n is not odd
    return -n / 2;
}

// Driver code

// no. of terms to find the sum
var n = 8;
document.write(calculateSum(n));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
-4
```