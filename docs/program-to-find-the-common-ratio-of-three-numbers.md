# 程序求三个数的公比

> 原文:[https://www . geesforgeks . org/program-to-find-common-ratio-of-three-numbers/](https://www.geeksforgeeks.org/program-to-find-the-common-ratio-of-three-numbers/)

给定 a:b 和 b:c .任务是编写一个程序来寻找比率 a:b:c
**示例:**

```
Input: a:b = 2:3, b:c = 3:4
Output: 2:3:4

Input:  a:b = 3:4, b:c = 8:9
Output: 6:8:9
```

**方法:**诀窍在于使两个比率中的常用术语‘b’相等。因此，将第一个比率乘以 b <sub>2</sub> (第二个比率的 b 项)，将第二个比率乘以 b <sub>1</sub> 。

> **给定:** a:b <sub>1</sub> 和 b <sub>2</sub> :c
> **解:**a:b:c =(a * b<sub>2</sub>):(b<sub>1</sub>* b<sub>2</sub>):(c * b<sub>1</sub>)
> **例如:**
> 如果 a : b = 5 : 9 和 b
> 因此，将第一个比率乘以 7，将第二个比率乘以 9。
> 所以，a : b = 35 : 63 和 b : c = 63 : 36
> 这样，a : b : c = 35 : 63 : 36

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print a:b:c
void solveProportion(int a, int b1, int b2, int c)
{
    int A = a * b2;
    int B = b1 * b2;
    int C = b1 * c;

    // To print the given proportion
    // in simplest form.
    int gcd = __gcd(__gcd(A, B), C);

    cout << A / gcd << ":"
         << B / gcd << ":"
         << C / gcd;
}

// Driver code
int main()
{

    // Get the ratios
    int a, b1, b2, c;

    // Get ratio a:b1
    a = 3;
    b1 = 4;

    // Get ratio b2:c
    b2 = 8;
    c = 9;

    // Find the ratio a:b:c
    solveProportion(a, b1, b2, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.util.*;
import java.lang.*;
import java.io.*;
class GFG{

static int __gcd(int a,int b){
    return b==0 ? a : __gcd(b, a%b);
}   

// Function to print a:b:c
static void solveProportion(int a, int b1, int b2, int c)
{
    int A = a * b2;
    int B = b1 * b2;
    int C = b1 * c;

    // To print the given proportion
    // in simplest form.
    int gcd = __gcd(__gcd(A, B), C);

    System.out.print( A / gcd + ":"
         + B / gcd + ":"
         + C / gcd);
}

// Driver code
public static void  main(String args[])
{

    // Get the ratios
    int a, b1, b2, c;

    // Get ratio a:b1
    a = 3;
    b1 = 4;

    // Get ratio b2:c
    b2 = 8;
    c = 9;

    // Find the ratio a:b:c
    solveProportion(a, b1, b2, c);
}
}
```

## 蟒蛇 3

```
# Python 3 implementation
# of above approach
import math

# Function to print a:b:c
def solveProportion(a, b1, b2, c):

    A = a * b2
    B = b1 * b2
    C = b1 * c

    # To print the given proportion
    # in simplest form.
    gcd1 = math.gcd(math.gcd(A, B), C)

    print( str(A // gcd1) + ":" +
           str(B // gcd1) + ":" +
           str(C // gcd1))

# Driver code
if __name__ == "__main__":

    # Get ratio a:b1
    a = 3
    b1 = 4

    # Get ratio b2:c
    b2 = 8
    c = 9

    # Find the ratio a:b:c
    solveProportion(a, b1, b2, c)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
static int __gcd(int a,int b)
{
    return b == 0 ? a : __gcd(b, a % b);
}

// Function to print a:b:c
static void solveProportion(int a, int b1,
                            int b2, int c)
{
    int A = a * b2;
    int B = b1 * b2;
    int C = b1 * c;

    // To print the given proportion
    // in simplest form.
    int gcd = __gcd(__gcd(A, B), C);

    Console.Write( A / gcd + ":" +
                   B / gcd + ":" +
                   C / gcd);
}

// Driver code
public static void Main()
{

    // Get the ratios
    int a, b1, b2, c;

    // Get ratio a:b1
    a = 3;
    b1 = 4;

    // Get ratio b2:c
    b2 = 8;
    c = 9;

    // Find the ratio a:b:c
    solveProportion(a, b1, b2, c);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

function __gcd($a, $b)
{
    return $b == 0 ? $a : __gcd($b, $a % $b);
}

// Function to print a:b:c
function solveProportion($a, $b1, $b2, $c)
{
    $A = $a * $b2;
    $B = $b1 * $b2;
    $C = $b1 * $c;

    // To print the given proportion
    // in simplest form.
    $gcd = __gcd(__gcd($A, $B), $C);

    echo ($A / $gcd) . ":" .
         ($B / $gcd) . ":" . ($C / $gcd);
}

// Driver code

// Get the ratios
// Get ratio a:b1
$a = 3;
$b1 = 4;

// Get ratio b2:c
$b2 = 8;
$c = 9;

// Find the ratio a:b:c
solveProportion($a, $b1, $b2, $c);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    function __gcd(a, b)
    {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Function to print a:b:c
    function solveProportion(a, b1, b2, c)
    {
        let A = a * b2;
        let B = b1 * b2;
        let C = b1 * c;

        // To print the given proportion
        // in simplest form.
        let gcd = __gcd(__gcd(A, B), C);

        document.write( A / gcd + ":" + B / gcd + ":" + C / gcd);
    }

    // Get the ratios
    let a, b1, b2, c;

    // Get ratio a:b1
    a = 3;
    b1 = 4;

    // Get ratio b2:c
    b2 = 8;
    c = 9;

    // Find the ratio a:b:c
    solveProportion(a, b1, b2, c);

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
6:8:9
```