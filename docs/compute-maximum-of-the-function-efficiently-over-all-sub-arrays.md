# 在所有子阵列上有效计算函数的最大值

> 原文:[https://www . geeksforgeeks . org/compute-最大功能高效覆盖所有子阵列/](https://www.geeksforgeeks.org/compute-maximum-of-the-function-efficiently-over-all-sub-arrays/)

给定一个数组， **arr[]** 和一个函数 **F(i，j)** 。任务是计算所有子阵列[I]上的**最大值{F(i，j)}** ..j]。
函数 F()定义为:

**示例:**

> **输入:** arr[] = { 1，5，4，7 }
> **输出:** 6
> 所有子阵列的 F(i，j)值:
> { 1，5 } = | 1–5 | *(1)= 4
> { 1，5，4 } = | 1–5 | *(1)+| 5–4 | *(-1)= 3
> { 1，5，4， 7 } = | 1–5 | *(1)+| 5–4 | *(-1)+| 4–7 | *(1)= 6
> { 5，4 } = | 5–4 | *(1)= 1
> { 5，4，7 } = | 5–4 | *(1)+| 4–7 | *(-1)=-2
> { 4，7 } = | 4–7 | *(1)= 3
> 以上所有值的最大值= 6。
> 
> **输入:** arr[] = { 1，4，2，3，1 }
> **输出:** 3

**天真法**:天真法是遍历所有子数组，计算函数 F 在所有子数组上的最大值。

**高效方法**:更好的方法是分别考虑奇数和偶数 **l** 的 F(l，r)中的线段。为此，可以构建两个不同的阵列 **B[]和 C[]** ，从而:

```
B[i] = |arr[i] - arr[i + 1]| * (-1)<sup>i</sup>
C[i] = |arr[i] - arr[i + 1]| * (-1)<sup>i + 1</sup>
```

现在如果我们仔细观察，只需要找到阵列 B[]和 C[]的[最大和子阵列](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)，函数的最终答案将是两个阵列中的最大值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>

#define MAX 100005

using namespace std;

// Function to return maximum sum of a sub-array
int kadaneAlgorithm(const int* ar, int n)
{
    int sum = 0, maxSum = 0;

    for (int i = 0; i < n; i++) {

        sum += ar[i];

        if (sum < 0)
            sum = 0;

        maxSum = max(maxSum, sum);
    }

    return maxSum;
}

// Function to return maximum value of function F
int maxFunction(const int* arr, int n)
{

    int b[MAX], c[MAX];

    // Compute arrays B[] and C[]
    for (int i = 0; i < n - 1; i++) {
        if (i & 1) {
            b[i] = abs(arr[i + 1] - arr[i]);
            c[i] = -b[i];
        }
        else {
            c[i] = abs(arr[i + 1] - arr[i]);
            b[i] = -c[i];
        }
    }

    // Find maximum sum sub-array of both of the
    // arrays and take maximum among them
    int ans = kadaneAlgorithm(b, n - 1);
    ans = max(ans, kadaneAlgorithm(c, n - 1));

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 5, 4, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxFunction(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int MAX = 100005;

// Function to return maximum sum of a sub-array
static int kadaneAlgorithm(int[] ar, int n)
{
    int sum = 0, maxSum = 0;

    for (int i = 0; i < n; i++)
    {
        sum += ar[i];

        if (sum < 0)
            sum = 0;

        maxSum = Math.max(maxSum, sum);
    }

    return maxSum;
}

// Function to return maximum value
// of function F
static int maxFunction(int[] arr, int n)
{

    int []b = new int[MAX];
    int []c = new int[MAX];

    // Compute arrays B[] and C[]
    for (int i = 0; i < n - 1; i++)
    {
        if (i % 2 == 1)
        {
            b[i] = Math.abs(arr[i + 1] - arr[i]);
            c[i] = -b[i];
        }
        else
        {
            c[i] = Math.abs(arr[i + 1] - arr[i]);
            b[i] = -c[i];
        }
    }

    // Find maximum sum sub-array of both of the
    // arrays and take maximum among them
    int ans = kadaneAlgorithm(b, n - 1);
    ans = Math.max(ans, kadaneAlgorithm(c, n - 1));

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 5, 4, 7 };
    int n = arr.length;
    System.out.println(maxFunction(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
MAX = 100005;

# Function to return maximum
# sum of a sub-array
def kadaneAlgorithm(ar, n) :

    sum = 0; maxSum = 0;

    for i in range(n) :

        sum += ar[i];

        if (sum < 0) :
            sum = 0;

        maxSum = max(maxSum, sum);

    return maxSum;

# Function to return maximum
# value of function F
def maxFunction(arr, n) :

    b = [0] * MAX;
    c = [0] * MAX;

    # Compute arrays B[] and C[]
    for i in range(n - 1) :
        if (i & 1) :
            b[i] = abs(arr[i + 1] - arr[i]);
            c[i] = -b[i];

        else :
            c[i] = abs(arr[i + 1] - arr[i]);
            b[i] = -c[i];

    # Find maximum sum sub-array of both of the
    # arrays and take maximum among them
    ans = kadaneAlgorithm(b, n - 1);
    ans = max(ans, kadaneAlgorithm(c, n - 1));

    return ans;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 5, 4, 7 ];
    n = len(arr)

    print(maxFunction(arr, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MAX = 100005;

// Function to return maximum sum of a sub-array
static int kadaneAlgorithm(int[] ar, int n)
{
    int sum = 0, maxSum = 0;

    for (int i = 0; i < n; i++)
    {
        sum += ar[i];

        if (sum < 0)
            sum = 0;

        maxSum = Math.Max(maxSum, sum);
    }

    return maxSum;
}

// Function to return maximum value
// of function F
static int maxFunction(int[] arr, int n)
{
    int []b = new int[MAX];
    int []c = new int[MAX];

    // Compute arrays B[] and C[]
    for (int i = 0; i < n - 1; i++)
    {
        if (i % 2 == 1)
        {
            b[i] = Math.Abs(arr[i + 1] - arr[i]);
            c[i] = -b[i];
        }
        else
        {
            c[i] = Math.Abs(arr[i + 1] - arr[i]);
            b[i] = -c[i];
        }
    }

    // Find maximum sum sub-array of both of the
    // arrays and take maximum among them
    int ans = kadaneAlgorithm(b, n - 1);
    ans = Math.Max(ans, kadaneAlgorithm(c, n - 1));

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 5, 4, 7 };
    int n = arr.Length;
    Console.WriteLine(maxFunction(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach
const MAX = 100005;

// Function to return maximum sum of a sub-array
function kadaneAlgorithm(ar, n)
{
    let sum = 0, maxSum = 0;

    for(let i = 0; i < n; i++)
    {
        sum += ar[i];

        if (sum < 0)
            sum = 0;

        maxSum = Math.max(maxSum, sum);
    }
    return maxSum;
}

// Function to return maximum
// value of function F
function maxFunction(arr, n)
{
    let b = new Array(MAX),
        c = new Array(MAX);

    // Compute arrays B[] and C[]
    for(let i = 0; i < n - 1; i++)
    {
        if (i & 1)
        {
            b[i] = Math.abs(arr[i + 1] -
                            arr[i]);
            c[i] = -b[i];
        }
        else
        {
            c[i] = Math.abs(arr[i + 1] -
                            arr[i]);
            b[i] = -c[i];
        }
    }

    // Find maximum sum sub-array of both of the
    // arrays and take maximum among them
    let ans = kadaneAlgorithm(b, n - 1);
    ans = Math.max(ans,
          kadaneAlgorithm(c, n - 1));

    return ans;
}

// Driver code
let arr = [ 1, 5, 4, 7 ];
let n = arr.length;

document.write(maxFunction(arr, n));

// This code is contributed by Manoj.

</script>
```

**Output:** 

```
6
```