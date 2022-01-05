# 打印总和小于 k 的三胞胎

> 原文:[https://www . geesforgeks . org/print-三胞胎-总和小于或等于-k/](https://www.geeksforgeeks.org/print-triplets-with-sum-less-than-or-equal-to-k/)

给定一组不同的整数和一个和值。打印总和小于给定总和值的所有三元组。预期时间复杂度为 0(n<sup>2</sup>)。

**示例** :

```
Input : arr[] = {-2, 0, 1, 3}
        sum = 2.
Output : (-2, 0, 1)
         (-2, 0, 3) 
Explanation :  The two triplets have sum less than 2.

Input : arr[] = {5, 1, 3, 4, 7}
        sum = 12.
Output : (1, 3, 4)
         (1, 3, 5)
         (1, 3, 7) 
         (1, 4, 5)

```

一个**简单的解决方案**是运行三个循环来逐个考虑所有的三胞胎。对于每个三元组，比较总和，如果其总和小于给定总和，则打印当前三元组。

## c++

```
// A Simple C++ program to count triplets with sum
// smaller than a given value
#include<bits/stdc++.h>
using namespace std;

int printTriplets(int arr[], int n, int sum)
{
    // Fix the first element as A[i]
    for (int i = 0; i < n-2; i++)
    {
       // Fix the second element as A[j]
       for (int j = i+1; j < n-1; j++)
       {
           // Now look for the third number
           for (int k = j+1; k < n; k++)
               if (arr[i] + arr[j] + arr[k] < sum)
                  cout << arr[i] << ", " << arr[j]
                       << ", " << arr[k] << endl;
       }
    }
}

// Driver program
int main()
{
    int arr[] = {5, 1, 3, 4, 7};
    int n = sizeof arr / sizeof arr[0];
    int sum = 12;
    printTriplets(arr, n, sum);
    return 0;
}
```

## Java

```
// A Simple Java program to
// count triplets with sum
// smaller than a given value
import java.io.*;

class GFG
{
static int printTriplets(int arr[],
                         int n, int sum)
{
    // Fix the first
    // element as A[i]
    for (int i = 0; i < n - 2; i++)
    {

    // Fix the second
    // element as A[j]
    for (int j = i + 1;
             j < n - 1; j++)
    {
        // Now look for
        // the third number
        for (int k = j + 1; k < n; k++)
            if (arr[i] + arr[j] + arr[k] < sum)
                System.out.println(arr[i] + ", " +
                                   arr[j] + ", " +
                                   arr[k]);
    }
    }
    return 0;
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = {5, 1, 3, 4, 7};
    int n = arr.length;
    int sum = 12;
    printTriplets(arr, n, sum);
}
}

// This code is contributed
// by anuj_67.
```

## python 3

```
# A Simple python 3 program to count
# triplets with sum smaller than a
# given value

def printTriplets(arr, n, sum):

    # Fix the first element as A[i]
    for i in range(0, n - 2, 1):

        # Fix the second element as A[j]
        for j in range(i + 1, n - 1, 1):

            # Now look for the third number
            for k in range(j + 1, n, 1):
                if (arr[i] + arr[j] + arr[k] < sum):
                    print(arr[i], ",", arr[j], ",", arr[k])
# Driver Code
if __name__ == '__main__':
    arr =[5, 1, 3, 4, 7]
    n = len(arr)
    sum = 12
    printTriplets(arr, n, sum)

# This code is contributed by
# Sahil_Shelangia
```

## c#

```
// A Simple C# program to
// count triplets with sum
// smaller than a given value
using System;
class GFG
{
static int printTriplets(int[] arr,
                        int n, int sum)
{
    // Fix the first
    // element as A[i]
    for (int i = 0; i < n - 2; i++)
    {

    // Fix the second
    // element as A[j]
    for (int j = i + 1;
            j < n - 1; j++)
    {
        // Now look for
        // the third number
        for (int k = j + 1; k < n; k++)
            if (arr[i] + arr[j] + arr[k] < sum)
                Console.WriteLine(arr[i] + ", " +
                                arr[j] + ", " +
                                arr[k]);
    }
    }
    return 0;
}

// Driver Code
public static void Main ()
{
    int[] arr = {5, 1, 3, 4, 7};
    int n = arr.Length;
    int sum = 12;
    printTriplets(arr, n, sum);
}
}

// This code is contributed
// by Mukul Singh.
```

## PHP

```
<?php
// A Simple PHP program to count triplets
// with sum smaller than a given value

function printTriplets(&$arr, $n, $sum)
{
    // Fix the first element as A[i]
    for ($i = 0; $i < $n - 2; $i++)
    {
    // Fix the second element as A[j]
    for ($j = $i + 1; $j < $n - 1; $j++)
    {
        // Now look for the third number
        for ($k = $j + 1; $k < $n; $k++)
            if ($arr[$i] + $arr[$j] +
                           $arr[$k] < $sum)
            {
                echo($arr[$i]);
                echo(", " );
                echo($arr[$j]);
                echo(", ");
                echo($arr[$k]);
                echo("\n");
            }
    }
    }
}

// Driver Code
$arr = array(5, 1, 3, 4, 7);
$n = sizeof($arr);
$sum = 12;
printTriplets($arr, $n, $sum);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## Javascript

```
<script>

// A Simple JavaScript program to
// count triplets with sum
// smaller than a given value

function printTriplets(arr, n, sum)
{
    // Fix the first element as A[i]
    for (let i = 0; i < n-2; i++)
    {
    // Fix the second element as A[j]
    for (let j = i+1; j < n-1; j++)
    {
        // Now look for the third number
        for (let k = j+1; k < n; k++)
            if (arr[i] + arr[j] + arr[k] < sum)
                document.write(arr[i] + ", " + arr[j]
                    + ", " + arr[k] + "<br>");
    }
    }
}

// Driver program
    let arr = [5, 1, 3, 4, 7];
    let n = arr.length;
    let sum = 12;
    printTriplets(arr, n, sum);

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
5, 1, 3
5, 1, 4
1, 3, 4
1, 3, 7
```