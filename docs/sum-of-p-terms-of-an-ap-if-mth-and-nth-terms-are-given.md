# 如果给定了第 m 个和第 n 个项，AP 的 P 项之和

> 原文:[https://www . geesforgeks . org/p-of-of-p-terms-of-an-AP-if-mth-and-n-terms-given/](https://www.geeksforgeeks.org/sum-of-p-terms-of-an-ap-if-mth-and-nth-terms-are-given/)

给定算术级数的 Mth 和 Nth 项。任务是找出它的前 p 项的和。
**例:**

> **输入:** m = 6，n = 10，mth = 12，n = 20，p = 5
> **输出:** 30
> **输入:** m = 10，n = 20，mth = 70，n = 10，p = 4
> **输出:** 70

**逼近:**设 a 为第一项，d 为给定 AP 的公差。因此

```
mth term = a + (m-1)d and
nth term = a + (n-1)d
```

从这两个方程，求 a 和 d 的值，现在用一个 AP 的 p 项之和的公式。
p 项之和=

```
( p * ( 2*a + (p-1) * d ) ) / 2;
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the value of the
pair<double, double> findingValues(double m,
               double n, double mth, double nth)
{
    // Calculate value of d using formula
    double d = (abs(mth - nth)) / abs((m - 1) - (n - 1));

    // Calculate value of a using formula
    double a = mth - ((m - 1) * d);

    // Return pair
    return make_pair(a, d);
}

// Function to calculate value sum
// of first p numbers of the series
double findSum(int m, int n, int mth, int nth, int p)
{

    pair<double, double> ad;

    // First calculate value of a and d
    ad = findingValues(m, n, mth, nth);

    double a = ad.first, d = ad.second;

    // Calculate the sum by using formula
    double sum = (p * (2 * a + (p - 1) * d)) / 2;

    // Return the sum
    return sum;
}

// Driven Code
int main()
{

    double m = 6, n = 10, mTerm = 12, nTerm = 20, p = 5;

    cout << findSum(m, n, mTerm, nTerm, p) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function to calculate the value of the
static ArrayList<Integer> findingValues(int m, int n,
                                int mth, int nth)
{

    // Calculate value of d using formula
    int d = (Math.abs(mth - nth)) /
        Math.abs((m - 1) - (n - 1));

    // Calculate value of a using formula
    int a = mth - ((m - 1) * d);
    ArrayList<Integer> res=new ArrayList<Integer>();
    res.add(a);
    res.add(d);

    // Return pair
    return res;
}

// Function to calculate value sum
// of first p numbers of the series
static int findSum(int m, int n, int mth,
                            int nth, int p)
{
    // First calculate value of a and d
    ArrayList<Integer> ad = findingValues(m, n, mth, nth);

    int a = ad.get(0);
    int d = ad.get(1);

    // Calculate the sum by using formula
    int sum = (p * (2 * a + (p - 1) * d)) / 2;

    // Return the sum
    return sum;
}

// Driver Code
public static void main (String[] args)
{
    int m = 6, n = 10, mTerm = 12, nTerm = 20, p = 5;
    System.out.println(findSum(m, n, mTerm, nTerm, p));
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import math as mt

# Function to calculate the value of the
def findingValues(m, n, mth, nth):

    # Calculate value of d using formula
    d = ((abs(mth - nth)) /
          abs((m - 1) - (n - 1)))

    # Calculate value of a using formula
    a = mth - ((m - 1) * d)

    # Return pair
    return a, d

# Function to calculate value sum
# of first p numbers of the series
def findSum(m, n, mth, nth, p):

    # First calculate value of a and d
    a,d = findingValues(m, n, mth, nth)

    # Calculate the sum by using formula
    Sum = (p * (2 * a + (p - 1) * d)) / 2

    # Return the Sum
    return Sum

# Driver Code
m = 6
n = 10
mTerm = 12
nTerm = 20
p = 5

print(findSum(m, n, mTerm, nTerm, p))

# This code is contributed by
# Mohit Kumar 29
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;

class GFG
{

// Function to calculate the value of the
static ArrayList findingValues(int m, int n,
                                int mth, int nth)
{

    // Calculate value of d using formula
    int d = (Math.Abs(mth - nth)) /
        Math.Abs((m - 1) - (n - 1));

    // Calculate value of a using formula
    int a = mth - ((m - 1) * d);
    ArrayList res=new ArrayList();
    res.Add(a);
    res.Add(d);

    // Return pair
    return res;
}

// Function to calculate value sum
// of first p numbers of the series
static int findSum(int m, int n, int mth,
                            int nth, int p)
{
    // First calculate value of a and d
    ArrayList ad = findingValues(m, n, mth, nth);

    int a = (int)ad[0];
    int d = (int)ad[1];

    // Calculate the sum by using formula
    int sum = (p * (2 * a + (p - 1) * d)) / 2;

    // Return the sum
    return sum;
}

// Driver Code
public static void Main ()
{
    int m = 6, n = 10, mTerm = 12, nTerm = 20, p = 5;
    Console.WriteLine(findSum(m, n, mTerm, nTerm, p));
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to calculate the value of the
function findingValues($m, $n, $mth, $nth)
{
    // Calculate value of d using formula
    $d = (abs($mth - $nth)) /
          abs(($m - 1) - ($n - 1));

    // Calculate value of a using formula
    $a = $mth - (($m - 1) * $d);

    // Return pair
    return array($a, $d);
}

// Function to calculate value sum
// of first p numbers of the series
function findSum($m, $n, $mth, $nth, $p)
{
    // First calculate value of a and d
    $ad = findingValues($m, $n, $mth, $nth);

    $a = $ad[0];
    $d = $ad[1];

    // Calculate the sum by using formula
    $sum = ($p * (2 * $a + ($p - 1) * $d)) / 2;

    // Return the sum
    return $sum;
}

// Driver Code
$m = 6;
$n = 10;
$mTerm = 12;
$nTerm = 20;
$p = 5;

echo findSum($m, $n, $mTerm, $nTerm, $p);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    // Function to calculate the value of the
    function findingValues(m, n, mth, nth)
    {

        // Calculate value of d using formula
        let d = parseInt(
        (Math.abs(mth - nth)) / Math.abs((m - 1) - (n - 1)), 10);

        // Calculate value of a using formula
        let a = mth - ((m - 1) * d);
        let res = [];
        res.push(a);
        res.push(d);

        // Return pair
        return res;
    }

    // Function to calculate value sum
    // of first p numbers of the series
    function findSum(m, n, mth, nth, p)
    {
        // First calculate value of a and d
        let ad = findingValues(m, n, mth, nth);

        let a = ad[0];
        let d = ad[1];

        // Calculate the sum by using formula
        let sum = parseInt((p * (2 * a + (p - 1) * d)) / 2, 10);

        // Return the sum
        return sum;
    }

    let m = 6, n = 10, mTerm = 12, nTerm = 20, p = 5;
    document.write(findSum(m, n, mTerm, nTerm, p));

</script>
```

**Output:** 

```
30
```