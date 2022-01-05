# 类区间算术平均值程序

> 原文:[https://www . geesforgeks . org/program-class-interval-算术平均值/](https://www.geeksforgeeks.org/program-class-interval-arithmetic-mean/)

给定一个类间隔和频率分布，任务是找到算术平均值。在频率分布的情况下，原始数据按具有相应频率的间隔排列。因此，如果我们有兴趣找到具有类区间的数据的算术平均值，我们必须知道中间变量 x。这个变量可以通过使用区间的中点来计算。

> 设区间的下限为 lower_limit[] = {1，6，11，16，21}
> 区间的上限为 upper_limit[] = {5，10，15，20，25}
> 并给出频率 freq[] = {10，20，30，40，50}。
> 式中(x) =(下[i] +上[I])/2；
> 和平均值=(freq[0]* mid[0]+freq[1]* mid[1]+。。。+freq[n–1]* mid[n–1])/(freq[0]+freq[1]+。。。+freq[n-1])
> = 2450/150
> = 16.3333

示例:

```
Input : lower_limit[] = {1, 6, 11, 16, 21}
        upper_limit[] = {5, 10, 15, 20, 25}
        freq[] = {10, 20, 30, 40, 50}
Output : 16.3333

Input : lower_limit[] = {10, 20, 30, 40, 50}
        upper_limit[] = {19, 29, 39, 49, 59}
        freq[] = {15, 20, 30, 35, 40}
Output : 38.6429
```

## C++

```
// CPP program to find class interval
// arithmetic mean.
#include <bits/stdc++.h>
using namespace std;

// Function to find class interval arithmetic mean.
float mean(int lower_limit[], int upper_limit[],
                              int freq[], int n)
{
    float mid[n];
    float sum = 0, freqSum = 0;

    // calculate sum of frequency and sum of
    // multiplication of interval mid value
    // and frequency.
    for (int i = 0; i < n; i++) {
        mid[i] = (lower_limit[i] +
                  upper_limit[i]) / 2;
        sum = sum + mid[i] * freq[i];
        freqSum = freqSum + freq[i];
    }
    return sum / freqSum;
}

// Driver function
int main()
{
    int lower_limit[] = { 1, 6, 11, 16, 21 };
    int upper_limit[] = { 5, 10, 15, 20, 25 };
    int freq[] = { 10, 20, 30, 40, 50 };
    int n = sizeof(freq) / sizeof(freq[0]);
    cout << mean(lower_limit, upper_limit, freq, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find
// class interval
import java.io.*;

class GFG {

    // Function to find class
    // interval arithmetic mean.
    static float mean(int lower_limit[],
        int upper_limit[], int freq[], int n)
    {
        float mid[] = new float[n];
        float sum = 0, freqSum = 0;

        // calculate sum of frequency and sum of
        // multiplication of interval mid value
        // and frequency.
        for (int i = 0; i < n; i++) {

            mid[i] = (lower_limit[i] +
                    upper_limit[i]) / 2;

            sum = sum + mid[i] * freq[i];
            freqSum = freqSum + freq[i];
        }

        return sum / freqSum;
    }
    // Driver function
    public static void main (String[] args) {

    int lower_limit[] = { 1, 6, 11, 16, 21 };
    int upper_limit[] = { 5, 10, 15, 20, 25 };
    int freq[] = { 10, 20, 30, 40, 50 };
    int n = freq.length;

    mean(lower_limit, upper_limit, freq, n);
        System.out.println(mean(lower_limit,
                        upper_limit, freq, n));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 program to find class interval
# arithmetic mean.

# Function to find class interval
# arithmetic mean.
def mean(lower_limit, upper_limit, freq, n):

    mid = [0.0] * n
    sum = 0
    freqSum = 0

    # calculate sum of frequency and
    # sum of multiplication of interval
    # mid value and frequency.
    for i in range( 0, n):
        mid[i] = ((lower_limit[i] +
                  upper_limit[i]) / 2)

        sum = sum + mid[i] * freq[i]
        freqSum = freqSum + freq[i]

    return sum / freqSum

# Driver function
lower_limit = [ 1, 6, 11, 16, 21 ]
upper_limit = [ 5, 10, 15, 20, 25 ]
freq = [10, 20, 30, 40, 50]
n = len(freq)
print(round(mean(lower_limit, upper_limit,
                             freq, n), 4))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find
// class interval
using System;

class GFG {

    // Function to find class
    // interval arithmetic mean.
    static float mean(int []lower_limit,
        int []upper_limit, int []freq, int n)
    {
        float []mid = new float[n];
        float sum = 0, freqSum = 0;

        // calculate sum of frequency and sum of
        // multiplication of interval mid value
        // and frequency.
        for (int i = 0; i < n; i++) {

            mid[i] = (lower_limit[i] +
                    upper_limit[i]) / 2;

            sum = sum + mid[i] * freq[i];
            freqSum = freqSum + freq[i];
        }

        return sum / freqSum;
    }

    // Driver function
    public static void Main () {

        int []lower_limit = { 1, 6, 11, 16, 21 };
        int []upper_limit = { 5, 10, 15, 20, 25 };
        int []freq = { 10, 20, 30, 40, 50 };
        int n = freq.Length;

        mean(lower_limit, upper_limit, freq, n);
            Console.WriteLine(mean(lower_limit,
                            upper_limit, freq, n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find class interval
// arithmetic mean.

// Function to find class interval
// arithmetic mean.
function mean( $lower_limit, $upper_limit,
                                $freq, $n)
{
    $mid = array();
    $sum = 0; $freqSum = 0;

    // calculate sum of frequency and
    // sum of multiplication of interval
    // mid value and frequency.
    for ( $i = 0; $i <$n; $i++)
    {
        $mid[$i] = ($lower_limit[$i] +
                $upper_limit[$i]) / 2;
        $sum = $sum + $mid[$i] * $freq[$i];
        $freqSum = $freqSum + $freq[$i];
    }

    return $sum / $freqSum;
}

// Driver function
$lower_limit = array( 1, 6, 11, 16, 21 );
$upper_limit = array( 5, 10, 15, 20, 25 );
$freq = array( 10, 20, 30, 40, 50 );
$n = count($freq);

echo mean($lower_limit, $upper_limit,
                             $freq, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find
// class interval

    // Function to find class
    // interval arithmetic mean.
    function mean(lower_limit,
        upper_limit, freq, n)
    {
        let mid = [];
        let sum = 0, freqSum = 0;

        // calculate sum of frequency and sum of
        // multiplication of interval mid value
        // and frequency.
        for (let i = 0; i < n; i++) {

            mid[i] = (lower_limit[i] +
                    upper_limit[i]) / 2;

            sum = sum + mid[i] * freq[i];
            freqSum = freqSum + freq[i];
        }

        return sum / freqSum;
    }

// Driver Code

    let lower_limit = [ 1, 6, 11, 16, 21 ];
    let upper_limit = [ 5, 10, 15, 20, 25 ];
    let freq = [ 10, 20, 30, 40, 50 ];
    let n = freq.length;

    mean(lower_limit, upper_limit, freq, n);
        document.write(mean(lower_limit,
                        upper_limit, freq, n));

       // This code is contributed by chinmoy1997pal.
</script>
```

输出:

```
16.3333
```