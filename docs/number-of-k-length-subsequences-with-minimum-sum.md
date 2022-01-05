# 最小和的 K 长度子序列数

> 原文:[https://www . geesforgeks . org/number-of-k-length-subseries-with-minimum-sum/](https://www.geeksforgeeks.org/number-of-k-length-subsequences-with-minimum-sum/)

给定一个大小为 **N** 的数组**arr【】**和一个整数 **K** ，任务是找到这个数组的 **K** 长度子序列的数量，使得这些子序列的和是最小可能的。

**示例:**

> **输入:** arr[] = {1，2，3，4}，K = 2
> **输出:** 1
> 长度为 2 的子序列为(1，2)，(1，3)，(1，4)，
> (2，3)，(2，4)和(3，4)。
> 最小和为 3，唯一有这个和的子序列
> 为(1，2)。
> 
> **输入:** arr[] = {2，1，2，2，2，1}，K = 3
> T3】输出: 4

**方法:**给定数组中长度为 **K** 的子序列的最小可能和是数组中最小元素 **K** 的和。设 **X** 为数组的 **K** 个最小元素中的最大元素，设其在数组的 **K、**个最小元素中出现的次数为 **Y** ，其在整个数组中的总出现次数为 **cntX** 。现在有**<sup>cntX</sup>C<sub>Y</sub>**的方式选择这个元素，在 **K** 最小的元素中，就是需要的子序列的个数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the value of
// Binomial Coefficient C(n, k)
int binomialCoeff(int n, int k)
{
    int C[n + 1][k + 1];
    int i, j;

    // Calculate value of Binomial Coefficient
    // in bottom up manner
    for (i = 0; i <= n; i++) {
        for (j = 0; j <= min(i, k); j++) {

            // Base Cases
            if (j == 0 || j == i)
                C[i][j] = 1;

            // Calculate value using previously
            // stored values
            else
                C[i][j] = C[i - 1][j - 1] + C[i - 1][j];
        }
    }

    return C[n][k];
}

// Function to return the count
// of valid subsequences
int cntSubSeq(int arr[], int n, int k)
{

    // Sort the array
    sort(arr, arr + n);

    // Maximum among the minimum K elements
    int num = arr[k - 1];

    // Y will store the frequency of num
    // in the minimum K elements
    int Y = 0;
    for (int i = k - 1; i >= 0; i--) {
        if (arr[i] == num)
            Y++;
    }

    // cntX will store the frequency of
    // num in the complete array
    int cntX = Y;
    for (int i = k; i < n; i++) {
        if (arr[i] == num)
            cntX++;
    }

    return binomialCoeff(cntX, Y);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(int);
    int k = 2;

    cout << cntSubSeq(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the value of
    // Binomial Coefficient C(n, k)
    static int binomialCoeff(int n, int k)
    {
        int C[][] = new int [n + 1][k + 1];
        int i, j;

        // Calculate value of Binomial Coefficient
        // in bottom up manner
        for (i = 0; i <= n; i++)
        {
            for (j = 0; j <= Math.min(i, k); j++)
            {

                // Base Cases
                if (j == 0 || j == i)
                    C[i][j] = 1;

                // Calculate value using previously
                // stored values
                else
                    C[i][j] = C[i - 1][j - 1] +
                              C[i - 1][j];
            }
        }
        return C[n][k];
    }

    // Function to return the count
    // of valid subsequences
    static int cntSubSeq(int arr[], int n, int k)
    {

        // Sort the array
        Arrays.sort(arr);

        // Maximum among the minimum K elements
        int num = arr[k - 1];

        // Y will store the frequency of num
        // in the minimum K elements
        int Y = 0;
        for (int i = k - 1; i >= 0; i--)
        {
            if (arr[i] == num)
                Y++;
        }

        // cntX will store the frequency of
        // num in the complete array
        int cntX = Y;
        for (int i = k; i < n; i++)
        {
            if (arr[i] == num)
                cntX++;
        }
        return binomialCoeff(cntX, Y);
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 3, 4 };
        int n = arr.length;
        int k = 2;

        System.out.println(cntSubSeq(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the value of
    // Binomial Coefficient C(n, k)
    static int binomialCoeff(int n, int k)
    {
        int [,]C = new int [n + 1, k + 1];
        int i, j;

        // Calculate value of Binomial Coefficient
        // in bottom up manner
        for (i = 0; i <= n; i++)
        {
            for (j = 0; j <= Math.Min(i, k); j++)
            {

                // Base Cases
                if (j == 0 || j == i)
                    C[i, j] = 1;

                // Calculate value using previously
                // stored values
                else
                    C[i, j] = C[i - 1, j - 1] +
                              C[i - 1, j];
            }
        }
        return C[n, k];
    }

    // Function to return the count
    // of valid subsequences
    static int cntSubSeq(int []arr, int n, int k)
    {

        // Sort the array
        Array.Sort(arr);

        // Maximum among the minimum K elements
        int num = arr[k - 1];

        // Y will store the frequency of num
        // in the minimum K elements
        int Y = 0;
        for (int i = k - 1; i >= 0; i--)
        {
            if (arr[i] == num)
                Y++;
        }

        // cntX will store the frequency of
        // num in the complete array
        int cntX = Y;
        for (int i = k; i < n; i++)
        {
            if (arr[i] == num)
                cntX++;
        }
        return binomialCoeff(cntX, Y);
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 1, 2, 3, 4 };
        int n = arr.Length;
        int k = 2;

        Console.WriteLine(cntSubSeq(arr, n, k));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the value of
# Binomial Coefficient C(n, k)
def binomialCoeff(n, k) :

    C = [[0 for i in range(n + 1)]
               for j in range(k + 1)]

    # Calculate value of Binomial Coefficient
    # in bottom up manner
    for i in range (0, n + 1 ):
        for j in range (0, min(i, k) + 1):

            # Base Cases
            if (j == 0 or j == i):
                C[i][j] = 1

            # Calculate value using previously
            # stored values
            else :
                C[i][j] = C[i - 1][j - 1] + C[i - 1][j]

    return C[n][k]

# Function to return the count
# of valid subsequences
def cntSubSeq(arr, n, k) :

    # Sort the array
    arr.sort()

    # Maximum among the minimum K elements
    num = arr[k - 1];

    # Y will store the frequency of num
    # in the minimum K elements
    Y = 0;
    for i in range (k - 1, -1, 1) :
        if (arr[i] == num):
            Y += 1

    # cntX will store the frequency of
    # num in the complete array
    cntX = Y;
    for i in range (k, n):
        if (arr[i] == num) :
            cntX += 1

    return binomialCoeff(cntX, Y)

# Driver code
arr = [ 1, 2, 3, 4 ]
n = len(arr)
k = 2
print(cntSubSeq(arr, n, k))

# This code is contributed by ihritik
```

## java 描述语言

```
<script>
// Javascript implementation of the
// above approach

// Function for the binomial coefficient
function binomialCoeff(n, k)
{

    var C = new Array(n + 1);
    // Loop to create 2D array using 1D array
    for (var i = 0; i < C.length; i++) {
        C[i] = new Array(k + 1);
    }
    var i, j;

    // Calculate value of Binomial Coefficient
    // in bottom up manner
    for (i = 0; i <= n; i++) {
        for (j = 0; j <= Math.min(i, k); j++) {
            // Base Cases
            if (j == 0 || j == i)
                C[i][j] = 1;

            // Calculate value using previously
            // stored values
            else
                C[i][j] = C[i - 1][j - 1] + C[i - 1][j];
        }
    }

    return C[n][k];
}

// Function to return the count
// of valid subsequences
function cntSubSeq(arr, n, k)
{

    // Sort the array
    arr.sort();

    // Maximum among the minimum K elements
    var num = arr[k - 1];

    // Y will store the frequency of num
    // in the minimum K elements
    var Y = 0;
    for (var i = k - 1; i >= 0; i--) {
        if (arr[i] == num)
            Y+=1;
    }

    // cntX will store the frequency of
    // num in the complete array
    var cntX = Y;
    for (var i = k; i < n; i++) {
        if (arr[i] == num)
            cntX+=1;
    }

    return binomialCoeff(cntX, Y);
}

// Driver code
var arr = [ 1, 2, 3, 4 ];
var n = arr.length;
var k = 2;
document.write(cntSubSeq(arr, n, k));

// This code is contributed by ShubhamSingh10
</script>
```

**Output:** 

```
1
```