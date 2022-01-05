# 排序一个接近排序(或 K 排序)的数组|集合 2 (Gap 方法–Shell 排序)

> 原文:[https://www . geesforgeks . org/sort-a-近排序-or-k-sorted-array-set-2-gap-method-shell-sort/](https://www.geeksforgeeks.org/sort-a-nearly-sorted-or-k-sorted-array-set-2-gap-method-shell-sort/)

给定一个由 **N** 个元素组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、 **arr[]** ，其中每个元素最多离开其目标位置 **K** ，任务是设计一个算法，在 **O(N*log(K))** 时间内进行排序。

**示例:**

> **输入:** arr[] = {10，9，8，7，4，70，60，50}，K = 4
> **输出:** 4 7 8 9 10 50 60 70
> **解释:**
> 按照以下步骤对数组进行排序:
> 
> 1.  从间隙= K(即 4)开始
>     *   **10** 9 8 7 **4** 70 60 50，交换指数 0 和 4 的元素。然后数组修改为{4，9，8，7，10，70，60，50}。
>         4**9**8 7 10**70**60 50，不要交换索引 1 和索引 5 的元素。
>         4 9**8**7 10 70**60**50，不要交换索引 2 和 6 的元素。
>         4 9 8**7**10 70 60**50、**不要交换指数 3 和 7 的元素。
> 2.  间隙= 4/2 = 2 的上限
>     *   **4** 9 **8** 7 10 70 60 50，不要交换指数 0 和 2 的元素。
>         4**9**8**7**10 70 60 50，交换指数 1 和 3 的元素。然后数组修改为{4，7，8，9，10，70，60，50}。
>         4 7**8**9**10**70 60 50，不要交换索引 2 和 4 的元素。
>         4 7 8**9**10**70**60 50，不要交换索引 3 和索引 5 的元素。
>         4 7 8 9**10**70**60**50，不要交换索引 4 和 6 的元素。
>         4 7 8 9 10**70**60**50、**在索引 5 和 7 处交换元素。然后数组修改为{4，7，8，9，10，70，60，50}。
>         4 7 8 9 10 50 60 70
> 3.  间隙= 2/2 = 1 的上限
>     *   **4** **7** 8 9 10 50 60 70，不要交换指数 0 和 1 的元素。
>         4 **7 8** 9 10 50 60 70，不要交换指数 1 和 2 的元素。
>         4 7 **8 9** 10 50 60 70，不要交换索引 2 和索引 3 的元素。
>         4 7 8 **9 10** 50 60 70，不要交换索引 3 和 4 的元素。
>         4 7 8 9 **10 50** 60 70，不要交换索引 4 和索引 5 的元素。
>         4 7 8 9 10 **50 60** 70，不要交换索引 5 和 6 的元素。
>         4 7 8 9 10 50 **60 70、**不要互换指数 6 和 7 的元素。
> 
> **输入:** arr[] = {6，5，3，2，8，10，9}，K = 3
> **输出:** 2 3 5 6 8 9 10

**方法:**给定问题[排序一个接近排序(或 K 排序)的数组](https://www.geeksforgeeks.org/nearly-sorted-algorithm/)已经解决。这里的思路是使用[外壳排序](https://www.geeksforgeeks.org/shellsort/)对数组进行排序。这里使用的思想类似于[就地合并排序](https://www.geeksforgeeks.org/in-place-merge-sort/)的合并步骤。按照以下步骤解决问题:

*   初始化一个变量，用值 **K** 表示**间隙**，对每个子列表的每个**间隙<sup>第</sup>** 元素进行排序。
*   重复直到**间隙**大于 **0** ，并执行以下步骤:
    *   使用变量 **i** 迭代范围**【0，N-间隙】**，在每次迭代中，如果 **arr[i]** 大于**arr[I+间隙]，**则交换数组元素。
    *   将**间隙**更新为**间隙=天花板(间隙/2)。**
*   最后，完成上述步骤后[打印数组的元素](https://www.geeksforgeeks.org/java-program-to-print-the-elements-of-an-array/) **arr[]** 。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the nextGap
int nextGap(double k)
{
    if (k < 2)
        return 0;
    return ceil(k / 2);
}

// A utility function to print the array
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}
// Function to sort a K sorted array
void kSort(int arr[], int K, int n)
{

    // Iterate until gap is atleast
    // greater than 0
    for (int gap = K; gap > 0; gap = nextGap(gap)) {

        // Iterate over the range [0, N]
        for (int i = 0; i + gap < n; i++) {

            // If arr[i] is greater
            // than arr[i+gap]
            if (arr[i] > arr[i + gap]) {

                // Swap arr[i] and
                // arr[i+gap]
                swap(arr[i], arr[i + gap]);
            }
        }
    }
    printArray(arr, n);
}

// Driver Code
int main()
{

    // Input
    int arr[] = { 10, 9, 8, 7, 4, 70, 60, 50 };
    int K = 3;
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    kSort(arr, K, n);
    return 0;
}

// This code is contributed by lokesh potta.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Iterator;
import java.util.PriorityQueue;

class GFG {

    // Function to sort a K sorted array
    static void kSort(int[] arr, int K)
    {
        // Iterate until gap is atleast
        // greater than 0
        for (int gap = K; gap > 0; gap = nextGap(gap)) {

            // Iterate over the range [0, N]
            for (int i = 0; i + gap < arr.length; i++) {

                // If arr[i] is greater
                // than arr[i+gap]
                if (arr[i] > arr[i + gap]) {

                    // Swap arr[i] and
                    // arr[i+gap]
                    swap(arr, i, i + gap);
                }
            }
        }
        printArray(arr);
    }

    // Function to find the nextGap
    static int nextGap(double k)
    {
        if (k < 2)
            return 0;
        return (int)Math.ceil(k / 2);
    }

    // Function to swap two elements
    // of the array arr[]
    static void swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // A utility function to print the array
    private static void printArray(int[] arr)
    {
        for (int i = 0; i < arr.length; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Input
        int arr[] = { 10, 9, 8, 7, 4, 70, 60, 50 };
        int K = 3;

        // Function call
        kSort(arr, K);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to find the nextGap
def nextGap(k):

    if (k < 2):
        return 0

    return math.ceil(k / 2)

# A utility function to print array
def printArray(arr, n):

    for i in range(n):
        print(arr[i], end = " ")

# Function to sort a K sorted array
def kSort(arr, K, n):

    # Iterate until gap is atleast
    # greater than 0
    gap = K

    while (gap > 0):

        # Iterate over the range [0, N]
        i = 0
        while (i + gap < n):

            # If arr[i] is greater
            # than arr[i+gap]
            if (arr[i] > arr[i + gap]):

                # Swap arr[i] and
                # arr[i+gap]
                arr[i], arr[i + gap] = arr[i + gap], arr[i]

            i += 1

        gap = nextGap(gap)

    printArray(arr, n)

# Driver Code

# Input
arr = [ 10, 9, 8, 7, 4, 70, 60, 50 ]
K = 3
n = len(arr)

# Function call
kSort(arr, K, n)

# This code is contributed by target_2
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to sort a K sorted array
    static void kSort(int[] arr, int K)
    {
        // Iterate until gap is atleast
        // greater than 0
        for (int gap = K; gap > 0; gap = nextGap(gap)) {

            // Iterate over the range [0, N]
            for (int i = 0; i + gap < arr.Length; i++) {

                // If arr[i] is greater
                // than arr[i+gap]
                if (arr[i] > arr[i + gap]) {

                    // Swap arr[i] and
                    // arr[i+gap]
                    swap(arr, i, i + gap);
                }
            }
        }
        printArray(arr);
    }

    // Function to find the nextGap
    static int nextGap(double k)
    {
        if (k < 2)
            return 0;
        return (int)Math.Ceiling(k / 2);
    }

    // Function to swap two elements
    // of the array arr[]
    static void swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // A utility function to print the array
    private static void printArray(int[] arr)
    {
        for (int i = 0; i < arr.Length; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver Code
    public static void Main(string[] args)
    {
        // Input
        int []arr = { 10, 9, 8, 7, 4, 70, 60, 50 };
        int K = 3;

        // Function call
        kSort(arr, K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the nextGap
function nextGap(k)
{
    if (k < 2)
        return 0;

    return Math.ceil(k / 2);
}

// A utility function to print the array
function printArray(arr, n)
{
    for(let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Function to sort a K sorted array
function kSort(arr, K, n)
{

    // Iterate until gap is atleast
    // greater than 0
    for(let gap = K; gap > 0; gap = nextGap(gap))
    {

        // Iterate over the range [0, N]
        for(let i = 0; i + gap < n; i++)
        {

            // If arr[i] is greater
            // than arr[i+gap]
            if (arr[i] > arr[i + gap])
            {

                // Swap arr[i] and
                // arr[i+gap]
                let temp = arr[i];
                arr[i] = arr[i + gap];
                arr[i + gap] = temp;
            }
        }
    }
    printArray(arr, n);
}

// Driver Code

// Input
let arr = [ 10, 9, 8, 7, 4, 70, 60, 50 ];
let K = 3;
let n = arr.length;

// Function call
kSort(arr, K, n);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output**

```
4 7 8 9 10 50 60 70 
```

***时间复杂度:** O(N*log K)*
***辅助空间:** O(1)*