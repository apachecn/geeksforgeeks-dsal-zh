# 范围和查询后从给定数组中找到初始数组

> 原文:[https://www . geesforgeks . org/find-the-initial-array-from-after-range-sum-query/](https://www.geeksforgeeks.org/find-the-initial-array-from-given-array-after-range-sum-queries/)

给定一个数组 **arr[]** ，它是在原始数组上执行多个查询时得到的数组。查询的形式为**【l，r，x】**，其中 **l** 是数组中的起始索引， **r** 是数组中的结束索引， **x** 是必须添加到索引范围**【l，r】**中所有元素的整数元素。任务是找到原始数组。
**示例:**

> **输入:** arr[] = {5，7，8}，l[] = {0}，r[] = {1}，x[] = {2}
> **输出:** 3 5 8
> 如果对数组{3，5，8}
> 执行查询[0，1，2]，得到的数组将是{5，7，8}
> **输入:**arr[= { 20，30，20，70，100}，【T100】

**天真法:**对于从 **l** 到 **r** 的每个范围，减去相应的 **x** 得到初始数组。
以下是实施办法:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print the contents of an array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}

// Function to find the original array
void findOrgArr(int arr[], int l[], int r[], int x[],
                int n, int q)
{
    for (int j = 0; j < q; j++) {
        for (int i = l[j]; i <= r[j]; i++) {

            // Decrement elements between
            // l[j] and r[j] by x[j]
            arr[i] = arr[i] - x[j];
        }
    }

    printArr(arr, n);
}

// Driver code
int main()
{
    // Final array
    int arr[] = { 20, 30, 20, 70, 100 };

    // Size of the array
    int n = sizeof(arr) / sizeof(arr[0]);

    // Queries
    int l[] = { 0, 1, 3 };
    int r[] = { 2, 4, 4 };
    int x[] = { 10, 20, 30 };

    // Number of queries
    int q = sizeof(l) / sizeof(l[0]);

    findOrgArr(arr, l, r, x, n, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Utility function to print the contents of an array
static void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        System.out.print(arr[i]+" ");
    }
}

// Function to find the original array
static void findOrgArr(int arr[], int l[], int r[], int x[],
                int n, int q)
{
    for (int j = 0; j < q; j++) {
        for (int i = l[j]; i <= r[j]; i++) {

            // Decrement elements between
            // l[j] and r[j] by x[j]
            arr[i] = arr[i] - x[j];
        }
    }

    printArr(arr, n);
}

// Driver code
public static void  main(String args[])
{
    // Final array
    int arr[] = { 20, 30, 20, 70, 100 };

    // Size of the array
    int n =  arr.length;

    // Queries
    int l[] = { 0, 1, 3 };
    int r[] = { 2, 4, 4 };
    int x[] = { 10, 20, 30 };

    // Number of queries
    int q = l.length;

    findOrgArr(arr, l, r, x, n, q);

}
}

// This code is contributed by
// Shashank_Sharma
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math as mt

# Utility function to print the
# contents of an array
def printArr(arr, n):

    for i in range(n):
        print(arr[i], end = " ")

# Function to find the original array
def findOrgArr(arr, l, r, x, n, q):

    for j in range(q):
        for i in range(l[j], r[j] + 1):

            # Decrement elements between
            # l[j] and r[j] by x[j]
            arr[i] = arr[i] - x[j]

    printArr(arr, n)

# Driver code

# Final array
arr = [20, 30, 20, 70, 100]

# Size of the array
n = len(arr)

# Queries
l = [0, 1, 3]
r = [ 2, 4, 4]
x = [ 10, 20, 30 ]

# Number of queries
q = len(l)

findOrgArr(arr, l, r, x, n, q)

# This code is contributed by
# mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Utility function to print the
// contents of an array
static void printArr(int[] arr, int n)
{
    for (int i = 0; i < n; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Function to find the original array
static void findOrgArr(int[] arr, int[] l,
                       int[] r, int[] x,
                       int n, int q)
{
    for (int j = 0; j < q; j++)
    {
        for (int i = l[j]; i <= r[j]; i++)
        {

            // Decrement elements between
            // l[j] and r[j] by x[j]
            arr[i] = arr[i] - x[j];
        }
    }

    printArr(arr, n);
}

// Driver code
public static void Main()
{
    // Final array
    int[] arr = { 20, 30, 20, 70, 100 };

    // Size of the array
    int n = arr.Length;

    // Queries
    int[] l = { 0, 1, 3 };
    int[] r = { 2, 4, 4 };
    int[] x = { 10, 20, 30 };

    // Number of queries
    int q = l.Length;

    findOrgArr(arr, l, r, x, n, q);

}
}

// This code is contributed by
// Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Utility function to print the contents
// of an array
function printArr(&$arr, $n)
{
    for ($i = 0; $i < $n; $i++)
    {
        echo($arr[$i]);
        echo(" ");
    }
}

// Function to find the original array
function findOrgArr(&$arr, &$l, &$r,
                        &$x, $n, $q)
{
    for ($j = 0; $j < $q; $j++)
    {
        for ($i = $l[$j]; $i <= $r[$j]; $i++)
        {

            // Decrement elements between
            // l[j] and r[j] by x[j]
            $arr[$i] = $arr[$i] - $x[$j];
        }
    }

    printArr($arr, $n);
}

// Driver code

// Final array
$arr = array(20, 30, 20, 70, 100);

// Size of the array
$n = sizeof($arr);

// Queries
$l = array(0, 1, 3 );
$r = array( 2, 4, 4 );
$x = array(10, 20, 30 );

// Number of queries
$q = sizeof($l);

findOrgArr($arr, $l, $r, $x, $n, $q);

// This code is contributed by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Utility function to print the contents of an array
function printArr(arr,n)
{
    for (let i = 0; i < n; i++) {
        document.write(arr[i]+" ");
    }
}

// Function to find the original array
function findOrgArr(arr,l,r,x,n,q)
{
     for (let j = 0; j < q; j++) {
        for (let i = l[j]; i <= r[j]; i++) {

            // Decrement elements between
            // l[j] and r[j] by x[j]
            arr[i] = arr[i] - x[j];
        }
    }

    printArr(arr, n);
}

// Driver code

// Final array
let arr = [ 20, 30, 20, 70, 100 ];

// Size of the array
let n =  arr.length;

// Queries
let l = [ 0, 1, 3 ];
let r = [ 2, 4, 4 ];
let x = [ 10, 20, 30 ];

// Number of queries
let q = l.length;

findOrgArr(arr, l, r, x, n, q);

// This code is contributed by patel2127
</script>
```

**输出:**

```
10 0 -10 20 50 
```

**时间复杂度:** O(n <sup>2</sup> )
**高效进场:**按照以下步骤到达初始阵位:

*   取一个给定数组大小的数组 **b[]** ，用 **0** 初始化它的所有元素。
*   在数组 **b[]** 中，对于每个查询更新**b[l]= b[l]–x**和 **b[r + 1] = b[r + 1] + x** 如果 **r + 1 < n** 。这是因为 **x** 在执行前缀求和时会抵消 **-x** 的效果。
*   取数组 **b[]** 的前缀和，加到给定的数组中，生成初始数组。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print the contents of an array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}

// Function to find the original array
void findOrgArr(int arr[], int l[], int r[], int x[],
                int n, int q)
{
    int b[n] = { 0 };

    for (int i = 0; i < q; i++) {

        // Decrement the element at l[i]th index by -x
        b[l[i]] += -x[i];

        // Increment the element at (r[i] + 1)th index
        // by x if (r[i] + 1) is a valid index
        if (r[i] + 1 < n)
            b[r[i] + 1] += x[i];
    }

    for (int i = 1; i < n; i++)
        // Prefix sum of array b
        b[i] = b[i - 1] + b[i];

    // Update the original array
    for (int i = 0; i < n; i++)
        arr[i] = arr[i] + b[i];

    printArr(arr, n);
}

// Driver code
int main()
{
    // Final array
    int arr[] = { 20, 30, 20, 70, 100 };

    // Size of the array
    int n = sizeof(arr) / sizeof(arr[0]);

    // Queries
    int l[] = { 0, 1, 3 };
    int r[] = { 2, 4, 4 };
    int x[] = { 10, 20, 30 };

    // Number of queries
    int q = sizeof(l) / sizeof(l[0]);

    findOrgArr(arr, l, r, x, n, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG{

    // Utility function to print the contents of an array
    static void printArr(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
        {
        System.out.print(arr[i] + " ") ;
        }
    }

    // Function to find the original array
    static void findOrgArr(int arr[], int l[], int r[], int x[],
                    int n, int q)
    {
        int b[] = new int[n] ;

        for (int i = 0; i < q; i++)
            b[i] = 0 ;

        for (int i = 0; i < q; i++)
        {

            // Decrement the element at l[i]th index by -x
            b[l[i]] += -x[i];

            // Increment the element at (r[i] + 1)th index
            // by x if (r[i] + 1) is a valid index
            if (r[i] + 1 < n)
                b[r[i] + 1] += x[i];
        }

        for (int i = 1; i < n; i++)
            // Prefix sum of array b
            b[i] = b[i - 1] + b[i];

        // Update the original array
        for (int i = 0; i < n; i++)
            arr[i] = arr[i] + b[i];

        printArr(arr, n);
    }

    // Driver code
    public static void main(String []args)
    {
        // Final array
        int arr[] = { 20, 30, 20, 70, 100 };

        // Size of the array
        int n = arr.length ;

        // Queries
        int l[] = { 0, 1, 3 };
        int r[] = { 2, 4, 4 };
        int x[] = { 10, 20, 30 };

        // Number of queries
        int q = l.length ;

        findOrgArr(arr, l, r, x, n, q);
        }
}

// This code is contributed by aishwarya.27
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to print the contents
# of an array
def printArr(arr, n):

    for i in range(n):
        print(arr[i], end = " ")

# Function to find the original array
def findOrgArr(arr, l, r, x, n, q):

    b = [0 for i in range(n)]

    for i in range(q):

        # Decrement the element at l[i]th
        # index by -x
        b[l[i]] += -x[i]

        # Increment the element at (r[i] + 1)th
        # index by x if (r[i] + 1) is a valid index
        if (r[i] + 1 < n):
            b[r[i] + 1] += x[i]

    for i in range(n):

        # Prefix sum of array b
        b[i] = b[i - 1] + b[i]

    # Update the original array
    for i in range(n):
        arr[i] = arr[i] + b[i]

    printArr(arr, n)

# Driver code
arr = [20, 30, 20, 70, 100]

# Size of the array
n = len(arr)

# Queries
l = [0, 1, 3 ]
r = [2, 4, 4 ]
x = [10, 20, 30 ]

# Number of queries
q = len(l)

findOrgArr(arr, l, r, x, n, q)

# This code Is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Utility function to print the
// contents of an array
static void printArr(int[] arr, int n)
{
    for (int i = 0; i < n; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Function to find the original array
static void findOrgArr(int[] arr, int[] l,
                       int[] r, int[] x,
                       int n, int q)
{
    int[] b = new int[n];

    for (int i = 0; i < q; i++)
        b[i] = 0 ;

    for (int i = 0; i < q; i++)
    {

        // Decrement the element at l[i]th
        // index by -x
        b[l[i]] += -x[i];

        // Increment the element at (r[i] + 1)th
        // index by x if (r[i] + 1) is a valid index
        if (r[i] + 1 < n)
            b[r[i] + 1] += x[i];
    }

    for (int i = 1; i < n; i++)

        // Prefix sum of array b
        b[i] = b[i - 1] + b[i];

    // Update the original array
    for (int i = 0; i < n; i++)
        arr[i] = arr[i] + b[i];

    printArr(arr, n);
}

// Driver code
public static void Main()
{
    // Final array
    int[] arr = { 20, 30, 20, 70, 100 };

    // Size of the array
    int n = arr.Length;

    // Queries
    int[] l = { 0, 1, 3 };
    int[] r = { 2, 4, 4 };
    int[] x = { 10, 20, 30 };

    // Number of queries
    int q = l.Length;

    findOrgArr(arr, l, r, x, n, q);
}
}

// This code is contributed
// by Akanksha Rai
```

**输出:**

```
10 0 -10 20 50 
```

**时间复杂度:** O(n)