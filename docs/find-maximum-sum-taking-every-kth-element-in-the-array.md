# 求数组中每第 Kth 个元素取的最大和

> 原文:[https://www . geesforgeks . org/find-max-sum-take-ever-kth-element-in-array/](https://www.geeksforgeeks.org/find-maximum-sum-taking-every-kth-element-in-the-array/)

给定一个整数数组 **arr[]** 和一个整数 **K** ，任务是找到每 K 个<sup>第</sup>个元素的最大和，即**和= arr[I]+arr[I+K]+arr[I+2 * K]+arr[I+3 * K]+……。arr[i + q * k]** 从任意 **i** 开始。
**举例:**

> **输入:** arr[] = {3，-5，6，3，10}，K = 3
> **输出:** 10
> 所有可能的顺序为:
> 3+3 = 6
> -5+10 = 5
> 6 = 6
> 3 = 3
> 10 = 10
> **输入:** arr[] = {3，6，4，7，2}，K = 2

****天真方法:**解决这个问题的思路是使用两个嵌套循环，从索引 **i** 开始，对每个 **K <sup>th</sup>** 元素进行求和，直到 **n** 为止，并从所有这些元素中找到最大值。该方法的时间复杂度为 **O(N <sup>2</sup> )**
以下是上述方法的实现:** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum sum for
// every possible sequence such that
// a[i] + a[i+k] + a[i+2k] + ... + a[i+qk]
// is maximized
int maxSum(int arr[], int n, int K)
{

    // Initialize the maximum with
    // the smallest value
    int maximum = INT_MIN;

    // Find maximum from all sequences
    for (int i = 0; i < n; i++) {

        int sumk = 0;

        // Sum of the sequence
        // starting from index i
        for (int j = i; j < n; j += K)
            sumk = sumk + arr[j];

        // Update maximum
        maximum = max(maximum, sumk);
    }

    return maximum;
}

// Driver code
int main()
{
    int arr[] = { 3, 6, 4, 7, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    cout << maxSum(arr, n, K);

    return (0);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum sum for
// every possible sequence such that
// a[i] + a[i+k] + a[i+2k] + ... + a[i+qk]
// is maximized
static int maxSum(int arr[], int n, int K)
{

    // Initialize the maximum with
    // the smallest value
    int maximum = Integer.MIN_VALUE;

    // Find maximum from all sequences
    for (int i = 0; i < n; i++)
    {

        int sumk = 0;

        // Sum of the sequence
        // starting from index i
        for (int j = i; j < n; j += K)
            sumk = sumk + arr[j];

        // Update maximum
        maximum = Math.max(maximum, sumk);
    }

    return maximum;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 6, 4, 7, 2 };
    int n = arr.length;
    int K = 2;

    System.out.println(maxSum(arr, n, K));
}
}

// This code is contributed by Code_Mech
```

## **蟒蛇 3**

```
# Python 3 implementation of the approach
import sys

# Function to return the maximum sum for
# every possible sequence such that
# a[i] + a[i+k] + a[i+2k] + ... + a[i+qk]
# is maximized
def maxSum(arr, n, K):

    # Initialize the maximum with
    # the smallest value
    maximum = -sys.maxsize - 1

    # Find maximum from all sequences
    for i in range(n):
        sumk = 0

        # Sum of the sequence
        # starting from index i
        for j in range(i, n, K):
            sumk = sumk + arr[j]

        # Update maximum
        maximum = max(maximum, sumk)

    return maximum

# Driver code
if __name__ == '__main__':
    arr = [3, 6, 4, 7, 2]
    n = len(arr)
    K = 2
    print(maxSum(arr, n, K))

# This code is contributed by
# Surendra_Gangwar
```

## **C#**

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum sum for
// every possible sequence such that
// a[i] + a[i+k] + a[i+2k] + ... + a[i+qk]
// is maximized
static int maxSum(int []arr, int n, int K)
{

    // Initialize the maximum with
    // the smallest value
    int maximum = int.MinValue;

    // Find maximum from all sequences
    for (int i = 0; i < n; i++)
    {

        int sumk = 0;

        // Sum of the sequence
        // starting from index i
        for (int j = i; j < n; j += K)
            sumk = sumk + arr[j];

        // Update maximum
        maximum = Math.Max(maximum, sumk);
    }

    return maximum;
}

// Driver code
public static void Main()
{
    int []arr = { 3, 6, 4, 7, 2 };
    int n = arr.Length;
    int K = 2;

    Console.WriteLine(maxSum(arr, n, K));
}
}

// This code is contributed by Akanksha Rai
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP implementation of the approach

// Function to return the maximum sum for
// every possible sequence such that
// a[i] + a[i+k] + a[i+2k] + ... + a[i+qk]
// is maximized
function maxSum($arr, $n, $K)
{

    // Initialize the maximum with
    // the smallest value
    $maximum = PHP_INT_MIN;

    // Find maximum from all sequences
    for ($i = 0; $i < $n; $i++)
    {
        $sumk = 0;

        // Sum of the sequence
        // starting from index i
        for ($j = $i; $j < $n; $j += $K)
            $sumk = $sumk + $arr[$j];

        // Update maximum
        $maximum = max($maximum, $sumk);
    }

    return $maximum;
}

// Driver code
$arr = array(3, 6, 4, 7, 2);
$n = sizeof($arr);
$K = 2;

echo maxSum($arr, $n, $K);

// This code is contributed by Akanksha Rai
?>
```

## **java 描述语言**

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum sum for
// every possible sequence such that
// a[i] + a[i+k] + a[i+2k] + ... + a[i+qk]
// is maximized
function maxSum(arr, n, K)
{

    // Initialize the maximum with
    // the smallest value
    var maximum = -1000000000;

    // Find maximum from all sequences
    for (var i = 0; i < n; i++) {

        var sumk = 0;

        // Sum of the sequence
        // starting from index i
        for (var j = i; j < n; j += K)
            sumk = sumk + arr[j];

        // Update maximum
        maximum = Math.max(maximum, sumk);
    }

    return maximum;
}

// Driver code
var arr = [3, 6, 4, 7, 2];
var n = arr.length;
var K = 2;
document.write( maxSum(arr, n, K));

</script>
```

****Output:** 

```
13
```** 

****高效方法:**这个问题可以通过使用[后缀数组](https://www.geeksforgeeks.org/suffix-array-set-1-introduction/)的概念来解决，我们从右侧迭代数组，并为每个 **(i+k)元素(即。，i+k < n)** ，求最大和。该方法的时间复杂度将为 **O(N)。**
以下是上述方法的实施。** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum sum for
// every possible sequence such that
// a[i] + a[i+k] + a[i+2k] + ... + a[i+qk]
// is maximized
int maxSum(int arr[], int n, int K)
{

    // Initialize the maximum with
    // the smallest value
    int maximum = INT_MIN;

    // Initialize the sum array with zero
    int sum[n] = { 0 };

    // Iterate from the right
    for (int i = n - 1; i >= 0; i--) {

        // Update the sum starting at
        // the current element
        if (i + K < n)
            sum[i] = sum[i + K] + arr[i];
        else
            sum[i] = arr[i];

        // Update the maximum so far
        maximum = max(maximum, sum[i]);
    }

    return maximum;
}

// Driver code
int main()
{
    int arr[] = { 3, 6, 4, 7, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    cout << maxSum(arr, n, K);

    return (0);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
class GFG {

    // Function to return the maximum sum for
    // every possible sequence such that
    // a[i] + a[i+k] + a[i+2k] + ... + a[i+qk]
    // is maximized
    static int maxSum(int arr[], int n, int K)
    {

        // Initialize the maximum with
        // the smallest value
        int maximum = Integer.MIN_VALUE;

        // Initialize the sum array with zero
        int[] sum = new int[n];

        // Iterate from the right
        for (int i = n - 1; i >= 0; i--) {

            // Update the sum starting at
            // the current element
            if (i + K < n)
                sum[i] = sum[i + K] + arr[i];
            else
                sum[i] = arr[i];

            // Update the maximum so far
            maximum = Math.max(maximum, sum[i]);
        }

        return maximum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 3, 6, 4, 7, 2 };
        int n = arr.length;
        int K = 2;

        System.out.print(maxSum(arr, n, K));
    }
}
```

## **计算机编程语言**

```
# Python implementation of the approach

# Function to return the maximum sum for
# every possible sequence such that
# a[i] + a[i + k] + a[i + 2k] + ... + a[i + qk]
# is maximized
def maxSum(arr, n, K):

    # Initialize the maximum with
    # the smallest value
    maximum = -2**32;

    # Initialize the sum array with zero
    sum = [0]*n

    # Iterate from the right
    for i in range(n-1, -1, -1):

        # Update the sum starting at
        # the current element
        if( i + K < n ):
            sum[i] = sum[i + K] + arr[i]
        else:
            sum[i] = arr[i];

        # Update the maximum so far
        maximum = max( maximum, sum[i] )

    return maximum;

# Driver code
arr = [3, 6, 4, 7, 2]
n = len(arr);
K = 2
print(maxSum(arr, n, K))
```

## **C#**

```
// C# implementation of the approach
using System;
class GFG {

    // Function to return the maximum sum for
    // every possible sequence such that
    // a[i] + a[i+k] + a[i+2k] + ... + a[i+qk]
    // is maximized
    static int maxSum(int[] arr, int n, int K)
    {

        // Initialize the maximum with
        // the smallest value
        int maximum = int.MinValue;

        // Initialize the sum array with zero
        int[] sum = new int[n];

        // Iterate from the right
        for (int i = n - 1; i >= 0; i--) {

            // Update the sum starting at
            // the current element
            if (i + K < n)
                sum[i] = sum[i + K] + arr[i];
            else
                sum[i] = arr[i];

            // Update the maximum so far
            maximum = Math.Max(maximum, sum[i]);
        }

        return maximum;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 3, 6, 4, 7, 2 };
        int n = arr.Length;
        int K = 2;

        Console.Write(maxSum(arr, n, K));
    }
}
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP implementation of the approach
// Function to return the maximum sum for
// every possible sequence such that
// a[i] + a[i+k] + a[i+2k] + ... + a[i+qk]
// is maximized
function maxSum($arr, $n, $K)
{

    // Initialize the maximum with
    // the smallest value
    $maximum = PHP_INT_MIN;

    // Initialize the sum array with zero
    $sum = array($n);

    // Iterate from the right
    for ($i = $n - 1; $i >= 0; $i--)
    {

        // Update the sum starting at
        // the current element
        if ($i + $K < $n)
            $sum[$i] = $sum[$i + $K] + $arr[$i];
        else
            $sum[$i] = $arr[$i];

        // Update the maximum so far
        $maximum = max($maximum, $sum[$i]);
    }

    return $maximum;
}

// Driver code
{
    $arr = array(3, 6, 4, 7, 2 );
    $n = sizeof($arr);
    $K = 2;

    echo(maxSum($arr, $n, $K));
}

// This code is contributed by Learner_
```

## **java 描述语言**

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum sum for
// every possible sequence such that
// a[i] + a[i+k] + a[i+2k] + ... + a[i+qk]
// is maximized
function maxSum(arr, n, K)
{

    // Initialize the maximum with
    // the smallest value
    var maximum = -1000000000;

    // Initialize the sum array with zero
    var sum = Array(n).fill(0);

    // Iterate from the right
    for (var i = n - 1; i >= 0; i--) {

        // Update the sum starting at
        // the current element
        if (i + K < n)
            sum[i] = sum[i + K] + arr[i];
        else
            sum[i] = arr[i];

        // Update the maximum so far
        maximum = Math.max(maximum, sum[i]);
    }

    return maximum;
}

// Driver code
var arr = [3, 6, 4, 7, 2 ];
var n = arr.length;
var K = 2;
document.write( maxSum(arr, n, K));

</script>
```

****Output:** 

```
13
```** 

****时间复杂度:** O(N)，其中 N 为数组中的元素个数。**