# 打印一个数组中所有最大递增的连续子数组

> 原文:[https://www . geeksforgeeks . org/print-all-maximum-递增-连续-阵列中的子阵列/](https://www.geeksforgeeks.org/print-all-maximal-increasing-contiguous-sub-array-in-an-array/)

给定一个数组 **arr[]** ，任务是找到给定数组中所有最大的连续递增子数组。

**示例**:

> **输入:**
> arr[] = { 80，50，60，70，40，50，80，70 }
> **输出:**
> 80
> 50 60 70
> 40 50 80
> 70
> 
> **输入:**
> arr[] = { 10，20，23，12，5，4，61，67，87，9 }
> **输出:**
> 10 20 23
> 12
> 5
> 4 61 67 87
> 9

**方法:**迭代数组，将每个元素与其下一个相邻元素进行比较，如果小于下一个元素，则打印它，否则在下一行单独打印它。
以下是上述办法的实施情况。

## C++

```
// C++ Implementation to print all the
// Maximal Increasing Sub-array of array
#include <bits/stdc++.h>
using namespace std;

// Function to print each of maximal
// contiguous increasing subarray
void printmaxSubseq(int arr[], int n)
{
    int i;

    // Loop to iterate through the array and print
    // the maximal contiguous increasing subarray.
    for (i = 0; i < n; i++) {
        // Condition to check whether the element at i, is
        // greater than its next neighbouring element or not.
        if (arr[i] < arr[i + 1])
            cout << arr[i] << " ";
        else
            cout << arr[i] << "\n";
    }
}

// Driver function
int main()
{
    int arr[] = { 9, 8, 11, 13, 10, 15, 14, 16, 20, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printmaxSubseq(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation to print all the
// Maximal Increasing Sub-array of array
import java.util.*;

class GFG
{

// Function to print each of maximal
// contiguous increasing subarray
static void printmaxSubseq(int arr[], int n)
{
    int i;

    // Loop to iterate through the array and print
    // the maximal contiguous increasing subarray.
    for (i = 0; i < n ; i++)
    {
        // Condition to check whether the element at i, is
        // greater than its next neighbouring element or not.
        if (i + 1 < n && arr[i] < arr[i + 1])
            System.out.print(arr[i] + " ");
        else
            System.out.print(arr[i] + "\n");
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 9, 8, 11, 13, 10, 15, 14, 16, 20, 5 };
    int n = arr.length;
    printmaxSubseq(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 Implementation to print all the
# Maximal Increasing Sub-array of array

# Function to print each of maximal
# contiguous increasing subarray
def printmaxSubseq(arr, n) :

    # Loop to iterate through the array and print
    # the maximal contiguous increasing subarray.
    for i in range(n - 1) :

        # Condition to check whether the element at i, is
        # greater than its next neighbouring element or not.
        if (arr[i] < arr[i + 1]) :
            print(arr[i], end = " ");
        else :
            print(arr[i]);

    print(arr[n - 1]);

# Driver function
if __name__ == "__main__" :

    arr = [ 9, 8, 11, 13, 10, 15, 14, 16, 20, 5 ];
    n = len(arr);
    printmaxSubseq(arr, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# Implementation to print all the
// Maximal Increasing Sub-array of array
using System;

class GFG
{

    // Function to print each of maximal
    // contiguous increasing subarray
    static void printmaxSubseq(int []arr, int n)
    {
        int i;

        // Loop to iterate through the array and print
        // the maximal contiguous increasing subarray.
        for (i = 0; i < n ; i++)
        {
            // Condition to check whether the element at i, is
            // greater than its next neighbouring element or not.
            if (i + 1 < n && arr[i] < arr[i + 1])
                Console.Write(arr[i] + " ");
            else
                Console.WriteLine(arr[i]);
        }
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 9, 8, 11, 13, 10, 15, 14, 16, 20, 5 };
        int n = arr.Length;
        printmaxSubseq(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript Implementation to print all the
// Maximal Increasing Sub-array of array

// Function to print each of maximal
// contiguous increasing subarray
function printmaxSubseq(arr, n)
{
    let i;

    // Loop to iterate through the array and print
    // the maximal contiguous increasing subarray.
    for (i = 0; i < n; i++) {
        // Condition to check whether the element at i, is
        // greater than its next neighbouring element or not.
        if (arr[i] < arr[i + 1])
            document.write(arr[i] + " ");
        else
            document.write(arr[i] + "<br>");
    }
}

// Driver function

let arr = [ 9, 8, 11, 13, 10, 15, 14, 16, 20, 5 ];
let n = arr.length;
printmaxSubseq(arr, n);
</script>
```

**Output:** 

```
9
8 11 13
10 15
14 16 20
5
```

**时间复杂度:** O(n)