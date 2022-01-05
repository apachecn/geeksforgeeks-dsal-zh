# 如果给定了第 m 个和第 n 个项，则找到 GP 的第 Pth 个项

> 原文:[https://www . geeksforgeeks . org/find-PTH-term-of-a-gp-if-mth-和-n-term-被给予/](https://www.geeksforgeeks.org/find-pth-term-of-a-gp-if-mth-and-nth-terms-are-given/)

给定一个[几何级数](https://www.geeksforgeeks.org/geometric-progression/)的第 m 项和第 n 项。找到它的 Pth 术语。
**例:**

> **输入:** m = 10，n = 5，mth = 2560，n = 80，p = 30
> **输出:** pth = 81920
> **输入:** m = 8，n = 2，mth = 1250，n = 960，p = 15
> **输出:** 24964.4

**逼近:**
设 a 为第一项，r 为给定几何级数的公比。因此

```
mth term = a * pow ( r, (m-1) ) ....... (i) and
nth term = a * pow ( r, (n-1) ) ....... (ii)
```

为了方便起见，假设 m > n
从这两个方程中，
由于我们已经给出了 m，n，第 n 项和第 n 项的值，因此

```
r = pow(A/B, 1.0/(m-n))
```

现在将 r 的值放入上述两个等式中的任何一个，计算 a 的值

> **a =第 n 项/幂(r，(m-1))或**
> **a =第 n 项/幂(r，(n-1) )**

找到 a 和 r 的值后，使用 GP 的 Pth 项公式。

> **GP = a *幂的 pth 项(r，(p-1.0))；**

以下是上述方法的实现:

## C++

```
#include <cmath>
#include <iostream>
#include <vector>
using namespace std;

// function to calculate the value
// of the a and r of geometric series
pair<double, double> values_of_r_and_a(double m,
                                       double n,
                                       double mth,
                                       double nth)
{
    double a, r;

    if (m < n) {
        swap(m, n);
        swap(mth, nth);
    }

    // calculate value of r using formula
    r = pow(mth / nth, 1.0 / (m - n));

    // calculate value of a using value of r
    a = mth / pow(r, (m - 1));

    // push both values in the vector and return it
    return make_pair(a, r);
}

// function to calculate the value
// of pth term of the series
double FindSum(int m, int n, double mth,
               double nth, int p)
{
    pair<double, double> ar;

    // first calculate value of a and r
    ar = values_of_r_and_a(m, n, mth, nth);

    double a = ar.first;
    double r = ar.second;

    // calculate pth term by using formula
    double pth = a * pow(r, (p - 1.0));

    // return the value of pth term
    return pth;
}

// Driven program to test
int main()
{
    int m = 10, n = 5, p = 15;
    double mth = 2560, nth = 80;
    cout << FindSum(m, n, mth, nth, p)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.ArrayList;

class GFG
{

// function to calculate the value
// of the a and r of geometric series
static ArrayList values_of_r_and_a(double m, double n,
                                double mth, double nth)
{
    if (m < n)
    {
        double t = m;
        n = m;
        m = t;
        t = mth;
        mth = nth;
        nth = t;
    }

    // calculate value of r using formula
    double r = Math.pow(mth / nth, 1.0 / (m - n));

    // calculate value of a using value of r
    double a = mth / Math.pow(r, (m - 1));

    // push both values in the vector
    // and return it
    ArrayList arr = new ArrayList();
    arr.add(a);
    arr.add(r);
    return arr;
}

// function to calculate the value
// of pth term of the series
static double FindSum(double m, double n,
                    double mth, double nth,
                    double p)
{

    // first calculate value of a and r
    ArrayList ar = values_of_r_and_a(m, n, mth, nth);

    double a = (double)ar.get(0);
    double r = (double)ar.get(1);

    // calculate pth term by using formula
    double pth = a * Math.pow(r, (p - 1.0));

    // return the value of pth term
    return pth;
}

// Driver Code
public static void main(String[] args)
{
    double m = 10;
    double n = 5;
    double p = 15;
    double mth = 2560;
    double nth = 80;

    System.out.println((int)FindSum(m, n, mth, nth, p));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for above approach

# function to calculate the value
# of the a and r of geometric series
def values_of_r_and_a(m, n, mth, nth):

    a, r = 0.0, 0.0

    if (m < n):
        m, n = n, m
        mth, nth = mth, nth

    # calculate value of r using formula
    r = pow(mth // nth, 1.0 /(m - n))

    # calculate value of a using value of r
    a = mth // pow(r, (m - 1))

    # push both values in the vector
    # and return it
    return a, r

# function to calculate the value
# of pth term of the series
def FindSum(m, n, mth, nth, p):

    # first calculate value of a and r
    a,r = values_of_r_and_a(m, n, mth, nth)

    # calculate pth term by using formula
    pth = a * pow(r, (p - 1.0))

    # return the value of pth term
    return pth

# Driven Code
m, n, p = 10, 5, 15
mth, nth = 2560.0, 80.0
print(FindSum(m, n, mth, nth, p))

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;

class GFG
{

// function to calculate the value
// of the a and r of geometric series
static ArrayList values_of_r_and_a(double m, double n,
                                double mth, double nth)
{
    if (m < n)
    {
        double t = m;
        n = m;
        m = t;
        t = mth;
        mth = nth;
        nth = t;
    }

    // calculate value of r using formula
    double r = Math.Pow(mth / nth, 1.0 / (m - n));

    // calculate value of a using value of r
    double a = mth / Math.Pow(r, (m - 1));

    // push both values in the vector
    // and return it
    ArrayList arr = new ArrayList();
    arr.Add(a);
    arr.Add(r);
    return arr;
}

// function to calculate the value
// of pth term of the series
static double FindSum(double m, double n,
                    double mth, double nth,
                    double p)
{

    // first calculate value of a and r
    ArrayList ar = values_of_r_and_a(m, n, mth, nth);

    double a = (double)ar[0];
    double r = (double)ar[1];

    // calculate pth term by using formula
    double pth = a * Math.Pow(r, (p - 1.0));

    // return the value of pth term
    return pth;
}

// Driver Code
static void Main()
{
    double m = 10;
    double n = 5;
    double p = 15;
    double mth = 2560;
    double nth = 80;

    Console.WriteLine(FindSum(m, n, mth, nth, p));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of the above approach
function swap($a1, $a2)
{
    $temp = $a1;
    $a1 = $a2;
    $a2 = $temp;
}

// function to calculate the value
// of the a and r of geometric series
function values_of_r_and_a($m, $n, $mth, $nth)
{
    if ($m < $n)
    {
        swap($m, $n);
        swap($mth, $nth);
    }

    // calculate value of r using formula
    $r = pow($mth / $nth, 1.0 / ($m - $n));

    // calculate value of a using value of r
    $a = $mth / pow($r, ($m - 1));

    // push both values in the vector
    // and return it
    return array($a, $r);
}

// function to calculate the value
// of pth term of the series
function FindSum($m, $n, $mth, $nth, $p)
{

    // first calculate value of a and r
    $ar = values_of_r_and_a($m, $n, $mth, $nth);

    $a = $ar[0];
    $r = $ar[1];

    // calculate pth term by using formula
    $pth = $a * pow($r, ($p - 1.0));

    // return the value of pth term
    return $pth;
}

// Driver Code
$m = 10;
$n = 5;
$p = 15;

$mth = 2560;
$nth = 80;

echo FindSum($m, $n, $mth, $nth, $p);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // function to calculate the value
    // of the a and r of geometric series
    function values_of_r_and_a(m, n, mth, nth)
    {
        if (m < n)
        {
            let t = m;
            n = m;
            m = t;
            t = mth;
            mth = nth;
            nth = t;
        }

        // calculate value of r using formula
        let r = Math.pow(mth / nth, 1.0 / (m - n));

        // calculate value of a using value of r
        let a = mth / Math.pow(r, (m - 1));

        // push both values in the vector
        // and return it
        let arr = [];
        arr.push(a);
        arr.push(r);
        return arr;
    }

    // function to calculate the value
    // of pth term of the series
    function FindSum(m, n, mth, nth, p)
    {

        // first calculate value of a and r
        let ar = values_of_r_and_a(m, n, mth, nth);

        let a = ar[0];
        let r = ar[1];

        // calculate pth term by using formula
        let pth = a * Math.pow(r, (p - 1.0));

        // return the value of pth term
        return pth;
    }

    let m = 10;
    let n = 5;
    let p = 15;
    let mth = 2560;
    let nth = 80;

    document.write(FindSum(m, n, mth, nth, p));

</script>
```

**Output:** 

```
81920
```