# 生成 N 长度阵列，其中非递减子阵列的长度最大，并且第一个和最后一个阵列元素之间的差异最小

> 原文:[https://www . geeksforgeeks . org/generate-an-n-length-array-具有非递减长度的子阵列-最大化和最小化第一个和最后一个阵列元素之间的差异/](https://www.geeksforgeeks.org/generate-an-n-length-array-having-length-of-non-decreasing-subarrays-maximized-and-minimum-difference-between-first-and-last-array-elements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[ ]** ，任务是打印一个 **N** 长度的数组，其所有非递减子数组的长度之和最大，第一个和最后一个元素之间的差最小。

**示例:**

> **输入:** N = 5，arr = {4，3，5，3，2}
> **输出:** {3，4，5，2，3}
> **说明:**第一个和最后一个元素的差最小，即 3–3 = 0，非递减子阵的和最大，即
> 1。{3，4，5}，长度= 3
> 2。{2，3}，长度= 2
> 因此非递减子阵列之和为 5。
> 
> **输入:** N = 8，arr = {4，6，2，6，8，2，6，4}
> **输出:** {2，4，4，6，6，6，8，2}

**进场:**问题可以解决 [**贪婪地**](https://www.geeksforgeeks.org/greedy-algorithms/) 。按照以下步骤解决问题:

*   [**按非递减顺序排列数组 arr[]**](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)。
*   求差最小的两个连续元素的指数，说 **i** 和 **i + 1** 。
*   将 **arr[0]** 替换为 **arr[i]** ，将 **arr[N]** 替换为 **arr[i + 1]** 。
*   将**arr[1:I–1]**替换为**arr[I+2:N–1]**。
*   打印数组 **arr[ ]** 。

下面是上述方法的实现:

## C++

```
// C++ program for above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print target array
void printArr(int arr[], int n)
{

    // Sort the given array
    sort(arr, arr + n);

    // Seeking for index of elements with minimum diff.
    int minDifference = INT_MAX;
    int minIndex = -1;

    // Seeking for index
    for (int i = 1; i < n; i++) {

        if (minDifference
            > abs(arr[i] - arr[i - 1])) {

            minDifference = abs(arr[i] - arr[i - 1]);
            minIndex = i - 1;
        }
    }

    // To store target array
    int Arr[n];

    Arr[0] = arr[minIndex];
    Arr[n - 1] = arr[minIndex + 1];
    int pos = 1;

    // Copying element
    for (int i = minIndex + 2; i < n; i++) {

        Arr[pos++] = arr[i];
    }

    // Copying remaining element
    for (int i = 0; i < minIndex; i++) {

        Arr[pos++] = arr[i];
    }

    // Printing target array
    for (int i = 0; i < n; i++) {

        cout << Arr[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given Input
    int N = 8;
    int arr[] = { 4, 6, 2, 6, 8, 2, 6, 4 };

    // Function Call
    printArr(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to print target array    
public static void printArr(int arr[], int n)
{

    // Sort the given array
    Arrays.sort(arr);

    // Seeking for index of elements
    // with minimum diff.
    int minDifference = 1000000007;
    int minIndex = -1;

    // Seeking for index
    for(int i = 1; i < n; i++)
    {
        if (minDifference >
            Math.abs(arr[i] - arr[i - 1]))
        {
            minDifference = Math.abs(arr[i] -
                                     arr[i - 1]);
            minIndex = i - 1;
        }
    }

    // To store target array
    int Arr[] = new int[n];

    Arr[0] = arr[minIndex];
    Arr[n - 1] = arr[minIndex + 1];
    int pos = 1;

    // Copying element
    for(int i = minIndex + 2; i < n; i++)
    {
        Arr[pos++] = arr[i];
    }

    // Copying remaining element
    for(int i = 0; i < minIndex; i++)
    {
        Arr[pos++] = arr[i];
    }

    // Printing target array
    for(int i = 0; i < n; i++)
    {
        System.out.print(Arr[i] + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 8;
    int arr[] = { 4, 6, 2, 6, 8, 2, 6, 4 };

    // Function Call
    printArr(arr, N);
}
}

// This code is contributed by maddler
```

## 蟒蛇 3

```
# Python3 program for above approach
import sys

# Function to print target array
def printArr(arr, n):

    # Sort the given array
    arr.sort()

    # Seeking for index of elements with minimum diff.
    minDifference = sys.maxsize
    minIndex = -1

    # Seeking for index
    for i in range(1,n,1):
        if (minDifference > abs(arr[i] - arr[i - 1])):

            minDifference = abs(arr[i] - arr[i - 1])
            minIndex = i - 1

    # To store target array
    Arr = [0 for i in range(n)]

    Arr[0] = arr[minIndex]
    Arr[n - 1] = arr[minIndex + 1]
    pos = 1

    # Copying element
    for i in range(minIndex + 2,n,1):
        Arr[pos] = arr[i]
        pos += 1

    # Copying remaining element
    for i in range(minIndex):
        Arr[pos] = arr[i]
        pos += 1

    # Printing target array
    for i in range(n):
        print(Arr[i],end = " ")

# Driver Code
if __name__ == '__main__':
    # Given Input
    N = 8
    arr = [4, 6, 2, 6, 8, 2, 6, 4]

    # Function Call
    printArr(arr, N)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to print target array    
public static void printArr(int []arr, int n)
{

    // Sort the given array
    Array.Sort(arr);

    // Seeking for index of elements
    // with minimum diff.
    int minDifference = 1000000007;
    int minIndex = -1;

    // Seeking for index
    for(int i = 1; i < n; i++)
    {
        if (minDifference >
            Math.Abs(arr[i] - arr[i - 1]))
        {
            minDifference = Math.Abs(arr[i] -
                                     arr[i - 1]);
            minIndex = i - 1;
        }
    }

    // To store target array
    int []Arr = new int[n];

    Arr[0] = arr[minIndex];
    Arr[n - 1] = arr[minIndex + 1];
    int pos = 1;

    // Copying element
    for(int i = minIndex + 2; i < n; i++)
    {
        Arr[pos++] = arr[i];
    }

    // Copying remaining element
    for(int i = 0; i < minIndex; i++)
    {
        Arr[pos++] = arr[i];
    }

    // Printing target array
    for(int i = 0; i < n; i++)
    {
        Console.Write(Arr[i] + " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    int N = 8;
    int []arr = { 4, 6, 2, 6, 8, 2, 6, 4 };

    // Function Call
    printArr(arr, N);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program for above approach

// Function to print target array
function printArr(arr, n)
{

    // Sort the given array
    arr.sort((a, b) => a - b);

    // Seeking for index of elements
    // with minimum diff.
    let minDifference = Number.MAX_SAFE_INTEGER;
    let minIndex = -1;

    // Seeking for index
    for(let i = 1; i < n; i++)
    {
        if (minDifference > Math.abs(arr[i] - arr[i - 1]))
        {
            minDifference = Math.abs(arr[i] - arr[i - 1]);
            minIndex = i - 1;
        }
    }

    // To store target array
    let Arr = new Array(n);

    Arr[0] = arr[minIndex];
    Arr[n - 1] = arr[minIndex + 1];
    let pos = 1;

    // Copying element
    for(let i = minIndex + 2; i < n; i++)
    {
        Arr[pos++] = arr[i];
    }

    // Copying remaining element
    for(let i = 0; i < minIndex; i++)
    {
        Arr[pos++] = arr[i];
    }

    // Printing target array
    for(let i = 0; i < n; i++)
    {
        document.write(Arr[i] + " ");
    }
}

// Driver Code

// Given Input
let N = 8;
let arr = [ 4, 6, 2, 6, 8, 2, 6, 4 ];

// Function Call
printArr(arr, N);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
2 4 4 6 6 6 8 2
```

***时间复杂度:**T3】O(N * logN)
T5】T6】辅助空间:T8】O(N)*