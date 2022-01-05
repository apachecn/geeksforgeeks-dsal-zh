# 数组最小和最大元素的和与积

> 原文:[https://www . geeksforgeeks . org/最小和最大数组元素之和与乘积/](https://www.geeksforgeeks.org/sum-and-product-of-minimum-and-maximum-element-of-an-array/)

给定一个数组。任务是找到给定数组的最大和最小元素的和与积。
**例** :

```
Input : arr[] = {12, 1234, 45, 67, 1}
Output : Sum = 1235
         Product = 1234

Input : arr[] = {5, 3, 6, 8, 4, 1, 2, 9}
Output : Sum = 10
         Product = 9
```

取变量 min 和 max 来存储数组的最小和最大元素。[求最小和最大元素](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)分别存储在这些变量中。最后，打印最小和最大元素的总和和乘积。
下面是说明上述方法的程序:

## C++

```
// CPP program to find the sum  and product
// of minimum and maximum element in an array

#include <iostream>
using namespace std;

// Function to find minimum element
int getMin(int arr[], int n)
{
    int res = arr[0];
    for (int i = 1; i < n; i++)
        res = min(res, arr[i]);
    return res;
}

// Function to find maximum element
int getMax(int arr[], int n)
{
    int res = arr[0];
    for (int i = 1; i < n; i++)
        res = max(res, arr[i]);
    return res;
}

// Function to get Sum
int findSum(int arr[], int n)
{
    int min = getMin(arr, n);
    int max = getMax(arr, n);

    return min + max;
}

// Function to get product
int findProduct(int arr[], int n)
{
    int min = getMin(arr, n);
    int max = getMax(arr, n);

    return min * max;
}

// Driver Code
int main()
{
    int arr[] = { 12, 1234, 45, 67, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Sum of min and max element
    cout << "Sum = " << findSum(arr, n) << endl;

    // Product of min and max element
    cout << "Product = " << findProduct(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to find the sum and product
// of minimum and maximum element in an array

import java.io.*;

class GFG {

    // Function to find minimum element
static int getMin(int arr[], int n)
{
    int res = arr[0];
    for (int i = 1; i < n; i++)
        res = Math.min(res, arr[i]);
    return res;
}

// Function to find maximum element
static int getMax(int arr[], int n)
{
    int res = arr[0];
    for (int i = 1; i < n; i++)
        res = Math.max(res, arr[i]);
    return res;
}

// Function to get Sum
static int findSum(int arr[], int n)
{
    int min = getMin(arr, n);
    int max = getMax(arr, n);

    return min + max;
}

// Function to get product
static int findProduct(int arr[], int n)
{
    int min = getMin(arr, n);
    int max = getMax(arr, n);

    return min * max;
}

// Driver Code

    public static void main (String[] args) {
    int arr[] = { 12, 1234, 45, 67, 1 };
    int n = arr.length;

    // Sum of min and max element
        System.out.println ("Sum = " + findSum(arr, n));

    // Product of min and max element
        System.out.println( "Product = " + findProduct(arr, n));

    }
}
//This Code is contributed by anuj_67....
```

## 蟒蛇 3

```
# Python 3 program to find the sum and product
# of minimum and maximum element in an array

# Function to find minimum element
def getMin(arr, n):
    res = arr[0]
    for i in range(1, n):
        res = min(res, arr[i])
    return res

# Function to find maximum element
def getMax(arr, n):
    res = arr[0]
    for i in range(1, n):
        res = max(res, arr[i])
    return res

# Function to get Sum
def findSum(arr, n):
    min = getMin(arr, n)
    max = getMax(arr, n)

    return min + max

# Function to get product
def findProduct(arr, n):
    min = getMin(arr, n)
    max = getMax(arr, n)

    return min * max

# Driver Code
if __name__ == "__main__":

    arr = [ 12, 1234, 45, 67, 1 ]
    n = len(arr)

    # Sum of min and max element
    print("Sum = " , findSum(arr, n))

    # Product of min and max element
    print("Product = " , findProduct(arr, n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find the sum and product
// of minimum and maximum element in an array
using System;

class GFG {

// Function to find minimum element
static int getMin(int []arr, int n)
{
    int res = arr[0];
    for (int i = 1; i < n; i++)
        res = Math.Min(res, arr[i]);
    return res;
}

// Function to find maximum element
static int getMax(int []arr, int n)
{
    int res = arr[0];
    for (int i = 1; i < n; i++)
        res = Math.Max(res, arr[i]);
    return res;
}

// Function to get Sum
static int findSum(int []arr, int n)
{
    int min = getMin(arr, n);
    int max = getMax(arr, n);

    return min + max;
}

// Function to get product
static int findProduct(int []arr, int n)
{
    int min = getMin(arr, n);
    int max = getMax(arr, n);

    return min * max;
}

    // Driver Code
    public static void Main()
    {
        int []arr = { 12, 1234, 45, 67, 1 };
        int n = arr.Length;

        // Sum of min and max element
        Console.WriteLine("Sum = " + findSum(arr, n));

        // Product of min and max element
        Console.WriteLine( "Product = " + findProduct(arr, n));
    }
}

// This Code is contributed by anuj_67....
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum and product
// of minimum and maximum element in an array

// Function to find minimum element
function getMin($arr, $n)
{
    $res = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $res = min($res, $arr[$i]);
    return $res;
}

// Function to find maximum element
function getMax($arr, $n)
{
    $res = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $res = max($res, $arr[$i]);
    return $res;
}

// Function to get Sum
function findSum($arr, $n)
{
    $min = getMin($arr, $n);
    $max = getMax($arr, $n);

    return $min + $max;
}

// Function to get product
function findProduct($arr, $n)
{
    $min = getMin($arr, $n);
    $max = getMax($arr, $n);

    return $min * $max;
}

// Driver Code
$arr = array(12, 1234, 45, 67, 1);
$n = sizeof($arr);

// Sum of min and max element
echo "Sum = " . findSum($arr, $n) . "\n";

// Product of min and max element
echo "Product = " . findProduct($arr, $n);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// JavaScript  program to find the sum and product
// of minimum and maximum element in an array

// Function to find minimum element
function getMin(arr,n)
{
    let res = arr[0];
    for (let i = 1; i < n; i++)
        res = Math.min(res, arr[i]);
    return res;
}

// Function to find maximum element
function getMax(arr,n)
{
    let res = arr[0];
    for (let i = 1; i < n; i++)
        res = Math.max(res, arr[i]);
    return res;
}

// Function to get Sum
function findSum(arr,n)
{
    let min = getMin(arr, n);
    let max = getMax(arr, n);

    return min + max;
}

// Function to get product
function findProduct(arr,n)
{
    let min = getMin(arr, n);
    let max = getMax(arr, n);

    return min * max;
}

// Driver Code
let arr=[12, 1234, 45, 67, 1];

let n = arr.length;
// Sum of min and max element
document.write ("Sum = " + findSum(arr, n)+"<br>");

// Product of min and max element
document.write( "Product = " + findProduct(arr, n)+"<br>");

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
Sum = 1235
Product = 1234
```