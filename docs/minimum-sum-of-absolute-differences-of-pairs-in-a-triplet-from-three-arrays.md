# 来自三个阵列的三元组中的对的绝对差的最小和

> 原文:[https://www . geeksforgeeks . org/三个数组中三个数组对的绝对差的最小和/](https://www.geeksforgeeks.org/minimum-sum-of-absolute-differences-of-pairs-in-a-triplet-from-three-arrays/)

给定大小分别为 **A** 、 **B** 和 **C** 的三个[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **a[]** 、 **b[]** 和 **c[]** ，任务是找到**ABS(A[I]–B[j])+ABS(B[j]–C[k])**的最小可能值，其中**0≤I≤A**，

**示例:**

> **输入:** A = 3，B = 2，C = 2，a[] = {1，8，5}，b[] = {2，9}，c[] = {5，4}
> **输出:** 3
> **解释:**
> 三元组(a[0]，b[0]，c[1])即(1，2，4)具有最小的对的绝对差之和，即 ABS(1–2)+ABS(2–4)= 1
> 
> **输入:** A = 4，B = 3，C = 3，a[] = {4，5，1，7}，b[] = {8，5，6}，c[] = {2，7，12}
> **输出:** 2
> **解释:**
> 三元组(a[1]，b[1]，c[1])，即(1，5，7)具有最小的绝对差对之和，即 ABS(5–5)+ABS

**方法:**解决这个问题的思路是[对数组](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)**a【】**和**c【】**进行排序，然后[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**b【】**找到满足给定条件的元素。

按照以下步骤解决问题:

*   初始化变量，说 **min** ，为 **INT_MAX** ，存储最小可能值。
*   [将数组](https://www.geeksforgeeks.org/sorting-algorithms/)**a【】**和**c【】**按升序排序。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **b[]** ，对于每个元素，说 **b[i]** ，从数组 **a[]** 和 **c[]** 中找到最接近 **b[i]** 的元素作为 **arr_close** 和 **crr_close** ，并执行以下操作:
    *   要找到最近的元素，首先要找到目标元素 **b[i]** 的 [**下界**](https://www.geeksforgeeks.org/lower_bound-in-cpp/) 。
    *   如果找到下限，检查它是否是数组的第一个元素。如果不是，则将下限及其前一个元素与目标元素进行比较，并找出最接近目标元素的元素。
    *   如果没有找到下限，那么最接近的元素将是数组的最后一个元素。
    *   将 **min** 更新为**ABS(b[I]–arr _ close)+ABS(b[I]–crr _ close)**的最小值。
*   完成上述步骤后，打印 **min** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to find the value
// closest to K in the array A[]
int closestValue(vector<int> A, int k)
{
    // Initialize close value as the
    // end element
    int close = A.back();

    // Find lower bound of the array
    auto it = lower_bound(A.begin(),
                          A.end(), k);

    // If lower_bound is found
    if (it != A.end()) {

        close = *it;

        // If lower_bound is not
        // the first array element
        if (it != A.begin()) {

            // If *(it - 1) is closer to k
            if ((k - *(it - 1))
                < (close - k)) {
                close = *(it - 1);
            }
        }
    }

    // Return closest value of k
    return close;
}

// Function to find the minimum sum of
// abs(arr[i] - brr[j]) and abs(brr[j]-crr[k])
void minPossible(vector<int> arr,
                 vector<int> brr,
                 vector<int> crr)
{
    // Sort the vectors arr and crr
    sort(arr.begin(), arr.end());
    sort(crr.begin(), crr.end());

    // Initialize minimum as INT_MAX
    int minimum = INT_MAX;

    // Traverse the array brr[]
    for (int val : brr) {

        // Stores the element closest
        // to val from the array arr[]
        int arr_close = closestValue(arr, val);

        // Stores the element closest
        // to val from the array crr[]
        int crr_close = closestValue(crr, val);

        // If sum of differences is minimum
        if (abs(val - arr_close)
                + abs(val - crr_close)
            < minimum)

            // Update the minimum
            minimum = abs(val - arr_close)
                      + abs(val - crr_close);
    }

    // Print the minimum absolute
    // difference possible
    cout << minimum;
}

// Driver Code
int main()
{
    vector<int> a = { 1, 8, 5 };
    vector<int> b = { 2, 9 };
    vector<int> c = { 5, 4 };

    // Function Call
    minPossible(a, b, c);

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

// Lower_bound function
public static int lower_bound(int arr[], int key)
{
    int low = 0;
    int high = arr.length - 1;

    while (low < high)
    {
        int mid = low + (high - low) / 2;
        if (arr[mid] >= key)
        {
            high = mid;
        }
        else
        {
            low = mid + 1;
        }
    }
    return low;
}

// Function to find the value
// closest to K in the array A[]
static int closestValue(int A[], int k)
{

    // Initialize close value as the
    // end element
    int close = A[A.length - 1];

    // Find lower bound of the array
    int it = lower_bound(A, k);

    // If lower_bound is found
    if (it != A.length)
    {
        close = A[it];

        // If lower_bound is not
        // the first array element
        if (it != 0)
        {

            // If *(it - 1) is closer to k
            if ((k - A[it - 1]) < (close - k))
            {
                close = A[it - 1];
            }
        }
    }

    // Return closest value of k
    return close;
}

// Function to find the minimum sum of
// abs(arr[i] - brr[j]) and abs(brr[j]-crr[k])
static void minPossible(int arr[], int brr[],
                        int crr[])
{

    // Sort the vectors arr and crr
    Arrays.sort(arr);
    Arrays.sort(crr);

    // Initialize minimum as INT_MAX
    int minimum = Integer.MAX_VALUE;

    // Traverse the array brr[]
    for(int val : brr)
    {

        // Stores the element closest
        // to val from the array arr[]
        int arr_close = closestValue(arr, val);

        // Stores the element closest
        // to val from the array crr[]
        int crr_close = closestValue(crr, val);

        // If sum of differences is minimum
        if (Math.abs(val - arr_close) +
            Math.abs(val - crr_close) < minimum)

            // Update the minimum
            minimum = Math.abs(val - arr_close) +
                      Math.abs(val - crr_close);
    }

    // Print the minimum absolute
    // difference possible
    System.out.println(minimum);
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 1, 8, 5 };
    int b[] = { 2, 9 };
    int c[] = { 5, 4 };

    // Function Call
    minPossible(a, b, c);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Lower_bound function
def lower_bound(arr, key):

    low = 0;
    high = len(arr) - 1;

    while (low < high):
        mid = low + (high - low) // 2;
        if (arr[mid] >= key):
            high = mid;
        else:
            low = mid + 1;
    return low;

# Function to find the value
# closest to K in the array A[]
def closestValue(A, k):

    # Initialize close value as the
    # end element
    close = A[-1];

    # Find lower bound of the array
    it = lower_bound(A, k);

    # If lower_bound is found
    if (it != len(A)):
        close = A[it];

        # If lower_bound is not
        # the first array element
        if (it != 0):

            # If *(it - 1) is closer to k
            if ((k - A[it - 1]) < (close - k)):
                close = A[it - 1];

    # Return closest value of k
    return close;

# Function to find the minimum sum of
# abs(arr[i] - brr[j]) and abs(brr[j]-crr[k])
def minPossible(arr, brr, crr):

    # Sort the vectors arr and crr
    arr.sort();
    crr.sort();

    # Initialize minimum as LET_MAX
    minimum = 10**9;

    # Traverse the array brr[]
    for val in brr:

        # Stores the element closest
        # to val from the array arr[]
        arr_close = closestValue(arr, val);

        # Stores the element closest
        # to val from the array crr[]
        crr_close = closestValue(crr, val);

        # If sum of differences is minimum
        if (abs(val - arr_close) +
            abs(val - crr_close) < minimum):

            # Update the minimum
            minimum = abs(val - arr_close) + abs(val - crr_close);

    # Print the minimum absolute
    # difference possible
    print(minimum);

# Driver code
a = [ 1, 8, 5 ];
b = [ 2, 9 ];
c = [ 5, 4 ];

# Function Call
minPossible(a, b, c);

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Lower_bound function
public static int lower_bound(int[] arr, int key)
{
    int low = 0;
    int high = arr.Length - 1;

    while (low < high)
    {
        int mid = low + (high - low) / 2;

        if (arr[mid] >= key)
        {
            high = mid;
        }
        else
        {
            low = mid + 1;
        }
    }
    return low;
}

// Function to find the value
// closest to K in the array A[]
static int closestValue(int []A, int k)
{

    // Initialize close value as the
    // end element
    int close = A[A.Length - 1];

    // Find lower bound of the array
    int it = lower_bound(A, k);

    // If lower_bound is found
    if (it != A.Length)
    {
        close = A[it];

        // If lower_bound is not
        // the first array element
        if (it != 0)
        {

            // If *(it - 1) is closer to k
            if ((k - A[it - 1]) < (close - k))
            {
                close = A[it - 1];
            }
        }
    }

    // Return closest value of k
    return close;
}

// Function to find the minimum sum of
// abs(arr[i] - brr[j]) and abs(brr[j]-crr[k])
static void minPossible(int[] arr, int[] brr,
                        int[] crr)
{

    // Sort the vectors arr and crr
    Array.Sort(arr);
    Array.Sort(crr);

    // Initialize minimum as INT_MAX
    int minimum = Int32.MaxValue;

    // Traverse the array brr[]
    foreach(int val in brr)
    {

        // Stores the element closest
        // to val from the array arr[]
        int arr_close = closestValue(arr, val);

        // Stores the element closest
        // to val from the array crr[]
        int crr_close = closestValue(crr, val);

        // If sum of differences is minimum
        if (Math.Abs(val - arr_close) +
            Math.Abs(val - crr_close) < minimum)

            // Update the minimum
            minimum = Math.Abs(val - arr_close) +
                      Math.Abs(val - crr_close);
    }

    // Print the minimum absolute
    // difference possible
    Console.WriteLine(minimum);
}

// Driver Code
static void Main()
{
    int []a = { 1, 8, 5 };
    int []b = { 2, 9 };
    int []c = { 5, 4 };

    // Function Call
    minPossible(a, b, c);
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Lower_bound function
function lower_bound(arr, key)
{
    let low = 0;
    let high = arr.length - 1;

    while (low < high)
    {
        let mid = low + Math.floor((high - low) / 2);
        if (arr[mid] >= key)
        {
            high = mid;
        }
        else
        {
            low = mid + 1;
        }
    }
    return low;
}

// Function to find the value
// closest to K in the array A[]
function closestValue(A, k)
{

    // Initialize close value as the
    // end element
    let close = A[A.length - 1];

    // Find lower bound of the array
    let it = lower_bound(A, k);

    // If lower_bound is found
    if (it != A.length)
    {
        close = A[it];

        // If lower_bound is not
        // the first array element
        if (it != 0)
        {

            // If *(it - 1) is closer to k
            if ((k - A[it - 1]) < (close - k))
            {
                close = A[it - 1];
            }
        }
    }

    // Return closest value of k
    return close;
}

// Function to find the minimum sum of
// abs(arr[i] - brr[j]) and abs(brr[j]-crr[k])
function minPossible(arr, brr, crr)
{

    // Sort the vectors arr and crr
    arr.sort();
    crr.sort();

    // Initialize minimum as LET_MAX
    let minimum = Number.MAX_VALUE;

    // Traverse the array brr[]
    for(let val in brr)
    {

        // Stores the element closest
        // to val from the array arr[]
        let arr_close = closestValue(arr, val);

        // Stores the element closest
        // to val from the array crr[]
        let crr_close = closestValue(crr, val);

        // If sum of differences is minimum
        if (Math.abs(val - arr_close) +
            Math.abs(val - crr_close) < minimum)

            // Update the minimum
            minimum = Math.abs(val - arr_close) +
                      Math.abs(val - crr_close);
    }

    // Print the minimum absolute
    // difference possible
   document.write(minimum);
}

// Driver code

    let a = [ 1, 8, 5 ];
    let b = [ 2, 9 ];
    let c = [ 5, 4 ];

    // Function Call
    minPossible(a, b, c);

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(A * log A+C * log C+B)*
T5**辅助空间:** O(A + B + C)