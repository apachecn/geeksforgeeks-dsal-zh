# 用给定范围内的元素之和构造和数组

> 原文:[https://www . geesforgeks . org/construct-sum-array-sum-elements-给定-range/](https://www.geeksforgeeks.org/construct-sum-array-sum-elements-given-range/)

给你一个 n 元素数组和一个奇数 T2 m。你必须从给定的数组构造一个新的 sum_array，使得**sum _ array[I]=σarr[j]为(i-(m/2)) < j (i+(m/2))** 。
**注:**为 0 > j 或 j > = n 取 arr[j] = 0。
**举例:**

```
Input : arr[] = {1, 2, 3, 4, 5}, 
            m = 3
Output : sum_array = {3, 6, 9, 12, 9}
Explanation : sum_array[0] = arr[0] + arr[1]
     sum_array[1] = arr[0] + arr[1] + arr[2]
     sum_array[2] = arr[1] + arr[2] + arr[3]
     sum_array[3] = arr[2] + arr[3] + arr[4]
     sum_array[4] = arr[3] + arr[4]

Input : arr[] = {2, 4, 3, 4, 2}, 
           m = 1
Output : sum_array = {2, 4, 3, 4, 2}
Explanation : sum_array[0] = arr[0] 
              sum_array[1] = arr[1]
              sum_array[2] = arr[2]
              sum_array[3] = arr[3]
              sum_array[4] = arr[4]
```

**基本方法:**根据问题陈述，我们通过迭代 *i-(m/2)到 i+(m/2)* 来计算 sum_array[i]。根据这种方法，我们有一个嵌套循环，这将导致时间复杂度为 O(n*m)。
**高效方法:**对于 sum_array 的计算是使用滑动窗口的概念，因此可以轻松节省我们的时间。对于滑动窗口，时间复杂度为 O(n)。
**算法**

```
calculate sum of first (m/2)+1 elementssum_array[0] = sumfor i=1 to i<nif( (i-(m/2)-1) >= 0 )
           sum -= arr[(i-(m/2)-1)]if( (i+m/2) < n)
           sum += arr[(i+m/2)]sum_array[i] = sumprint sum_array
```

## C++

```
// CPP Program to find sum array for a given
// array.
#include <bits/stdc++.h>
using namespace std;

// function to calc sum_array and print
void calcSum_array(int arr[], int n, int m)
{
    int sum = 0;
    int sum_array[n];

    // calc 1st m/2 + 1 element for 1st window
    for (int i = 0; i < m / 2 + 1; i++)
        sum += arr[i];
    sum_array[0] = sum;

    // use sliding window to
    // calculate rest of sum_array
    for (int i = 1; i < n; i++) {
        if (i - (m / 2) - 1 >= 0)
            sum -= arr[i - (m / 2) - 1];
        if (i + (m / 2) < n)
            sum += arr[i + (m / 2)];
        sum_array[i] = sum;
    }

    // print sum_array
    for (int i = 0; i < n; i++)
        cout << sum_array[i] << " ";
}

// driver program
int main()
{
    int arr[] = { 3, 6, 2, 7, 3, 8, 4,
                      9, 1, 5, 0, 4 };
    int m = 5;
    int n = sizeof(arr) / sizeof(int);
    calcSum_array(arr, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find sum array
// for a given array.
class GFG
{
    // function to calc sum_array and print
    static void calcSum_array(int arr[], int n, int m)
    {
        int sum = 0;
        int sum_array[] = new int[n];

        // calc 1st m/2 + 1 element
        // for 1st window
        for (int i = 0; i < m / 2 + 1; i++)
            sum += arr[i];
        sum_array[0] = sum;

        // use sliding window to
        // calculate rest of sum_array
        for (int i = 1; i < n; i++)
        {
            if (i - (m / 2) - 1 >= 0)
                sum -= arr[i - (m / 2) - 1];
            if (i + (m / 2) < n)
                sum += arr[i + (m / 2)];
            sum_array[i] = sum;
        }

        // print sum_array
        for (int i = 0; i < n; i++)
            System.out.print(sum_array[i] + " ");
    }

    // Driver program
    public static void main(String[] args)
    {
        int arr[] = { 3, 6, 2, 7, 3, 8, 4, 9, 1, 5, 0, 4 };
        int m = 5;
        int n = arr.length;
        calcSum_array(arr, n, m);
    }
}

// This code is contributed by prerna saini.
```

## 蟒蛇 3

```
# Python3 Program to find Sum array
# for a given array.
import math as mt

# function to calc Sum_array and print
def calcSum_array(arr, n, m):

    Sum = 0
    Sum_array = [0 for i in range(n)]

    # calc 1st m/2 + 1 element for 1st window
    for i in range(m // 2 + 1):
        Sum += arr[i]
    Sum_array[0] = Sum

    # use sliding window to
    # calculate rest of Sum_array
    for i in range(1, n):
        if (i - (m // 2) - 1 >= 0):
            Sum -= arr[i - (m // 2) - 1]
        if (i + (m / 2) < n):
            Sum += arr[i + (m //2)]
        Sum_array[i] = Sum

    # prSum_array
    for i in range(n):
        print(Sum_array[i], end = " ")

# Driver Code
arr = [ 3, 6, 2, 7, 3, 8, 4, 9, 1, 5, 0, 4 ]
m = 5
n = len(arr)
calcSum_array(arr, n, m)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# Program to find sum array
// for a given array.
using System;

class GFG
{
    // function to calc sum_array and print
    static void calcSum_array(int []arr, int n, int m)
    {
        int sum = 0;
        int []sum_array = new int[n];

        // calc 1st m/2 + 1 element
        // for 1st window
        for (int i = 0; i < m / 2 + 1; i++)
            sum += arr[i];
        sum_array[0] = sum;

        // use sliding window to
        // calculate rest of sum_array
        for (int i = 1; i < n; i++)
        {
            if (i - (m / 2) - 1 >= 0)
                sum -= arr[i - (m / 2) - 1];
            if (i + (m / 2) < n)
                sum += arr[i + (m / 2)];
            sum_array[i] = sum;
        }

        // print sum_array
        for (int i = 0; i < n; i++)
        Console.Write(sum_array[i] + " ");
    }

    // Driver program
    public static void Main()
    {
        int []arr = { 3, 6, 2, 7, 3, 8, 4, 9, 1, 5, 0, 4 };
        int m = 5;
        int n = arr.Length;
        calcSum_array(arr, n, m);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum array
// for a given array.

// function to calc sum_array and print
function calcSum_array(&$arr, $n, $m)
{
    $sum = 0;
    $sum_array = array();

    // calc 1st m/2 + 1 element
    // for 1st window
    for ($i = 0;
         $i < (int)($m / 2) + 1; $i++)
        $sum = $sum + $arr[$i];
    $sum_array[0] = $sum;

    // use sliding window to
    // calculate rest of sum_array
    for ($i = 1; $i < $n; $i++)
    {
        if ($i - (int)($m / 2) - 1 >= 0)
            $sum = $sum - $arr[$i -
                    (int)($m / 2) - 1];
        if ($i + (int)($m / 2) < $n)
            $sum = $sum + $arr[$i +
                    (int)($m / 2)];
        $sum_array[$i] = $sum;
    }

    // print sum_array
    for ($i = 0; $i < $n; $i++)
        echo $sum_array[$i] . " ";
}

// Driver Code
$arr = array(3, 6, 2, 7, 3, 8,
             4, 9, 1, 5, 0, 4 );
$m = 5;
$n = sizeof($arr);
calcSum_array($arr, $n, $m);

// This code is contributed by Mukul Singh
?>
```

## java 描述语言

```
<script>
// JavaScript Program to find sum array for a given
// array.

// function to calc sum_array and print
function calcSum_array(arr, n, m)
{
    let sum = 0;
    let sum_array = new Array(n);

    // calc 1st m/2 + 1 element for 1st window
    for (let i = 0; i < Math.floor(m / 2) + 1; i++)
        sum += arr[i];
    sum_array[0] = sum;

    // use sliding window to
    // calculate rest of sum_array
    for (let i = 1; i < n; i++)
    {
        if (i - Math.floor(m / 2) - 1 >= 0)
            sum -= arr[i - Math.floor(m / 2) - 1];
        if (i + Math.floor(m / 2) < n)
            sum += arr[i + Math.floor(m / 2)];
        sum_array[i] = sum;
    }

    // print sum_array
    for (let i = 0; i < n; i++)
        document.write(sum_array[i] + " ");
}

// Driver program

    let arr = [ 3, 6, 2, 7, 3, 8, 4,
                    9, 1, 5, 0, 4 ];
    let m = 5;
    let n = arr.length;
    calcSum_array(arr, n, m);

// This code is contributed by Surbhi Tyagi.
</script>
```

**输出:**

```
11 18 21 26 24 31 25 27 19 19 10 9 
```