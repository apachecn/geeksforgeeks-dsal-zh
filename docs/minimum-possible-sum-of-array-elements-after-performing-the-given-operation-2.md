# 执行给定操作后阵列元素的最小可能和

> 原文:[https://www . geeksforgeeks . org/执行给定操作后的最小可能数组元素总和-2/](https://www.geeksforgeeks.org/minimum-possible-sum-of-array-elements-after-performing-the-given-operation-2/)

给定一个大小为 **N** 的数组 **arr[]** 和一个数字 **X** 。如果数组的任何子数组(可能为空)arr[i]，arr[i+1]，…可以用 arr[I/x，arr[I+1/x，…]替换。任务是找到可以得到的数组的最小可能和。
**注意:**给定的操作只能执行一次。
**举例:**

> **输入:** N = 3，X = 2，arr[] = {1，-2，3}
> **输出:** 0.5
> **解释:**
> 在选择子阵列{3}并将其替换为{1.5}时，数组变为{1，-2，1.5}，这样就得出 sum = 0.5
> **输入:** N = 5，X = 5，arr[] = {5，5，5，5，5 }

**天真方法:**天真方法是用我们通过将其除以 **X** 得到的值替换所有可能的正子数组，并计算总和。但是任何给定阵列的子阵列总数是 **(N * (N + 1))/2** ，其中 N 是阵列的大小。所以这个算法的运行时间是 **O(N <sup>2</sup> )** 。
**高效途径:**这个问题可以在 O(N)时间内高效解决。仔细观察，可以推断出，如果被替换的子阵列满足以下条件，则和可以最小化:

1.  子阵列应该是正的。
2.  子阵列的总和应该最大。

因此，通过减少满足上述条件的子阵列，可以使总和最小。利用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)的微小变化就可以找到满足上述条件的子阵。
找到子阵的最大和后，可以从阵列的和中减去这个得到最小和。由于子阵列的最大和被最大和/ X 代替，这个因子可以被加到找到的和上。也就是:

```
Minimum sum = (sumOfArr - subSum) + (subSum/ X)
where sumOfArr is the sum of all elements of the array
and subSum is the maximum sum of the subarray.
```

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find the minimum possible sum
// of the array elements after performing
// the given operation
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
// of the sub array
double maxSubArraySum(double a[], int size)
{

    // max_so_far represents the maximum sum
    // found till now and max_ending_here
    // represents the maximum sum ending at
    // a specific index
    double max_so_far = INT_MIN,
           max_ending_here = 0;

    // Iterating through the array to find
    // the maximum sum of the subarray
    for (int i = 0; i < size; i++) {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        // If the maximum sum ending at a
        // specific index becomes less than 0,
        // then making it equal to 0.
        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to find the minimum possible sum
// of the array elements after performing
// the given operation
double minPossibleSum(double a[], int n, double x)
{
    double mxSum = maxSubArraySum(a, n);
    double sum = 0;

    // Finding the sum of the array
    for (int i = 0; i < n; i++) {
        sum += a[i];
    }

    // Computing the minimum sum of the array
    sum = sum - mxSum + mxSum / x;

    cout << setprecision(2) << sum << endl;
}

// Driver code
int main()
{
    int N = 3;
    double X = 2;
    double A[N] = { 1, -2, 3 };
    minPossibleSum(A, N, X);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum possible sum
// of the array elements after performing
// the given operation
class GFG{

// Function to find the maximum sum
// of the sub array
static double maxSubArraySum(double a[], int size)
{

    // max_so_far represents the maximum sum
    // found till now and max_ending_here
    // represents the maximum sum ending at
    // a specific index
    double max_so_far = Integer.MIN_VALUE,
           max_ending_here = 0;

    // Iterating through the array to find
    // the maximum sum of the subarray
    for (int i = 0; i < size; i++) {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        // If the maximum sum ending at a
        // specific index becomes less than 0,
        // then making it equal to 0.
        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to find the minimum possible sum
// of the array elements after performing
// the given operation
static void minPossibleSum(double a[], int n, double x)
{
    double mxSum = maxSubArraySum(a, n);
    double sum = 0;

    // Finding the sum of the array
    for (int i = 0; i < n; i++) {
        sum += a[i];
    }

    // Computing the minimum sum of the array
    sum = sum - mxSum + mxSum / x;

    System.out.print(sum +"\n");
}

// Driver code
public static void main(String[] args)
{
    int N = 3;
    double X = 2;
    double A[] = { 1, -2, 3 };
    minPossibleSum(A, N, X);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find the minimum possible sum
# of the array elements after performing
# the given operation

# Function to find the maximum sum
# of the sub array
def maxSubArraySum(a, size):

    # max_so_far represents the maximum sum
    # found till now and max_ending_here
    # represents the maximum sum ending at
    # a specific index
    max_so_far = -10**9
    max_ending_here = 0

    # Iterating through the array to find
    # the maximum sum of the subarray
    for i in range(size):
        max_ending_here = max_ending_here + a[i]
        if (max_so_far < max_ending_here):
            max_so_far = max_ending_here

        # If the maximum sum ending at a
        # specific index becomes less than 0,
        # then making it equal to 0.
        if (max_ending_here < 0):
            max_ending_here = 0
    return max_so_far

# Function to find the minimum possible sum
# of the array elements after performing
# the given operation
def minPossibleSum(a,n, x):
    mxSum = maxSubArraySum(a, n)
    sum = 0

    # Finding the sum of the array
    for i in range(n):
        sum += a[i]

    # Computing the minimum sum of the array
    sum = sum - mxSum + mxSum / x
    print(round(sum,2))

# Driver code
if __name__ == '__main__':
    N = 3
    X = 2
    A=[1, -2, 3]
    minPossibleSum(A, N, X)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the minimum possible sum
// of the array elements after performing
// the given operation
using System;

class GFG{

// Function to find the maximum sum
// of the sub array
static double maxSubArraySum(double[] a, int size)
{

    // max_so_far represents the maximum sum
    // found till now and max_ending_here
    // represents the maximum sum ending at
    // a specific index
    double max_so_far = Int32.MinValue,
           max_ending_here = 0;

    // Iterating through the array to find
    // the maximum sum of the subarray
    for (int i = 0; i < size; i++) {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        // If the maximum sum ending at a
        // specific index becomes less than 0,
        // then making it equal to 0.
        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to find the minimum possible sum
// of the array elements after performing
// the given operation
static void minPossibleSum(double[] a, int n, double x)
{
    double mxSum = maxSubArraySum(a, n);
    double sum = 0;

    // Finding the sum of the array
    for (int i = 0; i < n; i++) {
        sum += a[i];
    }

    // Computing the minimum sum of the array
    sum = sum - mxSum + mxSum / x;

    Console.Write(sum +"\n");
}

// Driver code
public static void Main()
{
    int N = 3;
    double X = 2;
    double[] A = { 1, -2, 3 };
    minPossibleSum(A, N, X);
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript program to find the minimum possible sum
// of the array elements after performing
// the given operation

// Function to find the maximum sum
// of the sub array
function maxSubArraySum( a, size)
{

    // max_so_far represents the maximum sum
    // found till now and max_ending_here
    // represents the maximum sum ending at
    // a specific index
    var max_so_far = -1000000000,
           max_ending_here = 0;

    // Iterating through the array to find
    // the maximum sum of the subarray
    for (var i = 0; i < size; i++) {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        // If the maximum sum ending at a
        // specific index becomes less than 0,
        // then making it equal to 0.
        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to find the minimum possible sum
// of the array elements after performing
// the given operation
function minPossibleSum(a, n, x)
{
    var mxSum = maxSubArraySum(a, n);
    var sum = 0;

    // Finding the sum of the array
    for (var i = 0; i < n; i++) {
        sum += a[i];
    }

    // Computing the minimum sum of the array
    sum = sum - mxSum + mxSum / x;

    document.write(sum);
}

// Driver code
var N = 3;
var X = 2;
var A = [ 1, -2, 3 ];
minPossibleSum(A, N, X);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
0.5
```

**时间复杂度:** O(N)

**辅助空间:** O(1)