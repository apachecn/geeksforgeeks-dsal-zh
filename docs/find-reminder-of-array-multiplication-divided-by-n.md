# 求数组乘法除以 n 的余数

> 原文:[https://www . geesforgeks . org/find-数组提醒-乘法-n 分频/](https://www.geeksforgeeks.org/find-reminder-of-array-multiplication-divided-by-n/)

给定多个数字和一个数字 n，任务是将所有数字相乘后的余数除以 n.
**示例:**

```
Input : arr[] = {100, 10, 5, 25, 35, 14}, 
            n = 11
Output : 9
100 x 10 x 5 x 25 x 35 x 14 = 61250000 % 11 = 9

Input : arr[] = {100, 10}, 
            n = 5 
Output : 0
100 x 10 = 1000 % 5 = 0
```

**天真的方法:**首先乘以所有的数，然后取%乘 n，然后求余数，但是在这种方法中，如果数是 2^64 的最大值，那么它给出错误的答案。
**避免溢出的方法:**首先取一个余数或像 arr[i] % n 这样的单个数，然后将余数与当前结果相乘。乘法后，再次取余数，避免溢出。这是因为模运算的分布特性。(a * b) % c = ( ( a % c ) * ( b % c ) ) % c

## C++

```
// C++ program to find
// remainder when all
// array elements are
// multiplied.
#include <iostream>
using namespace std;

// Find remainder of arr[0] * arr[1] *
// .. * arr[n-1]
int findremainder(int arr[], int len, int n)
{
    int mul = 1;

    // find the individual remainder
    // and multiple with mul.
    for (int i = 0; i < len; i++)
        mul = (mul * (arr[i] % n)) % n;

    return mul % n;
}

// Driver code
int main()
{
    int arr[] = { 100, 10, 5, 25, 35, 14 };
    int len = sizeof(arr) / sizeof(arr[0]);
    int n = 11;

    // print the remainder of after
    // multiple all the numbers
    cout << findremainder(arr, len, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// remainder when all
// array elements are
// multiplied.
import java.util.*;
import java.lang.*;

public class GfG{

    // Find remainder of arr[0] * arr[1] *
    // .. * arr[n-1]
    public static int findremainder(int arr[],
                                   int len, int n)
    {
        int mul = 1;

        // find the individual remainder
        // and multiple with mul.
        for (int i = 0; i < len; i++)
            mul = (mul * (arr[i] % n)) % n;

        return mul % n;
    }

    // Driver function
    public static void main(String argc[])
    {
        int[] arr = new int []{ 100, 10, 5,
                                25, 35, 14 };
        int len = 6;
        int n = 11;

        // print the remainder of after
        // multiple all the numbers
        System.out.println(findremainder(arr, len, n));
    }
}

/* This code is contributed by Sagar Shukla */
```

## 蟒蛇 3

```
# Python3 program to
# find remainder when
# all array elements
# are multiplied.

# Find remainder of arr[0] * arr[1]
# * .. * arr[n-1]
def findremainder(arr, lens, n):
    mul = 1

    # find the individual
    # remainder and
    # multiple with mul.
    for i in range(lens):
        mul = (mul * (arr[i] % n)) % n

    return mul % n

# Driven code
arr = [ 100, 10, 5, 25, 35, 14 ]
lens = len(arr)
n = 11

# print the remainder
# of after multiple
# all the numbers
print( findremainder(arr, lens, n))

# This code is contributed by "rishabh_jain".
```

## C#

```
// C# program to find
// remainder when all
// array elements are
// multiplied.
using System;

public class GfG{

    // Find remainder of arr[0] * arr[1] *
    // .. * arr[n-1]
    public static int findremainder(int []arr,
                                int len, int n)
    {
        int mul = 1;

        // find the individual remainder
        // and multiple with mul.
        for (int i = 0; i < len; i++)
            mul = (mul * (arr[i] % n)) % n;

        return mul % n;
    }

    // Driver function
    public static void Main()
    {
        int[] arr = new int []{ 100, 10, 5,
                                25, 35, 14 };
        int len = 6;
        int n = 11;

        // print the remainder of after
        // multiple all the numbers
        Console.WriteLine(findremainder(arr, len, n));
    }
}

/* This code is contributed by vt_m */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// remainder when all
// array elements are
// multiplied.

// Find remainder of arr[0] * arr[1] *
// .. * arr[n-1]
function findremainder($arr, $len, $n)
{
    $mul = 1;

    // find the individual remainder
    // and multiple with mul.
    for ($i = 0; $i < $len; $i++)
        $mul = ($mul * ($arr[$i] % $n)) % $n;

    return $mul % $n;
}

// Driver code
$arr = array(100, 10, 5, 25, 35, 14);
$len = sizeof($arr);
$n = 11;

// print the remainder of after
// multiple all the numbers
echo(findremainder($arr, $len, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find
    // remainder when all
    // array elements are
    // multiplied.

    // Find remainder of arr[0] * arr[1] *
    // .. * arr[n-1]
    function findremainder(arr, len, n)
    {
        let mul = 1;

        // find the individual remainder
        // and multiple with mul.
        for (let i = 0; i < len; i++)
            mul = (mul * (arr[i] % n)) % n;

        return mul % n;
    }

    let arr = [ 100, 10, 5, 25, 35, 14 ];
    let len = 6;
    let n = 11;

    // print the remainder of after
    // multiple all the numbers
    document.write(findremainder(arr, len, n));

// This code is contributed by rameshtravel07.
</script>
```

输出:

```
9
```