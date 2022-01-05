# 可以用数组中的所有数字组成一个可被 3 整除的数

> 原文:[https://www . geeksforgeeks . org/使用数组中的所有数字进行 3 整除的可能性/](https://www.geeksforgeeks.org/possible-to-make-a-divisible-by-3-number-using-all-digits-in-an-array/)

给定一个整数数组，任务是找出是否有可能用这些数字的所有数字构造一个整数，使它能被 3 整除。如果可能，则打印“是”，否则打印“否”。
示例:

```
Input : arr[] = {40, 50, 90}
Output : Yes
We can construct a number which is
divisible by 3, for example 945000\. 
So the answer is Yes. 

Input : arr[] = {1, 4}
Output : No
The only possible numbers are 14 and 41,
but both of them are not divisible by 3, 
so the answer is No.
```

这个想法是基于这样一个事实，即[一个数可以被 3 整除，如果它的位数之和可以被 3 整除](https://www.geeksforgeeks.org/check-large-number-divisible-3-not/)。所以我们简单地求数组元素的和。如果总和能被 3 整除，我们的答案是肯定的，否则就是否定的

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find if it is possible
// to make a number divisible by 3 using
// all digits of given array
#include <bits/stdc++.h>
using namespace std;

bool isPossibleToMakeDivisible(int arr[], int n)
{
    // Find remainder of sum when divided by 3
    int remainder = 0;
    for (int i=0; i<n; i++)
       remainder = (remainder + arr[i]) % 3;

    // Return true if remainder is 0.
    return (remainder == 0);
}

// Driver code
int main()
{
    int arr[] = { 40, 50, 90 };
    int n = sizeof(arr) / sizeof(arr[0]);
    if (isPossibleToMakeDivisible(arr, n))
        printf("Yes\n");
    else
        printf("No\n");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if it is possible
// to make a number divisible by 3 using
// all digits of given array

import java.io.*;
import java.util.*;

class GFG
{
    public static boolean isPossibleToMakeDivisible(int arr[], int n)
    {
        // Find remainder of sum when divided by 3
        int remainder = 0;
        for (int i=0; i<n; i++)
            remainder = (remainder + arr[i]) % 3;

        // Return true if remainder is 0.
        return (remainder == 0);
    }

    public static void main (String[] args)
    {
        int arr[] = { 40, 50, 90 };
        int n = 3;
        if (isPossibleToMakeDivisible(arr, n))
            System.out.print("Yes\n");
        else
            System.out.print("No\n");
    }
}

// Code Contributed by Mohit Gupta_OMG <(0_o)>
```

## 蟒蛇 3

```
# Python program to find if it is possible
# to make a number divisible by 3 using
# all digits of given array

def isPossibleToMakeDivisible(arr, n):
    # Find remainder of sum when divided by 3
    remainder = 0
    for i in range (0, n):
        remainder = (remainder + arr[i]) % 3

    # Return true if remainder is 0.
    return (remainder == 0)

# main()

arr = [40, 50, 90 ];
n = 3
if (isPossibleToMakeDivisible(arr, n)):
    print("Yes")
else:
    print("No")

# Code Contributed by Mohit Gupta_OMG <(0_o)>
```

## C#

```
// C# program to find if it is possible
// to make a number divisible by 3 using
// all digits of given array
using System;

class GFG
{
    public static bool isPossibleToMakeDivisible(int []arr, int n)
    {
        // Find remainder of sum when divided by 3
        int remainder = 0;

        for (int i = 0; i < n; i++)
            remainder = (remainder + arr[i]) % 3;

        // Return true if remainder is 0.
        return (remainder == 0);
    }

    public static void Main ()
    {
        int []arr = { 40, 50, 90 };
        int n = 3;

        if (isPossibleToMakeDivisible(arr, n))
                        Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if it is possible
// to make a number divisible by 3 using
// all digits of given array

function isPossibleToMakeDivisible($arr, $n)
{

    // Find remainder of sum
    // when divided by 3
    $remainder = 0;
    for ($i = 0; $i < $n; $i++)
    $remainder = ($remainder + $arr[$i]) % 3;

    // Return true if remainder is 0.
    return ($remainder == 0);
}

// Driver code
$arr = array( 40, 50, 90 );
$n = sizeof($arr);
if (isPossibleToMakeDivisible($arr, $n))
    echo("Yes\n");
else
    echo("No\n");

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// javascript program to find if it is possible
// to make a number divisible by 3 using
// all digits of given array

function isPossibleToMakeDivisible(arr , n)
{
    // Find remainder of sum when divided by 3
    var remainder = 0;
    for (i=0; i<n; i++)
        remainder = (remainder + arr[i]) % 3;

    // Return true if remainder is 0.
    return (remainder == 0);
}

var arr = [ 40, 50, 90 ];
var n = 3;
if (isPossibleToMakeDivisible(arr, n))
    document.write("Yes\n");
else
    document.write("No\n");

// This code contributed by Princi Singh

</script>
```

**输出:**

```
Yes
```

时间复杂度:O(n)