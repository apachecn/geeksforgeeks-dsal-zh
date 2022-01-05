# 从给定频率阵列的排序序列范围中计数不同的元素

> 原文:[https://www . geesforgeks . org/count-distinct-elements-from-range-of-sorted-sequence-from-a-给定频率-array/](https://www.geeksforgeeks.org/count-distinct-elements-from-a-range-of-a-sorted-sequence-from-a-given-frequency-array/)

给定两个整数 **L** 和 **R** 以及一个由 **N** 正整数( *1 基索引*)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，使得排序序列的第 **i** <sup>第</sup>元素的频率为**arr【I】**。任务是从序列 **A[]** 中的**【L，R】**范围内找到不同元素的数量。

**示例:**

> **输入:** arr[] = {3，6，7，1，8}，L = 3，R = 7
> **输出:** 2
> **说明:**从给定的频率数组来看，排序后的数组将是{1，1，1，2，2，2，2，2，3，3，…。}.现在，范围[3，7]中不同元素的数量是 2( = {1，2})。
> 
> **输入:** arr[] = {1，2，3，4}，L = 3，R = 4
> T3】输出: 1

**朴素方法:**解决给定问题的最简单方法是使用给定的频率从给定的数组**arr【】**构建排序的序列，然后[在范围**【L，R】**上遍历构建的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，以计算不同元素的数量。

***时间复杂度:**O(N+R–L)*
***辅助空间:** O(S)，其中 S 为* [*数组元素之和*](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) *。*

**高效方法:**上述方法可以通过使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)和[前缀求和技术](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)来优化，以找到范围**【L，R】**内不同元素的数量。按照以下步骤解决给定问题:

*   初始化一个辅助数组，比如说**前缀[]** ，存储给定数组元素的前缀和。
*   找到给定数组的[前缀和，并将其存储在数组**前缀[]** 中。](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)
*   使用二分搜索法，找到**前缀【】**中的值至少为**L**的[第一个索引](https://www.geeksforgeeks.org/implementing-upper_bound-and-lower_bound-in-c/)，说**左**。
*   使用二分搜索法，找到**前缀[]** 中的值至少为**的[第一个索引](https://www.geeksforgeeks.org/implementing-upper_bound-and-lower_bound-in-c/)，说**右**。**
*   完成上述步骤后，打印**(右–左+ 1)** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the first index
// with value is at least element
int binarysearch(int array[], int right,
                 int element)
{

    // Update the value of left
    int left = 1;

    // Update the value of right

    // Binary search for the element
    while (left <= right)
    {

        // Find the middle element
        int mid = (left + right / 2);

        if (array[mid] == element)
        {
            return mid;
        }

        // Check if the value lies
        // between the elements at
        // index mid - 1 and mid
        if (mid - 1 > 0 && array[mid] > element &&
           array[mid - 1] < element)
        {
            return mid;
        }

        // Check in the right subarray
        else if (array[mid] < element)
        {

            // Update the value
            // of left
            left = mid + 1;
        }

        // Check in left subarray
        else
        {

            // Update the value of
            // right
            right = mid - 1;
        }
    }
    return 1;
}

// Function to count the number of
// distinct elements over the range
// [L, R] in the sorted sequence
void countDistinct(vector<int> arr,
                          int L, int R)
{

    // Stores the count of distinct
    // elements
    int count = 0;

    // Create the prefix sum array
    int pref[arr.size() + 1];

    for(int i = 1; i <= arr.size(); ++i)
    {

        // Update the value of count
        count += arr[i - 1];

        // Update the value of pref[i]
        pref[i] = count;
    }

    // Calculating the first index
    // of L and R using binary search
    int left = binarysearch(pref, arr.size() + 1, L);
    int right = binarysearch(pref, arr.size() + 1, R);

    // Print the resultant count
    cout << right - left + 1;
}

// Driver Code
int main()
{
    vector<int> arr{ 3, 6, 7, 1, 8 };
    int L = 3;
    int R = 7;

    countDistinct(arr, L, R);
}

// This code is contributed by ipg2016107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to find the first index
    // with value is at least element
    static int binarysearch(int array[],
                            int element)
    {
        // Update the value of left
        int left = 1;

        // Update the value of right
        int right = array.length - 1;

        // Binary search for the element
        while (left <= right) {

            // Find the middle element
            int mid = (int)(left + right / 2);

            if (array[mid] == element) {
                return mid;
            }

            // Check if the value lies
            // between the elements at
            // index mid - 1 and mid
            if (mid - 1 > 0
                && array[mid] > element
                && array[mid - 1] < element) {

                return mid;
            }

            // Check in the right subarray
            else if (array[mid] < element) {

                // Update the value
                // of left
                left = mid + 1;
            }

            // Check in left subarray
            else {

                // Update the value of
                // right
                right = mid - 1;
            }
        }

        return 1;
    }

    // Function to count the number of
    // distinct elements over the range
    // [L, R] in the sorted sequence
    static void countDistinct(int arr[],
                              int L, int R)
    {
        // Stores the count of distinct
        // elements
        int count = 0;

        // Create the prefix sum array
        int pref[] = new int[arr.length + 1];

        for (int i = 1; i <= arr.length; ++i) {

            // Update the value of count
            count += arr[i - 1];

            // Update the value of pref[i]
            pref[i] = count;
        }

        // Calculating the first index
        // of L and R using binary search
        int left = binarysearch(pref, L);
        int right = binarysearch(pref, R);

        // Print the resultant count
        System.out.println(
            (right - left) + 1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 3, 6, 7, 1, 8 };
        int L = 3;
        int R = 7;
        countDistinct(arr, L, R);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the first index
# with value is at least element
def binarysearch(array,  right,
                 element):

    # Update the value of left
    left = 1

    # Update the value of right

    # Binary search for the element
    while (left <= right):

        # Find the middle element
        mid = (left + right // 2)

        if (array[mid] == element):
            return mid

        # Check if the value lies
        # between the elements at
        # index mid - 1 and mid
        if (mid - 1 > 0 and array[mid] > element and
                        array[mid - 1] < element):
            return mid

        # Check in the right subarray
        elif (array[mid] < element):

            # Update the value
            # of left
            left = mid + 1

        # Check in left subarray
        else:

            # Update the value of
            # right
            right = mid - 1

    return 1

# Function to count the number of
# distinct elements over the range
# [L, R] in the sorted sequence
def countDistinct(arr, L, R):

    # Stores the count of distinct
    # elements
    count = 0

    # Create the prefix sum array
    pref = [0] * (len(arr) + 1)

    for i in range(1, len(arr) + 1):

        # Update the value of count
        count += arr[i - 1]

        # Update the value of pref[i]
        pref[i] = count

    # Calculating the first index
    # of L and R using binary search
    left = binarysearch(pref, len(arr) + 1, L)
    right = binarysearch(pref, len(arr) + 1, R)

    # Print the resultant count
    print(right - left + 1)

# Driver Code
if __name__ == "__main__":

    arr = [ 3, 6, 7, 1, 8 ]
    L = 3
    R = 7

    countDistinct(arr, L, R)

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the first index
// with value is at least element
static int binarysearch(int []array, int right,
                        int element)
{

    // Update the value of left
    int left = 1;

    // Update the value of right

    // Binary search for the element
    while (left <= right)
    {

        // Find the middle element
        int mid = (left + right / 2);

        if (array[mid] == element)
        {
            return mid;
        }

        // Check if the value lies
        // between the elements at
        // index mid - 1 and mid
        if (mid - 1 > 0 && array[mid] > element &&
            array[mid - 1] < element)
        {
            return mid;
        }

        // Check in the right subarray
        else if (array[mid] < element)
        {

            // Update the value
            // of left
            left = mid + 1;
        }

        // Check in left subarray
        else
        {

            // Update the value of
            // right
            right = mid - 1;
        }
    }
    return 1;
}

// Function to count the number of
// distinct elements over the range
// [L, R] in the sorted sequence
static void countDistinct(List<int> arr,
                          int L, int R)
{

    // Stores the count of distinct
    // elements
    int count = 0;

    // Create the prefix sum array
    int []pref = new int[arr.Count + 1];

    for(int i = 1; i <= arr.Count; ++i)
    {

        // Update the value of count
        count += arr[i - 1];

        // Update the value of pref[i]
        pref[i] = count;
    }

    // Calculating the first index
    // of L and R using binary search
    int left = binarysearch(pref, arr.Count + 1, L);
    int right = binarysearch(pref, arr.Count + 1, R);

    // Print the resultant count
    Console.Write(right - left + 1);
}

// Driver Code
public static void Main()
{
    List<int> arr = new List<int>(){ 3, 6, 7, 1, 8 };
    int L = 3;
    int R = 7;

    countDistinct(arr, L, R);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the first index
// with value is at least element
function binarysearch(array, right, element)
{

    // Update the value of left
    let left = 1;

    // Update the value of right

    // Binary search for the element
    while (left <= right)
    {

        // Find the middle element
        let mid = Math.floor((left + right / 2));

        if (array[mid] == element)
        {
            return mid;
        }

        // Check if the value lies
        // between the elements at
        // index mid - 1 and mid
        if (mid - 1 > 0 && array[mid] > element &&
            array[mid - 1] < element)
        {
            return mid;
        }

        // Check in the right subarray
        else if (array[mid] < element)
        {

            // Update the value
            // of left
            left = mid + 1;
        }

        // Check in left subarray
        else
        {

            // Update the value of
            // right
            right = mid - 1;
        }
    }
    return 1;
}

// Function to count the number of
// distinct elements over the range
// [L, R] in the sorted sequence
function countDistinct(arr, L, R)
{

    // Stores the count of distinct
    // elements
    let count = 0;

    // Create the prefix sum array
    let pref = Array.from(
        {length: arr.length + 1}, (_, i) => 0);

    for(let i = 1; i <= arr.length; ++i)
    {

        // Update the value of count
        count += arr[i - 1];

        // Update the value of pref[i]
        pref[i] = count;
    }

    // Calculating the first index
    // of L and R using binary search
    let left = binarysearch(pref, arr.length + 1, L);
    let right = binarysearch(pref, arr.length + 1, R);

        // Print the resultant count
        document.write((right - left) + 1);
}

// Driver Code
let arr = [ 3, 6, 7, 1, 8 ];
let L = 3;
let R = 7;

countDistinct(arr, L, R);

// This code is contributed by susmitakundugoaldanga

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)