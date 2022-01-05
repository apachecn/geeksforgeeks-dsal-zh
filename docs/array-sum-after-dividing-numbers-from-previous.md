# 将前一个

的数字相除后的数组和

> 原文:[https://www . geesforgeks . org/array-除数后的和-from-previous/](https://www.geeksforgeeks.org/array-sum-after-dividing-numbers-from-previous/)

求数组元素与前一个元素除后的级数之和。
示例:

```
Input : 3 7 9 10 12 18
Explanation:  3 + 7/3 + 9/7 + 10/9 + 
12/10 + 18/12 = 9 (taking only integer 
part)   
Output : 9

Input : 1 12 24 30 60
Output : 18 
```

> **方法:**我们取一个数组中的元素，把这个元素和前面的元素分开。除了第一个元素，我们对数组的所有元素都执行这个过程。将除法后的结果和第一个元素相加。
> **注意:**如果数组中的任何元素为零，则它无法完成任务，并返回负一。

## C++

```
// C++  program for divide and
// sum the number of series
#include <bits/stdc++.h>
using namespace std;

int divideAndSum(int arr[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++) {

        // checking whether element
        // is zero or not
        if (arr[i] == 0)
            return -1;

        if (i == 0)
            sum += arr[i];
        else

            // divide element from
            // previous element
            sum += arr[i] / arr[i - 1];
    }

    return sum;
}

// Driver code
int main()
{
    int arr[] = { 3, 7, 9, 10, 12, 18 };
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << divideAndSum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for divide and
// sum the number of series
import java.io.*;

class GFG
{

    static int divideAndSum(int arr[], int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++) {

            // checking whether element
            // is zero or not
            if (arr[i] == 0)
                return -1;

            if (i == 0)
                sum += arr[i];
            else

                // divide element from
                // previous element
                sum += arr[i] / arr[i - 1];
        }

        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 3, 7, 9, 10, 12, 18 };
        int n = arr.length;
        System.out.println( divideAndSum(arr, n));

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 program for divide and
# sum the number of series

def divideAndSum(arr, n):

    sum = 0
    for i in range(0,n): 

         # checking whether element
         # is zero or not
        if (arr[i] == 0):
            return -1

        if (i == 0):
            sum += arr[i]
        else:

                     # divide element from
             # previous element
             sum += int(arr[i] / arr[i - 1])

    return int(sum)

# Driver code
arr =   [3, 7, 9, 10, 12, 18]  

n = len(arr)
print(divideAndSum(arr, n))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program for divide and
// sum the number of series
using System;

class GFG
{

    static int divideAndSum(int []arr, int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++) {

            // checking whether element
            // is zero or not
            if (arr[i] == 0)
                return -1;

            if (i == 0)
                sum += arr[i];
            else

                // divide element from
                // previous element
                sum += arr[i] / arr[i - 1];
        }

        return sum;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { 3, 7, 9, 10, 12, 18 };
        int n = arr.Length;
        Console.WriteLine( divideAndSum(arr, n));

    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program for divide and
// sum the number of series

function divideAndSum($arr, $n)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++) {

        // checking whether element
        // is zero or not
        if ($arr[$i] == 0)
            return -1;

        if ($i == 0)
            $sum += $arr[$i];
        else

            // divide element from
            // previous element
            $sum += floor($arr[$i] /
                    $arr[$i - 1]);
    }

    return $sum;
}

// Driver code
{
    $arr = array(3, 7, 9, 10, 12, 18);
    $n = sizeof($arr) / sizeof($arr[0]);
    echo divideAndSum($arr, $n);
    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// javascript program for divide and
// sum the number of series

    function divideAndSum(arr , n)
    {
        var sum = 0;
        for (i = 0; i < n; i++) {

            // checking whether element
            // is zero or not
            if (arr[i] == 0)
                return -1;

            if (i == 0)
                sum += arr[i];
            else

                // divide element from
                // previous element
                sum += parseInt(arr[i] / arr[i - 1]);
        }

        return sum;
    }

    // Driver code

        var arr = [ 3, 7, 9, 10, 12, 18 ];
        var n = arr.length;
        document.write( divideAndSum(arr, n));

// This code contributed by umadevi9616
</script>
```

**输出:**

```
9
```

**时间复杂度:** O(N)

**辅助空间:** O(N)