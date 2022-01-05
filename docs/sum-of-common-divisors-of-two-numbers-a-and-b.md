# 两个数 A 和 B 的公约数之和

> 原文:[https://www . geeksforgeeks . org/两个数 a 和 b 的公约数之和/](https://www.geeksforgeeks.org/sum-of-common-divisors-of-two-numbers-a-and-b/)

给定两个数字 a 和 b，任务是找出两个数字 a 和 b 的公共因子之和。数字 a 和 b 小于 10^8.
**例:**

```
Input: A = 10, B = 15
Output: Sum = 6
The common factors are 1, 5, so their sum is 6 

Input: A = 100, B = 150
Output: Sum = 93
```

**天真法:**从 i = 1 迭代到 A 和 B 的最小值，检查 **i** 是否是 A 和 B 的因子，如果 **i** 是 **A** 和 **B** 的因子，则相加。在循环结束时显示总和。
以下是上述方法的实施:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// print the sum of common factors
int sum(int a, int b)
{
    // sum of common factors
    int sum = 0;

    // iterate from 1 to minimum of a and b
    for (int i = 1; i <= min(a, b); i++)

        // if i is the common factor
        // of both the numbers
        if (a % i == 0 && b % i == 0)
            sum += i;

    return sum;
}

// Driver code
int main()
{
    int A = 10, B = 15;

    // print the sum of common factors
    cout << "Sum = " << sum(A, B) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;

class GFG {

// print the sum of common factors
static int sum(int a, int b)
{
    // sum of common factors
    int sum = 0;

    // iterate from 1 to minimum of a and b
    for (int i = 1; i <= Math.min(a, b); i++)

        // if i is the common factor
        // of both the numbers
        if (a % i == 0 && b % i == 0)
            sum += i;

    return sum;
}

// Driver code

    public static void main (String[] args) {
            int A = 10, B = 15;

    // print the sum of common factors
    System.out.print("Sum = " + sum(A, B));
    }
}
// This code is contributed by shs..
```

## 蟒蛇 3

```
# Python 3 implementation of
# above approach

# print the sum of common factors
def sum(a, b):

    # sum of common factors
    sum = 0

    # iterate from 1 to minimum of a and b
    for i in range (1, min(a, b)):

        # if i is the common factor
        # of both the numbers
        if (a % i == 0 and b % i == 0):
            sum += i

    return sum

# Driver Code
A = 10
B = 15

# print the sum of common factors
print("Sum =", sum(A, B))

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# implementation of above approach

using System;

class GFG {

// print the sum of common factors
static int sum(int a, int b)
{
    // sum of common factors
    int sum = 0;

    // iterate from 1 to minimum of a and b
    for (int i = 1; i <= Math.Min(a, b); i++)

        // if i is the common factor
        // of both the numbers
        if (a % i == 0 && b % i == 0)
            sum += i;

    return sum;
}

// Driver code

    public static void Main () {
            int A = 10, B = 15;

    // print the sum of common factors
    Console.WriteLine("Sum = " + sum(A, B));
    }
}
// This code is contributed by shs..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// print the sum of common factors
function sum($a, $b)
{
    // sum of common factors
    $sum = 0;

    // iterate from 1 to minimum of a and b
    for ($i = 1; $i <= min($a, $b); $i++)

        // if i is the common factor
        // of both the numbers
        if ($a %$i == 0 && $b %$i == 0)
            $sum += $i;

    return $sum;
}

// Driver code
$A = 10; $B = 15;

// print the sum of common factors
echo "Sum = " , sum($A, $B);

// This code is contributed by shs.
?>
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// print the sum of common factors
function sum(a, b)
{
    // sum of common factors
    var sum = 0;

    // iterate from 1 to minimum of a and b
    for (var i = 1; i <= Math.min(a, b); i++)

        // if i is the common factor
        // of both the numbers
        if (a % i == 0 && b % i == 0)
            sum += i;

    return sum;
}

var A = 10, B = 15;

// print the sum of common factors
document.write("Sum = " + sum(A, B) + "<br>");

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
Sum = 6
```

一种**有效的方法**是使用与[两个数](https://www.geeksforgeeks.org/common-divisors-of-two-numbers/)的公约数相同的概念。计算给定两个数的最大公约数(gcd)，然后求出该 gcd 的除数之和。

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate gcd of two numbers
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to calculate all common divisors
// of two given numbers
// a, b --> input integer numbers
int sumcommDiv(int a, int b)
{
    // find gcd of a, b
    int n = gcd(a, b);

    // Find the sum of divisors of n.
    int sum = 0;
    for (int i = 1; i <= sqrt(n); i++) {

        // if 'i' is factor of n
        if (n % i == 0) {

            // check if divisors are equal
            if (n / i == i)
                sum += i;
            else
                sum += (n / i) + i;
        }
    }

    return sum;
}

// Driver program to run the case
int main()
{
    int a = 10, b = 15;
    cout << "Sum = " << sumcommDiv(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of above approach

import java.io.*;

class GFG {

// Function to calculate gcd of two numbers
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to calculate all common divisors
// of two given numbers
// a, b --> input integer numbers
static int sumcommDiv(int a, int b)
{
    // find gcd of a, b
    int n = gcd(a, b);

    // Find the sum of divisors of n.
    int sum = 0;
    for (int i = 1; i <= Math.sqrt(n); i++) {

        // if 'i' is factor of n
        if (n % i == 0) {

            // check if divisors are equal
            if (n / i == i)
                sum += i;
            else
                sum += (n / i) + i;
        }
    }

    return sum;
}

// Driver program to run the case
    public static void main (String[] args) {

    int a = 10, b = 15;
    System.out.println("Sum = " + sumcommDiv(a, b));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of above approach
from math import gcd,sqrt

# Function to calculate all common divisors
# of two given numbers
# a, b --> input integer numbers
def sumcommDiv(a, b):
    # find gcd of a, b
    n = gcd(a, b)

    # Find the sum of divisors of n.
    sum = 0
    N = int(sqrt(n))+1
    for i in range(1,N,1):
        # if 'i' is factor of n
        if (n % i == 0):
            # check if divisors are equal
            if (n / i == i):
                sum += i
            else:
                sum += (n / i) + i

    return sum

# Driver program to run the case
if __name__ == '__main__':
    a = 10
    b = 15
    print("Sum =",int(sumcommDiv(a, b)))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of above approach

using System;

public class GFG{

// Function to calculate gcd of two numbers
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to calculate all common divisors
// of two given numbers
// a, b --> input integer numbers
static int sumcommDiv(int a, int b)
{
    // find gcd of a, b
    int n = gcd(a, b);

    // Find the sum of divisors of n.
    int sum = 0;
    for (int i = 1; i <= Math.Sqrt(n); i++) {

        // if 'i' is factor of n
        if (n % i == 0) {

            // check if divisors are equal
            if (n / i == i)
                sum += i;
            else
                sum += (n / i) + i;
        }
    }

    return sum;
}

// Driver program to run the case
    static public void Main (){
        int a = 10, b = 15;
        Console.WriteLine("Sum = " + sumcommDiv(a, b));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to calculate gcd of two numbers
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// Function to calculate all common divisors
// of two given numbers
// a, b --> input integer numbers
function  sumcommDiv($a, $b)
{
    // find gcd of a, b
$n = gcd($a, $b);

    // Find the sum of divisors of n.
    $sum = 0;
    for ($i = 1; $i <= sqrt($n); $i++) {

        // if 'i' is factor of n
        if ($n % $i == 0) {

            // check if divisors are equal
            if ($n / $i == $i)
                $sum += $i;
            else
                $sum += ($n / $i) + $i;
        }
    }

    return $sum;
}

// Driver program to run the case
    $a = 10;
    $b = 15;
    echo "Sum = " , sumcommDiv($a, $b);

?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to calculate gcd of two numbers
function gcd(a, b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to calculate all common divisors
// of two given numbers
// a, b --> input integer numbers
function sumcommDiv(a, b)
{
    // find gcd of a, b
    var n = gcd(a, b);

    // Find the sum of divisors of n.
    var sum = 0;
    for (var i = 1; i <= Math.sqrt(n); i++) {

        // if 'i' is factor of n
        if (n % i == 0) {

            // check if divisors are equal
            if (n / i == i)
                sum += i;
            else
                sum += (n / i) + i;
        }
    }

    return sum;
}

// Driver program to run the case
var a = 10, b = 15;
document.write( "Sum = " + sumcommDiv(a, b));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
Sum = 6
```