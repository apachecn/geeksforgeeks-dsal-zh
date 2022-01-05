# 从给定阵列的四个元素组中获得的最小和

> 原文:[https://www . geeksforgeeks . org/从给定数组的四个元素组中获得的最小和/](https://www.geeksforgeeks.org/minimum-sum-obtained-from-groups-of-four-elements-from-the-given-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，其中 **N % 4 = 0** ，任务是将这些整数分成四个一组，这样当取所有组中最大两个元素的总和时，它是最小可能的。打印最小化总和。
**举例:**

> **输入:** arr[] = {1，1，2，2}
> **输出:** 4
> 唯一的组将是{1，1，2，2}。
> 2 + 2 = 4
> **输入:** arr[] = {1，1，10，2，2，1，8}
> **输出:** 21
> {1，1，2，1}和{10，2，2，8}是将
> 给出最小和为 1 + 2 + 10 + 8 = 21 的组。

**方法:**为了最小化和，数组中最大的四个元素必须在同一个组中，因为最大的两个元素无论是哪个组的一部分，都肯定会包含在和中，但是如果它们是该组的一部分，则可以防止接下来的两个最大元素。以同样的方式分组，将给出最小可能的总和。因此，按降序对数组进行排序，从第一个元素开始，形成由四个连续元素组成的组。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum required sum
int minSum(int arr[], int n)
{

    // To store the required sum
    int sum = 0;

    // Sort the array in descending order
    sort(arr, arr + n, greater<int>());
    for (int i = 0; i < n; i++) {

        // The indices which give 0 or 1 as
        // the remainder when divided by 4
        // will be the maximum two
        // elements of the group
        if (i % 4 < 2)
            sum = sum + arr[i];
    }

    return sum;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 10, 2, 2, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the minimum required sum
static int minSum(Integer arr[], int n)
{

    // To store the required sum
    int sum = 0;

    // Sort the array in descending order
    Arrays.sort(arr, Collections.reverseOrder());
    for (int i = 0; i < n; i++)
    {

        // The indices which give 0 or 1 as
        // the remainder when divided by 4
        // will be the maximum two
        // elements of the group
        if (i % 4 < 2)
            sum = sum + arr[i];
    }

    return sum;
}

// Driver code
public static void main(String[] args)
{
    Integer []arr = { 1, 1, 10, 2, 2, 2, 1 };
    int n = arr.length;

    System.out.println(minSum(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum required sum
def minSum(arr, n) :

    # To store the required sum
    sum = 0;

    # Sort the array in descending order
    arr.sort(reverse = True)

    for i in range(n) :

        # The indices which give 0 or 1 as
        # the remainder when divided by 4
        # will be the maximum two
        # elements of the group
        if (i % 4 < 2) :
            sum += arr[i];

    return sum;

# Driver code
if __name__ == "__main__" :
    arr = [ 1, 1, 10, 2, 2, 2, 1 ];
    n = len(arr);
    print(minSum(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;            

class GFG
{

// Function to return the minimum required sum
static int minSum(int []arr, int n)
{

    // To store the required sum
    int sum = 0;

    // Sort the array in descending order
    Array.Sort(arr);
    Array.Reverse(arr);
    for (int i = 0; i < n; i++)
    {

        // The indices which give 0 or 1 as
        // the remainder when divided by 4
        // will be the maximum two
        // elements of the group
        if (i % 4 < 2)
            sum = sum + arr[i];
    }
    return sum;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 1, 10, 2, 2, 2, 1 };
    int n = arr.Length;

    Console.WriteLine(minSum(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum required sum
function minSum(arr, n)
{

    // To store the required sum
    let sum = 0;

    // Sort the array in descending order
    arr.sort(function(a, b){return b-a});
    for (let i = 0; i < n; i++) {

        // The indices which give 0 or 1 as
        // the remainder when divided by 4
        // will be the maximum two
        // elements of the group
        if (i % 4 < 2)
            sum = sum + arr[i];
    }

    return sum;
}

// Driver code
    let arr = [ 1, 1, 10, 2, 2, 2, 1 ];
    let n = arr.length;

    document.write(minSum(arr, n));

</script>
```

**Output:** 

```
14
```