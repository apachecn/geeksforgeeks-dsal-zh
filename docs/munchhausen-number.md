# 明希仙号

> 原文:[https://www.geeksforgeeks.org/munchhausen-number/](https://www.geeksforgeeks.org/munchhausen-number/)

给定一个数字 N，输出从 1 到 N 的所有芒奇豪森数。
**简介:**一个芒奇豪森数是一个等于其数字加到每个数字幂的和的数。类似于[自恋号](https://www.geeksforgeeks.org/narcissistic-number/)。

例如:
3435 = 3<sup>3</sup>+4<sup>4</sup>+3<sup>3</sup>+5<sup>5</sup>
One 也可以认为是 münchausen Number，因为 1 的幂 1 加 1 本身就是 1。
由于数字 3435 可以表示为数字的每一位数的和，当数字的每一位数被提升到与位数本身相等的幂时，即((3 的 3 次方)+ (4 的 4 次方)+ (3 的 3 次方)+ (5 的 5 次方))将输出相同的数字，即 3435，那么该数字可以称为 münchausen Number。

**示例:**

```
Input : 500
Output : 1
One is the only Münchhausen Number smaller
than or equal to 500.

Input : 5000
Output : 1  3435
1 and 3435 are the only Münchhausen Numbers smaller
than or equal to 5000.
```

我们预计 I 为每一个可能的数字 I 的幂 I，I 从 0 到 9 不等。在预计算这些值之后，我们遍历每个小于等于 n 的数字的所有数字，并计算升到幂的数字的和。

## C++

```
// C++ code for Münchhausen Number
#include <bits/stdc++.h>
using namespace std;

// pwr[i] is going to store i raised to
// power i.
unsigned pwr[10];

// Function to check out whether
// the number is Münchhausen
// Number or not
bool isMunchhausen(unsigned n) {
    unsigned sum = 0;
    int temp = n;

    while (temp) {
        sum += pwr[(temp % 10)];
        temp /= 10;
    }

    return (sum == n);
}

void printMunchhausenNumbers(int n)
{
    // Precompute i raised to power i for every i
    for (int i = 0; i < 10; i++ )
        pwr[i] = (unsigned)pow( (float)i, (float)i );

    // The input here is fixed i.e. it will
    // check up to n
    for (unsigned i = 1; i <= n; i++)

        // check the integer for Münchhausen Number,
        // if yes then print out the number
        if (isMunchhausen(i))
            cout << i << "\n";
}

// Driver Code
int main() {
    int n = 10000;
    printMunchhausenNumbers(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for Munchhausen Number

import java.io.*;
import java.util.*;

class GFG {
// pwr[i] is going to store i raised to
// power i.
static long[] pwr;

// Function to check out whether
// the number is Munchhausen
// Number or not
static Boolean isMunchhausen(int n) {
    long sum = 0l;
    int temp = n;

    while (temp>0) {
        int index= temp%10;
        sum =sum + pwr[index];
        temp /= 10;
    }

    return (sum == n);
}

static void printMunchhausenNumbers(int n)
{
    pwr= new long[10];

    // Precompute i raised to
    // power i for every i
    for (int i = 0; i < 10; i++ )
        pwr[i] = (long)Math.pow( (float)i, (float)i );

    // The input here is fixed i.e. it will
    // check up to n
    for (int i = 1; i <= n; i++)

        // check the integer for Munchhausen Number,
        // if yes then print out the number
        if (isMunchhausen(i)==true)
            System.out.println(i );
}
    public static void main (String[] args) {
    int n = 10000;
    printMunchhausenNumbers(n);
     }
}
// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python 3 code for
# Münchhausen Number
import math

# pwr[i] is going to
# store i raised to
# power i.
pwr = [0] * 10

# Function to check out
# whether the number is
# Münchhausen Number or
# not
def isMunchhausen(n) :

    sm = 0
    temp = n

    while (temp) :
        sm= sm + pwr[(temp % 10)]
        temp = temp // 10

    return (sm == n)

def printMunchhausenNumbers(n) :

    # Precompute i raised to
    # power i for every i
    for i in range(0, 10) :
        pwr[i] = math.pow((float)(i), (float)(i))

    # The input here is fixed
    # i.e. it will check up to n
    for i in range(1,n+1) :

        # check the integer for
        # Münchhausen Number, if
        # yes then print out the
        # number
        if (isMunchhausen(i)) :
            print( i )

# Driver Code
n = 10000
printMunchhausenNumbers(n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# code for Munchhausen Number
using System;

class GFG {

    // pwr[i] is going to store i
    // raised to power i.
    static long[] pwr;

    // Function to check out whether
    // the number is Munchhausen
    // Number or not
    static bool isMunchhausen(int n)
    {
        long sum = 0;
        int temp = n;

        while (temp > 0) {
            int index = temp % 10;
            sum = sum + pwr[index];
            temp /= 10;
        }

        return (sum == n);
    }

    static void printMunchhausenNumbers(int n)
    {
        pwr = new long[10];

        // Precompute i raised to
        // power i for every i
        for (int i = 0; i < 10; i++)
            pwr[i] = (long)Math.Pow((float)i, (float)i);

        // The input here is fixed i.e.
        // it will check up to n
        for (int i = 1; i <= n; i++)

            // check the integer for Munchhausen Number,
            // if yes then print out the number
            if (isMunchhausen(i) == true)
                Console.WriteLine(i);
    }

    // Driver Code
    public static void Main()
    {
        int n = 10000;
        printMunchhausenNumbers(n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code for Münchhausen Number

// pwr[i] is going to store i raised
// to power i.
$pwr = array_fill(0, 10, 0);

// Function to check out whether the
// number is Münchhausen Number or not
function isMunchhausen($n)
{
    global $pwr;
    $sm = 0;
    $temp = $n;

    while ($temp)
    {
        $sm= $sm + $pwr[($temp % 10)];
        $temp = (int)($temp / 10);
    }
    return ($sm == $n);
}

function printMunchhausenNumbers($n)
{
    global $pwr;

    // Precompute i raised to power
    // i for every i
    for ($i = 0; $i < 10; $i++)
        $pwr[$i] = pow((float)($i), (float)($i));

    // The input here is fixed i.e. it
    // will check up to n
    for ($i = 1; $i < $n + 1; $i++)

        // check the integer for Münchhausen
        // Number, if yes then print out the
        // number
        if (isMunchhausen($i))
            print($i . "\n");
}

// Driver Code
$n = 10000;
printMunchhausenNumbers($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript code for Munchhausen Number
// pwr[i] is going to store i raised to

// power i.
var pwr;

// Function to check out whether
// the number is Munchhausen
// Number or not
function isMunchhausen(n)
{
    var sum = 0;
    var temp = n;

    while (temp > 0)
    {
        var index= temp % 10;
        sum =sum + pwr[index];
        temp = parseInt(temp / 10);
    }
    return (sum == n);
}

function printMunchhausenNumbers(n)
{
    pwr = Array.from({length: 10}, (_, i) => 0);

    // Precompute i raised to
    // power i for every i
    for(var i = 0; i < 10; i++)
        pwr[i] = Math.pow(i, i);

    // The input here is fixed i.e. it will
    // check up to n
    for(var i = 1; i <= n; i++)

        // check the integer for Munchhausen Number,
        // if yes then print out the number
        if (isMunchhausen(i) == true)
            document.write(i + "<br>");
}

// Driver code
var n = 10000;

printMunchhausenNumbers(n);

// This code is contributed by Princi Singh

</script>
```

**输出:**

```
1
3435
```

**注:**如果采用 0^0 = 0 的定义，那么正好有四个 münchausen 数:0、1、3435 和 438579088【来源:[math world](http://mathworld.wolfram.com/MuenchhausenNumber.html)】