# 实现分组数据标准差的程序

> 原文:[https://www . geesforgeks . org/program-implement-标准差-分组-data/](https://www.geeksforgeeks.org/program-implement-standard-deviation-grouped-data/)

给定一个类间隔和类频率，任务是找出分组数据的标准差。
求标准差的公式

> 标准差=√((∑(F x M<sup>2</sup>–n xμ<sup>2</sup>)/(n-1))
> 其中，
> **F**–类的频率。
> **M**–班级区间的中间值。
> **μ**–分组数据的平均值。
> **n**–频率之和。

示例:

```
Input : lower_limit[] = {50, 61, 71, 86, 96}
        upper_limit[] = {60, 70, 85, 95, 100}
        freq[] = {9, 7, 9, 12, 8}
Output : 15.757
Explanation : 
Standard deviation = sqrt(287127.75 - 45 * 
             78.3444 * 78.3444) / (45 - 1)
           = 15.757

Input : lower_limit[] = {37, 47, 57, 67}
        upper_limit[] = {46, 56, 66, 76}
        freq[] = {19, 23, 27, 28}
Output : 10.9817
```

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP Program to implement standard
// deviation of grouped data.
#include <bits/stdc++.h>
using namespace std;

// Function to find mean of grouped data.
float mean(float mid[], int freq[], int n)
{
    float sum = 0, freqSum = 0;
    for (int i = 0; i < n; i++) {
        sum = sum + mid[i] * freq[i];
        freqSum = freqSum + freq[i];
    }
    return sum / freqSum;
}

// Function to find standard
// deviation of grouped data.
float groupedSD(float lower_limit[],
                float upper_limit[],
                int freq[], int n)
{
    float mid[n], sum = 0, freqSum = 0, sd;
    for (int i = 0; i < n; i++) {
        mid[i] = (lower_limit[i] + upper_limit[i]) / 2;
        sum = sum + freq[i] * mid[i] * mid[i];
        freqSum = freqSum + freq[i];
    }

    // Formula to find standard deviation
    // of grouped data.
    sd = sqrt((sum - freqSum * mean(mid, freq, n) *
              mean(mid, freq, n)) / (freqSum - 1));
    return sd;
}

// Driver function.
int main()
{
    // Declare and initialize
    // the lower limit of interval.
    float lower_limit[] = { 50, 61, 71, 86, 96 };

    // Declare and initialize
    // the upper limit of interval.
    float upper_limit[] = { 60, 70, 85, 95, 100 };
    int freq[] = { 9, 7, 9, 12, 8 };

    // Calculating the size of array.
    int n = sizeof(lower_limit) / sizeof(lower_limit[0]);

    cout << groupedSD(lower_limit, upper_limit, freq, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// standard deviation of grouped data.
import java.io.*;

class GFG {

    // Function to find mean of grouped data.
    static float mean(float mid[], int freq[], int n)
    {
        float sum = 0, freqSum = 0;
        for (int i = 0; i < n; i++)
        {
            sum = sum + mid[i] * freq[i];
            freqSum = freqSum + freq[i];
        }
        return sum / freqSum;
    }

    // Function to find standard
    // deviation of grouped data.
    static float groupedSD(float lower_limit[],
                          float upper_limit[],
                            int freq[], int n)
    {
        float mid[] = new float[n];
        float sum = 0, freqSum = 0, sd;
        for (int i = 0; i < n; i++)
        {
            mid[i] = (lower_limit[i] + upper_limit[i]) / 2;
            sum = sum + freq[i] * mid[i] * mid[i];
            freqSum = freqSum + freq[i];
        }

        // Formula to find standard deviation
        // deviation of grouped data.
        sd = (float)Math.sqrt((sum - freqSum * mean(mid, freq, n) *
                        mean(mid, freq, n)) / (freqSum - 1));
        return sd;
    }

    // Driver function.
    public static void main (String[] args)
    {
        // Declare and initialize
        // the lower limit of interval.
        float lower_limit[] = { 50, 61, 71, 86, 96 };

        // Declare and initialize
        // the upper limit of interval.
        float upper_limit[] = { 60, 70, 85, 95, 100 };
        int freq[] = { 9, 7, 9, 12, 8 };

        // Calculating the size of array.
        int n = lower_limit.length;

        System.out.println( groupedSD(lower_limit,
                            upper_limit, freq, n));

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python Program to implement standard
# deviation of grouped data.

import math

# Function to find mean of grouped data.
def mean( mid, freq, n):

    sum = 0
    freqSum = 0
    for i in range(0,n):
        sum = sum + mid[i] * freq[i]
        freqSum = freqSum + freq[i]

    return sum / freqSum

# Function to find standard
# deviation of grouped data.
def groupedSD(lower_limit, upper_limit ,freq , n):

    mid=[[0] for i in range(0,n)]
    sum = 0
    freqSum = 0
    sd=0
    for i in range(0,n):
        mid[i] = (lower_limit[i] + upper_limit[i]) / 2
        sum = sum + freq[i] * mid[i] * mid[i]
        freqSum = freqSum + freq[i]

    # Formula to find standard deviation
    # of grouped data.
    sd = math.sqrt((sum - freqSum * mean(mid, freq, n)* mean(mid, freq, n)) / (freqSum - 1))
    return sd

#  driver code
# Declare and initialize
# the lower limit of interval.
lower_limit= [ 50, 61, 71, 86, 96 ]

# Declare and initialize
# the upper limit of interval.
upper_limit= [ 60, 70, 85, 95, 100 ]
freq =[ 9, 7, 9, 12, 8 ]

# Calculating the size of array.
n = len(lower_limit)

print(groupedSD(lower_limit, upper_limit, freq, n))

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to implement
// standard deviation of grouped data.
using System;

class GFG {

    // Function to find mean of grouped data.
    static float mean(float []mid, int []freq,
                                       int n)
    {
        float sum = 0, freqSum = 0;
        for (int i = 0; i < n; i++)
        {
            sum = sum + mid[i] * freq[i];
            freqSum = freqSum + freq[i];
        }
        return sum / freqSum;
    }

    // Function to find standard
    // deviation of grouped data.
    static float groupedSD(float []lower_limit,
                           float []upper_limit,
                            int []freq, int n)
    {
        float []mid = new float[n];
        float sum = 0, freqSum = 0, sd;

        for (int i = 0; i < n; i++)
        {
            mid[i] = (lower_limit[i] + upper_limit[i]) / 2;

            sum = sum + freq[i] * mid[i] * mid[i];

            freqSum = freqSum + freq[i];
        }

        // Formula to find standard deviation
        // deviation of grouped data.
        sd = (float)Math.Sqrt((sum - freqSum * mean(mid,
             freq, n) * mean(mid, freq, n)) / (freqSum - 1));

        return sd;
    }

    // Driver function.
    public static void Main ()
    {
        // Declare and initialize
        // the lower limit of interval.
        float []lower_limit = { 50, 61, 71, 86, 96 };

        // Declare and initialize
        // the upper limit of interval.
        float []upper_limit = { 60, 70, 85, 95, 100 };
        int []freq = { 9, 7, 9, 12, 8 };

        // Calculating the size of array.
        int n = lower_limit.Length;

        Console.WriteLine(groupedSD(lower_limit,
                         upper_limit, freq, n));

    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to implement standard
// deviation of grouped data.

// Function to find mean of grouped data.
function mean($mid, $freq, $n)
{
    $sum = 0; $freqSum = 0;
    for ( $i = 0; $i <$n; $i++)
    {
        $sum = $sum + $mid[$i] *
                       $freq[$i];
        $freqSum = $freqSum + $freq[$i];
    }
    return $sum / $freqSum;
}

// Function to find standard
// deviation of grouped data.
function groupedSD($lower_limit,
                   $upper_limit,
                      $freq, $n)
{
    $mid=array(); $sum = 0;
    $freqSum = 0; $sd;
    for ( $i = 0; $i < $n; $i++)
    {
        $mid[$i] = ($lower_limit[$i] +
                    $upper_limit[$i]) / 2;
        $sum = $sum + $freq[$i] *
               $mid[$i] * $mid[$i];
        $freqSum = $freqSum + $freq[$i];
    }

    // Formula to find standard deviation
    // of grouped data.
    $sd = sqrt(($sum - $freqSum *
          mean($mid, $freq, $n) *
          mean($mid, $freq, $n)) /
                   ($freqSum - 1));
    return $sd;
}

    // Driver Code
    // Declare and initialize
    // the lower limit of interval.
    $lower_limit = array(50, 61, 71, 86, 96);

    // Declare and initialize
    // the upper limit of interval.
    $upper_limit = array(60, 70, 85, 95, 100);
    $freq = array( 9, 7, 9, 12, 8 );

    // Calculating the size of array.
    $n = count($lower_limit);

    echo groupedSD($lower_limit, $upper_limit,
                                   $freq, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript  program to implement
// standard deviation of grouped data.

    // Function to find mean of grouped data.
    function mean(mid, freq, n)
    {
        let sum = 0, freqSum = 0;
        for (let i = 0; i < n; i++)
        {
            sum = sum + mid[i] * freq[i];
            freqSum = freqSum + freq[i];
        }
        return sum / freqSum;
    }

    // Function to find standard
    // deviation of grouped data.
    function groupedSD(lower_limit,
                          upper_limit,
                            freq, n)
    {
        let mid = [];
        let sum = 0, freqSum = 0, sd;
        for (let i = 0; i < n; i++)
        {
            mid[i] = (lower_limit[i] + upper_limit[i]) / 2;
            sum = sum + freq[i] * mid[i] * mid[i];
            freqSum = freqSum + freq[i];
        }

        // Formula to find standard deviation
        // deviation of grouped data.
        sd = Math.sqrt((sum - freqSum * mean(mid, freq, n) *
                        mean(mid, freq, n)) / (freqSum - 1));
        return sd;
    }

// Driver code

        // Declare and initialize
        // the lower limit of interval.
        let lower_limit = [50, 61, 71, 86, 96];

        // Declare and initialize
        // the upper limit of interval.
        let upper_limit = [ 60, 70, 85, 95, 100 ];
        let freq = [ 9, 7, 9, 12, 8];

        // Calculating the size of array.
        let n = lower_limit.length;

        document.write( groupedSD(lower_limit,
                            upper_limit, freq, n));

</script>
```

**Output:** 

```
15.757
```