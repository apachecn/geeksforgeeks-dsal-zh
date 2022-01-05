# 最大比率连续子阵列

> 原文:[https://www . geeksforgeeks . org/最大比率-连续-subarray/](https://www.geeksforgeeks.org/largest-ratio-contiguous-subarray/)

给定一个由 **N** 个数字组成的数组 **arr[]** ，任务是从给定的数组中找到最大比例的[邻接子数组](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)。

**示例:**

> **输入:** arr = { -1，10，0.1，-8，-2 }
> **输出:** 100
> **解释:**
> 子阵{10，0.1}给出 10 / 0.1 = 100 哪个比例最大。
> 
> **输入:** arr = { 2，2，4，-0.2，-1 }
> **输出:** 20
> **解释:**
> 子阵{4，-0.2，-1 }的最大比值为 20。

**方法:**思路是[生成阵列的所有子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，对于每个子阵，求子阵的比值为 arr[i] / arr[i+1] / arr[i+2]等等。记录最大比率，并在最后返回。
以下是上述办法的实施情况:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return maximum
// of two double values
double maximum(double a, double b)
{
    // Check if a is greater
    // than b then return a
    if (a > b)
        return a;

    return b;
}

// Function that returns the
// Ratio of max Ratio subarray
double maxSubarrayRatio(
  double arr[], int n)
{

    // Variable to store
    // the maximum ratio
    double maxRatio = INT_MIN;

    // Compute the product while
    // traversing for subarrays
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {

            double ratio = arr[i];

            for (int k = i + 1; k <= j; k++) {

                // Calculate the ratio
                ratio = ratio / arr[k];
            }

            // Update max ratio
            maxRatio = maximum(maxRatio, ratio);
        }
    }

    // Print the answer
    return maxRatio;
}

// Driver code
int main()
{
    double arr[] = { 2, 2, 4, -0.2, -1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxSubarrayRatio(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to return maximum
// of two double values
static double maximum(double a, double b)
{

    // Check if a is greater
    // than b then return a
    if (a > b)
        return a;

    return b;
}

// Function that returns the
// Ratio of max Ratio subarray
static double maxSubarrayRatio(double arr[],
                               int n)
{

    // Variable to store
    // the maximum ratio
    double maxRatio = Integer.MIN_VALUE;

    // Compute the product while
    // traversing for subarrays
    for(int i = 0; i < n; i++)
    {
        for(int j = i; j < n; j++)
        {
            double ratio = arr[i];

            for(int k = i + 1; k <= j; k++)
            {

                // Calculate the ratio
                ratio = ratio / arr[k];
            }

            // Update max ratio
            maxRatio = maximum(maxRatio, ratio);
        }
    }

    // Print the answer
    return maxRatio;
}

// Driver code   
public static void main(String[] args)
{
    double arr[] = { 2, 2, 4, -0.2, -1 };
    int n = arr.length;

    System.out.println(maxSubarrayRatio(arr, n));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to return maximum
# of two double values
def maximum(a, b):

    # Check if a is greater
    # than b then return a
    if (a > b):
        return a

    return b

# Function that returns the
# Ratio of max Ratio subarray
def maxSubarrayRatio(arr, n):

    # Variable to store
    # the maximum ratio
    maxRatio = -sys.maxsize - 1

    # Compute the product while
    # traversing for subarrays
    for i in range(n):
        for j in range(i, n):
            ratio = arr[i]

            for k in range(i + 1, j + 1):

                # Calculate the ratio
                ratio = ratio // arr[k]

            # Update max ratio
            maxRatio = maximum(maxRatio, ratio)

    # Print the answer
    return int(maxRatio)

# Driver code
if __name__ == "__main__":

    arr = [ 2, 2, 4, -0.2, -1 ]
    n = len(arr)

    print(maxSubarrayRatio(arr, n))

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to return maximum
// of two double values
static double maximum(double a, double b)
{

    // Check if a is greater
    // than b then return a
    if (a > b)
        return a;

    return b;
}

// Function that returns the
// Ratio of max Ratio subarray
static double maxSubarrayRatio(double []arr,
                               int n)
{

    // Variable to store
    // the maximum ratio
    double maxRatio = int.MinValue;

    // Compute the product while
    // traversing for subarrays
    for(int i = 0; i < n; i++)
    {
        for(int j = i; j < n; j++)
        {
            double ratio = arr[i];

            for(int k = i + 1; k <= j; k++)
            {

                // Calculate the ratio
                ratio = ratio / arr[k];
            }

            // Update max ratio
            maxRatio = maximum(maxRatio, ratio);
        }
    }

    // Print the answer
    return maxRatio;
}

// Driver code
public static void Main(String[] args)
{
    double []arr = { 2, 2, 4, -0.2, -1 };
    int n = arr.Length;

    Console.WriteLine(maxSubarrayRatio(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return maximum
// of two double values
function maximum(a, b)
{

    // Check if a is greater
    // than b then return a
    if (a > b)
        return a;

    return b;
}

// Function that returns the
// Ratio of max Ratio subarray
function maxSubarrayRatio(arr, n)
{

    // Variable to store
    // the maximum ratio
    var maxRatio = -1000000000;

    // Compute the product while
    // traversing for subarrays
    for (var i = 0; i < n; i++)
    {
        for (var j = i; j < n; j++)
        {

            var ratio = arr[i]; 
            for (var k = i + 1; k <= j; k++)
            {

                // Calculate the ratio
                ratio = ratio / arr[k];
            }

            // Update max ratio
            maxRatio = maximum(maxRatio, ratio);
        }
    }

    // Print the answer
    return maxRatio;
}

// Driver code
var arr = [ 2, 2, 4, -0.2, -1 ];
var n = arr.length;
document.write( maxSubarrayRatio(arr, n));

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
20
```

***时间复杂度:** (N <sup>3</sup> )*
***辅助空间:** O(1)*