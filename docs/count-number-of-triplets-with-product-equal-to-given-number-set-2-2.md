# 计数乘积等于给定数的三胞胎数|集合 2

> 原文:[https://www . geeksforgeeks . org/count-三胞胎数量与给定数量相等-set-2-2/](https://www.geeksforgeeks.org/count-number-of-triplets-with-product-equal-to-given-number-set-2-2/)

给定一组不同的整数(仅考虑正数)和一个数字“m”，求乘积等于“m”的三元组的数目。
**例:**

```
Input: arr[] = { 1, 4, 6, 2, 3, 8}  
            m = 24
Output: 3

Input: arr[] = { 0, 4, 6, 2, 3, 8}  
            m = 18
Output: 0
```

在之前的[帖子](https://www.geeksforgeeks.org/count-number-triplets-product-equal-given-number)中已经讨论过一个有 O(n)个额外空间的方法。在这篇文章中，我们将讨论一种具有 0(1)空间复杂度的方法。
**进场:**思路是用三分球技术:

1.  对输入数组进行排序。
2.  将第一个元素固定为 A[i]，其中 I 从 0 到数组大小–2。
3.  固定三元组的第一个元素后，使用 [2 指针技术找到另外两个元素。](https://www.geeksforgeeks.org/two-pointers-technique)

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count such triplets
int countTriplets(int arr[], int n, int m)
{
    int count = 0;

    // Sort the array
    sort(arr, arr + n);
    int end, start, mid;

    // three pointer technique
    for (end = n - 1; end >= 2; end--) {
        int start = 0, mid = end - 1;
        while (start < mid) {

            // Calculate the product of a triplet
            long int prod = arr[end] * arr[start] * arr[mid];

            // Check if that product is greater than m,
            // decrement mid
            if (prod > m)
                mid--;

            // Check if that product is smaller than m,
            // increment start
            else if (prod < m)
                start++;

            // Check if that product is equal to m,
            // decrement mid, increment start and
            // increment the count of pairs
            else if (prod == m) {
                count++;
                mid--;
                start++;
            }
        }
    }

    return count;
}

// Drivers code
int main()
{
    int arr[] = { 1, 1, 1, 1, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int m = 1;

    cout << countTriplets(arr, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// above approach
import java.io.*;
import java.util.*;

class GFG
{

// Function to count such triplets
static int countTriplets(int arr[],
                         int n, int m)
{
    int count = 0;

    // Sort the array
    Arrays.sort(arr);
    int end, start, mid;

    // three pointer technique
    for (end = n - 1; end >= 2; end--)
    {
        start = 0; mid = end - 1;
        while (start < mid)
        {

            // Calculate the product
            // of a triplet
            long prod = arr[end] *
                        arr[start] *
                        arr[mid];

            // Check if that product
            // is greater than m,
            // decrement mid
            if (prod > m)
                mid--;

            // Check if that product
            // is smaller than m,
            // increment start
            else if (prod < m)
                start++;

            // Check if that product is equal
            // to m, decrement mid, increment
            // start and increment the
            // count of pairs
            else if (prod == m)
            {
                count++;
                mid--;
                start++;
            }
        }
    }

    return count;
}

// Driver code
public static void main (String[] args)
{
    int []arr = { 1, 1, 1, 1, 1, 1 };
    int n = arr.length;
    int m = 1;

    System.out.println(countTriplets(arr, n, m));
}
}

// This code is contributed
// by inder_verma.
```

## 蟒蛇 3

```
# Python3 implementation
# of above approach

# Function to count such triplets
def countTriplets(arr, n, m):

    count = 0

    # Sort the array
    arr.sort()

    # three pointer technique
    for end in range(n - 1, 1, -1) :
        start = 0
        mid = end - 1
        while (start < mid) :

            # Calculate the product
            # of a triplet
            prod = (arr[end] *
                    arr[start] * arr[mid])

            # Check if that product is
            # greater than m, decrement mid
            if (prod > m):
                mid -= 1

            # Check if that product is
            # smaller than m, increment start
            elif (prod < m):
                start += 1

            # Check if that product is equal
            # to m, decrement mid, increment
            # start and increment the count
            # of pairs
            elif (prod == m):
                count += 1
                mid -= 1
                start += 1

    return count

# Drivers code
if __name__ == "__main__":
    arr = [ 1, 1, 1, 1, 1, 1 ]
    n = len(arr)
    m = 1

    print(countTriplets(arr, n, m))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to count such triplets
static int countTriplets(int []arr,
                         int n, int m)
{
    int count = 0;

    // Sort the array
    Array.Sort(arr);
    int end, start, mid;

    // three pointer technique
    for (end = n - 1; end >= 2; end--)
    {
        start = 0; mid = end - 1;
        while (start < mid)
        {

            // Calculate the product
            // of a triplet
            long prod = arr[end] *
                        arr[start] *
                        arr[mid];

            // Check if that product
            // is greater than m,
            // decrement mid
            if (prod > m)
                mid--;

            // Check if that product
            // is smaller than m,
            // increment start
            else if (prod < m)
                start++;

            // Check if that product
            // is equal to m,
            // decrement mid, increment
            // start and increment the
            // count of pairs
            else if (prod == m)
            {
                count++;
                mid--;
                start++;
            }
        }
    }

    return count;
}

// Driver code
public static void Main (String []args)
{
    int []arr = { 1, 1, 1, 1, 1, 1 };
    int n = arr.Length;
    int m = 1;

    Console.WriteLine(countTriplets(arr, n, m));
}
}

// This code is contributed
// by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP  implementation of above approach

// Function to count such triplets

function  countTriplets($arr, $n, $m)
{
     $count = 0;

    // Sort the array
    sort($arr);
    $end; $start; $mid;

    // three pointer technique
    for ($end = $n - 1; $end >= 2; $end--) {
         $start = 0;
         $mid = $end - 1;
        while ($start < $mid) {

            // Calculate the product of a triplet
            $prod = $arr[$end] * $arr[$start] * $arr[$mid];

            // Check if that product is greater than m,
            // decrement mid
            if ($prod > $m)
                $mid--;

            // Check if that product is smaller than m,
            // increment start
            else if ($prod < $m)
                $start++;

            // Check if that product is equal to m,
            // decrement mid, increment start and
            // increment the count of pairs
            else if ($prod == $m) {
                $count++;
                $mid--;
                $start++;
            }
        }
    }

    return $count;
}

// Drivers code

    $arr = array( 1, 1, 1, 1, 1, 1 );
     $n = sizeof($arr) / sizeof($arr[0]);
    $m = 1;

    echo  countTriplets($arr, $n, $m);

#This Code is Contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of above approach

    // Function to count such triplets
    function countTriplets(arr, n, m)
    {
        let count = 0;

        // Sort the array
        arr.sort(function(a, b){return a - b});
        let end, start, mid;

        // three pointer technique
        for (end = n - 1; end >= 2; end--)
        {
            start = 0; mid = end - 1;
            while (start < mid)
            {

                // Calculate the product
                // of a triplet
                let prod = arr[end] * arr[start] * arr[mid];

                // Check if that product
                // is greater than m,
                // decrement mid
                if (prod > m)
                    mid--;

                // Check if that product
                // is smaller than m,
                // increment start
                else if (prod < m)
                    start++;

                // Check if that product
                // is equal to m,
                // decrement mid, increment
                // start and increment the
                // count of pairs
                else if (prod == m)
                {
                    count++;
                    mid--;
                    start++;
                }
            }
        }

        return count;
    }

    let arr = [ 1, 1, 1, 1, 1, 1 ];
    let n = arr.length;
    let m = 1;

    document.write(countTriplets(arr, n, m));

</script>
```

**Output:** 

```
6
```

**时间复杂度:**o(n^2)
T3】空间复杂度: O(1)