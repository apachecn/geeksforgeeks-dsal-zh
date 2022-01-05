# 排序给定阵列需要重新排列的子阵列数量

> 原文:[https://www . geeksforgeeks . org/子数组数量-需要重新排列才能对给定数组进行排序/](https://www.geeksforgeeks.org/number-of-subarrays-required-to-be-rearranged-to-sort-the-given-array/)

给定一个由第一个 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到需要重新排列的最小数量的子数组，从而对最终的[数组进行排序](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)。

**示例:**

> ***输入:** arr[] = {2，1，4，3，5}*
> ***输出:** 1*
> ***解释:***
> ***操作 1:** 选择子阵列{arr[0]，arr[3]}，即{2，1，4，3 }。将此子阵列的元素重新排列为{1，2，3，4}。数组修改为{1，2，3，4，5}。*
> 
> ***输入:** arr[] = {5，2，3，4，1}*
> ***输出:** 3*

**方法:**给定的问题可以通过观察以下场景来解决:

*   如果给定数组 **arr[]** 已经排序，则打印 **0** 。
*   如果第一个和最后一个元素分别是 **1** 和 **N** ，那么只需要对 1 个子阵列**arr【1，N–2】**或**arr【2，N–1】**进行排序。因此，打印 **1** 。
*   如果第一个和最后一个元素分别是 **N** 和 **1** ，则需要对 3 个子阵列即**arr【0，N–2】**、**arr【1，N–1】**、**arr【0，1】**进行排序。因此，打印 **3** 。
*   否则，对两个子阵列进行排序，即 **arr[1，N–1]**，和 **arr[0，N–2]【T3]。**

因此，打印需要重新排列的最小子阵列数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number
// of subarrays required to be
// rearranged to sort the given array
void countSubarray(int arr[], int n)
{
    // Base Case
    int ans = 2;

    // Check if the given array is
    // already sorted
    if (is_sorted(arr, arr + n)) {
        ans = 0;
    }

    // Check if the first element of
    // array is 1 or last element is
    // equal to size of array
    else if (arr[0] == 1
             || arr[n - 1] == n) {
        ans = 1;
    }
    else if (arr[0] == n
             && arr[n - 1] == 1) {
        ans = 3;
    }

    // Print the required answer
    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 5, 2, 3, 4, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    countSubarray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function that returns 0 if a pair
// is found unsorted
static int arraySortedOrNot(int arr[], int n)
{

    // Array has one or no element or the
    // rest are already checked and approved.
    if (n == 1 || n == 0)
        return 1;

    // Unsorted pair found (Equal values allowed)
    if (arr[n - 1] < arr[n - 2])
        return 0;

    // Last pair was sorted
    // Keep on checking
    return arraySortedOrNot(arr, n - 1);
}

// Function to count the number
// of subarrays required to be
// rearranged to sort the given array
static void countSubarray(int arr[], int n)
{

    // Base Case
    int ans = 2;

    // Check if the given array is
    // already sorted
    if (arraySortedOrNot(arr, arr.length) != 0)
    {
        ans = 0;
    }

    // Check if the first element of
    // array is 1 or last element is
    // equal to size of array
    else if (arr[0] == 1 ||
             arr[n - 1] == n)
    {
        ans = 1;
    }
    else if (arr[0] == n &&
             arr[n - 1] == 1)
    {
        ans = 3;
    }

    // Print the required answer
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, 2, 3, 4, 1 };
    int N = arr.length;

    countSubarray(arr, N);
}   
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number
# of subarrays required to be
# rearranged to sort the given array
def countSubarray(arr, n):

    # Base Case
    ans = 2

    # Check if the given array is
    # already sorted
    if (sorted(arr) == arr):
        ans = 0

    # Check if the first element of
    # array is 1 or last element is
    # equal to size of array
    elif (arr[0] == 1 or arr[n - 1] == n):
        ans = 1
    elif (arr[0] == n and arr[n - 1] == 1):
        ans = 3

    # Print the required answer
    print(ans)

# Driver Code
arr = [ 5, 2, 3, 4, 1 ]
N = len(arr)

countSubarray(arr, N)

# This code is contributed by amreshkumar3
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function that returns 0 if a pair
// is found unsorted
static int arraySortedOrNot(int []arr, int n)
{

    // Array has one or no element or the
    // rest are already checked and approved.
    if (n == 1 || n == 0)
        return 1;

    // Unsorted pair found (Equal values allowed)
    if (arr[n - 1] < arr[n - 2])
        return 0;

    // Last pair was sorted
    // Keep on checking
    return arraySortedOrNot(arr, n - 1);
}

// Function to count the number
// of subarrays required to be
// rearranged to sort the given array
static void countSubarray(int []arr, int n)
{

    // Base Case
    int ans = 2;

    // Check if the given array is
    // already sorted
    if (arraySortedOrNot(arr, arr.Length) != 0)
    {
        ans = 0;
    }

    // Check if the first element of
    // array is 1 or last element is
    // equal to size of array
    else if (arr[0] == 1 ||
             arr[n - 1] == n)
    {
        ans = 1;
    }
    else if (arr[0] == n &&
             arr[n - 1] == 1)
    {
        ans = 3;
    }

    // Print the required answer
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    int []arr = { 5, 2, 3, 4, 1 };
    int N = arr.Length;

    countSubarray(arr, N);
}   
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that returns 0 if a pair
// is found unsorted
function arraySortedOrNot(arr, n)
{

    // Array has one or no element or the
    // rest are already checked and approved.
    if (n == 1 || n == 0)
        return 1;

    // Unsorted pair found (Equal values allowed)
    if (arr[n - 1] < arr[n - 2])
        return 0;

    // Last pair was sorted
    // Keep on checking
    return arraySortedOrNot(arr, n - 1);
}

// Function to count the number
// of subarrays required to be
// rearranged to sort the given array
function countSubarray(arr, n)
{

    // Base Case
    var ans = 2;

    // Check if the given array is
    // already sorted
    if (arraySortedOrNot(arr, arr.length) != 0)
    {
        ans = 0;
    }

    // Check if the first element of
    // array is 1 or last element is
    // equal to size of array
    else if (arr[0] == 1 ||
             arr[n - 1] == n)
    {
        ans = 1;
    }
    else if (arr[0] == n &&
             arr[n - 1] == 1)
    {
        ans = 3;
    }

    // Print the required answer
    document.write(ans);
}

// Driver Code
var arr = [ 5, 2, 3, 4, 1 ];
var N = arr.length;

countSubarray(arr, N);

// This code is contributed by SURENDRA_GANGWAR

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)