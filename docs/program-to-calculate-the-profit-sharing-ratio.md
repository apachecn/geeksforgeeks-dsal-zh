# 计算利润分成比例的程序

> 原文:[https://www . geeksforgeeks . org/计算利润分成比例的程序/](https://www.geeksforgeeks.org/program-to-calculate-the-profit-sharing-ratio/)

给定一系列金额和时间段，表示 N 个人投资的金额和他们投资的时间段。任务是计算**末利润比**。
**例:**

> **输入:** n = 2，
> Amount1 = 7000，时间 1 = 12 个月
> Amount2 = 6000，时间 2 = 6 个月
> T5】输出:7:3
> T8】输入: n = 3，
> Amount1 = 5000，时间 1 = 6 个月
> Amount2 = 6000，时间 2 = 6 个月
> Amount3 = 1000，时间

**公式:**

> 第一人股:(第一人出资额)*(第一个时间段)
> 第二人股:(第二人出资额)*(第二个时间段)
> 第三人股:(第三人出资额)*(第三个时间段)以此类推……
> T3】比例:第一人股:第二人股:第三人股

下面是需要的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Calculating GCD of an array.
int find_Gcd(int crr[], int n)
{
    int i;
    int result = crr[0];
    for (i = 1; i < n; i++)
        result = __gcd(crr[i], result);

    return result;
}

// Function to calculate the Share
void profitRatio(int amountArr[], int timeTrr[],
                 int n)
{
    int i, crr[n];
    for (i = 0; i < n; i++)
        crr[i] = amountArr[i] * timeTrr[i];

    int Share = find_Gcd(crr, n);

    for (i = 0; i < n - 1; i++)
        cout << crr[i] / Share << " : ";
    cout << crr[i] / Share;
}

// Driver Code
int main()
{
    int amountArr[] = { 5000, 6000, 1000 };
    int timeTrr[] = { 6, 6, 12 };

    int n = sizeof(amountArr) / sizeof(amountArr[0]);

    profitRatio(amountArr, timeTrr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// above approach
import java.io.*;

class GFG
{

// Recursive function to
// return gcd of a and b
static int __gcd(int a, int b)
{
    // Everything divides 0
    if (a == 0 || b == 0)
    return 0;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);
    return __gcd(a, b - a);
}

// Calculating GCD of an array.
static int find_Gcd(int crr[], int n)
{
    int i;
    int result = crr[0];
    for (i = 1; i < n; i++)
        result = __gcd(crr[i], result);

    return result;
}

// Function to calculate the Share
static void profitRatio(int amountArr[],
                        int timeTrr[],
                        int n)
{
    int i;
    int crr[] = new int[n] ;
    for (i = 0; i < n; i++)
        crr[i] = amountArr[i] *
                 timeTrr[i];

    int Share = find_Gcd(crr, n);

    for (i = 0; i < n - 1; i++)
    System.out.print(crr[i] / Share + " : ");
    System.out.print(crr[i] / Share);
}

// Driver Code
public static void main (String[] args)
{
    int amountArr[] = {5000, 6000, 1000};
    int timeTrr[] = {6, 6, 12};

    int n = amountArr.length;

    profitRatio(amountArr, timeTrr, n);
}
}

// This code is contributed
// by inder_verma.
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Recursive function to
# return gcd of a and b
def __gcd(a, b):

    # Everything divides 0
    if(a == 0 or b == 0):
        return 0;

    # base case
    if(a == b):
        return a;

    # a is greater
    if(a > b):
        return __gcd(a - b, b);
    return __gcd(a, b - a);

# Calculating GCD of an array.
def find_Gcd(crr, n):
    result = crr[0];
    for i in range(1, n):
        result = __gcd(crr[i], result);
    return result;

# Function to calculate the Share
def profitRatio(amountArr, timeTrr, n):
    i = 0;
    crr = [0] * n;
    for i in range(n):
        crr[i] = amountArr[i] * timeTrr[i];

    Share = find_Gcd(crr, n);

    for i in range(n - 1):
        print(int(crr[i] / Share),
                     end = " : ");
    print(int(crr[i + 1] / Share));

# Driver Code
amountArr = [5000, 6000, 1000];
timeTrr = [6, 6, 12];

n = len(amountArr);

profitRatio(amountArr, timeTrr, n);

# This code is contributed
# by mits
```

## C#

```
// C# implementation of
// above approach
using System;

class GFG
{

// Recursive function to
// return gcd of a and b
static int __gcd(int a, int b)
{
    // Everything divides 0
    if (a == 0 || b == 0)
    return 0;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);
    return __gcd(a, b - a);
}

// Calculating GCD of an array.
static int find_Gcd(int []crr, int n)
{
    int i;
    int result = crr[0];
    for (i = 1; i < n; i++)
        result = __gcd(crr[i], result);

    return result;
}

// Function to calculate the Share
static void profitRatio(int []amountArr,
                        int []timeTrr,
                        int n)
{
    int i;
    int []crr = new int[n] ;
    for (i = 0; i < n; i++)
        crr[i] = amountArr[i] *
                timeTrr[i];

    int Share = find_Gcd(crr, n);

    for (i = 0; i < n - 1; i++)
    Console.Write(crr[i] / Share + " : ");
    Console.Write(crr[i] / Share);
}

// Driver Code
public static void Main ()
{
    int []amountArr = {5000, 6000, 1000};
    int []timeTrr = {6, 6, 12};

    int n = amountArr.Length;

    profitRatio(amountArr, timeTrr, n);
}
}

// This code is contributed
// by inder_verma.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of
// above approach

// Recursive function to
// return gcd of a and b
function __gcd($a, $b)
{
    // Everything divides 0
    if ($a == 0 or $b == 0)
    return 0;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return __gcd($a - $b, $b);
    return __gcd($a, $b - $a);
}

// Calculating GCD of an array.
function find_Gcd($crr, $n)
{
    $i;
    $result = $crr[0];
    for ($i = 1; $i < $n; $i++)
        $result = __gcd($crr[$i],
                        $result);

    return $result;
}

// Function to calculate the Share
function profitRatio($amountArr,
                     $timeTrr, $n)
{
    $i;
    $crr = array();
    for ($i = 0; $i < $n; $i++)
        $crr[$i] = $amountArr[$i] *
                   $timeTrr[$i];

    $Share = find_Gcd($crr, $n);

    for ($i = 0; $i < $n - 1; $i++)
        echo $crr[$i] / $Share , " : ";
    echo $crr[$i] / $Share;
}

// Driver Code
$amountArr = array(5000, 6000, 1000);
$timeTrr = array(6, 6, 12);

$n = count($amountArr);

profitRatio($amountArr, $timeTrr, $n);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>
// javascript implementation of
// above approach

    // Recursive function to
    // return gcd of a and b
    function __gcd(a , b) {
        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);
        return __gcd(a, b - a);
    }

    // Calculating GCD of an array.
    function find_Gcd(crr , n) {
        var i;
        var result = crr[0];
        for (i = 1; i < n; i++)
            result = __gcd(crr[i], result);

        return result;
    }

    // Function to calculate the Share
    function profitRatio(amountArr , timeTrr , n) {
        var i;
        var crr = Array(n).fill(0);
        for (i = 0; i < n; i++)
            crr[i] = amountArr[i] * timeTrr[i];

        var Share = find_Gcd(crr, n);

        for (i = 0; i < n - 1; i++)
            document.write(crr[i] / Share + " : ");
        document.write(crr[i] / Share);
    }

    // Driver Code

        var amountArr = [ 5000, 6000, 1000 ];
        var timeTrr = [ 6, 6, 12 ];

        var n = amountArr.length;

        profitRatio(amountArr, timeTrr, n);

// This code contributed by aashish1995

</script>
```

**Output:** 

```
5 : 6 : 2
```