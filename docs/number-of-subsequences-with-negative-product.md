# 负积子序列数

> 原文:[https://www . geeksforgeeks . org/负积子序列数/](https://www.geeksforgeeks.org/number-of-subsequences-with-negative-product/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找出数组中所有具有负乘积的子序列的计数。

**示例:**

> **输入:** arr[] = {1，-5，-6}
> **输出:** 4
> **解释**
> {-5}、{-6}、{1，-5}和{1，-6}是唯一可能的子序列
> 
> **输入:** arr[] = {2，3，1}
> **输出:** 0
> **解释**
> 不存在负积的可能子序列

**天真方法:**
生成数组的所有子序列，并计算所有子序列的乘积。如果乘积为负，则计数增加 1。

**有效方法:**

*   计算数组中正负元素的数量
*   可以为子序列选择奇数个负元素，以保持负乘积。具有奇数个负元素的子序列的不同组合的数量将是**次方(2，负元素的计数–1)**
*   可以为子序列选择任意数量的正元素，以保持负乘积。具有所有正元素的子序列的不同组合的数量将是**次方(2，正元素的计数)**

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of all
// the subsequences with negative product
int cntSubSeq(int arr[], int n)
{
    // To store the count of positive
    // elements in the array
    int pos_count = 0;

    // To store the count of negative
    // elements in the array
    int neg_count = 0;

    int result;

    for (int i = 0; i < n; i++) {

        // If the current element
        // is positive
        if (arr[i] > 0)
            pos_count++;

        // If the current element
        // is negative
        if (arr[i] < 0)
            neg_count++;
    }

    // For all the positive
    // elements of the array
    result = pow(2, pos_count);

    // For all the negative
    // elements of the array
    if (neg_count > 0)
        result *= pow(2, neg_count - 1);
    else
        result = 0;

    return result;
}

// Driver code
int main()
{
    int arr[] = { 3, -4, -1, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << cntSubSeq(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count of all
// the subsequences with negative product
static int cntSubSeq(int arr[], int n)
{
    // To store the count of positive
    // elements in the array
    int pos_count = 0;

    // To store the count of negative
    // elements in the array
    int neg_count = 0;

    int result;

    for (int i = 0; i < n; i++)
    {

        // If the current element
        // is positive
        if (arr[i] > 0)
            pos_count++;

        // If the current element
        // is negative
        if (arr[i] < 0)
            neg_count++;
    }

    // For all the positive
    // elements of the array
    result = (int) Math.pow(2, pos_count);

    // For all the negative
    // elements of the array
    if (neg_count > 0)
        result *= Math.pow(2, neg_count - 1);
    else
        result = 0 ;

    return result;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3,-4, -1, 6 };
    int n = arr.length;

    System.out.print(cntSubSeq(arr, n));
}
}

// This code is contributed by ANKITKUMAR34
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
import math

# Function to return the count of all
# the subsequences with negative product
def cntSubSeq(arr, n):

    # To store the count of positive
    # elements in the array
    pos_count = 0;

    # To store the count of negative
    # elements in the array
    neg_count = 0

    for i in range (n):

        # If the current element
        # is positive
        if (arr[i] > 0) :
            pos_count += 1

        # If the current element
        # is negative
        if (arr[i] < 0):
            neg_count += 1

    # For all the positive
    # elements of the array
    result = int(math.pow(2, pos_count))

    # For all the negative
    # elements of the array
    if (neg_count > 0):
        result *= int(math.pow(2, neg_count - 1))
    else:
        result = 0

    return result

# Driver code
arr = [ 2, -3, -1, 4 ]
n = len (arr);

print (cntSubSeq(arr, n))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of all
// the subsequences with negative product
static int cntSubSeq(int []arr, int n)
{
    // To store the count of positive
    // elements in the array
    int pos_count = 0;

    // To store the count of negative
    // elements in the array
    int neg_count = 0;

    int result;

    for (int i = 0; i < n; i++)
    {

        // If the current element
        // is positive
        if (arr[i] > 0)
            pos_count++;

        // If the current element
        // is negative
        if (arr[i] < 0)
            neg_count++;
    }

    // For all the positive
    // elements of the array
    result = (int) Math.Pow(2, pos_count);

    // For all the negative
    // elements of the array
    if (neg_count > 0)
        result *= (int)Math.Pow(2, neg_count - 1);
    else
        result = 0 ;

    return result;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3,-4, -1, 6 };
    int n = arr.Length;

    Console.Write(cntSubSeq(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of all
// the subsequences with negative product
function cntSubSeq(arr, n)
{

    // To store the count of positive
    // elements in the array
    var pos_count = 0;

    // To store the count of negative
    // elements in the array
    var neg_count = 0;

    var result;

    for(var i = 0; i < n; i++)
    {

        // If the current element
        // is positive
        if (arr[i] > 0)
            pos_count++;

        // If the current element
        // is negative
        if (arr[i] < 0)
            neg_count++;
    }

    // For all the positive
    // elements of the array
    result = Math.pow(2, pos_count);

    // For all the negative
    // elements of the array
    if (neg_count > 0)
        result *= Math.pow(2, neg_count - 1);
    else
        result = 0;

    return result;
}

// Driver code
var arr = [ 3, -4, -1, 6 ];
var n = arr.length;

document.write(cntSubSeq(arr, n));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
8
```

**时间复杂度:** O(n)
**另一种方法:**
我们也可以通过从**子序列总数**中减去**正子序列总数**来计算负积子序列的数量。
使用本文中讨论的方法来寻找具有正积的子序列的总数。