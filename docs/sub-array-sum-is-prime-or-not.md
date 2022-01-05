# 子阵和是否为素数

> 原文:[https://www . geesforgeks . org/sub array-sum-is-prime-or-not/](https://www.geeksforgeeks.org/sub-array-sum-is-prime-or-not/)

给定一个数组和界限(下限和上限)，检查给定界限内的子数组之和是否为质数

**例:**

```
Input  :  a[] = {1, 2, 3, 5, 5, 4, 7, 8, 9};
          lower = 3, upper = 6
Output :  Yes
Explanation:- subarray is {3, 5, 5, 4} and 
sum of subarray 3+5+5+4 = 17 which is prime, so
the output is yes  

Input  :  a[] = {1, 6, 4, 5, 5, 4, 7, 8, 9};
          lower = 2, upper = 5
Output :  No
Explanation:- subarray is {6, 4, 5, 5} and sum
of subarray 6+4+5+5 = 20 which is Not prime so the
output is No  
```

1.  Use the upper and lower limits first.
2.  Calculate the sum of subarrays, and then check whether the sum is a prime number.
3.  If it is a prime number, it returns true, otherwise it returns false.

让我们使用下面的代码来理解这种方法。

## c++

```
// A C++ program to check the given
// subarray is prime or not
#include <iostream>
using namespace std;

// function to check the array
bool isPrime(int a[], int lower,
             int upper)
{
    int n = 0;

    // Calculate the sum of
    // the subarray
    for (int i = lower - 1;
         i <= upper - 1;
         i++)
        n += a[i];

    // check the sum of the
    // subarray is prime or
    // not (Corner case)
    if (n <= 1)
        return false;

    // Check from 2 to n - 1
    for (int i = 2; i < n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Driver Code
int main()
{
    // taking input
    int a[] = { 1, 2, 3, 5, 5,
                4, 7, 8, 9 };
    int lower = 3, upper = 6;
    if (isPrime(a, lower, upper))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}
```

## Java

```
// A java program to check the given
// subarray is prime or not
import java.io.*;

public class GFG {

    // function to check the array
    static boolean isPrime(int a[],
                           int lower,
                           int upper)
    {
        int n = 0;

        // Calculate the sum of
        // the subarray
        for (int i = lower - 1;
             i <= upper - 1; i++)
            n += a[i];

        // check the sum of the
        // subarray is prime or
        // not (Corner case)
        if (n <= 1)
            return false;

        // Check from 2 to n-1
        for (int i = 2; i < n; i++)
            if (n % i == 0)
                return false;

        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        // taking input
        int a[] = { 1, 2, 3, 5, 5, 4, 7, 8, 9 };
        int lower = 3, upper = 6;

        if (isPrime(a, lower, upper))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Sam007.
```

## python 3

T2

## c#

T21

```
// A C# program to check the given
// subarray is prime or not
using System;

class GFG {
    // function to check the array
    static bool isPrime(int[] a,
                        int lower,
                        int upper)
    {
        int n = 0;

        // Calculate the sum of
        // the subarray
        for (int i = lower - 1;
             i <= upper - 1;
             i++)
            n += a[i];

        // check the sum of the
        // subarray is prime or
        // not (Corner case)
        if (n <= 1)
            return false;

        // Check from 2 to n-1
        for (int i = 2; i < n; i++)
            if (n % i == 0)
                return false;

        return true;
    }

    // Driver Code
    public static void Main()
    {
        // taking input
        int[] a = { 1, 2, 3, 5, 5,
                    4, 7, 8, 9 };
        int lower = 3, upper = 6;
        if (isPrime(a, lower, upper))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by Sam007
```

## PHP

```
<?php
// A PHP program to check the given
// subarray is prime or not

// function to check the array
function isPrime($a, $lower, $upper)
{
    $n = 0;

    // Calculate the sum of
    // the subarray
    for ($i = $lower - 1;
            $i <= $upper - 1; $i++)
        $n += $a[$i];

    // check the sum of the
    // subarray is prime or
    // not (Corner case)
    if ($n <= 1)
        return false;

    // Check from 2 to n - 1
    for ($i = 2; $i < $n; $i++)
        if ($n % $i == 0)
            return false;

    return true;
}

    // Driver Code

    // taking input
    $a = array(1, 2, 3, 5, 5,
                  4, 7, 8, 9);
    $lower = 3; $upper = 6;
    if (isPrime($a, $lower, $upper))
        echo "Yes", " \n";
    else
        echo "No", " \n";

// This code is contributed by ajit
?>
```

## Javascript

```
<script>

// A Javascript program to check the given
// subarray is prime or not

// Function to check the array
function isPrime(a, lower, upper)
{
    let n = 0;

    // Calculate the sum of
    // the subarray
    for(let i = lower - 1;
            i <= upper - 1; i++)
        n += a[i];

    // Check the sum of the
    // subarray is prime or
    // not (Corner case)
    if (n <= 1)
        return false;

    // Check from 2 to n-1
    for(let i = 2; i < n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Driver code

// Taking input
let a = [ 1, 2, 3, 5, 5, 4, 7, 8, 9 ];
let lower = 3, upper = 6;

if (isPrime(a, lower, upper))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rameshtravel07

</script>
```

**输出:**

```
Yes
```