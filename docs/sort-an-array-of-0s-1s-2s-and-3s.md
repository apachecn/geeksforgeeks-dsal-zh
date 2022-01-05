# 对 0、1、2s 和 3s 的数组进行排序

> 原文:[https://www . geesforgeks . org/sort-a-array-0s-1s-2s-和-3s/](https://www.geeksforgeeks.org/sort-an-array-of-0s-1s-2s-and-3s/)

给定一个由 **0** 、 **1** 、 **2** 和 **3** 组成的大小为 **N** 的[数组 **arr[]** ，任务是](https://www.geeksforgeeks.org/introduction-to-arrays/)[按照升序排列给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。

**示例:**

> **输入:** arr[] = {0，3，1，2，0，3，1，2}
> **输出:**0 0 1 2 3 3
> 
> **输入:** arr[] = {0，1，3，1，0，1，3，2，1，2，0，3，0，1}
> **输出:**0 0 0 1 1 1 1 2 3 3

**方法:**给定的问题可以基于本文中讨论的方法来解决。其思想是首先将所有的 **0s** 和 **3s** 定位在数组的开头和结尾，然后对整数 **1** 和 **2** 的出现进行排序。

按照以下步骤解决问题:

*   初始化三个变量，比如 **i** 、**中**和 **j** 。将 **i** 和 **mid** 的值设置为 **0** ，将 **j** 设置为**(N–1)**。
*   [重复一个循环](https://www.geeksforgeeks.org/range-based-loop-c/)直到 **mid ≤ j** ，并执行以下步骤:
    *   如果 **arr[mid]** 的值为 **0** ，则交换 **arr[i]** 和 **arr[mid]** ，并将 **i** 和 **mid** 的值增加 **1** 。
    *   否则，如果 **arr[mid]** 的值为 **3** ，则交换 **arr[mid]** 和 **arr[j]** ，并将 **j** 减 **1** 。
    *   否则，如果**arr【I】**的值为 **1** 或 **2** ，则将**中间**的值增加 **1** 。
*   现在到[通过迭代直到 **i ≤ j** 对范围**【I，j】**内的子阵列](https://www.geeksforgeeks.org/stdpartial_sort-in-cpp/)进行排序，并执行以下操作:
    *   如果 **arr[i]** 的值为 **2** ，则用 **1** 交换 **arr[i]** 和 **arr[j]** 并将的值减去 **j** 。
    *   否则，将 **i** 的值增加 **1** 。
*   完成上述步骤后，[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **arr[]** 作为结果排序数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to sort the array having
// array element only 0, 1, 2, and 3
void sortArray(int arr[], int N)
{
    int i = 0, j = N - 1, mid = 0;

    // Iterate until mid <= j
    while (mid <= j) {

        // If arr[mid] is 0
        if (arr[mid] == 0) {

            // Swap integers at
            // indices i and mid
            swap(arr[i], arr[mid]);

            // Increment i
            i++;

            // Increment mid
            mid++;
        }

        // Otherwise if the value of
        // arr[mid] is 3
        else if (arr[mid] == 3) {

            // Swap arr[mid] and arr[j]
            swap(arr[mid], arr[j]);

            // Decrement j
            j--;
        }

        // Otherwise if the value of
        // arr[mid] is either 1 or 2
        else if (arr[mid] == 1
                 || arr[mid] == 2) {

            // Increment the value of mid
            mid++;
        }
    }

    // Iterate until i <= j
    while (i <= j) {

        // If arr[i] the value of is 2
        if (arr[i] == 2) {

            // Swap arr[i] and arr[j]
            swap(arr[i], arr[j]);

            // Decrement j
            j--;
        }

        // Otherwise, increment i
        else {
            i++;
        }
    }

    // Print the sorted array arr[]
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 1, 0, 2, 3, 1, 0 };
    int N = sizeof(arr) / sizeof(arr[0]);
    sortArray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to sort the array having
// array element only 0, 1, 2, and 3
static void sortArray(int[] arr, int N)
{
    int i = 0, j = N - 1, mid = 0;

    // Iterate until mid <= j
    while (mid <= j)
    {

        // If arr[mid] is 0
        if (arr[mid] == 0)
        {

            // Swap integers at
            // indices i and mid
            int temp = arr[i];
            arr[i] = arr[mid];
            arr[mid] = temp;

            // Increment i
            i++;

            // Increment mid
            mid++;
        }

        // Otherwise if the value of
        // arr[mid] is 3
        else if (arr[mid] == 3)
        {

            // Swap arr[mid] and arr[j]
            int temp = arr[mid];
            arr[mid] = arr[j];
            arr[j] = temp;

            // Decrement j
            j--;
        }

        // Otherwise if the value of
        // arr[mid] is either 1 or 2
        else if (arr[mid] == 1 || arr[mid] == 2)
        {

            // Increment the value of mid
            mid++;
        }
    }

    // Iterate until i <= j
    while (i <= j)
    {

        // If arr[i] the value of is 2
        if (arr[i] == 2)
        {

            // Swap arr[i] and arr[j]
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;

            // Decrement j
            j--;
        }

        // Otherwise, increment i
        else
        {
            i++;
        }
    }

    // Print the sorted array arr[]
    for(int k = 0; k < N; k++)
    {
        System.out.print(arr[k] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 3, 2, 1, 0, 2, 3, 1, 0 };
    int N = arr.length;

    sortArray(arr, N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to sort the array having
# array element only 0, 1, 2, and 3
def sortArray(arr, N):
    i = 0
    j = N - 1
    mid = 0

    # Iterate until mid <= j
    while (mid <= j):

        # If arr[mid] is 0
        if (arr[mid] == 0):

            # Swap integers at
            # indices i and mid
            arr[i], arr[mid] = arr[mid], arr[i]

            # Increment i
            i += 1

            # Increment mid
            mid += 1

        # Otherwise if the value of
        # arr[mid] is 3
        elif (arr[mid] == 3):

            # Swap arr[mid] and arr[j]
            arr[mid], arr[j] = arr[j], arr[mid]

            # Decrement j
            j -= 1

        # Otherwise if the value of
        # arr[mid] is either 1 or 2
        elif (arr[mid] == 1 or arr[mid] == 2):
            # Increment the value of mid
            mid += 1

    # Iterate until i <= j
    while (i <= j):

        # If arr[i] the value of is 2
        if (arr[i] == 2):

            # Swap arr[i] and arr[j]
            arr[i], arr[j] = arr[j], arr[i]

            # Decrement j
            j -= 1

        # Otherwise, increment i
        else:
            i += 1

    # Print the sorted array arr[]
    for i in range(N):
        print(arr[i], end = " ")

# Driver Code
if __name__ == '__main__':
    arr = [3, 2, 1, 0, 2, 3, 1, 0]
    N = len(arr)
    sortArray(arr, N)

#  This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to sort the array having
// array element only 0, 1, 2, and 3
static void sortArray(int[] arr, int N)
{
    int i = 0, j = N - 1, mid = 0;

    // Iterate until mid <= j
    while (mid <= j)
    {

        // If arr[mid] is 0
        if (arr[mid] == 0)
        {

            // Swap integers at
            // indices i and mid
            int temp = arr[i];
            arr[i] = arr[mid];
            arr[mid] = temp;

            // Increment i
            i++;

            // Increment mid
            mid++;
        }

        // Otherwise if the value of
        // arr[mid] is 3
        else if (arr[mid] == 3)
        {

            // Swap arr[mid] and arr[j]
            int temp = arr[mid];
            arr[mid] = arr[j];
            arr[j] = temp;

            // Decrement j
            j--;
        }

        // Otherwise if the value of
        // arr[mid] is either 1 or 2
        else if (arr[mid] == 1 || arr[mid] == 2)
        {

            // Increment the value of mid
            mid++;
        }
    }

    // Iterate until i <= j
    while (i <= j)
    {

        // If arr[i] the value of is 2
        if (arr[i] == 2)
        {

            // Swap arr[i] and arr[j]
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;

            // Decrement j
            j--;
        }

        // Otherwise, increment i
        else
        {
            i++;
        }
    }

    // Print the sorted array arr[]
    for(int k = 0; k < N; k++)
    {
        Console.Write(arr[k] + " ");
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 3, 2, 1, 0, 2, 3, 1, 0 };
    int N = arr.Length;

    sortArray(arr, N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to sort the array having
// array element only 0, 1, 2, and 3
function sortArray(arr, N)
{
    var i = 0, j = N - 1, mid = 0;

    // Iterate until mid <= j
    while (mid <= j) {

        // If arr[mid] is 0
        if (arr[mid] == 0) {

            // Swap integers at
            // indices i and mid
            var temp = arr[i];
            arr[i] = arr[mid];
            arr[mid] = temp;

            // Increment i
            i++;

            // Increment mid
            mid++;
        }

        // Otherwise if the value of
        // arr[mid] is 3
        else if (arr[mid] == 3) {

            var temp = arr[mid];
            arr[mid] = arr[j];
            arr[j] = temp;

            // Decrement j
            j--;
        }

        // Otherwise if the value of
        // arr[mid] is either 1 or 2
        else if (arr[mid] == 1
                 || arr[mid] == 2) {

            // Increment the value of mid
            mid++;
        }
    }

    // Iterate until i <= j
    while (i <= j) {

        // If arr[i] the value of is 2
        if (arr[i] == 2) {

            // Swap arr[i] and arr[j]
            var temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;

            // Decrement j
            j--;
        }

        // Otherwise, increment i
        else {
            i++;
        }
    }

    // Print the sorted array arr[]
    for (i = 0; i < N; i++) {
        document.write(arr[i] + " ");
    }
}

// Driver Code
    var arr = [3, 2, 1, 0, 2, 3, 1, 0];
    var N = arr.length;
    sortArray(arr, N);

</script>
```

**Output:** 

```
0 0 1 1 2 2 3 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)