# 用两个等式

找出重复和缺失的数字

> 原文:[https://www . geeksforgeeks . org/使用两个等式找到重复和缺失的数字/](https://www.geeksforgeeks.org/find-the-repeating-and-the-missing-number-using-two-equations/)

给定一个大小为 **N** 的数组**arr【】**，除了出现两次的 **A** 和缺少**的**B**之外，范围**【1，N】**中的每个整数都恰好出现一次。任务是找到编号 **A** 和 **B** 。
**例:**** 

> **输入:** arr[] = {1，2，2，3，4}
> **输出:**
> A = 2
> B = 5
> **输入:** arr[] = {5，3，4，1，1}
> **输出:**
> A = 1
> B = 2

**方法:**从第一个 **N** 自然数之和，

> SumN = 1+2+3+……+N =(N *(N+1))/2
> 并且，让所有数组元素的和为**和**。现在，
> SumN = Sum–A+B
> A–B = Sum–SumN…(等式 1)

根据第一个 **N 个**自然数的平方和，

> SumSqN = 1<sup>2</sup>+2<sup>2</sup>+3<sup>2</sup>+…+N<sup>2</sup>=(N *(N+1)*(2 * N+1))/6
> 并且，让所有数组元素的平方和为 **SumSq** 。现在，
> SumSq = SumSqN+A<sup>2</sup>–B<sup>2</sup>
> SumSq–SumSqN =(A+B)*(A–B)……(等式 2)

将等式 1 中的(A–B)值放入等式 2 中，
SumSq–SumSqN =(A+B)*(Sum–SumN)
A+B =(SumSq–SumSqN)/(Sum–SumN)……(等式 3)
求解等式 1 和等式 3 将得到，

> **B =(((SumSq–SumSqN)/(Sum–SumN))+SumN–Sum)/2**
> 和，**A = Sum–SumN+B**

以下是上述方法的实现:

## C++

```
//C++ implementation of the approach

#include <cmath>
#include<bits/stdc++.h>
#include <iostream>

using namespace std;

    // Function to print the required numbers
 void findNumbers(int arr[], int n)
    {

        // Sum of first n natural numbers
        int sumN = (n * (n + 1)) / 2;

        // Sum of squares of first n natural numbers
        int sumSqN = (n * (n + 1) * (2 * n + 1)) / 6;

        // To store the sum and sum of squares
        // of the array elements
        int sum = 0, sumSq = 0, i;

        for (i = 0; i < n; i++) {
            sum += arr[i];
            sumSq = sumSq + (pow(arr[i], 2));
        }

        int B = (((sumSq - sumSqN) / (sum - sumN)) + sumN - sum) / 2;
        int A = sum - sumN + B;
         cout << "A = " ;
         cout << A << endl;
         cout << "B = " ;
         cout << B << endl;
    }

    // Driver code
int main() {
        int arr[] = { 1, 2, 2, 3, 4 };
        int n = sizeof(arr)/sizeof(arr[0]);
        findNumbers(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function to print the required numbers
    static void findNumbers(int arr[], int n)
    {

        // Sum of first n natural numbers
        int sumN = (n * (n + 1)) / 2;

        // Sum of squares of first n natural numbers
        int sumSqN = (n * (n + 1) * (2 * n + 1)) / 6;

        // To store the sum and sum of squares
        // of the array elements
        int sum = 0, sumSq = 0, i;

        for (i = 0; i < n; i++) {
            sum += arr[i];
            sumSq += Math.pow(arr[i], 2);
        }

        int B = (((sumSq - sumSqN) / (sum - sumN)) + sumN - sum) / 2;
        int A = sum - sumN + B;
        System.out.println("A = " + A + "\nB = " + B);
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 2, 3, 4 };
        int n = arr.length;

        findNumbers(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

import math
# Function to print the required numbers
def findNumbers(arr, n):

        # Sum of first n natural numbers
        sumN = (n * (n + 1)) / 2;

        # Sum of squares of first n natural numbers
        sumSqN = (n * (n + 1) * (2 * n + 1)) / 6;

        # To store the sum and sum of squares
        # of the array elements
        sum = 0;
        sumSq = 0;

        for i in range(0,n):
            sum = sum + arr[i];
            sumSq = sumSq + (math.pow(arr[i], 2));

        B = (((sumSq - sumSqN) / (sum - sumN)) + sumN - sum) / 2;
        A = sum - sumN + B;
        print("A = ",int(A)) ;
        print("B = ",int(B));

# Driver code

arr = [ 1, 2, 2, 3, 4 ];
n = len(arr);
findNumbers(arr, n);

#This code is contributed by Shivi_Aggarwal   
```

## C#

```
// C# implementation of the approach
using System;
public class GFG {

    // Function to print the required numbers
    static void findNumbers(int []arr, int n)
    {

        // Sum of first n natural numbers
        int sumN = (n * (n + 1)) / 2;

        // Sum of squares of first n natural numbers
        int sumSqN = (n * (n + 1) * (2 * n + 1)) / 6;

        // To store the sum and sum of squares
        // of the array elements
        int sum = 0, sumSq = 0, i;

        for (i = 0; i < n; i++) {
            sum += arr[i];
            sumSq += (int)Math.Pow(arr[i], 2);
        }

        int B = (((sumSq - sumSqN) / (sum - sumN)) + sumN - sum) / 2;
        int A = sum - sumN + B;
        Console.WriteLine("A = " + A + "\nB = " + B);
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 2, 2, 3, 4 };
        int n = arr.Length;

        findNumbers(arr, n);
    }
}
// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the required numbers
function findNumbers($arr, $n)
{

    // Sum of first n natural numbers
    $sumN = ($n * ($n + 1)) / 2;

    // Sum of squares of first n
    // natural numbers
    $sumSqN = ($n * ($n + 1) *
                (2 * $n + 1)) / 6;

    // To store the sum and sum of
    // squares of the array elements
    $sum = 0 ;
    $sumSq = 0 ;

    for ($i = 0; $i < $n; $i++)
    {
        $sum += $arr[$i];
        $sumSq += pow($arr[$i], 2);
    }

    $B = ((($sumSq - $sumSqN) / ($sum - $sumN)) +
                                 $sumN - $sum) / 2;
    $A = $sum - $sumN + $B;
    echo "A = ", $A, "\nB = ", $B;
}

// Driver code
$arr = array( 1, 2, 2, 3, 4 );
$n = sizeof($arr) ;

findNumbers($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the required numbers
function findNumbers(arr, n)
{

    // Sum of first n natural numbers
    sumN = (n * (n + 1)) / 2;

    // Sum of squares of first n
    // natural numbers
    sumSqN = (n * (n + 1) *
                (2 * n + 1)) / 6;

    // To store the sum and sum of
    // squares of the array elements
    let sum = 0 ;
    let sumSq = 0 ;

    for (let i = 0;i < n; i++)
    {
        sum += arr[i];
        sumSq += Math.pow(arr[i], 2);
    }

    B = (((sumSq - sumSqN) / (sum - sumN)) +
                                sumN - sum) / 2;
    A = sum - sumN + B;
    document.write( "A = "+ A, "<br>B = ", B);
}

// Driver code
let arr = [ 1, 2, 2, 3, 4 ];
n = arr.length ;

findNumbers(arr, n);

// This code is contributed
// by bobby

</script>
```

**Output:** 

```
A = 2
B = 5
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)