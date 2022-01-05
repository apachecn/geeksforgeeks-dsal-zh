# 求给定阵列中子阵列平均值

> 原文:[https://www . geesforgeks . org/find-mean-subarray-mean-given-array/](https://www.geeksforgeeks.org/find-mean-subarray-means-given-array/)

给你一个 n 元素的数组，你必须找到数组的平均值，作为所有可能的 m 长度数组的所有连续 m 元素的平均值。
示例:

```
Input :arr[] = {3, 5, 1, 8, 9, 4}, 
           m = 4 
Output : Mean = 5.16667
Explanation : {3, 5, 1, 8}, {5, 1, 8, 9}, 
{1, 8, 9, 4} are three set of m-consecu-
tive elements. Mean of mean of sets 
is (17/4 + 23/4 + 22/4 )/ 3

Input : arr[] = {9, 4}, m = 1
Output : Mean = 6.5
Explanation : {9}, {4} are two set of
1-consecutive element. Mean of means 
of sets is (9 + 4 )/ 2
```

一个**简单的解决方案**是考虑所有 m 大小的子阵，计算它们的均值。最后返回均值的均值。
一个**有效的解决方案**是使用[滑动窗口算法](https://www.geeksforgeeks.org/window-sliding-technique/)来解决这个问题，在这个问题中，我们找到 m 长度窗口的和，然后将每个窗口的平均值加到一个值和上。最后，我们将通过将总和除以可能的窗口数得到我们的结果，这也是总和/(n-m+1)。

## C++

```
// CPP program to find mean of means
#include <bits/stdc++.h>
using namespace std;

// function to find mean value
float findMean(int arr[], int n, int m)
{
    // declare sum and winSum (window sum)
    float sum = 0, winSum = 0;
    int i = 0;

    // find sum for 1st m-length window
    for (; i < m; i++)
        winSum += arr[i];
    sum += (winSum / m);

    // iterate over array to find sum
    // of all m-length means
    for (; i < n; i++) {
        winSum = winSum - arr[i - m] + arr[i];
        sum += (winSum / m);
    }

    // mean of means will be sum of means
    // divided by no of such means
    return (sum / (n - m + 1));
}

// Driver code
int main()
{
    int arr[] = { 2, 5, 7, 1, 9, 3, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int m = 4;
    cout << "Mean = " << findMean(arr, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find mean of means
import java.util.*;
import java.lang.*;

public class GeeksforGeeks{

    // function to find mean value
    public static float findMean(int arr[], int n,
                                          int m){

        // declare sum and winSum (window sum)
        float sum = 0, winSum = 0;
        int i = 0;

        // find sum for 1st m-length window
        for (; i < m; i++)
            winSum += arr[i];
        sum += (winSum / m);

        // iterate over array to find sum
        // of all m-length means
        for (; i < n; i++) {
            winSum = winSum - arr[i - m] + arr[i];
            sum += (winSum / m);
        }

        // mean of means will be sum of means
        // divided by no of such means
        return (sum / (n - m + 1));
    }

    // driver code
    public static void main(String argc[]){
    int arr[] = { 2, 5, 7, 1, 9, 3, 9 };
    int n = 7;
    int m = 4;
    System.out.println("Mean = " +
                      findMean(arr, n, m));
    }
}

/*This code is contributed by Sagar Shukla.*/
```

## 蟒蛇 3

```
# Python3 program to find mean of means

# function to find mean value
def findMean(arr, n, m) :

    # declare sum and winSum (window sum)
    sum = float(0)
    winSum = float(0)
    i = 0

    # find sum for 1st m-length window
    while (i < m):
        winSum = winSum + arr[i]
        i = i + 1
    sum = sum + (winSum / m);

    # iterate over array to find sum
    # of all m-length means
    while (i < n):
        winSum = winSum - arr[i - m] + arr[i]
        sum = sum + (winSum / m)
        i = i + 1

    # mean of means will be sum of means
    # divided by no of such means
    return (sum / (n - m + 1));

# Driven code
arr = [ 2, 5, 7, 1, 9, 3, 9 ]
n = len(arr)
m = 4
print ("Mean = ", findMean(arr, n, m))

# This code is contributed by "rishabh_jain".
```

## C#

```
// Java program to find mean of means
using System;

public class GeeksforGeeks{

    // function to find mean value
    public static float findMean(int []arr, int n,
                                            int m)
    {

        // declare sum and winSum (window sum)
        float sum = 0, winSum = 0;
        int i = 0;

        // find sum for 1st m-length window
        for (; i < m; i++)
            winSum += arr[i];

        sum += (winSum / m);

        // iterate over array to find sum
        // of all m-length means
        for (; i < n; i++) {
            winSum = winSum - arr[i - m] + arr[i];

            sum += (winSum / m);
        }

        // mean of means will be sum of means
        // divided by no of such means
        return (sum / (n - m + 1));
    }

    // driver code
    public static void Main(){
    int []arr = { 2, 5, 7, 1, 9, 3, 9 };
    int n = 7;
    int m = 4;

    Console.WriteLine("Mean = " +
                    findMean(arr, n, m));
    }
}

/* This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find mean of means

// function to find mean value
function findMean($arr, $n, $m)
{

    // declare sum and
    // winSum (window sum)
    $sum = 0;
    $winSum = 0;
    $i = 0;

    // find sum for 1st
    // m-length window
    for (; $i < $m; $i++)
        $winSum += $arr[ $i];
    $sum += ( $winSum / $m);

    // iterate over array to find sum
    // of all m-length means
    for (; $i < $n; $i++)
    {
        $winSum = $winSum - $arr[ $i - $m] +
                                 $arr[ $i];
        $sum += ( $winSum / $m);
    }

    // mean of means will be sum of means
    // divided by no of such means
    return ($sum / ($n - $m + 1));
}

    // Driver code
    $arr = array(2, 5, 7, 1, 9, 3, 9);
    $n =count($arr);
    $m = 4;
    echo "Mean = ", findMean($arr, $n, $m);

// This code is contributed by anuj_67
?>
```

## java 描述语言

```
<script>

// Javascript program to find mean of means

// function to find mean value
function findMean(arr, n, m)
{
    // declare sum and winSum (window sum)
    var sum = 0, winSum = 0;
    var i = 0;

    // find sum for 1st m-length window
    for (; i < m; i++)
        winSum += arr[i];
    sum += (winSum / m);

    // iterate over array to find sum
    // of all m-length means
    for (; i < n; i++) {
        winSum = winSum - arr[i - m] + arr[i];
        sum += (winSum / m);
    }

    // mean of means will be sum of means
    // divided by no of such means
    return (sum / (n - m + 1));
}

// Driver code
var arr = [ 2, 5, 7, 1, 9, 3, 9 ];
var n = arr.length;
var m = 4;
document.write( "Mean = " + findMean(arr, n, m));

</script>
```

**输出:**

```
Mean = 4.9375 
```