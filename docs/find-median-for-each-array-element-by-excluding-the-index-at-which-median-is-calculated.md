# 通过排除计算中值的指数，找出每个数组元素的中值

> 原文:[https://www . geeksforgeeks . org/find-每个数组元素的中值，不包括计算中值的索引/](https://www.geeksforgeeks.org/find-median-for-each-array-element-by-excluding-the-index-at-which-median-is-calculated/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[]** ，其中 **N** 为**偶数，**。任务是生成一个中值数组，其中数组的[中值](https://www.geeksforgeeks.org/median-two-sorted-arrays-different-sizes-ologminn-m/)是通过取数组 **A[]** 的中值，不包括**A[I]-第**个元素来计算的。

**示例:**

> **输入** N = 4，A =【2，4，4，3】
> **输出:**【4，3，3，4】
> **说明:**去掉 A 后的中位数【0】:新排序数组将为【3，4，4】。中位数= 4。
> 移除 A[1]后的中位数:新排序数组将为[2，3，4]。中位数= 3。
> 移除 A[0]后的中位数:新排序数组将为[2，3，4]。中位数= 3。
> 移除 A[0]后的中位数:新排序数组将为[2，4，4]。中位数= 4。
> 
> **输入:** N = 6，A = [5，5，4，4，3，3]
> **输出:**【4，4，4，4，4，4】

**天真方法:**对于范围**【0，N】**中的每个 **i** 移除当前元素并[排序](https://www.geeksforgeeks.org/quick-sort/)剩余数组，然后计算新数组的中值。
***时间复杂度:**O(N * N * log(N))*
***辅助空间:** O(N)*

**有效途径:**由于 **N** 为偶数，当前数组中有两个中心元素，可以是当前数组的中值。去掉任何一个元素，就会有奇数个元素，其中一个中心元素永远是答案。让我们表示两个中心值为 **L** 和 **R** 。有两种可能的情况——当当前**A【I】<= L**时，那么 **R** 将是数组的最终中值。否则，当当前**A【I】>= R**时，则 **L** 将是数组的最终中值。按照以下步骤解决问题:

*   [初始化一个数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **B[]** 来存储数组中元素的原始位置。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下步骤:
    *   将**A【I】**存储在新数组**B【I】中。**
*   [排序阵](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/) **A[]** 找到中心元素。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下步骤:
    *   如果 **B[i]** 小于或等于 **L，**则 **R** 将是除 **A[i]之外的数组中值。**
    *   否则， **L** 将是所需的中间值。

下面是上述方法的实现。

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return Median array after
// excluding each individual element
int findMedianExcludedArray(int A[], int N)
{

    // Store the original array in another
    // array to store the sorted version
    // and the original position of the array
    // element is also important
    int B[N];
    for (int i = 0; i < N; i++) {
        B[i] = A[i];
    }

    // Sort the original array
    sort(A, A + N);

    // Stores the left median
    int L = A[N / 2 - 1];

    // Stores the right median
    int R = A[N / 2];

    // Iterate over the range
    for (int i = 0; i < N; i++) {

        // If A[i] is less than equal to L,
        // then after removing it, R will become
        // the central element, otherwise L
        if (B[i] <= L) {
            cout << R;
        }
        else {
            cout << L;
        }
        if (i != N - 1) {
            cout << ", ";
        }
    }

    return 0;
}

// Driver Code
int main()
{
    int N = 4;
    int A[] = { 2, 4, 4, 3 };
    findMedianExcludedArray(A, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for above approach
import java.util.*;

class GFG{

// Function to return Median array after
// excluding each individual element
static int findMedianExcludedArray(int[] A, int N)
{

    // Store the original array in another
    // array to store the sorted version
    // and the original position of the array
    // element is also important
    int[] B = new int[N];
    for (int i = 0; i < N; i++) {
        B[i] = A[i];
    }

    // Sort the original array
    Arrays.sort(A);

    // Stores the left median
    int L = A[N / 2 - 1];

    // Stores the right median
    int R = A[N / 2];

    // Iterate over the range
    for (int i = 0; i < N; i++) {

        // If A[i] is less than equal to L,
        // then after removing it, R will become
        // the central element, otherwise L
        if (B[i] <= L) {
             System.out.print(R);
        }
        else {
             System.out.print(L);
        }
        if (i != N - 1) {
             System.out.print(", ");
        }
    }

    return 0;
}

// Driver Code
public static void main(String[] args)
{
    int N = 4;
    int[] A = { 2, 4, 4, 3 };
    findMedianExcludedArray(A, N);
}
}

// This code is contributed by target_2.
```

## 蟒蛇 3

```
# Function to return Median array after
# excluding each individual element
def findMedianExcludedArray(A, N):

    # Store the original array in another
    # array to store the sorted version
    # and the original position of the array
    # element is also important
    B = []
    for i in range(N):
        B.append(A[i])

        # sort the original array
    A.sort()

    # Stores the left median
    L = A[N//2 - 1]

    # Stores the right median
    R = A[N//2]

     # Iterate over the range
    for i in range(N):

         # If A[i] is less than equal to L,
        # then after removing it, R will become
        # the central element, otherwise L
        if B[i] <= L:
            print(R, end="")
        else:
            print(L, end="")
        if i != N-1:
            print(", ", end="")

# Driver code
N = 4
A = [2, 4, 4, 3]
findMedianExcludedArray(A, N)

# This code is contributed by Parth Manchanda
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to return Median array after
// excluding each individual element
static int findMedianExcludedArray(int[] A, int N)
{

    // Store the original array in another
    // array to store the sorted version
    // and the original position of the array
    // element is also important
    int[] B = new int[N];
    for (int i = 0; i < N; i++) {
        B[i] = A[i];
    }

    // Sort the original array
    Array.Sort(A);

    // Stores the left median
    int L = A[N / 2 - 1];

    // Stores the right median
    int R = A[N / 2];

    // Iterate over the range
    for (int i = 0; i < N; i++) {

        // If A[i] is less than equal to L,
        // then after removing it, R will become
        // the central element, otherwise L
        if (B[i] <= L) {
             Console.Write(R);
        }
        else {
             Console.Write(L);
        }
        if (i != N - 1) {
             Console.Write(", ");
        }
    }

    return 0;
}

// Driver Code
static void Main()
{
    int N = 4;
    int[] A = { 2, 4, 4, 3 };
    findMedianExcludedArray(A, N);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to return Median array after
// excluding each individual element
function findMedianExcludedArray(A, N)
{

    // Store the original array in another
    // array to store the sorted version
    // and the original position of the array
    // element is also important
    let B = new Array(N);
    for (let i = 0; i < N; i++) {
        B[i] = A[i];
    }

    // Sort the original array
    A.sort();

    // Stores the left median
    let L = A[N / 2 - 1];

    // Stores the right median
    let R = A[N / 2];

    // Iterate over the range
    for (let i = 0; i < N; i++) {

        // If A[i] is less than equal to L,
        // then after removing it, R will become
        // the central element, otherwise L
        if (B[i] <= L) {
             document.write(R);
        }
        else {
             document.write(L);
        }
        if (i != N - 1) {
             document.write(", ");
        }
    }

    return 0;
}

// Driver Code

    let N = 4;
    let A = [ 2, 4, 4, 3 ];
    findMedianExcludedArray(A, N);

// This code is contributed by splevel62.
</script>
```

**Output:** 

```
4, 3, 3, 4
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*