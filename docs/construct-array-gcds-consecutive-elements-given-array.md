# 从给定数组中连续元素的 GCDs 构建一个数组

> 原文:[https://www . geesforgeks . org/construct-array-gcds-continuous-elements-given-array/](https://www.geeksforgeeks.org/construct-array-gcds-consecutive-elements-given-array/)

给定一个由 **n** 个元素组成的数组**。任务是找到 n + 1 的数组(比如 b[])，使得 b[i]和 b[i + 1]的最大公约数等于 a[i]。如果存在多个解，打印数组和最小的那个。
示例:** 

```
Input : a[] = { 1, 2, 3 }
Output : 1 2 6 3
GCD(1, 2) = 1
GCD(2, 6) = 2
GCD(6, 3) = 3
Also, 1 + 2 + 6 + 3 = 12 which is smallest among all
possible value of array that can be constructed.

Input : a[] = { 5, 10, 5 }
Output : 5 10 10 5
```

**假设给定数组 a[]中只有一个数字。假设它是 K，那么构造的数组中的两个数字(比如 b[])都将是 K 和 K。
所以，b[0]的值将只是 a[0]。现在考虑一下，我们已经完成了指数 **i** ，也就是说，我们已经处理了指数 I 并计算了 b[i + 1]。
现在的 gcd(b[i + 1]，b[i + 2]) = a[i + 1]和 gcd(b[i + 2]，b[i + 3]) = a[i + 2]。所以，b[i + 2] > = lcm(a[i + 1]，a[i + 2])。或者，b[i + 2]将是 lcm 的倍数(a[i + 1]，a[i + 2])。因为我们想要最小和，所以我们想要 b[i + 2]的最小值。所以，b[i + 2] = lcm(a[i + 2]，a[i + 3])。
以下是本办法的实施情况:** 

## **C++**

```
// CPP Program to construct an array whose GCD of
// every consecutive element is the given array
#include <bits/stdc++.h>
using namespace std;

// Return the LCM of two numbers.
int lcm(int a, int b)
{
    return (a * b) / __gcd(a, b);
}

// Print the required constructed array
void printArray(int a[], int n)
{
    // printing the first element.
    cout << a[0] << " ";

    // finding and printing the LCM of consecutive
    // element of given array.
    for (int i = 0; i < n - 1; i++)
        cout << lcm(a[i], a[i + 1]) << " ";

    // printing the last element of the given array.
    cout << a[n - 1] << endl;
}

// Driven Program
int main()
{
    int a[] = { 1, 2, 3 };
    int n = sizeof(a) / sizeof(a[0]);
    printArray(a, n);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program to construct an array whose
// GCD of every consecutive element is the
// given array

import java.io.*;

class GFG {

    // Recursive function to return gcd of
    // a and b
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

    // Return the LCM of two numbers.
    static int lcm(int a, int b)
    {
        return (a * b) / __gcd(a, b);
    }

    // Print the required constructed array
    static void printArray(int a[], int n)
    {

        // printing the first element.
        System.out.print( a[0] + " ");

        // finding and printing the LCM of
        // consecutive element of given array.
        for (int i = 0; i < n - 1; i++)
            System.out.print(lcm(a[i],
                            a[i + 1]) + " ");

        // printing the last element of the
        // given array.
        System.out.print(a[n - 1]);
    }

    // Driven Program
    public static void main (String[] args)
    {
        int a[] = { 1, 2, 3 };
        int n = a.length;
        printArray(a, n);
    }
}

// This code is contributed by anuj_67.
```

## **蟒蛇 3**

```
# Python Program to construct an array whose
# GCD of every consecutive element is the
# given array

# Recursive function to return gcd of
# a and b
def __gcd( a, b):

    # Everything divides 0
    if (a == 0 or b == 0):
        return 0

    # base case
    if (a == b):
        return a

    # a is greater
    if (a > b):
        return __gcd(a - b, b)        
    return __gcd(a, b - a)

# Return the LCM of two numbers.
def lcm(a, b):
    return (a * b) / __gcd(a, b)

# Print the required constructed array
def printArray(a, n):

    # printing the first element.
    print ( str(a[0]) + " ")

    # finding and printing the LCM of
    # consecutive element of given array.
    for i in range(0,n-1):
        print (str(lcm(a[i],a[i + 1])) + " ")

    # printing the last element of the
    # given array.
    print (a[n - 1])

# Driver code
a = [1, 2, 3 ]
n = len(a)
printArray(a, n)

# This code is contributed by Prateek Bajaj
```

## **C#**

```
// C# Program to construct an array whose
// GCD of every consecutive element is the
// given array
using System;
class GFG {

    // Recursive function to return
    // gcd of a and b
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

    // Return the LCM of two numbers.
    static int lcm(int a, int b)
    {
        return (a * b) / __gcd(a, b);
    }

    // Print the required constructed array
    static void printArray(int []a, int n)
    {

        // printing the first element.
        Console.Write( a[0] + " ");

        // finding and printing the LCM of
        // consecutive element of given array.
        for (int i = 0; i < n - 1; i++)
            Console.Write(lcm(a[i],
                  a[i + 1]) + " ");

        // printing the last element
        // of the given array.
        Console.Write(a[n - 1]);
    }

    // Driver Code
    public static void Main ()
    {
        int []a = {1, 2, 3};
        int n = a.Length;
        printArray(a, n);
    }
}

// This code is contributed by anuj_67.
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP Program to construct
// an array whose GCD of
// every consecutive element
// is the given array

// Recursive function to
// return gcd of a and b
function __gcd($a, $b)
{

    // Everything divides 0
    if($a == 0 or $b == 0)
        return 0 ;

    // base case
    if($a == $b)
        return $a ;

    // a is greater
    if($a > $b)
        return __gcd( $a - $b , $b ) ;

    return __gcd( $a , $b - $a ) ;
}

// Return the LCM of two numbers.
function lcm($a, $b)
{
    return ($a * $b) / __gcd($a, $b);
}

// Print the required constructed array
function printArray( $a, $n)
{

    // printing the first element.
    echo $a[0] , " ";

    // finding and printing
    // the LCM of consecutive
    // element of given array.
    for ( $i = 0; $i < $n - 1; $i++)
        echo lcm($a[$i], $a[$i + 1]) , " ";

    // printing the last element
    // of the given array.
    echo $a[$n - 1] ,"\n";
}

    // Driver Code
    $a = array(1, 2, 3);
    $n = count($a);
    printArray($a, $n);

// This code is contributed by anuj_67.
?>
```

## **java 描述语言**

```
<script>

// Javascript Program to construct an array whose GCD of
// every consecutive element is the given array

function __gcd(a, b)
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

// Return the LCM of two numbers.
function lcm(a, b)
{
    return (a * b) / __gcd(a, b);
}

// Print the required constructed array
function printArray(a, n)
{

    // printing the first element.
    document.write( a[0] + " ");

    // finding and printing the LCM of consecutive
    // element of given array.
    for (var i = 0; i < n - 1; i++)
        document.write( lcm(a[i], a[i + 1]) + " ");

    // printing the last element of the given array.
    document.write( a[n - 1] + "<br>");
}

// Driven Program
var a = [ 1, 2, 3 ];
var n = a.length;
printArray(a, n);

// This code is contributed by rrrtnx.
</script>
```

****输出**T2】**

```
1 2 6 3
```