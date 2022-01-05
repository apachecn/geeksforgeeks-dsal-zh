# 数组方差和标准差程序

> 原文:[https://www . geesforgeks . org/数组方差和标准差程序/](https://www.geeksforgeeks.org/program-for-variance-and-standard-deviation-of-an-array/)

给定一个数组，我们需要计算数组元素的方差和标准差。
**例:**

```
Input  : arr[] = [1, 2, 3, 4, 5]
Output : Variance = 2
         Standard Deviation = 1   

Input  : arr[] = [7, 7, 8, 8, 3]
Output : Variance = 3
         Standard Deviation = 1
```

我们已经讨论了寻找数组平均值的程序。

> 平均值是元素的平均值。
> **表示 arr【0】的**..n-1] = ∑(arr[i]) / n
> 其中 0 < = i < n
> 方差是平均值除以元素数的平方差之和。
> **方差**=∑(arr[I]–均值) <sup>2</sup> / n
> 标准差为方差的平方根
> **标准差** = √(方差)
> 详见[均值、方差和标准差](https://www.geeksforgeeks.org/mathematics-mean-variance-and-standard-deviation/)。

以下是上述方法的实现:

## C++

```
// CPP program to find variance
// and standard deviation of
// given array.
#include <bits/stdc++.h>
using namespace std;

// Function for calculating variance
int variance(int a[], int n)
{
    // Compute mean (average of elements)
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += a[i];
    double mean = (double)sum /
                  (double)n;

    // Compute sum squared
    // differences with mean.
    double sqDiff = 0;
    for (int i = 0; i < n; i++)
        sqDiff += (a[i] - mean) *
                  (a[i] - mean);
    return sqDiff / n;
}

double standardDeviation(int arr[],
                         int n)
{
    return sqrt(variance(arr, n));
}

// Driver Code
int main()
{
    int arr[] = {600, 470, 170, 430, 300};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Variance: "
         << variance(arr, n) << "\n";
    cout << "Standard Deviation: "
         << standardDeviation(arr, n) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find variance
// and standard deviation of
// given array.
import java.io.*;

class GFG
{

    // Function for calculating
    // variance
    static double variance(double a[],
                           int n)
    {
        // Compute mean (average
        // of elements)
        double sum = 0;

        for (int i = 0; i < n; i++)
            sum += a[i];
        double mean = (double)sum /
                      (double)n;

        // Compute sum squared
        // differences with mean.
        double sqDiff = 0;
        for (int i = 0; i < n; i++)
            sqDiff += (a[i] - mean) *
                      (a[i] - mean);

        return (double)sqDiff / n;
    }

    static double standardDeviation(double arr[],
                                    int n)
    {
        return Math.sqrt(variance(arr, n));
    }

    // Driver Code
    public static void main (String[] args)
    {

    double arr[] = {600, 470, 170, 430, 300};
    int n = arr.length;

    System.out.println( "Variance: " +
                         variance(arr, n));
    System.out.println ("Standard Deviation: " +
                         standardDeviation(arr, n));

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to find variance
# and standard deviation of
# given array.
import math

# Function for calculating variance
def variance(a, n):

    # Compute mean (average of
    # elements)
    sum = 0
    for i in range(0 ,n):
        sum += a[i]
    mean = sum /n

    # Compute sum squared
    # differences with mean.
    sqDiff = 0
    for i in range(0 ,n):
        sqDiff += ((a[i] - mean)
                * (a[i] - mean))
    return sqDiff / n

def standardDeviation(arr, n):

    return math.sqrt(variance(arr, n))

# Driver Code
arr = [600, 470, 170, 430, 300]
n = len(arr)
print("Variance: ", int(variance(arr, n)))
print("Standard Deviation: ",
      round(standardDeviation(arr, n), 3))

# This code is contributed by Smitha
```

## C#

```
// C# program to find variance and
// standard deviation of given array.
using System;

class GFG
{

    // Function for calculating
    // variance
    static float variance(double []a,
                          int n)
    {

        // Compute mean (average
        // of elements)
        double sum = 0;

        for (int i = 0; i < n; i++)
            sum += a[i];

        double mean = (double)sum /
                      (double)n;

        // Compute sum squared
        // differences with mean.
        double sqDiff = 0;

        for (int i = 0; i < n; i++)
            sqDiff += (a[i] - mean) *
                      (a[i] - mean);

        return (float)sqDiff / n;
    }

    static float standardDeviation(double []arr,
                                   int n)
    {
        return (float)Math.Sqrt(variance(arr, n));
    }

    // Driver Code
    public static void Main ()
    {

        double []arr = {600, 470, 170, 430, 300};
        int n = arr.Length;

        Console.WriteLine( "Variance: " +
                            variance(arr, n));

        Console.WriteLine ("Standard Deviation: " +
                            standardDeviation(arr, n));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find variance
// and standard deviation of
// given array.

// Function for calculating.
// variance
function variance( $a, $n)
{
    // Compute mean (average
    // of elements)
    $sum = 0;
    for ( $i = 0; $i < $n; $i++)
        $sum += $a[$i];
    $mean = $sum / $n;

    // Compute sum squared
    // differences with mean.
    $sqDiff = 0;
    for ( $i = 0; $i < $n; $i++)
        $sqDiff += ($a[$i] - $mean) *
                   ($a[$i] - $mean);
    return $sqDiff / $n;
}

function standardDeviation($arr, $n)
{
    return sqrt(variance($arr, $n));
}

// Driver Code
$arr = array(600, 470, 170, 430, 300);
$n = count($arr);
echo "Variance: " ,
      variance($arr, $n) , "\n";
echo"Standard Deviation: " ,
     standardDeviation($arr, $n) ,"\n";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find variance and
// standard deviation of given array.

    // Function for calculating
    // variance

    function variance(a,  n)
    {

        // Compute mean (average of elements)

        var sum = 0;

        for (var i = 0; i < n; i++){
            sum += a[i];
         }

        var mean = sum / n;

        // Compute sum squared
        // differences with mean.

        var sqDiff = 0;

        for (var i = 0; i < n; i++) {
            sqDiff += (a[i] - mean) * (a[i] - mean);
        }

        return sqDiff / n;
    }

    function standardDeviation(arr , n)
    {
        return Math.sqrt(variance(arr, n));
    }

    // Driver Code

        var arr = [600, 470, 170, 430, 300]
        var n = arr.length;

        document.write( "Variance: " + 
        variance(arr, n) + "<br>");

        document.write ("Standard Deviation: " +
        standardDeviation(arr, n).toFixed(3));

     </script>
```

**输出:**

```
Variance: 21704
Standard Deviation: 147.323
```

程序的时间复杂度为 **O(n)** 。
本文由 [**喜马拉雅冉冉**](https://auth.geeksforgeeks.org/profile.php?user=himanshu_300) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。