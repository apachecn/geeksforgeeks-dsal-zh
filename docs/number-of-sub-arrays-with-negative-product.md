# 负积子阵列数量

> 原文:[https://www . geeksforgeeks . org/负积子数组数/](https://www.geeksforgeeks.org/number-of-sub-arrays-with-negative-product/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找出负积子阵的个数。
**例:**

> **输入:** arr[] = {-1，2，-2}
> T3】输出: 4
> 负积的斯巴瑞分别为{-1}、{-2}、{-1，2 }和{2，-2}。
> **输入:** arr[] = {5，-4，-3，2，-5}
> **输出:** 8

**进场:**

*   用 **1** 代替正阵元，用 **-1** 代替负阵元。
*   创建前缀产品数组 **pre[]** ，其中 **pre[i]** 存储从索引 **arr[0]** 到 **arr[i]** 的所有元素的产品。
*   现在，可以注意到，只有当 **pre[i] * pre[j]** 为负时，子阵列 **arr[i…j]** 才有负积。
*   因此，具有负乘积的子阵列的总计数将是前缀乘积阵列中计数正和负元素的乘积。

以下是上述方法的实现:

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

// Driver code
int main()
{
    int arr[] = { 5, -4, -3, 2, -5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << negProdSubArr(arr, n);

    return (0);
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

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 5, -4, -3, 2, -5 };
        int n = arr.length;

        System.out.println(negProdSubArr(arr, n));
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

# Driver code
arr = [5, -4, -3, 2, -5]
n = len(arr)

print(negProdSubArr(arr, n))

# This code is contributed by Mohit Kumar
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

    // Driver code
    static public void Main ()
    {
        int []arr = { 5, -4, -3, 2, -5 };
        int n = arr.Length;

        Console.Write(negProdSubArr(arr, n));
    }
}

// This code is contributed by Sachin.
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
    for (let i = 0; i < n; i++) {

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

// Driver code
    let arr = [ 5, -4, -3, 2, -5 ];
    let n = arr.length;

    document.write(negProdSubArr(arr, n));

</script>
```

**Output:** 

```
8
```