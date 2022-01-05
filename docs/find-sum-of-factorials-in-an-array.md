# 求数组中阶乘的和

> 原文:[https://www . geeksforgeeks . org/find-数组中的因子和/](https://www.geeksforgeeks.org/find-sum-of-factorials-in-an-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** 。任务是找出数组中每个元素的阶乘之和。

**示例:**

> **输入:** arr[] = {7，3，5，4，8 }
> T3】输出: 45510
> 7！+ 3!+ 5!+ 4!+ 8!= 5040 + 6 + 120 + 24 + 40320 = 45510
> 
> **输入:** arr[] = {2，1，3 }
> T3】输出: 9

**方法:**实现一个函数**阶乘(n)** ，该函数找到 **n** 的阶乘，并初始化 **sum = 0** 。现在，遍历给定的数组，对于每个元素 **arr[i]** 更新 **sum = sum +阶乘(arr[i])** 。最后打印计算出的**和**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
#include <bits/stdc++.h>
using namespace std;

// Function to return the factorial of n
int factorial(int n)
{
    int f = 1;
    for (int i = 1; i <= n; i++)
    {
        f *= i;
    }
    return f;
}

// Function to return the sum of
// factorials of the array elements
int sumFactorial(int *arr, int n)
{

    // To store the required sum
    int s = 0,i;
    for (i = 0; i < n; i++)
    {

        // Add factorial of all the elements
        s += factorial(arr[i]);
    }
    return s;
}

// Driver code
int main()
{
    int arr[] = { 7, 3, 5, 4, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << sumFactorial(arr, n);
    return 0;
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the factorial of n
    static int factorial(int n)
    {
        int f = 1;
        for (int i = 1; i <= n; i++) {
            f *= i;
        }
        return f;
    }

    // Function to return the sum of
    // factorials of the array elements
    static int sumFactorial(int[] arr, int n)
    {

        // To store the required sum
        int s = 0;
        for (int i = 0; i < n; i++) {

            // Add factorial of all the elements
            s += factorial(arr[i]);
        }
        return s;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 7, 3, 5, 4, 8 };
        int n = arr.length;
        System.out.println(sumFactorial(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the factorial of n
def factorial(n):
    f = 1;
    for i in range(1, n + 1):
        f *= i;
    return f;

# Function to return the sum of
# factorials of the array elements
def sumFactorial(arr, n):

    # To store the required sum
    s = 0;
    for i in range(0,n):

        # Add factorial of all the elements
        s += factorial(arr[i]);
    return s;

# Driver code
arr = [7, 3, 5, 4, 8 ];
n = len(arr);
print(sumFactorial(arr, n));

# This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the factorial of n
    static int factorial(int n)
    {
        int f = 1;
        for (int i = 1; i <= n; i++)
        {
            f *= i;
        }
        return f;
    }

    // Function to return the sum of
    // factorials of the array elements
    static int sumFactorial(int[] arr, int n)
    {

        // To store the required sum
        int s = 0;
        for (int i = 0; i < n; i++)
        {

            // Add factorial of all the elements
            s += factorial(arr[i]);
        }
        return s;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 7, 3, 5, 4, 8 };
        int n = arr.Length;
        Console.WriteLine(sumFactorial(arr, n));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP implementation of the approach

// Function to return the factorial of n
function factorial( $n)
{
    $f = 1;
    for ( $i = 1; $i <= $n; $i++)
    {
        $f *=$i;
    }
    return $f;
}

// Function to return the sum of
// factorials of the array elements
function sumFactorial($arr,  $n)
{

    // To store the required sum
    $s = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // Add factorial of all the elements
        $s += factorial($arr[$i]);
    }
    return $s;
}

// Driver code

$arr = array( 7, 3, 5, 4, 8 );
$n = sizeof($arr);
echo sumFactorial($arr, $n);

// This code is contributed by ihritik

?>

```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the factorial of n
function factorial(n)
{
    let f = 1;
    for(let i = 1; i <= n; i++)
    {
        f *= i;
    }
    return f;
}

// Function to return the sum of
// factorials of the array elements
function sumFactorial(arr, n)
{

    // To store the required sum
    let s = 0;
    for (let i = 0; i < n; i++)
    {

        // Add factorial of all the elements
        s += factorial(arr[i]);
    }
    return s;
}

// Driver code
let arr = [ 7, 3, 5, 4, 8 ];
let n = arr.length;

document.write(sumFactorial(arr, n));

// This code is contributed by bobby

</script>
```

**Output:** 

```
45510
```