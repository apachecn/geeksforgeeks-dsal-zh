# 最近使用的 K(MRU)应用程序程序

> 原文:[https://www . geesforgeks . org/program-for-k-最近使用的-mru-apps/](https://www.geeksforgeeks.org/program-for-k-most-recently-used-mru-apps/)

给定一个整数 **K** 和一个由 **N** 个整数组成的数组 **arr[]** ,该数组包含系统中打开的应用的**id**,其中

1.  **arr[0]** 是当前正在使用的应用程序
2.  **arr[1]** 是最近使用的 app，并且
3.  **arr[N–1]**是最近使用最少的 app。

任务是当使用系统的用户按下 **Alt + Tab** 的次数正好是 **K** 的次数时，打印数组的内容。**注意**按下 **Alt + Tab** 键后，根据按下次数，app 打开指针将从第 0 个索引向右移动，因此按下结束的 app 将移动到第 0 个索引，因为这将成为最近打开的 app。
**举例:**

> **输入:** arr[] = {3，5，2，4，1}，K = 3
> **输出:** 4 3 5 2 1
> 用户想要切换到 id 为 4 的应用，它将成为当前活动的应用，而之前活动的应用(id 为 3)将是最近使用的应用。
> **输入:** arr[] = {5，7，2，3，4，1，6}，K = 10
> **输出:** 3 5 7 2 4 1 6

**方式:**获取用户想要切换到的 app 的索引，即 **appIndex = K % N** 。现在，当前活动的应用程序将是**arr【appIndex】**，并且索引范围**【0，appIndex–1】**中的所有其他应用程序将必须向右移动 1 个元素。
以下是上述方法的实施:

## C++14

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to update the array
// in most recently used fashion
void mostRecentlyUsedApps(int* arr, int N, int K)
{
    int app_index = 0;

    // Finding the end index after K presses
    app_index = (K % N);

    // Shifting elements by 1 towards the found index
    // on which the K press ends
    int x = app_index, app_id = arr[app_index];
    while (x > 0) {
        arr[x] = arr[--x];
    }

    // Update the current active app
    arr[0] = app_id;
}

// Utility function to print
// the contents of the array
void printArray(int* arr, int N)
{
    for (int i = 0; i < N; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int K = 3;
    int arr[] = { 3, 5, 2, 4, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    mostRecentlyUsedApps(arr, N, K);
    printArray(arr, N);
    return 0;
}
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to update the array
// in most recently used fashion
static void mostRecentlyUsedApps(int []arr, int N, int K)
{
    int app_index = 0;

    // Finding the end index after K presses
    app_index = (K % N);

    // Shifting elements by 1 towards the found index
    // on which the K press ends
    int x = app_index, app_id = arr[app_index];
    while (x > 0)
    {
        arr[x] = arr[--x];
    }

    // Update the current active app
    arr[0] = app_id;
}

// Utility function to print
// the contents of the array
static void printArray(int []arr, int N)
{
    for (int i = 0; i < N; i++)
        Console.Write(arr[i]+" ");
}

// Driver code
static void Main()
{
    int K = 3;
    int []arr = { 3, 5, 2, 4, 1 };
    int N = arr.Length;

    mostRecentlyUsedApps(arr, N, K);
    printArray(arr, N);
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to update the array
// in most recently used fashion
function mostRecentlyUsedApps(arr, N, K) {
    let app_index = 0;

    // Finding the end index after K presses
    app_index = (K % N);

    // Shifting elements by 1 towards the found index
    // on which the K press ends
    let x = app_index, app_id = arr[app_index];
    while (x > 0) {
        arr[x] = arr[--x];
    }

    // Update the current active app
    arr[0] = app_id;
}

// Utility function to print
// the contents of the array
function printArray(arr, N) {
    for (let i = 0; i < N; i++)
        document.write(arr[i] + " ");
}

// Driver code

let K = 3;
let arr = [3, 5, 2, 4, 1];
let N = arr.length;

mostRecentlyUsedApps(arr, N, K);
printArray(arr, N);

// This code is contributed by gfgking.
</script>
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
    public static void main(String[] args)
    {
        int[] num = { 3, 5, 2, 4, 1 };
        int size = num.length;
        // 8,6,7,9,0,2,1,12,89
        int d = 3;

        int appIndex = d % size;
        int appId = num[appIndex];

        for (int i = appIndex; i > 0; i--) {
            num[i] = num[i - 1];
        }
        num[0] = appId;

        for (int i = 0; i < num.length; i++) {
            System.out.print(" " + num[i]);
        }
    }
}
```

**Output**

```
4 3 5 2 1 
```

**时间复杂度:** O(N)