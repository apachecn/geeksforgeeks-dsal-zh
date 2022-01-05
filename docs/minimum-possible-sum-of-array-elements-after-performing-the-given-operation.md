# 执行给定操作后阵列元素的最小可能和

> 原文:[https://www . geeksforgeeks . org/执行给定操作后的最小可能数组元素总和/](https://www.geeksforgeeks.org/minimum-possible-sum-of-array-elements-after-performing-the-given-operation/)

给定一个正整数数组 **arr[]** 和一个整数 **x** ，任务是在最多执行一次给定操作后，最小化数组元素的总和。在单次运算中，数组中的任何元素都可以被 **x** 除(如果可以被 x 整除)，同时，数组中的任何其他元素都必须被 **x** 相乘。
**举例:**

> **输入:** arr[] = {1，2，3，4，5}，x = 2
> **输出:**14
> 1 乘以 x 即 1 * 2 = 2
> 4 除以 x 即 4 / 2 = 2
> 更新后的和将为 2 + 2 + 3 + 2 + 5 = 14
> **输入:** arr[] = {5，5，5，5，6}，x = 3

**方法:**对于最优解， **x** 必须与数组中最小的元素相乘，只有最大的元素可被 **x** 除。假设**sumafterproperties**是执行运算后计算的数组元素之和， **sum** 是原始数组所有元素之和，那么最小化的和将是 **min(sum，sumafterproperties)**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to return the minimized sum
ll minSum(int arr[], int n, int x)
{
    ll sum = 0;

    // To store the largest element
    // from the array which is
    // divisible by x
    int largestDivisible = -1, minimum = arr[0];
    for (int i = 0; i < n; i++) {

        // Sum of array elements before
        // performing any operation
        sum += arr[i];

        // If current element is divisible by x
        // and it is maximum so far
        if (arr[i] % x == 0 && largestDivisible < arr[i])
            largestDivisible = arr[i];

        // Update the minimum element
        if (arr[i] < minimum)
            minimum = arr[i];
    }

    // If no element can be reduced then there's no point
    // in performing the operation as we will end up
    // increasing the sum when an element is multiplied by x
    if (largestDivisible == -1)
        return sum;

    // Subtract the chosen elements from the sum
    // and then add their updated values
    ll sumAfterOperation = sum - minimum - largestDivisible
                           + (x * minimum) + (largestDivisible / x);

    // Return the minimized sum
    return min(sum, sumAfterOperation);
}

// Driver code
int main()
{
    int arr[] = { 5, 5, 5, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 3;
    cout << minSum(arr, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimized sum
static int minSum(int arr[], int n, int x)
{
    int sum = 0;

    // To store the largest element
    // from the array which is
    // divisible by x
    int largestDivisible = -1,
        minimum = arr[0];
    for (int i = 0; i < n; i++)
    {

        // Sum of array elements before
        // performing any operation
        sum += arr[i];

        // If current element is divisible
        // by x and it is maximum so far
        if (arr[i] % x == 0 &&
            largestDivisible < arr[i])
            largestDivisible = arr[i];

        // Update the minimum element
        if (arr[i] < minimum)
            minimum = arr[i];
    }

    // If no element can be reduced then
    // there's no point in performing the
    // operation as we will end up increasing
    // the sum when an element is multiplied by x
    if (largestDivisible == -1)
        return sum;

    // Subtract the chosen elements from the
    // sum and then add their updated values
    int sumAfterOperation = sum - minimum - largestDivisible +
                            (x * minimum) + (largestDivisible / x);

    // Return the minimized sum
    return Math.min(sum, sumAfterOperation);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 5, 5, 5, 5, 6 };
    int n =arr.length;
    int x = 3;
    System.out.println(minSum(arr, n, x));
}
}

// This code is contributed
// by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimized sum
def minSum(arr, n, x):

    Sum = 0

    # To store the largest element
    # from the array which is
    # divisible by x
    largestDivisible, minimum = -1, arr[0]
    for i in range(0, n):

        # Sum of array elements before
        # performing any operation
        Sum += arr[i]

        # If current element is divisible by x
        # and it is maximum so far
        if(arr[i] % x == 0 and
           largestDivisible < arr[i]):
            largestDivisible = arr[i]

        # Update the minimum element
        if arr[i] < minimum:
            minimum = arr[i]

    # If no element can be reduced then there's
    # no point in performing the operation as
    # we will end up increasing the sum when an
    # element is multiplied by x
    if largestDivisible == -1:
        return Sum

    # Subtract the chosen elements from the
    # sum and then add their updated values
    sumAfterOperation = (Sum - minimum - largestDivisible +
                        (x * minimum) + (largestDivisible // x))

    # Return the minimized sum
    return min(Sum, sumAfterOperation)

# Driver code
if __name__ == "__main__":

    arr = [5, 5, 5, 5, 6]
    n = len(arr)
    x = 3
    print(minSum(arr, n, x))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimized sum
static int minSum(int[] arr, int n, int x)
{
    int sum = 0;

    // To store the largest element
    // from the array which is
    // divisible by x
    int largestDivisible = -1,
        minimum = arr[0];
    for (int i = 0; i < n; i++)
    {

        // Sum of array elements before
        // performing any operation
        sum += arr[i];

        // If current element is divisible
        // by x and it is maximum so far
        if (arr[i] % x == 0 &&
            largestDivisible < arr[i])
            largestDivisible = arr[i];

        // Update the minimum element
        if (arr[i] < minimum)
            minimum = arr[i];
    }

    // If no element can be reduced then
    // there's no point in performing the
    // operation as we will end up increasing
    // the sum when an element is multiplied by x
    if (largestDivisible == -1)
        return sum;

    // Subtract the chosen elements from the
    // sum and then add their updated values
    int sumAfterOperation = sum - minimum - largestDivisible +
                            (x * minimum) + (largestDivisible / x);

    // Return the minimized sum
    return Math.Min(sum, sumAfterOperation);
}

// Driver code
public static void Main()
{
    int[] arr = { 5, 5, 5, 5, 6 };
    int n = arr.Length;
    int x = 3;
    Console.WriteLine(minSum(arr, n, x));
}
}

// This code is contributed
// by Code_Mech
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimized sum
function minSum($arr, $n, $x)
{
    $sum = 0;

    // To store the largest element
    // from the array which is
    // divisible by x
    $largestDivisible = -1;
    $minimum = $arr[0];
    for ($i = 0; $i < $n; $i++)
    {

        // Sum of array elements before
        // performing any operation
        $sum += $arr[$i];

        // If current element is divisible
        // by x and it is maximum so far
        if ($arr[$i] % $x == 0 &&
            $largestDivisible < $arr[$i])
            $largestDivisible = $arr[$i];

        // Update the minimum element
        if ($arr[$i] < $minimum)
            $minimum = $arr[$i];
    }

    // If no element can be reduced then
    // there's no point in performing the
    // operation as we will end up increasing
    // the sum when an element is multiplied by x
    if ($largestDivisible == -1)
        return $sum;

    // Subtract the chosen elements from the
    // sum and then add their updated values
    $sumAfterOperation = $sum - $minimum - $largestDivisible +
                        ($x * $minimum) + ($largestDivisible / $x);

    // Return the minimized sum
    return min($sum, $sumAfterOperation);
}

// Driver code
$arr = array( 5, 5, 5, 5, 6 );
$n = sizeof($arr);
$x = 3;

print(minSum($arr, $n, $x));

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to return the minimized sum
    function minSum(arr , n , x) {
        var sum = 0;

        // To store the largest element
        // from the array which is
        // divisible by x
        var largestDivisible = -1, minimum = arr[0];
        for (i = 0; i < n; i++) {

            // Sum of array elements before
            // performing any operation
            sum += arr[i];

            // If current element is divisible
            // by x and it is maximum so far
            if (arr[i] % x == 0 && largestDivisible < arr[i])
                largestDivisible = arr[i];

            // Update the minimum element
            if (arr[i] < minimum)
                minimum = arr[i];
        }

        // If no element can be reduced then
        // there's no point in performing the
        // operation as we will end up increasing
        // the sum when an element is multiplied by x
        if (largestDivisible == -1)
            return sum;

        // Subtract the chosen elements from the
        // sum and then add their updated values
        var sumAfterOperation = sum - minimum - largestDivisible
        + (x * minimum) + (largestDivisible / x);

        // Return the minimized sum
        return Math.min(sum, sumAfterOperation);
    }

    // Driver code

        var arr = [ 5, 5, 5, 5, 6 ];
        var n = arr.length;
        var x = 3;
        document.write(minSum(arr, n, x));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
26
```