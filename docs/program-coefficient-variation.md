# 变异系数程序

> 原文:[https://www . geesforgeks . org/program-变异系数/](https://www.geeksforgeeks.org/program-coefficient-variation/)

给定一个 n 大小的数组，任务是找到[变异系数](https://en.wikipedia.org/wiki/Coefficient_of_variation)。变异系数是标准差和平均值的比值。变异系数的主要目的是通过测量概率或频率分布的总体数据的离散度，或通过确定物质样本数据的含量或质量，来寻找质量保证的研究。测量[标准偏差](https://www.geeksforgeeks.org/mathematics-mean-variance-and-standard-deviation/)与平均值之比的方法也称为相对标准偏差，通常缩写为 RSD。
**例:**

```
Input : arr[] = {60.25, 62.38, 65.32, 61.41, 63.23}
Output : 0.0307144

Input : arr[] = {15, 36, 53.67, 25.45, 67.8, 56, 78.09}
Output : 0.48177
```

**进场:**

```
Coefficient of Variation = **Standard deviation / mean** 
Example:
arr[] = {60.25, 62.38, 65.32, 61.41, 63.23}
mean = 62.518
Standard Deviation = 1.9202
Coefficient of Variation = Standard deviation / mean
                         = 1.9202 / 62.518
                         = 0.0307144
```

下面是上面公式的实现:

## C++

```
// Program to find coefficient of
// variation of given array.
#include <bits/stdc++.h>
using namespace std;

// Function to find mean of given array.
float mean(float arr[], int n)
{
    float sum = 0;
    for (int i = 0; i < n; i++)
        sum = sum + arr[i];
    return sum / n;
}

// Function to find standard deviation
// of given array.
float standardDeviation(float arr[], int n)
{
    float sum = 0;
    for (int i = 0; i < n; i++)
        sum = sum + (arr[i] - mean(arr, n)) *
                    (arr[i] - mean(arr, n));

    return sqrt(sum / (n - 1));
}

// Function to find coefficient of variation.
float coefficientOfVariation(float arr[], int n)
{
   return standardDeviation(arr, n) / mean(arr, n);
}

// Driver Program
int main()
{
    float arr[] = { 15, 36, 53.67, 25.45,
                    67.8, 56, 78.09 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << coefficientOfVariation(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java Program to find coefficient of
// variation of given array
import java.io.*;

class GFG {

    // Function to find mean of given array.
    static double mean(double arr[], int n)
    {
        double sum = 0;

        for (int i = 0; i < n; i++)
            sum = sum + arr[i];
        return sum / n;
    }

    // Function to find standard 
    // deviation of given array.
    static double standardDeviation(double arr[],
                                            int n)
    {
        double sum = 0;

        for (int i = 0; i < n; i++)
            sum = sum + (arr[i] - mean(arr, n)) *
                            (arr[i] - mean(arr, n));

        return Math.sqrt(sum / (n - 1));
    }

    // Function to find coefficient of variation.
    static double coefficientOfVariation(double arr[],
                                                int n)
    {
    return (standardDeviation(arr, n) / mean(arr, n));
    }

    // Driver Program
    public static void main (String[] args) {

    double arr[] = { 15, 36, 53.67, 25.45,
                              67.8, 56, 78.09 };
    int n = arr.length;

    System.out.println( coefficientOfVariation(arr, n));

    }
}

//This article is contributed by vt_m.
```

## 蟒蛇 3

```
# Program to find coefficient
# of variation of given array.
import math

# Function to find mean of
# given array.
def mean(arr, n):
    sum = 0

    for i in range(0, n):
        sum = sum + arr[i]
    return (sum / n)

# Function to find standard
# deviation of given array.
def standardDeviation(arr, n):
    sum = 0

    for i in range(0, n):
        sum = (sum + (arr[i] - mean(arr, n)) *
                      (arr[i] - mean(arr, n)))

    return math.sqrt(sum / (n - 1))

# Function to find coefficient
# of variation.
def coefficientOfVariation(arr, n):
    return (standardDeviation(arr, n) /
                          mean(arr, n))

# Driver Program
arr = [15, 36, 53.67, 25.45,
            67.8, 56, 78.09]
n = len(arr)

print(round(coefficientOfVariation(arr, n), 5))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
//C# Program to find coefficient of
// variation of given array
using System;

class GFG {

    // Function to find mean of given array.
    static float mean(double []arr, int n)
    {
        double sum = 0;

        for (int i = 0; i < n; i++)
            sum = sum + arr[i];
        return (float)sum / n;
    }

    // Function to find standard
    // deviation of given array.
    static float standardDeviation(double []arr,
                                            int n)
    {
        double sum = 0;

        for (int i = 0; i < n; i++)
            sum = sum + (arr[i] - mean(arr, n)) *
                        (arr[i] - mean(arr, n));

        return (float)Math.Sqrt(sum / (n - 1));
    }

    // Function to find coefficient of variation.
    static float coefficientOfVariation(double []arr,
                                                int n)
    {
        return(float) (standardDeviation(arr, n) / mean(arr, n));
    }

    // Driver Program
    public static void Main () {

    double []arr = { 15, 36, 53.67, 25.45,
                            67.8, 56, 78.09 };
    int n = arr.Length;

    Console.WriteLine( coefficientOfVariation(arr, n));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to find coefficient of
// variation of given array.

// Function to find mean
// of given array.
function mean($arr, $n)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum = $sum + $arr[$i];
    return $sum /$n;
}

// Function to find standard
// deviation of given array.
function standardDeviation($arr, $n)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum = $sum + ($arr[$i] -
                mean($arr, $n)) *
               ($arr[$i] - mean($arr, $n));

    return sqrt($sum / ($n - 1));
}

// Function to find coefficient of variation.
function coefficientOfVariation($arr, $n)
{
return standardDeviation($arr, $n) /
                    mean($arr, $n);
}

// Driver Code
$arr = array( 15, 36, 53.67, 25.45,
                  67.8, 56, 78.09 );
$n = count($arr);
echo coefficientOfVariation($arr, $n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

    // JavaScript Program to find coefficient of
    // variation of given array

    // Function to find mean of given array.
    function mean(arr, n)
    {
        let sum = 0;

        for (let i = 0; i < n; i++)
            sum = sum + arr[i];
        return sum / n;
    }

    // Function to find standard
    // deviation of given array.
    function standardDeviation(arr, n)
    {
        let sum = 0;

        for (let i = 0; i < n; i++)
            sum = sum + (arr[i] - mean(arr, n)) *
                        (arr[i] - mean(arr, n));

        return Math.sqrt(sum / (n - 1));
    }

    // Function to find coefficient of variation.
    function coefficientOfVariation(arr, n)
    {
        return (standardDeviation(arr, n) / mean(arr, n));
    }

    let arr = [ 15, 36, 53.67, 25.45, 67.8, 56, 78.09 ];
    let n = arr.length;

    document.write( coefficientOfVariation(arr, n).toFixed(5));

</script>
```

**输出:**

```
0.48177
```