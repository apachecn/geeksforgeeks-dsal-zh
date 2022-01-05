# 用立方体替换奇数位置的元素，用正方形替换偶数位置的元素

> 原文:[https://www . geeksforgeeks . org/用它们的立方体替换奇数位置的元素，用它们的正方形替换偶数位置的元素/](https://www.geeksforgeeks.org/replace-the-odd-positioned-elements-with-their-cubes-and-even-positioned-elements-with-their-squares/)

给定一个由 **n** 个元素组成的数组 **arr[]** ，任务是用它们的立方体替换所有奇数位置的元素，用它们的正方形替换偶数位置的元素，即得到的数组必须是 **{arr[0] <sup>3</sup> ，arr[1] <sup>2</sup> ，arr[2] <sup>3</sup> ，arr[3] <sup>2</sup> ，…}** 。
**示例:**

> **输入:** arr[]= {2，3，4，5}
> **输出:** 8 9 64 25
> 更新阵将为{2 <sup>3</sup> ，3 <sup>2</sup> ，4 <sup>3</sup> ，5 <sup>2</sup> } - > {8，9，64，25}
> **输入:** arr[] = {3，4，5，2

**方法:**对于数组**arr【I】**中的任何元素，只有当 **(i + 1)** 为**奇数**时，它才是奇数位置，因为索引从 **0** 开始。现在，遍历数组，用立方体替换所有奇数位置的元素，用正方形替换偶数位置的元素。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Utility function to print
// the contents of an array
void printArr(ll arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to update the array
void updateArr(ll arr[], int n)
{
    for (int i = 0; i < n; i++) {

        // In case of even positioned element
        if ((i + 1) % 2 == 0)
            arr[i] = (ll)pow(arr[i], 2);

        // Odd positioned element
        else
            arr[i] = (ll)pow(arr[i], 3);
    }

    // Print the updated array
    printArr(arr, n);
}

// Driver code
int main()
{
    ll arr[] = { 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    updateArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.lang.Math;

class GFG
{

// Utility function to print
// the contents of an array
static void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Function to update the array
static void updateArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
    {

        // In case of even positioned element
        if ((i + 1) % 2 == 0)
            arr[i] = (int)Math.pow(arr[i], 2);

        // Odd positioned element
        else
            arr[i] = (int)Math.pow(arr[i], 3);
    }

    // Print the updated array
    printArr(arr, n);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 4, 5, 6 };
    int n = arr.length;

    updateArr(arr, n);
}
}

// This code is contributed
// by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to print
# the contents of an array
def printArr(arr,n):
    for i in range(n):
        print(arr[i], end = " ")

# Function to update the array
def updateArr(arr, n):
    for i in range(n):

        # In case of even positioned element
        if ((i + 1) % 2 == 0):
            arr[i] = pow(arr[i], 2)

        # Odd positioned element
        else:
            arr[i] = pow(arr[i], 3)

    # Print the updated array
    printArr(arr, n)

# Driver code
arr = [ 2, 3, 4, 5, 6 ]
n = len(arr)

updateArr(arr, n)

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Utility function to print
// the contents of an array
static void printArr(int []arr, int n)
{
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Function to update the array
static void updateArr(int []arr, int n)
{
    for (int i = 0; i < n; i++)
    {

        // In case of even positioned element
        if ((i + 1) % 2 == 0)
            arr[i] = (int)Math.Pow(arr[i], 2);

        // Odd positioned element
        else
            arr[i] = (int)Math.Pow(arr[i], 3);
    }

    // Print the updated array
    printArr(arr, n);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 3, 4, 5, 6 };
    int n = arr.Length;

    updateArr(arr, n);
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Utility function to print
// the contents of an array
function printArr($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i] . " ";
}

// Function to update the array
function updateArr($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
    {

        // In case of even positioned element
        if (($i + 1) % 2 == 0)
            $arr[$i] = pow($arr[$i], 2);

        // Odd positioned element
        else
            $arr[$i] = pow($arr[$i], 3);
    }

    // Print the updated array
    printArr($arr, $n);
}

// Driver code
$arr = array( 2, 3, 4, 5, 6 );
$n = count($arr);

updateArr($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Utility function to print
    // the contents of an array
    function printArr(arr , n) {
        for (i = 0; i < n; i++)
            document.write(arr[i] + " ");
    }

    // Function to update the array
    function updateArr(arr , n) {
        for (i = 0; i < n; i++) {

            // In case of even positioned element
            if ((i + 1) % 2 == 0)
                arr[i] = parseInt( Math.pow(arr[i], 2));

            // Odd positioned element
            else
                arr[i] = parseInt( Math.pow(arr[i], 3));
        }

        // Print the updated array
        printArr(arr, n);
    }

    // Driver code

        var arr = [ 2, 3, 4, 5, 6 ];
        var n = arr.length;

        updateArr(arr, n);

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
8 9 64 25 216
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*