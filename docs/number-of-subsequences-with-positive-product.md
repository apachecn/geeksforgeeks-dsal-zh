# 乘积为正的子序列数

> 原文:[https://www . geeksforgeeks . org/带正积的子序列数/](https://www.geeksforgeeks.org/number-of-subsequences-with-positive-product/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找出数组中所有具有正积的子序列的计数。

**示例:**

> **输入:** arr[] = {2，-3，-1}
> **输出:** 3
> {2}、{-3，-1}和{2，-3，-1}是唯一可能的子序列。
> 
> **输入:** arr[] = {2，3，-1，4，5}
> **输出:** 15

**天真方法:**生成数组的所有子序列，并计算所有子序列的乘积。如果产品为正，则按 **1** 递增计数。

**高效方法:**

1.  计算数组中正负元素的数量。
2.  可以为子序列选择任意数量的正元素，以保持正乘积。具有所有正元素的子序列的不同组合的数量将是**次方(2，正元素的计数)**。
3.  可以为子序列选择偶数个负元素，以保持正乘积。具有偶数个负元素的子序列的不同组合的数量将是**次方(2，负元素的计数–1)**。
4.  之后，从空子序列的结果中删除 **1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of all
// the subsequences with positive product
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

    // For the empty subsequence
    result -= 1;

    return result;
}

// Driver code
int main()
{
    int arr[] = { 2, -3, -1, 4 };
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
// the subsequences with positive product
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

    // For the empty subsequence
    result -= 1;

    return result;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, -3, -1, 4 };
    int n = arr.length;

    System.out.print(cntSubSeq(arr, n));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
import math

# Function to return the count of all
# the subsequences with positive product
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

    # For the empty subsequence
    result -= 1

    return result

# Driver code
arr = [ 2, -3, -1, 4 ]
n = len (arr);

print (cntSubSeq(arr, n))

# This code is contributed by ANKITKUMAR34
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count of all
    // the subsequences with positive product
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

        // For the empty subsequence
        result -= 1;

        return result;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 2, -3, -1, 4 };
        int n = arr.Length;

        Console.Write(cntSubSeq(arr, n));

    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the count of all
// the subsequences with positive product
function cntSubSeq(arr, n) {
    // To store the count of positive
    // elements in the array
    let pos_count = 0;

    // To store the count of negative
    // elements in the array
    let neg_count = 0;

    let result;

    for (let i = 0; i < n; i++) {

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

    // For the empty subsequence
    result -= 1;

    return result;
}

// Driver code

let arr = [2, -3, -1, 4];
let n = arr.length;

document.write(cntSubSeq(arr, n));
</script>
```

**Output:** 

```
7
```

**时间复杂度:** O(n)