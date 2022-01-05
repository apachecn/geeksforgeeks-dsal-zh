# 计算功率 k 倍% m 的功率

> 原文:[https://www . geesforgeks . org/compute-power-of-power-k-times-m/](https://www.geeksforgeeks.org/compute-power-of-power-k-times-m/)

给定 x，k 和 m. Compute (x <sup>xxx…k</sup> )%m，x 为 k 次幂。给定 x 总是素数，m 大于 x。

**例:**

```
Input : 2 3 3
Output : 1
Explanation : ((2 ^ 2) ^ 2) % 3 
           = (4 ^ 2) % 3 
           = 1

Input : 3 2 3
Output : 0
Explanation : (3^3)%3 = 0
```

一种**天真的**方法是计算 x 的 k 次幂，每次做模运算。

## c++

```
// C++ program for computing
// x^x^x^x.. %m
#include <bits/stdc++.h>
using namespace std;

// Function to compute the given value
int calculate(int x, int k, int m)
{
    int result = x;
    k--;

    // compute power k times
    while (k--) {
        result = pow(result, x);

        if (result > m)
            result %= m;
    }

    return result;
}

// Driver Code
int main()
{
    int x = 5, k = 2, m = 3;

    // Calling function
    cout << calculate(x, k, m);

    return 0;
}
```

## Java

```
// Java program for computing
// x^x^x^x.. %m
class GFG
{

// Function to compute
// the given value
static int calculate(int x,
                     int k, int m)
{
    int result = x;
    k--;

    // compute power k times
    while (k --> 0)
    {
        result = (int)Math.pow(result, x);

        if (result > m)
            result %= m;
    }

    return result;
}

// Driver Code
public static void main(String args[])
{
    int x = 5, k = 2, m = 3;

    // Calling function
    System.out.println( calculate(x, k, m));
}
}

// This code is contributed by Arnab Kundu
```

## python 3

```
# Python3 program for
# computing x^x^x^x.. %m
import math

# Function to compute
# the given value
def calculate(x, k, m):
    result = x;
    k = k - 1;

    # compute power k times
    while (k):
        result = math.pow(result, x);
        if (result > m):
            result = result % m;
        k = k - 1;
    return int(result);

# Driver Code
x = 5;
k = 2;
m = 3;

# Calling function
print(calculate(x, k, m));

# This code is contributed
# by mits
```

## c#

```
// C# program for computing
// x^x^x^x.. %m
using System;

class GFG
{

// Function to compute
// the given value
static int calculate(int x,
                     int k,
                     int m)
{
    int result = x;
    k--;

    // compute power
    // k times
    while (k --> 0)
    {
        result = (int)Math.Pow(result, x);

        if (result > m)
            result %= m;
    }

    return result;
}

// Driver Code
static public void Main ()
{
    int x = 5, k = 2, m = 3;

    // Calling function
    Console.WriteLine(
            calculate(x, k, m));
}
}

// This code is contributed
// by ajit
```

## PHP

```
<?php
// PHP program for computing
// x^x^x^x.. %m

// Function to compute
// the given value
function calculate($x, $k, $m)
{
    $result = $x;
    $k--;

    // compute power k times
    while ($k--)
    {
        $result = pow($result, $x);

        if ($result > $m)
            $result %= $m;
    }

    return $result;
}

// Driver Code
$x = 5;
$k = 2;
$m = 3;

// Calling function
echo calculate($x, $k, $m);

// This code is contributed
// by akt_mit
?>
```

## Javascript

```
<script>
//program for computing
// x^x^x^x.. %m

// Function to compute
// the given value
function calculate(x, k, m)
{
    let result = x;
    k = k - 1;

    // compute power k times
    while (k--)
    {
        result = Math.pow(result, x);

        if (result > m)
            result %= m;
    }

    return result;
}

// Driver Code
let x = 5;
let k = 2;
let m = 3;

// Calling function
document.write(calculate(x, k, m));

// This code is contributed
// by sravan kumar
</script>
```

**输出:**

```
2
```