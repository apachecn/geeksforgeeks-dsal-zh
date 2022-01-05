# 一个数组中每一个可能对的和的异或

> 原文:[https://www . geesforgeks . org/xor-sum-every-pair-array/](https://www.geeksforgeeks.org/xor-sum-every-possible-pair-array/)

给定大小为 n 的数组 a，任务是生成具有大小为 N^2 的新序列 b，该序列具有数组 a 的每对的元素和，并找到所有形成的对的和的 xor 值。
注:这里(A[i]、A[i])、(A[i]、A[j])、(A[j]、A[i])都被认为是不同的对。

**示例:**

```
Input: arr = {1, 5, 6}
Output: 4
B[3*3] = { 1+1, 1+5, 1+6, 5+1, 5+5, 5+6, 6+1, 6+5, 6+6}
B[9] = { 2, 6, 7, 6, 10, 11, 7, 11, 12}
So, 2 ^ 6 ^ 7 ^ 6 ^ 10 ^ 11 ^ 7 ^ 6 ^ 11 ^ 12 = 4

Input :1, 2
Output :6
```

一种天真的方法是运行两个循环。考虑每一对，取它们的和，计算所有对和的异或值。
一种有效的**方法基于相同值的异或为 0 的事实。
像(a[i]、a[j])和(a[j]、a[i])这样的所有对将具有相同的和。所以，它们的异或值将为 0。只有像(a[i]，a[i])这样的配对才会给出不同的结果。所以，对给定数组的所有元素进行异或运算，然后乘以 2。**

## **C++**

```
// C++ program to find XOR of
// sum of every possible pairs
// in an array
#include <bits/stdc++.h>
using namespace std;

// Function to find XOR of sum
// of all pairs
int findXor(int arr[], int n)
{

    // Calculate xor of all the elements
    int xoR = 0;
    for (int i = 0; i < n; i++) {
        xoR = xoR ^ arr[i];
    }

    // Return twice of xor value
    return xoR * 2;
}

// Drivers code
int main()
{
    int arr[3] = { 1, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findXor(arr, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find XOR of
// sum of every possible pairs
// in an array
import java.io.*;

class GFG {

    // Function to find XOR of sum
    // of all pairs
    static int findXor(int arr[], int n)
    {

        // Calculate xor of all the
        // elements
        int xoR = 0;
        for (int i = 0; i < n; i++) {
            xoR = xoR ^ arr[i];
        }

        // Return twice of xor value
        return xoR * 2;
    }

    // Drivers code
    public static void main (String[] args)
    {
        int arr[] = { 1, 5, 6 };
        int n = arr.length;
        System.out.println( findXor(arr, n));
    }
}

// This code is contributed by anuj_67.
```

## **蟒蛇 3**

```
# Python3 program to find
# XOR of sum of every
# possible pairs in an array

# Function to find XOR
# of sum of all pairs
def findXor(arr,n):

    # Calculate xor of
    # all the elements
    xoR = 0;
    for i in range (0, n ) :
        xoR = xoR ^ arr[i]

    # Return twice of
    # xor value
    return xoR * 2

# Driver code
arr = [ 1, 5, 6 ]
n = len(arr)
print(findXor(arr, n))

# This code is contributed
# by ihritik

```

## **C#**

```
// C# program to find XOR of
// sum of every possible pairs
// in an array
using System;

class GFG {

    // Function to find XOR of sum
    // of all pairs
    static int findXor(int []arr, int n)
    {

        // Calculate xor of all the
        // elements
        int xoR = 0;
        for (int i = 0; i < n; i++) {
            xoR = xoR ^ arr[i];
        }

        // Return twice of xor value
        return xoR * 2;
    }

    // Drivers code
    public static void Main ()
    {
        int []arr = { 1, 5, 6 };
        int n = arr.Length;
        Console.WriteLine( findXor(arr, n));
    }
}

// This code is contributed by anuj_67.
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP program to find XOR
// of sum of every possible
// pairs in an array

// Function to find XOR
// of sum of all pairs
function findXor($arr, $n)
{

    // Calculate xor of
    // all the elements
    $xoR = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $xoR = $xoR ^ $arr[$i];
    }

    // Return twice
    // of xor value
    return $xoR * 2;
}

// Driver code
$arr = array(1, 5, 6);
$n = count($arr);

echo findXor($arr, $n);

// This code is contributed
// by anuj_67.
?>
```

## **java 描述语言**

```
<script>
// Javascript program to find XOR of
// sum of every possible pairs
// in an array

// Function to find XOR of sum
// of all pairs
function findXor(arr, n)
{

    // Calculate xor of all the elements
    let xoR = 0;
    for (let i = 0; i < n; i++) {
        xoR = xoR ^ arr[i];
    }

    // Return twice of xor value
    return xoR * 2;
}

// Drivers code
    let arr = [ 1, 5, 6 ];
    let n = arr.length;

    document.write(findXor(arr, n));

</script>
```

****Output:** 

```
4
```**