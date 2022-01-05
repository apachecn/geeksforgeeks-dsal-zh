# 在循环调度中找到给定 N 个进程的执行顺序

> 原文:[https://www . geeksforgeeks . org/find-循环调度中给定 n 个进程的执行顺序/](https://www.geeksforgeeks.org/find-the-order-of-execution-of-given-n-processes-in-round-robin-scheduling/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**表示使用[循环算法](https://www.geeksforgeeks.org/program-round-robin-scheduling-set-1/)调度的 **N 个**进程的突发时间，给定时间量 **Q** 。假设所有流程都在时间 **t = 0** 到达，任务是找到流程执行的顺序。

**示例:**

> **输入:** arr[] = {3，7，4}，q = 3
> **输出:** 0 2 1
> **解释:**
> 执行顺序如下 P0，P1，P2，P1，P2，P1
> 由于 P0 的爆发时间为 3，量子时间也为 3，先完成。
> P1 的爆发时间为 7，因此在执行 3 个单元后，它会进行上下文切换，P2 会执行。
> P2 的突发时间为 4，因此在执行 3 个单元后，它会进行上下文切换，P1 会执行。
> P1 再次开始执行，因为它还有 4 个单位的突发时间，所以它执行另外 3 个单位，然后上下文切换。
> 现在，流程 P2 执行 1 个单元并完成。
> 最终过程 P1 完成。
> 他们按照 P1 P2 P0 的顺序完成处决。
> 
> **输入:** arr[] = {13，8，5}，q = 6
> **输出:** 2 1 0
> **解释:**
> 最初 P0 开始，6 个单位后，其上下文切换。
> P1 执行 6 个单元和上下文切换。
> 由于 P2 的爆发时间比量子时间短，所以执行 5 个单位，先完成。
> P0 剩余突发时间 7 个单位，因此再次执行 6 个单位和上下文切换。
> P1 剩余爆发时间为 2 单位，第二次完成。
> 最终，过程 P0 完成。
> 他们按照 P2、P1、P0 的顺序完成处决。

**方法:**想法是创建一个包含进程与 [CPU](https://www.geeksforgeeks.org/difference-between-cpu-and-gpu/) 交互次数的**频率**的辅助数组。然后 **freq[]** 数组可以按照频率递增的顺序排序。频率最低的过程首先完成，然后是第二个过程，依此类推。**排序的**数组给出了过程的顺序完成。以下是步骤:

*   初始化一个数组 **freq[]** ，其中 **freq[i]** 是 **i <sup>th</sup>** 进程与 CPU 交互的次数。
*   初始化数组**订单【】**存储**完成流程的订单**并存储**订单【I】= I**。
*   [按照**freq【】**的递增顺序对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **进行排序，使得**freq[顺序[I]]≤freq[顺序[I+1]]【T7]。****
*   打印数组**顺序[]** ，这是进程完成执行的顺序。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to sort the array order[]
// on the basis of the array freq[]
void merge(int* order, int* freq, int i,
           int mid, int j)
{
    int tempOrder[j - i + 1];
    int temp = mid + 1, index = -1;

    while (i <= mid && temp <= j) {

        // If order[i]th is less than
        // order[temp]th process
        if (freq[order[i]]
            <= freq[order[temp]]) {
            tempOrder[++index] = order[i++];
        }

        // Otherwise
        else {
            tempOrder[++index] = order[temp++];
        }
    }

    // Add the left half to tempOrder[]
    while (i <= mid) {
        tempOrder[++index] = order[i++];
    }

    // Add right half to tempOrder[]
    while (temp <= j) {
        tempOrder[++index] = order[temp++];
    }

    // Copy the tempOrder[] array to
    // order[] array
    for (index; index >= 0; index--) {
        order[j--] = tempOrder[index];
    }
}

// Utility function to sort the array
// order[] on the basis of freq[]
void divide(int* order, int* freq,
            int i, int j)
{
    // Base Case
    if (i >= j)
        return;

    // Divide array into 2 parts
    int mid = i / 2 + j / 2;

    // Sort the left array
    divide(order, freq, i, mid);

    // Sort the right array
    divide(order, freq, mid + 1, j);

    // Merge the sorted arrays
    merge(order, freq, i, mid, j);
}

// Function to find the order of
// processes in which execution occurs
void orderProcesses(int A[], int N, int q)
{
    int i = 0;

    // Store the frequency
    int freq[N];

    // Find elements in array freq[]
    for (i = 0; i < N; i++) {
        freq[i] = (A[i] / q)
                  + (A[i] % q > 0);
    }

    // Store the order of completion
    // of processes
    int order[4];

    // Initialize order[i] as i
    for (i = 0; i < N; i++) {
        order[i] = i;
    }

    // Function Call to find the order
    // of execution
    divide(order, freq, 0, N - 1);

    // Print order of completion
    // of processes
    for (i = 0; i < N; i++) {
        cout << order[i] << "  ";
    }
}

// Driver Code
int main()
{
    // Burst Time of the processes
    int arr[] = { 3, 7, 4 };

    // Quantum Time
    int Q = 3;

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    orderProcesses(arr, N, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to sort the array order[]
// on the basis of the array freq[]
static void merge(int order[], int freq[], int i,
           int mid, int j)
{
    int tempOrder[] = new int[j - i + 1];
    int temp = mid + 1, index = -1;

    while (i <= mid && temp <= j)
    {

        // If order[i]th is less than
        // order[temp]th process
        if (freq[order[i]]
            <= freq[order[temp]])
        {
            tempOrder[++index] = order[i++];
        }

        // Otherwise
        else
        {
            tempOrder[++index] = order[temp++];
        }
    }

    // Add the left half to tempOrder[]
    while (i <= mid)
    {
        tempOrder[++index] = order[i++];
    }

    // Add right half to tempOrder[]
    while (temp <= j)
    {
        tempOrder[++index] = order[temp++];
    }

    // Copy the tempOrder[] array to
    // order[] array
  int ind= index;
    for (index= ind; index >= 0; index--)
    {
        order[j--] = tempOrder[index];
    }
}

// Utility function to sort the array
// order[] on the basis of freq[]
static void divide(int order[], int freq[],
            int i, int j)
{
    // Base Case
    if (i >= j)
        return;

    // Divide array into 2 parts
    int mid = i / 2 + j / 2;

    // Sort the left array
    divide(order, freq, i, mid);

    // Sort the right array
    divide(order, freq, mid + 1, j);

    // Merge the sorted arrays
    merge(order, freq, i, mid, j);
}

// Function to find the order of
// processes in which execution occurs
static void orderProcesses(int A[], int N, int q)
{
    int i = 0;

    // Store the frequency
    int freq[] = new int[N];

    // Find elements in array freq[]
    for (i = 0; i < N; i++)
    {
        freq[i] = (A[i] / q);
        if (A[i] % q > 0)
              freq[i] += 1;
    }

    // Store the order of completion
    // of processes
    int order[] = new int[4];

    // Initialize order[i] as i
    for (i = 0; i < N; i++) {
        order[i] = i;
    }

    // Function Call to find the order
    // of execution
    divide(order, freq, 0, N - 1);

    // Print order of completion
    // of processes
    for (i = 0; i < N; i++) {
        System.out.print( order[i] + "  ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Burst Time of the processes
    int arr[] = { 3, 7, 4 };

    // Quantum Time
    int Q = 3;

    int N = arr.length;

    // Function Call
    orderProcesses(arr, N, Q);
}
}

// This code is contributed by chitranayal.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to sort the array order[]
// on the basis of the array freq[]
static void merge(int[] order, int[] freq, int i,
                  int mid, int j)
{
    int[] tempOrder = new int[j - i + 1];
    int temp = mid + 1, index = -1;

    while (i <= mid && temp <= j)
    {

        // If order[i]th is less than
        // order[temp]th process
        if (freq[order[i]] <= freq[order[temp]])
        {
            tempOrder[++index] = order[i++];
        }

        // Otherwise
        else
        {
            tempOrder[++index] = order[temp++];
        }
    }

    // Add the left half to tempOrder[]
    while (i <= mid)
    {
        tempOrder[++index] = order[i++];
    }

    // Add right half to tempOrder[]
    while (temp <= j)
    {
        tempOrder[++index] = order[temp++];
    }

    // Copy the tempOrder[] array to
    // order[] array
    int ind = index;
    for(index = ind; index >= 0; index--)
    {
        order[j--] = tempOrder[index];
    }
}

// Utility function to sort the array
// order[] on the basis of freq[]
static void divide(int[] order, int[] freq,
                   int i, int j)
{

    // Base Case
    if (i >= j)
        return;

    // Divide array into 2 parts
    int mid = i / 2 + j / 2;

    // Sort the left array
    divide(order, freq, i, mid);

    // Sort the right array
    divide(order, freq, mid + 1, j);

    // Merge the sorted arrays
    merge(order, freq, i, mid, j);
}

// Function to find the order of
// processes in which execution occurs
static void orderProcesses(int[] A, int N, int q)
{
    int i = 0;

    // Store the frequency
    int[] freq = new int[N];

    // Find elements in array freq[]
    for(i = 0; i < N; i++)
    {
        freq[i] = (A[i] / q);

        if (A[i] % q > 0)
              freq[i] += 1;
    }

    // Store the order of completion
    // of processes
    int[] order = new int[4];

    // Initialize order[i] as i
    for(i = 0; i < N; i++)
    {
        order[i] = i;
    }

    // Function Call to find the order
    // of execution
    divide(order, freq, 0, N - 1);

    // Print order of completion
    // of processes
    for(i = 0; i < N; i++)
    {
        Console.Write( order[i] + "  ");
    }
}

// Driver Code
public static void Main()
{

    // Burst Time of the processes
    int[] arr = { 3, 7, 4 };

    // Quantum Time
    int Q = 3;

    int N = arr.Length;

    // Function Call
    orderProcesses(arr, N, Q);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to sort the array order[]
// on the basis of the array freq[]
function merge(order, freq, i, mid, j)
{
    var tempOrder = Array(j - i + 1);
    var temp = mid + 1, index = -1;

    while (i <= mid && temp <= j) {

        // If order[i]th is less than
        // order[temp]th process
        if (freq[order[i]]
            <= freq[order[temp]]) {
            tempOrder[++index] = order[i++];
        }

        // Otherwise
        else {
            tempOrder[++index] = order[temp++];
        }
    }

    // Add the left half to tempOrder[]
    while (i <= mid) {
        tempOrder[++index] = order[i++];
    }

    // Add right half to tempOrder[]
    while (temp <= j) {
        tempOrder[++index] = order[temp++];
    }

    // Copy the tempOrder[] array to
    // order[] array
    for (index; index >= 0; index--) {
        order[j--] = tempOrder[index];
    }
}

// Utility function to sort the array
// order[] on the basis of freq[]
function divide(order, freq, i, j)
{
    // Base Case
    if (i >= j)
        return;

    // Divide array into 2 parts
    var mid = parseInt(i / 2) + parseInt(j / 2);

    // Sort the left array
    divide(order, freq, i, mid);

    // Sort the right array
    divide(order, freq, mid + 1, j);

    // Merge the sorted arrays
    merge(order, freq, i, mid, j);
}

// Function to find the order of
// processes in which execution occurs
function orderProcesses(A, N, q)
{
    var i = 0;

    // Store the frequency
    var freq = Array(N);

    // Find elements in array freq[]
    for (i = 0; i < N; i++) {
        freq[i] = (A[i] / q)
                  + (A[i] % q > 0);
    }

    // Store the order of completion
    // of processes
    var order = Array(4);

    // Initialize order[i] as i
    for (i = 0; i < N; i++) {
        order[i] = i;
    }

    // Function Call to find the order
    // of execution
    divide(order, freq, 0, N - 1);

    // Print order of completion
    // of processes
    for (i = 0; i < N; i++) {
        document.write( order[i] + "  ");
    }
}

// Driver Code

// Burst Time of the processes
var arr = [3, 7, 4];

// Quantum Time
var Q = 3;
var N = arr.length;

// Function Call
orderProcesses(arr, N, Q);

</script>
```

**Output:** 

```
0  2  1
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*