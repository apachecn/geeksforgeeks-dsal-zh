# 转换数组，使数组的 GCD 变为 1

> 原文:[https://www . geesforgeks . org/convert-array-gcd-array-变成-1/](https://www.geeksforgeeks.org/convert-array-gcd-array-becomes-1/)

给定一个正元素数组和一个正整数 k，任务是将数组的 GCD 转换为 1。为了实现这一点，任何时候只允许进行一次操作，即选择数组中的任何元素并用数字 d 除，其中 d <= k.
**示例:**

> 输入:arr = {10，15，30}，k = 6
> 输出:是
> 将数组的所有元素除以 5，因为它是
> 所有元素的除数，也小于 k，即 6。
> 给出类似{2，3，6}的序列。现在，把
> 2 除以 2，3 除以 3，6 除以 2。然后，序列
> 变成{1，1，3}。现在，数组的 gcd 是 1。
> 输入:arr = {5，10，20}，k = 4
> 输出:No
> 这里，10 除以 2 的顺序变成
> {5，5，20}。然后，20 除以 2，再除以 2。
> 最后，序列变成{5，5，5}。要使
> 成为该序列的 gcd 1，将每个元素
> 除以 5。但是 5 > 4 所以这里不可能做成
> gcd 1。

**进场:**

*   如果存在一个大于 k 的正质数来划分数组的每个元素，那么答案是否定的
*   如果数组的 GCD 的最大质因数小于或等于 k，那么答案是肯定的。
*   首先，找到数组的 GCD，然后检查 GCD 是否存在大于 k 的质因数。
*   为此，计算 GCD 的最大质因数。

## C++

```
// C++ program to check if it is
// possible to convert the gcd of
// the array to 1 by applying the
// given operation
#include <bits/stdc++.h>
using namespace std;

// Function to get gcd of the array.
int getGcd(int* arr, int n)
{
    int gcd = arr[0];
    for (int i = 1; i < n; i++)
        gcd = __gcd(arr[i], gcd);

    return gcd;
}

// Function to check if it is possible.
bool convertGcd(int* arr, int n, int k)
{
    // Getting the gcd of array
    int gcd = getGcd(arr, n);

    // Initially taking max_prime factor is 1.
    int max_prime = 1;

    // find maximum of all the prime factors
    // till sqrt(gcd).
    for (int i = 2; i <= sqrt(gcd); i++) {
        while (gcd % i == 0) {
            gcd /= i;
            max_prime = max(max_prime, i);
        }
    }

    // either GCD is reduced to 1 or a prime factor
    // greater than sqrt(gcd)
    max_prime = max(max_prime, gcd);

    return (max_prime <= k);
}

// Drivers code
int main()
{
    int arr[] = { 10, 15, 30 };
    int k = 6;
    int n = sizeof(arr) / sizeof(arr[0]);

    if (convertGcd(arr, n, k) == true)
       cout << "Yes";
    else
       cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if it is
// possible to convert the gcd of
// the array to 1 by applying the
// given operation
import java.io.*;

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
            return __gcd(a-b, b);
        return __gcd(a, b-a);
    }

    // Function to get gcd of the array.
    static int getGcd(int arr[], int n)
    {
        int gcd = arr[0];
        for (int i = 1; i < n; i++)
            gcd = __gcd(arr[i], gcd);

        return gcd;
    }

    // Function to check if it is possible.
    static boolean convertGcd(int []arr,
                             int n, int k)
    {
        // Getting the gcd of array
        int gcd = getGcd(arr, n);

        // Initially taking max_prime
        // factor is 1.
        int max_prime = 1;

        // find maximum of all the prime
        // factors till sqrt(gcd).
        for (int i = 2; i <= Math.sqrt(gcd);
                                        i++)
        {
            while (gcd % i == 0) {
                gcd /= i;
                max_prime =
                     Math.max(max_prime, i);
            }
        }

        // either GCD is reduced to 1 or a
        // prime factor greater than sqrt(gcd)
        max_prime = Math.max(max_prime, gcd);

        return (max_prime <= k);
    }

    // Drivers code
    public static void main (String[] args)
    {
        int []arr = { 10, 15, 30 };
        int k = 6;
        int n = arr.length;

        if (convertGcd(arr, n, k) == true)
            System.out.println( "Yes");
        else
            System.out.println( "No");
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to check if it is
# possible to convert the gcd of
# the array to 1 by applying the
# given operation
from math import gcd as __gcd, sqrt

# Function to get gcd of the array.
def getGcd(arr, n):
    gcd = arr[0];
    for i in range(1, n, 1):
        gcd = __gcd(arr[i], gcd)

    return gcd

# Function to check if it is possible.
def convertGcd(arr, n, k):

    # Getting the gcd of array
    gcd = getGcd(arr, n)

    # Initially taking max_prime
    # factor is 1.
    max_prime = 1

    # find maximum of all the
    # prime factors till sqrt(gcd)
    p = int(sqrt(gcd)) + 1
    for i in range(2, p, 1):
        while (gcd % i == 0):
            gcd = int(gcd / i)
            max_prime = max(max_prime, i)

    # either GCD is reduced to 1 or a
    # prime factor greater than sqrt(gcd)
    max_prime = max(max_prime, gcd)

    return (max_prime <= k)

# Drivers code
if __name__ == '__main__':
    arr = [10, 15, 30]
    k = 6
    n = len(arr)

    if (convertGcd(arr, n, k) == True):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# program to check if it is
// possible to convert the gcd of
// the array to 1 by applying the
// given operation
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
            return __gcd(a-b, b);
        return __gcd(a, b-a);
    }

    // Function to get gcd of the array.
    static int getGcd(int []arr, int n)
    {
        int gcd = arr[0];
        for (int i = 1; i < n; i++)
            gcd = __gcd(arr[i], gcd);

        return gcd;
    }

    // Function to check if it is possible.
    static bool convertGcd(int []arr,
                            int n, int k)
    {
        // Getting the gcd of array
        int gcd = getGcd(arr, n);

        // Initially taking max_prime
        // factor is 1.
        int max_prime = 1;

        // find maximum of all the prime
        // factors till sqrt(gcd).
        for (int i = 2; i <= Math.Sqrt(gcd);
                                        i++)
        {
            while (gcd % i == 0) {
                gcd /= i;
                max_prime =
                    Math.Max(max_prime, i);
            }
        }

        // either GCD is reduced to 1 or a
        // prime factor greater than sqrt(gcd)
        max_prime = Math.Max(max_prime, gcd);

        return (max_prime <= k);
    }

    // Drivers code
    public static void Main ()
    {
        int []arr = { 10, 15, 30 };
        int k = 6;
        int n = arr.Length;

        if (convertGcd(arr, n, k) == true)
            Console.WriteLine( "Yes");
        else
            Console.WriteLine( "No");
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if it is
// possible to convert the gcd of
// the array to 1 by applying the
// given operation

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
        return __gcd($a - $b , $b) ;

    return __gcd( $a , $b - $a) ;
}

// Function to get gcd of the array.
function getGcd($arr, $n)
{
    $gcd = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $gcd = __gcd($arr[$i], $gcd);

    return $gcd;
}

// Function to check if it is possible.
function convertGcd( $arr, $n, $k)
{

    // Getting the gcd of array
    $gcd = getGcd($arr, $n);

    // Initially taking max_prime
    // factor is 1.
    $max_prime = 1;

    // find maximum of all the prime
    // factors till sqrt(gcd).
    for($i = 2; $i <= sqrt($gcd); $i++)
    {
        while ($gcd % $i == 0)
        {
            $gcd /= $i;
            $max_prime = max($max_prime, $i);
        }
    }

    // either GCD is reduced
    // to 1 or a prime factor
    // greater than sqrt(gcd)
    $max_prime = max($max_prime, $gcd);

    return ($max_prime <= $k);
}

    // Driver Code
    $arr = array(10, 15, 30);
    $k = 6;
    $n = count($arr);

    if (convertGcd($arr, $n, $k) == true)
        echo "Yes";
    else
        echo "No";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to check if it is
    // possible to convert the gcd of
    // the array to 1 by applying the
    // given operation

    // Recursive function to return
    // gcd of a and b
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
            return __gcd(a-b, b);
        return __gcd(a, b-a);
    }

    // Function to get gcd of the array.
    function getGcd(arr, n)
    {
        let gcd = arr[0];
        for (let i = 1; i < n; i++)
            gcd = __gcd(arr[i], gcd);

        return gcd;
    }

    // Function to check if it is possible.
    function convertGcd(arr, n, k)
    {
        // Getting the gcd of array
        let gcd = getGcd(arr, n);

        // Initially taking max_prime
        // factor is 1.
        let max_prime = 1;

        // find maximum of all the prime
        // factors till sqrt(gcd).
        for (let i = 2; i <= Math.sqrt(gcd); i++)
        {
            while (gcd % i == 0) {
                gcd = parseInt(gcd / i, 10);
                max_prime = Math.max(max_prime, i);
            }
        }

        // either GCD is reduced to 1 or a
        // prime factor greater than sqrt(gcd)
        max_prime = Math.max(max_prime, gcd);

        return (max_prime <= k);
    }

    let arr = [ 10, 15, 30 ];
    let k = 6;
    let n = arr.length;

    if (convertGcd(arr, n, k) == true)
      document.write("Yes");
    else
      document.write( "No");

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
Yes
```