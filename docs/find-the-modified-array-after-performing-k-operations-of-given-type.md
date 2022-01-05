# 执行给定类型的 k 次运算后找到修改后的数组

> 原文:[https://www . geeksforgeeks . org/在执行给定类型的 k 操作后查找修改后的数组/](https://www.geeksforgeeks.org/find-the-modified-array-after-performing-k-operations-of-given-type/)

给定一个由 **n** 个整数和一个整数 **K** 组成的数组 **arr[]** 。在一个操作中，数组的每个元素都被该元素与数组最大值之差所取代。任务是执行 **K** 操作后打印数组。
**举例:**

> **输入:** arr[] = {4，8，12，16}，k = 2
> **输出:** 0 4 8 12
> k = 1，arr[] = {12，8，4，0}
> k = 2，arr[] = {0，4，8，12}
> **输入:** arr[] = {14，28，14，106，223}，k = 12

****方法:**有两种可能的情况:** 

1.  **如果 **k 为奇数**，那么新数组将为范围**【0，n】**内所有 **i** 的**max(arr)–arr【I】**。**
2.  **如果 **k 为偶数**，则新数组将为范围**【0，n】**中所有 **i** 的**arr[I]–min(arr)**。**

****例如:**** 

> **设 arr[] = {4，8，12，16}
> 对于 k = 1，arr[] = (12，8，4，0)}
> 对于 k = 2，arr[] = (0，4，8，12)}
> 对于 k = 3，arr[] = (12，8，4，0)}
> 对于 k = 4，arr[] = (0，4，8，12)}
> 可以观察到数组每 2 次运算后重复一次。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print
// the contents of an array
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to remove the minimum value of
// the array from every element of the array
void removeMin(int arr[], int n)
{
    int i, minVal = arr[0];

    // Get the minimum value from the array
    for (i = 1; i < n; i++)
        minVal = min(minVal, arr[i]);

    // Remove the minimum value from
    // every element of the array
    for (i = 0; i < n; i++)
        arr[i] = arr[i] - minVal;
}

// Function to remove every element of the
// array from the maximum value of the array
void removeFromMax(int arr[], int n)
{
    int i, maxVal = arr[0];

    // Get the maximum value from the array
    for (i = 1; i < n; i++)
        maxVal = max(maxVal, arr[i]);

    // Remove every element of the array from
    // the maximum value of the array
    for (i = 0; i < n; i++)
        arr[i] = maxVal - arr[i];
}

// Function to print the modified array
// after k operations
void modifyArray(int arr[], int n, int k)
{

    // If k is odd then remove the minimum element
    // of the array from every element of the array
    if (k % 2 == 0)
        removeMin(arr, n);

    // Else remove every element of the array from
    // the maximum value from the array
    else
        removeFromMax(arr, n);

    // Print the modified array
    printArray(arr, n);
}

// Driver code
int main()
{
    int arr[] = { 4, 8, 12, 16 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    modifyArray(arr, n, k);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
class GFG {

    // Utility function to print
    // the contents of an array
    static void printArray(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Function to remove the minimum value of
    // the array from every element of the array
    static void removeMin(int arr[], int n)
    {
        int i, minVal = arr[0];

        // Get the minimum value from the array
        for (i = 1; i < n; i++)
            minVal = Math.min(minVal, arr[i]);

        // Remove the minimum value from
        // every element of the array
        for (i = 0; i < n; i++)
            arr[i] = arr[i] - minVal;
    }

    // Function to remove every element of the
    // array from the maximum value of the array
    static void removeFromMax(int arr[], int n)
    {
        int i, maxVal = arr[0];

        // Get the maximum value from the array
        for (i = 1; i < n; i++)
            maxVal = Math.max(maxVal, arr[i]);

        // Remove every element of the array from
        // the maximum value of the array
        for (i = 0; i < n; i++)
            arr[i] = maxVal - arr[i];
    }

    // Function to print the modified array
    // after k operations
    static void modifyArray(int arr[], int n, int k)
    {

        // If k is odd then remove the minimum element
        // of the array from every element of the array
        if (k % 2 == 0)
            removeMin(arr, n);

        // Else remove every element of the array from
        // the maximum value from the array
        else
            removeFromMax(arr, n);

        // Print the modified array
        printArray(arr, n);
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 4, 8, 12, 16 };
        int n = arr.length;
        int k = 2;
        modifyArray(arr, n, k);
    }
}
```

## **蟒蛇 3**

```
# Python 3 implementation of the approach

# Utility function to print
# the contents of an array
def printArray(arr, n) :

    for i in range(n) :
        print(arr[i], end = " ");

# Function to remove the minimum
# value of the array from every
# element of the array
def removeMin(arr, n) :

    minVal = arr[0];

    # Get the minimum value from
    # the array
    for i in range(1, n) :
        minVal = min(minVal, arr[i]);

    # Remove the minimum value from
    # every element of the array
    for i in range(n) :
        arr[i] = arr[i] - minVal;

# Function to remove every element
# of the array from the maximum
# value of the array
def removeFromMax(arr, n) :

    maxVal = arr[0];

    # Get the maximum value from
    # the array
    for i in range(1, n) :
        maxVal = max(maxVal, arr[i]);

    # Remove every element of the
    # array from the maximum value
    # of the array
    for i in range(n) :
        arr[i] = maxVal - arr[i];

# Function to print the modified 
# array after k operations
def modifyArray(arr, n, k) :

    # If k is odd then remove the minimum
    # element of the array from every
    # element of the array
    if (k % 2 == 0) :
        removeMin(arr, n);

    # Else remove every element of
    # the array from the maximum
    # value from the array
    else :
        removeFromMax(arr, n);

    # Print the modified array
    printArray(arr, n);

# Driver code
if __name__ == "__main__" :

    arr = [ 4, 8, 12, 16 ];
    n = len(arr)

    k = 2;
    modifyArray(arr, n, k);

# This code is contributed by Ryuga
```

## **C#**

```
// C# implementation of the approach
using System;
class GFG {

    // Utility function to print
    // the contents of an array
    static void printArray(int[] arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Function to remove the minimum value of
    // the array from every element of the array
    static void removeMin(int[] arr, int n)
    {
        int i, minVal = arr[0];

        // Get the minimum value from the array
        for (i = 1; i < n; i++)
            minVal = Math.Min(minVal, arr[i]);

        // Remove the minimum value from
        // every element of the array
        for (i = 0; i < n; i++)
            arr[i] = arr[i] - minVal;
    }

    // Function to remove every element of the
    // array from the maximum value of the array
    static void removeFromMax(int[] arr, int n)
    {
        int i, maxVal = arr[0];

        // Get the maximum value from the array
        for (i = 1; i < n; i++)
            maxVal = Math.Max(maxVal, arr[i]);

        // Remove every element of the array from
        // the maximum value of the array
        for (i = 0; i < n; i++)
            arr[i] = maxVal - arr[i];
    }

    // Function to print the modified array
    // after k operations
    static void modifyArray(int[] arr, int n, int k)
    {

        // If k is odd then remove the minimum element
        // of the array from every element of the array
        if (k % 2 == 0)
            removeMin(arr, n);

        // Else remove every element of the array from
        // the maximum value from the array
        else
            removeFromMax(arr, n);

        // Print the modified array
        printArray(arr, n);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 4, 8, 12, 16 };
        int n = arr.Length;
        int k = 2;
        modifyArray(arr, n, k);
    }
}
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP implementation of the approach

// Utility function to print
// the contents of an array
function printArray($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i] . " ";
}

// Function to remove the minimum value of
// the array from every element of the array
function removeMin(&$arr, $n)
{
    $minVal = $arr[0];

    // Get the minimum value from the array
    for ($i = 1; $i < $n; $i++)
        $minVal = min($minVal, $arr[$i]);

    // Remove the minimum value from
    // every element of the array
    for ($i = 0; $i < $n; $i++)
        $arr[$i] = $arr[$i] - $minVal;
}

// Function to remove every element of the
// array from the maximum value of the array
function removeFromMax(&$arr, $n)
{
    $maxVal = $arr[0];

    // Get the maximum value from the array
    for ($i = 1; $i < $n; $i++)
        $maxVal = max($maxVal, $arr[$i]);

    // Remove every element of the array from
    // the maximum value of the array
    for ($i = 0; $i < $n; $i++)
        $arr[$i] = $maxVal - $arr[$i];
}

// Function to print the modified array
// after k operations
function modifyArray($arr, $n, $k)
{

    // If k is odd then remove the minimum element
    // of the array from every element of the array
    if ($k % 2 == 0)
        removeMin($arr, $n);

    // Else remove every element of the array
    // from the maximum value from the array
    else
        removeFromMax($arr, $n);

    // Print the modified array
    printArray($arr, $n);
}

// Driver code
$arr = array( 4, 8, 12, 16 );
$n = count($arr);
$k = 2;
modifyArray($arr, $n, $k);

// This code is contributed by mits
?>
```

## **java 描述语言**

```
<script>
// Javascript implementation of the approach

// Utility function to print
// the contents of an array
function printArray(arr, n)
{
    for (var i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Function to remove the minimum value of
// the array from every element of the array
function removeMin(arr, n)
{
    var i, minVal = arr[0];

    // Get the minimum value from the array
    for (i = 1; i < n; i++)
        minVal = Math.min(minVal, arr[i]);

    // Remove the minimum value from
    // every element of the array
    for (i = 0; i < n; i++)
        arr[i] = arr[i] - minVal;
}

// Function to remove every element of the
// array from the maximum value of the array
function removeFromMax(arr, n)
{
    var i, maxVal = arr[0];

    // Get the maximum value from the array
    for (i = 1; i < n; i++)
        maxVal = Math.max(maxVal, arr[i]);

    // Remove every element of the array from
    // the maximum value of the array
    for (i = 0; i < n; i++)
        arr[i] = maxVal - arr[i];
}

// Function to print the modified array
// after k operations
function modifyArray(arr, n, k)
{

    // If k is odd then remove the minimum element
    // of the array from every element of the array
    if (k % 2 == 0)
        removeMin(arr, n);

    // Else remove every element of the array from
    // the maximum value from the array
    else
        removeFromMax(arr, n);

    // Print the modified array
    printArray(arr, n);
}

// Driver code
arr = [ 4, 8, 12, 16 ]
var n = arr.length;
var k = 2;
modifyArray(arr, n, k);

// This code is contributed by noob2000.
</script>
```

****Output:** 

```
0 4 8 12
```** 

****时间复杂度:** O(n)**