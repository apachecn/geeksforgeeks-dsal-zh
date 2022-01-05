# 计算可被所有数组元素整除的范围内的数字

> 原文:[https://www . geesforgeks . org/count-可被所有数组元素整除的范围内数字/](https://www.geeksforgeeks.org/count-numbers-in-a-range-that-are-divisible-by-all-array-elements/)

给定 N 个数字和两个数字 L 和 R，任务是打印范围[L，R]内可被数组所有元素整除的数字的计数。
**例:**

> **输入:** a[] = {1，4，2]，L = 1，R = 10
> **输出:** 2
> 在范围[1，10]内，数字 4 和 8 可被所有数组元素整除。
> **输入:** a[] = {1，3，2]，L = 7，R = 11
> **输出:** 0

一种**简单的**方法是从 L 迭代到 R，并计算可被所有数组元素整除的数字。
**时间复杂度:** O((R-L) * N)
一种**高效的**方法是找到 N 个数的 [LCM，然后统计在[L，R]范围内可被 LCM 整除的个数。直到 R 都可以被 LCM 整除的数是 R/LCM。所以利用排除原理，计数将是(R/LCM)–((L–1)/LCM)。
以下是上述办法的实施情况。](https://www.geeksforgeeks.org/lcm-of-given-array-elements/) 

## C++

```
// C++ program to count numbers in a range
// that are divisible by all array elements
#include <bits/stdc++.h>
using namespace std;

// Function to find the lcm of array
int findLCM(int arr[], int n)
{
    int lcm = arr[0];

    // Iterate in the array
    for (int i = 1; i < n; i++) {

        // Find lcm
        lcm = (lcm * arr[i]) / __gcd(arr[i], lcm);
    }

    return lcm;
}

// Function to return the count of numbers
int countNumbers(int arr[], int n, int l, int r)
{

    // Function call to find the
    // LCM of N numbers
    int lcm = findLCM(arr, n);

    // Return the count of numbers
    int count = (r / lcm) - ((l - 1) / lcm);
}

// Driver Code
int main()
{
    int arr[] = { 1, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int l = 1, r = 10;

    cout << countNumbers(arr, n, l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count numbers in a range
// that are divisible by all array elements
class GFG
{

// Function to calculate gcd
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

// Function to find the lcm of array
static int findLCM(int arr[], int n)
{
    int lcm = arr[0];

    // Iterate in the array
    for (int i = 1; i < n; i++)
    {

        // Find lcm
        lcm = (lcm * arr[i]) / __gcd(arr[i], lcm);
    }

    return lcm;
}

// Function to return the count of numbers
static int countNumbers(int arr[], int n,
                        int l, int r)
{

    // Function call to find the
    // LCM of N numbers
    int lcm = findLCM(arr, n);

    // Return the count of numbers
    int count = (r / lcm) - ((l - 1) / lcm);

    return count;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 1, 4, 2 };
    int n = arr.length;
    int l = 1, r = 10;

    System.out.println(countNumbers(arr, n, l, r));
}
}

// This code is contributed by Mukul Singh
```

## 蟒蛇 3

```
# Python program to count numbers in
# a range that are divisible by all
# array elements
import math

# Function to find the lcm of array
def findLCM(arr, n):

    lcm = arr[0]

    # Iterate in the array
    for i in range(1, n - 1):

        # Find lcm
        lcm = (lcm * arr[i]) / math.gcd(arr[i], lcm)

    return lcm

# Function to return the count of numbers
def countNumbers(arr, n, l, r):

    # Function call to find the
    # LCM of N numbers
    lcm = int(findLCM(arr, n))

    # Return the count of numbers
    count = (r / lcm) - ((l - 1) / lcm)
    print(int(count))

# Driver Code
arr = [1, 4, 2]
n = len(arr)
l = 1
r = 10

countNumbers(arr, n, l, r)

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# program to count numbers in a range
// that are divisible by all array elements
using System;

class GFG
{

// Function to calculate gcd
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

// Function to find the lcm of array
static int findLCM(int []arr, int n)
{
    int lcm = arr[0];

    // Iterate in the array
    for (int i = 1; i < n; i++)
    {

        // Find lcm
        lcm = (lcm * arr[i]) / __gcd(arr[i], lcm);
    }

    return lcm;
}

// Function to return the count of numbers
static int countNumbers(int []arr, int n,
                        int l, int r)
{

    // Function call to find the
    // LCM of N numbers
    int lcm = findLCM(arr, n);

    // Return the count of numbers
    int count = (r / lcm) - ((l - 1) / lcm);

    return count;
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 4, 2 };
    int n = arr.Length;
    int l = 1, r = 10;

    Console.WriteLine(countNumbers(arr, n, l, r));
}
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count numbers in a range
// that are divisible by all array elements

// Function to calculate gcd
function __gcd($a, $b)
{

    // Everything divides 0
    if ($a == 0 || $b == 0)
        return 0;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return __gcd($a - $b, $b);

    return __gcd($a, $b - $a);
}

// Function to find the lcm of array
function findLCM($arr, $n)
{
    $lcm = $arr[0];

    // Iterate in the array
    for ($i = 1; $i < $n; $i++)
    {

        // Find lcm
        $lcm = ($lcm * $arr[$i]) /
                 __gcd($arr[$i], $lcm);
    }

    return $lcm;
}

// Function to return the count of numbers
function countNumbers($arr, $n, $l, $r)
{

    // Function call to find the
    // LCM of N numbers
    $lcm = findLCM($arr, $n);

    // Return the count of numbers
    $count = (int)($r / $lcm) -
             (int)(($l - 1) / $lcm);

    return $count;
}

// Driver Code
$arr = array(1, 4, 2);
$n = sizeof($arr);
$l = 1; $r = 10;
echo countNumbers($arr, $n, $l, $r);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to count numbers in a range
// that are divisible by all array elements   

// Function to calculate gcd
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

    // Function to find the lcm of array
    function findLCM(arr , n) {
        var lcm = arr[0];

        // Iterate in the array
        for (i = 1; i < n; i++) {

            // Find lcm
            lcm = parseInt((lcm * arr[i]) / __gcd(arr[i], lcm));
        }

        return lcm;
    }

    // Function to return the count of numbers
    function countNumbers(arr , n , l , r) {

        // Function call to find the
        // LCM of N numbers
        var lcm = findLCM(arr, n);

        // Return the count of numbers
        var count = parseInt((r / lcm) - ((l - 1) / lcm));

        return count;
    }

    // Driver Code

        var arr = [ 1, 4, 2 ];
        var n = arr.length;
        var l = 1, r = 10;

        document.write(countNumbers(arr, n, l, r));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
2
```