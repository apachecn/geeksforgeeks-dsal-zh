# 求最小数 K，使得乘以 K 后的数组之和超过 S

> 原文:[https://www . geeksforgeeks . org/find-最小数-k-so-k 乘 k 后的数组和-over-s/](https://www.geeksforgeeks.org/find-minimum-number-k-such-that-sum-of-array-after-multiplication-by-k-exceed-s/)

给定一个由 **N** 元素组成的数组**arr【】**和一个整数 **S** ，任务是在将所有元素乘以 **K** 后，找到最小数量 **K** ，使得数组元素的总和不超过 **S** 。
**示例:**

> **输入:** arr[] = { 1 }，S = 50
> **输出:** 51
> **说明:**
> 数组元素之和为 1。
> 现在 1 与 51 相乘得到 51，也就是> 50。
> 因此 K 的最小值为 51。
> **输入:** arr[] = { 10，7，8，10，12，19 }，S = 200
> **输出:** 4
> **说明:**
> 数组元素之和为 66。
> 现在 66 与 4 相乘得到 256 > 200。
> 因此 K 的最小值为 4。

**进场:**

*   求数组所有元素的[和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)，存储在变量**和**中。
*   取 [**上限**](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/) 除以(S + 1)之和。这将是所需的最小值 k。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum value of k
// that satisfies the given condition
int findMinimumK(int a[], int n, int S)
{
    // store sum of array elements
    int sum = 0;

    // Calculate the sum after
    for (int i = 0; i < n; i++) {
        sum += a[i];
    }

    // return minimum possible K
    return ceil(((S + 1) * 1.0)
                / (sum * 1.0));
}

// Driver code
int main()
{
    int a[] = { 10, 7, 8, 10, 12, 19 };
    int n = sizeof(a) / sizeof(a[0]);
    int S = 200;

    cout << findMinimumK(a, n, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.lang.Math;

class GFG {

// Function to return the minimum value of k
// that satisfies the given condition
static int findMinimumK(int a[], int n, int S)
{

    // Store sum of array elements
    int sum = 0;

    // Calculate the sum after
    for (int i = 0; i < n; i++)
    {
        sum += a[i];
    }

    // Return minimum possible K
    return (int) Math.ceil(((S + 1) * 1.0) /
                               (sum * 1.0));
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 10, 7, 8, 10, 12, 19 };
    int n = a.length;
    int S = 200;
    System.out.print(findMinimumK(a, n, S));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function to return the minimum value of k
# that satisfies the given condition
def findMinimumK(a, n, S) :

    # store sum of array elements
    sum = 0

    # Calculate the sum after
    for i in range(0,n):
        sum += a[i]

    # return minimum possible K
    return math.ceil(((S + 1) * 1.0)/(sum * 1.0))

# Driver code
a = [ 10, 7, 8, 10, 12, 19 ]
n = len(a)
s = 200
print(findMinimumK(a, n, s))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

// Function to return the minimum value of k
// that satisfies the given condition
static int findMinimumK(int []a, int n, int S)
{

    // Store sum of array elements
    int sum = 0;

    // Calculate the sum after
    for(int i = 0; i < n; i++)
    {
       sum += a[i];
    }

    // Return minimum possible K
    return (int) Math.Ceiling(((S + 1) * 1.0) /
                                  (sum * 1.0));
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 10, 7, 8, 10, 12, 19 };
    int n = a.Length;
    int S = 200;

    Console.Write(findMinimumK(a, n, S));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the minimum value of k
    // that satisfies the given condition
    function findMinimumK(a, n, S)
    {
        // store sum of array elements
        let sum = 0;

        // Calculate the sum after
        for (let i = 0; i < n; i++) {
            sum += a[i];
        }

        // return minimum possible K
        return Math.ceil(((S + 1) * 1.0) / (sum * 1.0));
    }

    let a = [ 10, 7, 8, 10, 12, 19 ];
    let n = a.length;
    let S = 200;

    document.write(findMinimumK(a, n, S));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*
***空间复杂度:** O(1)*