# 用接下来两个连续元素的和替换数组元素

> 原文:[https://www . geeksforgeeks . org/用下两个连续元素的总和替换数组元素/](https://www.geeksforgeeks.org/replace-array-elements-by-sum-of-next-two-consecutive-elements/)

给定一个大小为 **n** 的数组 **arr[]** ，任务是以**循环**的方式用接下来两个连续元素的和替换数组中的每个元素，即 **arr[0] = arr[1] + arr[2]** ， **arr[1] = arr[2] + arr[3]** ，…**arr[n–1]= arr[0]+arr[1]**。
**示例:**

> **输入:** arr[] = {3，4，2，1，6}
> **输出:**6 3 7 9 7
> T6】输入: arr[] = {5，2，1，3，8}
> **输出:** 3 4 11 13 7

**方法:**将数组的第一个和第二个元素存储在变量**第一个**和**第二个**中。现在对于除了数组的最后一个和第二个元素之外的每个元素，更新 **arr[i] = arr[i + 1] + arr[i + 2]** 。然后将最后一个和第二个最后一个元素更新为**arr[n–2]= arr[n–1]+第一个**和**arr[n–1]=第一个+第二个**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print the
// contents of an array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to update every element of
// the array as the sum of next two elements
void updateArr(int arr[], int n)
{

    // Invalid array
    if (n < 3)
        return;

    // First and second elements of the array
    int first = arr[0];
    int second = arr[1];

    // Update every element as required
    // except the last and the
    // second last element
    for (int i = 0; i < n - 2; i++)
        arr[i] = arr[i + 1] + arr[i + 2];

    // Update the last and the second
    // last element of the array
    arr[n - 2] = arr[n - 1] + first;
    arr[n - 1] = first + second;

    // Print the updated array
    printArr(arr, n);
}

// Driver code
int main()
{
    int arr[] = { 3, 4, 2, 1, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    updateArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Utility function to print the
    // contents of an array
    static void printArr(int[] arr, int n)
    {
        for (int i = 0; i < n; i++)
        {
            System.out.print(arr[i] + " ");
        }
    }

    // Function to update every element of
    // the array as the sum of next two elements
    static void updateArr(int[] arr, int n)
    {

        // Invalid array
        if (n < 3)
        {
            return;
        }

        // First and second elements of the array
        int first = arr[0];
        int second = arr[1];

        // Update every element as required
        // except the last and the
        // second last element
        for (int i = 0; i < n - 2; i++)
        {
            arr[i] = arr[i + 1] + arr[i + 2];
        }

        // Update the last and the second
        // last element of the array
        arr[n - 2] = arr[n - 1] + first;
        arr[n - 1] = first + second;

        // Print the updated array
        printArr(arr, n);
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = {3, 4, 2, 1, 6};
        int n = arr.length;
        updateArr(arr, n);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Utility function to print the
# contents of an array
def printArr(arr, n):
    for i in range(n):
        print(arr[i], end = " ")

# Function to update every element of
# the array as the sum of next two elements
def updateArr(arr, n):

    # Invalid array
    if (n < 3):
        return

    # First and second elements of the array
    first = arr[0]
    second = arr[1]

    # Update every element as required
    # except the last and the
    # second last element
    for i in range(n - 2):
        arr[i] = arr[i + 1] + arr[i + 2]

    # Update the last and the second
    # last element of the array
    arr[n - 2] = arr[n - 1] + first
    arr[n - 1] = first + second

    # Print the updated array
    printArr(arr, n)

# Driver code
if __name__ == '__main__':
    arr = [3, 4, 2, 1, 6]
    n = len(arr)
    updateArr(arr, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Utility function to print the
// contents of an array
static void printArr(int []arr, int n)
{
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Function to update every element of
// the array as the sum of next two elements
static void updateArr(int []arr, int n)
{

    // Invalid array
    if (n < 3)
        return;

    // First and second elements of the array
    int first = arr[0];
    int second = arr[1];

    // Update every element as required
    // except the last and the
    // second last element
    for (int i = 0; i < n - 2; i++)
        arr[i] = arr[i + 1] + arr[i + 2];

    // Update the last and the second
    // last element of the array
    arr[n - 2] = arr[n - 1] + first;
    arr[n - 1] = first + second;

    // Print the updated array
    printArr(arr, n);
}

// Driver code
public static void Main()
{
    int []arr = { 3, 4, 2, 1, 6 };
    int n = arr.Length;
    updateArr(arr, n);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Utility function to print the
// contents of an array
function printArr($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i], " ";
}

// Function to update every element
// of the array as the sum of next
// two elements
function updateArr($arr, $n)
{

    // Invalid array
    if ($n < 3)
        return;

    // First and second elements
    // of the array
    $first = $arr[0];
    $second = $arr[1];

    // Update every element as required
    // except the last and the
    // second last element
    for ($i = 0; $i < ($n - 2); $i++)
        $arr[$i] = $arr[$i + 1] +
                   $arr[$i + 2];

    // Update the last and the second
    // last element of the array
    $arr[$n - 2] = $arr[$n - 1] + $first;
    $arr[$n - 1] = $first + $second;

    // Print the updated array
    printArr($arr, $n);
}

// Driver code
$arr = array (3, 4, 2, 1, 6 );
$n = sizeof($arr);
updateArr($arr, $n);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Utility function to print the
// contents of an array
function printArr( arr, n)
{
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Function to update every element of
// the array as the sum of next two elements
function updateArr( arr, n)
{

    // Invalid array
    if (n < 3)
        return;

    // First and second elements of the array
    let first = arr[0];
    let second = arr[1];

    // Update every element as required
    // except the last and the
    // second last element
    for (let i = 0; i < n - 2; i++)
        arr[i] = arr[i + 1] + arr[i + 2];

    // Update the last and the second
    // last element of the array
    arr[n - 2] = arr[n - 1] + first;
    arr[n - 1] = first + second;

    // Print the updated array
    printArr(arr, n);
}

    // driver code
    let arr = [ 3, 4, 2, 1, 6 ];
    let n = arr.length;
    updateArr(arr, n);

// This code is contributed by jana_sayantan.

</script>
```

**Output:** 

```
6 3 7 9 7
```