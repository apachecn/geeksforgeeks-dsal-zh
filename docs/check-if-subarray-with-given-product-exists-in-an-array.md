# 检查给定产品的子阵列是否存在于阵列中

> 原文:[https://www . geeksforgeeks . org/检查给定产品的子阵列是否存在于阵列中/](https://www.geeksforgeeks.org/check-if-subarray-with-given-product-exists-in-an-array/)

给定一个由正整数和负整数以及数字 K 组成的数组，任务是检查数组中是否存在任何带有乘积 K 的子数组。
**例:**

```
Input: arr[] = {-2, -1, 3, -4, 5}, K = 2
Output: YES

Input: arr[] = {3, -1, -1, -1, 5}, K = 3
Output: NO
```

**方法:**该方法类似于[最大产品子阵](https://www.geeksforgeeks.org/maximum-product-subarray-set-3/)中使用的方法，唯一的任务是同时检查产品是否等于 k。
以下是上述方法的实施:

## C++

```
// CPP program to check if there is
// any Subarray with product equal to K
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum product subarray
bool maxProduct(int* arr, int n, int p)
{
    // Variables to store maximum and minimum
    // product till ith index.
    int minVal = arr[0];
    int maxVal = arr[0];

    int maxProduct = arr[0];

    for (int i = 1; i < n; i++) {

        // When multiplied by -ve number,
        // maxVal becomes minVal
        // and minVal becomes maxVal.
        if (arr[i] < 0)
            swap(maxVal, minVal);

        // maxVal and minVal stores the
        // product of subarray ending at arr[i].
        maxVal = max(arr[i], maxVal * arr[i]);
        minVal = min(arr[i], minVal * arr[i]);

        // Check if the current product is
        // equal to the given product
        if (minVal == p || maxVal == p) {
            return true;
        }

        // Max Product of array.
        maxProduct = max(maxProduct, maxVal);
    }

    // Return maximum product found in array.
    return false;
}

// Driver Program to test above function
int main()
{
    int arr[] = { 1, 2, -5, -4 };
    int product = -10;
    int n = sizeof(arr) / sizeof(arr[0]);

    if (maxProduct(arr, n, product)) {
        cout << "YES" << endl;
    }
    else
        cout << "NO" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if there
// is any Subarray with product
// equal to K
import java.io.*;

class GFG
{

// Function to find maximum
// product subarray
static boolean maxProduct(int arr[],
                          int n, int p)
{
    // Variables to store maximum
    // and minimum product till
    // ith index.
    int minVal = arr[0];
    int maxVal = arr[0];

    int maxProduct = arr[0];

    for (int i = 1; i < n; i++)
    {

        // When multiplied by -ve number,
        // maxVal becomes minVal
        // and minVal becomes maxVal.
        if (arr[i] < 0)
        {
            int temp = maxVal;
            maxVal = minVal;
            minVal = temp;
        }

        // maxVal and minVal stores
        // the product of subarray
        // ending at arr[i].
        maxVal = Math.max(arr[i],
                      maxVal * arr[i]);
        minVal = Math.min(arr[i],
                      minVal * arr[i]);

        // Check if the current product
        // is equal to the given product
        if (minVal == p || maxVal == p)
        {
            return true;
        }

        // Max Product of array.
        maxProduct = Math.max(maxProduct,
                              maxVal);
    }

    // Return maximum product
    // found in array.
    return false;
}

// Driver Code
public static void main (String[] args)
{
    int []arr = { 1, 2, -5, -4 };
    int product = -10;
    int n = arr.length;

    if (maxProduct(arr, n, product))
    {
        System.out.println( "YES");
    }
    else
        System.out.println( "NO");
}
}

// This code is contributed
// by inder_verma
```

## 蟒蛇 3

```
# Python 3 program to check if there is
# any Subarray with product equal to K

# Function to find maximum
# product subarray
def maxProduct(arr,n, p):

    # Variables to store maximum and
    # minimum product till ith index.
    minVal = arr[0]
    maxVal = arr[0]

    maxProduct = arr[0]

    for i in range( 1, n):

        # When multiplied by -ve number,
        # maxVal becomes minVal
        # and minVal becomes maxVal.
        if (arr[i] < 0):
            maxVal, minVal = minVal, maxVal

        # maxVal and minVal stores the
        # product of subarray ending at arr[i].
        maxVal = max(arr[i], maxVal * arr[i])
        minVal = min(arr[i], minVal * arr[i])

        # Check if the current product is
        # equal to the given product
        if (minVal == p or maxVal == p):
            return True

        # Max Product of array.
        maxProduct = max(maxProduct, maxVal)

    # Return maximum product
    # found in array.
    return False

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, -5, -4 ]
    product = -10
    n = len(arr)

    if (maxProduct(arr, n, product)):
        print("YES")
    else:
        print("NO")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to check if there
// is any Subarray with product
// equal to K
using System;

class GFG
{

// Function to find maximum
// product subarray
static bool maxProduct(int []arr,
                       int n, int p)
{
    // Variables to store maximum
    // and minimum product till
    // ith index.
    int minVal = arr[0];
    int maxVal = arr[0];

    int maxProduct = arr[0];

    for (int i = 1; i < n; i++)
    {

        // When multiplied by -ve number,
        // maxVal becomes minVal
        // and minVal becomes maxVal.
        if (arr[i] < 0)
        {
            int temp = maxVal;
            maxVal = minVal;
            minVal = temp;
        }

        // maxVal and minVal stores
        // the product of subarray
        // ending at arr[i].
        maxVal = Math.Max(arr[i],
                    maxVal * arr[i]);
        minVal = Math.Min(arr[i],
                    minVal * arr[i]);

        // Check if the current product
        // is equal to the given product
        if (minVal == p || maxVal == p)
        {
            return true;
        }

        // Max Product of array.
        maxProduct = Math.Max(maxProduct,
                              maxVal);
    }

    // Return maximum product
    // found in array.
    return false;
}

// Driver Code
public static void Main ()
{
    int []arr = { 1, 2, -5, -4 };
    int product = -10;
    int n = arr.Length;

    if (maxProduct(arr, n, product))
    {
        Console.WriteLine( "YES");
    }
    else
        Console.WriteLine( "NO");
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if there is
// any Subarray with product equal to K

// Function to find maximum
// product subarray
function maxProduct(&$arr, $n, $p)
{
    // Variables to store maximum
    // and minimum product till
    // ith index.
    $minVal = $arr[0];
    $maxVal = $arr[0];

    $maxProduct = $arr[0];

    for ($i = 1; $i < $n; $i++)
    {

        // When multiplied by -ve number,
        // maxVal becomes minVal
        // and minVal becomes maxVal.
        if ($arr[$i] < 0)
        {
            $temp = $maxVal;
            $maxVal = $minVal;
            $minVal = $temp;
        }
        // maxVal and minVal stores the
        // product of subarray ending at arr[i].
        $maxVal = max($arr[$i], $maxVal *
                                $arr[$i]);
        $minVal = min($arr[$i], $minVal *
                                $arr[$i]);

        // Check if the current product is
        // equal to the given product
        if ($minVal == $p || $maxVal == $p)
        {
            return true;
        }

        // Max Product of array.
        $maxProduct = max($maxProduct, $maxVal);
    }

    // Return maximum product
    // found in array.
    return false;
}

// Driver Code
$arr = array(1, 2, -5, -4 );
$product = -10;
$n = sizeof($arr);

if (maxProduct($arr, $n, $product))
{
    echo ("YES") ;
}
else
    echo ("NO");

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to check if there
// is any Subarray with product
// equal to K

    // Function to find maximum
   // product subarray
    function maxProduct(arr,n,p)
    {
        // Variables to store maximum
    // and minimum product till
    // ith index.
    let minVal = arr[0];
    let maxVal = arr[0];

    let maxProduct = arr[0];

    for (let i = 1; i < n; i++)
    {

        // When multiplied by -ve number,
        // maxVal becomes minVal
        // and minVal becomes maxVal.
        if (arr[i] < 0)
        {
            let temp = maxVal;
            maxVal = minVal;
            minVal = temp;
        }

        // maxVal and minVal stores
        // the product of subarray
        // ending at arr[i].
        maxVal = Math.max(arr[i],
                      maxVal * arr[i]);
        minVal = Math.min(arr[i],
                      minVal * arr[i]);

        // Check if the current product
        // is equal to the given product
        if (minVal == p || maxVal == p)
        {
            return true;
        }

        // Max Product of array.
        maxProduct = Math.max(maxProduct,
                              maxVal);
    }

    // Return maximum product
    // found in array.
    return false;
    }

    // Driver Code
    let arr=[1, 2, -5, -4];
    let product = -10;
    let n = arr.length;
    if (maxProduct(arr, n, product))
    {
        document.write( "YES");
    }
    else
        document.write( "NO");

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
YES
```