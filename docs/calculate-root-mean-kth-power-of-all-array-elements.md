# 计算所有数组元素的根平均 k 次方

> 原文:[https://www . geeksforgeeks . org/calculate-root-mean-kth-所有数组元素的幂/](https://www.geeksforgeeks.org/calculate-root-mean-kth-power-of-all-array-elements/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **K** ，任务是计算所有数组元素的**K**次幂的[算术平均值](https://www.geeksforgeeks.org/arithmetic-mean/)的 K <sup>次</sup>根。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 2
> **输出:** 3.31662
> **解释:**
> 数组元素的所有 K <sup>次</sup>次幂的和= 1 + 4 + 9 + 16 + 25 = 55
> 数组元素的根均值 K <sup>次</sup>次幂的值= √(55 / 5) = √11 = 3
> 
> **输入:** arr[] = {10，4，6，8}，K = 3
> T3】输出: 7.34847

**方法:**数组元素的 **K <sup>次</sup>次**次幂的根均值由下式给出:

> ![\sqrt[k]{\frac{arr_{1}^{k} + arr_{2}^{k} + arr_{2}^{k} + ..... arr_{n}^{k}}{n}}        ](img/0dd44506330abb5f7cbe72b84704d7ac.png "Rendered by QuickLaTeX.com")

因此，思路是计算每个阵元的 **K <sup>次方</sup>次方**。然后，找到那些元素的**算术平均值**。最后，计算计算平均值的 **K <sup>th</sup> 根**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the Nth root
double nthRoot(int A, int N)
{
    // Initially guessing random
    // numberbetween 0 and 9
    double xPre = rand() % 10;

    // Smaller eps for more accuracy
    double eps = 1e-3;

    // Initialize difference between
    // the two roots by INT_MAX
    double delX = INT_MAX;

    // xK denotes current value of x
    double xK;

    // Iterate until desired
    // accuracy is reached
    while (delX > eps) {

        // Find the current value
        // from previous value by
        // newton's method
        xK = ((N - 1.0) * xPre
              + (double)A / pow(xPre, N - 1))
             / (double)N;

        delX = abs(xK - xPre);
        xPre = xK;
    }

    return xK;
}

// Function to calculate the Root
// Mean kth power of array elements
float RMNValue(int arr[], int n, int k)
{
    int Nth = 0;

    float mean = 0.0, root = 0.0;

    // Calculate sum of kth power
    for (int i = 0; i < n; i++) {
        Nth += pow(arr[i], k);
    }

    // Calculate Mean
    mean = (Nth / (float)(n));

    // Calculate kth Root of mean
    root = nthRoot(mean, k);

    return root;
}

// Driver Code
int main()
{
    int arr[] = { 10, 4, 6, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;

    // Function Call
    cout << RMNValue(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
class GFG{

// Function to find the
  // Nth root
static double nthRoot(int A,
                      int N)
{
  // Initially guessing random
  // numberbetween 0 and 9
  double xPre = (Math.random() * 10) % 10;

  // Smaller eps for more accuracy
  double eps = 1e-3;

  // Initialize difference between
  // the two roots by Integer.MAX_VALUE
  double delX = Integer.MAX_VALUE;

  // xK denotes current value of x
  double xK = 0;

  // Iterate until desired
  // accuracy is reached
  while (delX > eps)
  {
    // Find the current value
    // from previous value by
    // newton's method
    xK = ((N - 1.0) * xPre +
          (double)A /
          Math.pow(xPre, N - 1)) /
          (double)N;

    delX = Math.abs(xK - xPre);
    xPre = xK;
  }

  return xK;
}

// Function to calculate the Root
// Mean kth power of array elements
static float RMNValue(int arr[],
                      int n, int k)
{
  int Nth = 0;
  float mean = 0, root = 0;

  // Calculate sum of kth power
  for (int i = 0; i < n; i++)
  {
    Nth += Math.pow(arr[i], k);
  }

  // Calculate Mean
  mean = (Nth / (float)(n));

  // Calculate kth Root of mean
  root = (float) nthRoot((int)mean, k);

  return root;
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {10, 4, 6, 8};
  int N = arr.length;
  int K = 3;

  // Function Call
  System.out.print(RMNValue(arr, N, K));

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
import sys
import random

# Function to find
# the Nth root
def nthRoot(A, N):

    # Initially guessing random
    # numberbetween 0 and 9
    xPre = random.random() % 10

    # Smaller eps for
    # more accuracy
    eps = 1e-3

    # Initialize difference between
    # the two roots by INT_MAX
    delX = sys.maxsize

    # xK denotes current
    # value of x
    xK = 0

    # Iterate until desired
    # accuracy is reached
    while (delX > eps):

        # Find the current value
        # from previous value by
        # newton's method
        xK = (((N - 1.0) * xPre +
                A / pow(xPre, N - 1)) / N)
        delX = abs(xK - xPre)
        xPre = xK

    return xK

# Function to calculate the Root
# Mean kth power of array elements
def RMNValue(arr, n, k):

    Nth = 0
    mean = 0.0
    root = 0.0

    # Calculate sum of kth power
    for i in range (n):
        Nth += pow(arr[i], k)

    # Calculate Mean
    mean = (Nth // (n))

    # Calculate kth Root of mean
    root = nthRoot(mean, k)

    return root

# Driver Code
if __name__ == "__main__":

    arr = [10, 4, 6, 8 ]
    N = len(arr)
    K = 3

    # Function Call
    print ( RMNValue(arr, N, K))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach 
using System;

class GFG{

// Function to find the
// Nth root
static double nthRoot(int A, int N)
{

    // Instantiate random number generator
    Random rand = new Random();

    // Initially guessing random
    // numberbetween 0 and 9
    double xPre = (rand.Next() * 10) % 10;

    // Smaller eps for more accuracy
    double eps = 1e-3;

    // Initialize difference between
    // the two roots by Integer.MAX_VALUE
    double delX = Int32.MaxValue;

    // xK denotes current value of x
    double xK = 0;

    // Iterate until desired
    // accuracy is reached
    while (delX > eps)
    {

        // Find the current value
        // from previous value by
        // newton's method
        xK = ((N - 1.0) * xPre +
              (double)A /
              Math.Pow(xPre, N - 1)) /
              (double)N;

        delX = Math.Abs(xK - xPre);
        xPre = xK;
    }
    return xK;
}

// Function to calculate the Root
// Mean kth power of array elements
static float RMNValue(int[] arr, int n,
                                 int k)
{
    int Nth = 0;
    float mean = 0, root = 0;

    // Calculate sum of kth power
    for(int i = 0; i < n; i++)
    {
        Nth += (int)Math.Pow(arr[i], k);
    }

    // Calculate Mean
    mean = (Nth / (float)(n));

    // Calculate kth Root of mean
    root = (float)nthRoot((int)mean, k);

    return root;
}

// Driver Code
public static void Main()
{
    int[] arr = { 10, 4, 6, 8 };
    int N = arr.Length;
    int K = 3;

    // Function call
    Console.Write(RMNValue(arr, N, K));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript program for the above approach 

// Function to find the
// Nth root
function nthRoot(A, N)
{

    // Initially guessing random
    // numberbetween 0 and 9
    var xPre = (Math.random() * 10) % 10;

    // Smaller eps for more accuracy
    var eps = 1e-3;

    // Initialize difference between
    // the two roots by Integer.MAX_VALUE
    var delX = Number.MAX_VALUE;

    // xK denotes current value of x
    var xK = 0;

    // Iterate until desired
    // accuracy is reached
    while (delX > eps)
    {

        // Find the current value
        // from previous value by
        // newton's method
        xK = ((N - 1.0) * xPre + A /
              Math.pow(xPre, N - 1)) / N;

        delX = Math.abs(xK - xPre);
        xPre = xK;
    }
    return xK;
}

// Function to calculate the Root
// Mean kth power of array elements
function RMNValue(arr, n, k)
{
    var Nth = 0;
    var mean = 0, root = 0;

    // Calculate sum of kth power
    for(var i = 0; i < n; i++)
    {
        Nth += Math.pow(arr[i], k);
    }

    // Calculate Mean
    mean = (Nth / (n));

    // Calculate kth Root of mean
    root = nthRoot(mean, k);

    return root;
}

// Driver Code
var arr = [ 10, 4, 6, 8 ];
var N = arr.length;
var K = 3;

// Function Call
document.write(RMNValue(arr, N, K));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
7.65172
```

***时间复杂度:** O(N*log(sum))，其中**之和为数组中所有给定数字的**平方的**之和。*
***辅助空间:** O(1)*