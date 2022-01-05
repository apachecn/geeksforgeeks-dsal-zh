# 正积子阵数量

> 原文:[https://www . geeksforgeeks . org/正积子阵数量/](https://www.geeksforgeeks.org/number-of-subarrays-with-positive-product/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找出具有正积的子数组的个数。
**例:**

> **输入:** arr[] = {-1，2，-2}
> **输出:** 2
> 正积的子阵为{2}和{-1，2，-2}。
> **输入:** arr[] = {5，-4，-3，2，-5}
> **输出:** 7

**方法:**寻找负积子阵的方法已经在[这篇](https://www.geeksforgeeks.org/number-of-sub-arrays-with-negative-product/)文章中讨论过了。如果 **cntNeg** 是负积子阵列的计数，而 **total** 是给定阵列的所有可能子阵列的计数，那么正积子阵列的计数将是**cntPos = total–cntNeg**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// subarrays with negative product
int negProdSubArr(int arr[], int n)
{
    int positive = 1, negative = 0;
    for (int i = 0; i < n; i++) {

        // Replace current element with 1
        // if it is positive else replace
        // it with -1 instead
        if (arr[i] > 0)
            arr[i] = 1;
        else
            arr[i] = -1;

        // Take product with previous element
        // to form the prefix product
        if (i > 0)
            arr[i] *= arr[i - 1];

        // Count positive and negative elements
        // in the prefix product array
        if (arr[i] == 1)
            positive++;
        else
            negative++;
    }

    // Return the required count of subarrays
    return (positive * negative);
}

// Function to return the count of
// subarrays with positive product
int posProdSubArr(int arr[], int n)
{

    // Total subarrays possible
    int total = (n * (n + 1)) / 2;

    // Count to subarrays with negative product
    int cntNeg = negProdSubArr(arr, n);

    // Return the count of subarrays
    // with positive product
    return (total - cntNeg);
}

// Driver code
int main()
{
    int arr[] = { 5, -4, -3, 2, -5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << posProdSubArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of
// subarrays with negative product
static int negProdSubArr(int arr[], int n)
{
    int positive = 1, negative = 0;
    for (int i = 0; i < n; i++)
    {

        // Replace current element with 1
        // if it is positive else replace
        // it with -1 instead
        if (arr[i] > 0)
            arr[i] = 1;
        else
            arr[i] = -1;

        // Take product with previous element
        // to form the prefix product
        if (i > 0)
            arr[i] *= arr[i - 1];

        // Count positive and negative elements
        // in the prefix product array
        if (arr[i] == 1)
            positive++;
        else
            negative++;
    }

    // Return the required count of subarrays
    return (positive * negative);
}

// Function to return the count of
// subarrays with positive product
static int posProdSubArr(int arr[], int n)
{

    // Total subarrays possible
    int total = (n * (n + 1)) / 2;

    // Count to subarrays with negative product
    int cntNeg = negProdSubArr(arr, n);

    // Return the count of subarrays
    // with positive product
    return (total - cntNeg);
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 5, -4, -3, 2, -5 };
    int n = arr.length;

    System.out.println(posProdSubArr(arr, n));
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# subarrays with negative product
def negProdSubArr(arr, n):

    positive = 1

    negative = 0

    for i in range(n):

        # Replace current element with 1
        # if it is positive else replace
        # it with -1 instead
        if (arr[i] > 0):

            arr[i] = 1

        else:

            arr[i] = -1

        # Take product with previous element
        # to form the prefix product
        if (i > 0):

            arr[i] *= arr[i - 1]

        # Count positive and negative elements
        # in the prefix product array
        if (arr[i] == 1):

            positive += 1

        else:

            negative += 1

    # Return the required count of subarrays
    return (positive * negative)

# Function to return the count of
# subarrays with positive product
def posProdSubArr(arr, n):

    total = (n * (n + 1)) / 2;

    # Count to subarrays with negative product
    cntNeg = negProdSubArr(arr, n);

    # Return the count of subarrays
    # with positive product
    return (total - cntNeg);

# Driver code
arr = [5, -4, -3, 2, -5]
n = len(arr)
print(posProdSubArr(arr, n))

# This code is contributed by Mehul Bhutalia
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// subarrays with negative product
static int negProdSubArr(int []arr, int n)
{
    int positive = 1, negative = 0;
    for (int i = 0; i < n; i++)
    {

        // Replace current element with 1
        // if it is positive else replace
        // it with -1 instead
        if (arr[i] > 0)
            arr[i] = 1;
        else
            arr[i] = -1;

        // Take product with previous element
        // to form the prefix product
        if (i > 0)
            arr[i] *= arr[i - 1];

        // Count positive and negative elements
        // in the prefix product array
        if (arr[i] == 1)
            positive++;
        else
            negative++;
    }

    // Return the required count of subarrays
    return (positive * negative);
}

// Function to return the count of
// subarrays with positive product
static int posProdSubArr(int []arr, int n)
{

    // Total subarrays possible
    int total = (n * (n + 1)) / 2;

    // Count to subarrays with negative product
    int cntNeg = negProdSubArr(arr, n);

    // Return the count of subarrays
    // with positive product
    return (total - cntNeg);
}

// Driver code
public static void Main (String[] args)
{
    int []arr = { 5, -4, -3, 2, -5 };
    int n = arr.Length;

    Console.WriteLine(posProdSubArr(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the count of
// subarrays with negative product
function negProdSubArr(arr, n)
{
    let positive = 1, negative = 0;
    for (let i = 0; i < n; i++)
    {

        // Replace current element with 1
        // if it is positive else replace
        // it with -1 instead
        if (arr[i] > 0)
            arr[i] = 1;
        else
            arr[i] = -1;

        // Take product with previous element
        // to form the prefix product
        if (i > 0)
            arr[i] *= arr[i - 1];

        // Count positive and negative elements
        // in the prefix product array
        if (arr[i] == 1)
            positive++;
        else
            negative++;
    }

    // Return the required count of subarrays
    return (positive * negative);
}

// Function to return the count of
// subarrays with positive product
function posProdSubArr(arr, n)
{

    // Total subarrays possible
    let total = parseInt((n * (n + 1)) / 2);

    // Count to subarrays with negative product
    let cntNeg = negProdSubArr(arr, n);

    // Return the count of subarrays
    // with positive product
    return (total - cntNeg);
}

// Driver code
    let arr = [ 5, -4, -3, 2, -5 ];
    let n = arr.length;

    document.write(posProdSubArr(arr, n));

// This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
7
```