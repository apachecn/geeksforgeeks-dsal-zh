# 数组中连续两个元素的和

> 原文:[https://www . geesforgeks . org/sum-continuous-elements-array/](https://www.geeksforgeeks.org/sum-consecutive-elements-array/)

给定两两连续元素的数组打印和。

示例:

```
Input  : 8, 5, 4, 3, 15, 20
Output : 13, 9, 7, 18, 35

Input  : 5, 10, 15, 20
Output : 15, 25, 35 
```

解决方案是遍历数组，并将连续数字的总和保存在变量 sum 中。

## c++

```
// C++ program to print the
// sum of the consecutive elements.
#include <stdio.h>
#include <stdlib.h>

// Function to print pairwise sum
void pairwiseSum(int arr[], int n)
{
    int sum = 0;  
    for (int i = 0; i < n - 1; i++)
    {
        // adding the alternate numbers
        sum = arr[i] + arr[i + 1];
        printf(" %d ", sum);
    }
}

// Driver function to test function
int main()
{
    int arr[] = {4, 10, 15, 5, 6};
    int n = sizeof(arr) / sizeof(arr[0]);

    pairwiseSum(arr, n);
    return 0;
}
```

## Java

```
// Java program to print the
// sum of the consecutive elements.

class Arraysum {

    // Function to print Alternatesum
    static void pairwiseSum(int arr[], int n)
    {
        int sum = 0;
        for (int i = 0; i + 1 < n; i++)
        {
            // adding the alternate numbers
            sum = arr[i] + arr[i + 1];
            System.out.print(sum + " ");
        }
    }

    /*driver function to test function*/
    public static void main(String[] args)
    {

        int arr[] = {4, 10, 15, 5, 6};
        int n = arr.length;
        pairwiseSum(arr, n);
    }
}
```

## python 3

T2

## c#

T21

```
// C# program to print the
// sum of the consecutive elements.
using System;

class Arraysum {

    // Function to print Alternatesum
    static void pairwiseSum(int []arr, int n)
    {
        int sum = 0;
        for (int i = 0; i + 1 < n; i++)
        {
            // adding the alternate numbers
            sum = arr[i] + arr[i + 1];
            Console.Write(sum + " ");
        }
    }

    // Driver function
    public static void Main()
    {

        int []arr = {4, 10, 15, 5, 6};
        int n = arr.Length;
        pairwiseSum(arr, n);
    }
}

// This code is contributed by vt_m.
```

## PHP

```
<?php
// PHP program to print the
// sum of the consecutive elements.

// Function to print pairwise sum
function pairwiseSum($arr, $n)
{
    $sum = 0;
    for ($i = 0; $i < $n - 1; $i++)
    {

        // adding the alternate numbers
        $sum = $arr[$i] + $arr[$i + 1];
        echo $sum," ";
    }
}

    // Driver Code
    $arr = array (4, 10, 15, 5, 6);
    $n = sizeof($arr) ;
    pairwiseSum($arr, $n);

// This code is contributed by ajit
?>
```

## Javascript

```
<script>

// Javascript program to print the
// sum of the consecutive elements.

// Function to print Alternatesum
function pairwiseSum(arr, n)
{
    let sum = 0;
    for(let i = 0; i + 1 < n; i++)
    {

        // Adding the alternate numbers
        sum = arr[i] + arr[i + 1];
        document.write(sum + " ");
    }
}

// Driver code
let arr = [ 4, 10, 15, 5, 6 ];
let n = arr.length;

pairwiseSum(arr, n);

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
14 25 20 11
```