# 就地合并排序

> 原文:[https://www.geeksforgeeks.org/in-place-merge-sort/](https://www.geeksforgeeks.org/in-place-merge-sort/)

实现[合并排序](https://www.geeksforgeeks.org/merge-sort/)，即保持排序算法不变的标准实现。
就地意味着它不像标准情况那样占用额外的内存进行合并操作。

**示例:**

> **输入:** arr[] = {2，3，4，1}
> **输出:** 1 2 3 4
> 
> **输入:** arr[] = {56，2，45 }
> T3】输出: 2 45 56

**方法 1:**

*   保持两个指针指向需要合并的段的开始。
*   比较指针所在的元素。
*   如果*元素 1 <元素 2* 那么*元素 1* 位置正确，只需增加*指针 1* 。
*   否则，将元素 1 和*元素 2(包括元素 1 但不包括元素 2)* 之间的所有元素向右移动 1，然后将元素 2 放在元素 1 的前一个位置*(即向右移动之前)*。将所有指针增加 *1* 。

下面是上述方法的实现:

## C++

```
// C++ program in-place Merge Sort
#include <iostream>
using namespace std;

// Merges two subarrays of arr[].
// First subarray is arr[l..m]
// Second subarray is arr[m+1..r]
// Inplace Implementation
void merge(int arr[], int start, int mid, int end)
{
    int start2 = mid + 1;

    // If the direct merge is already sorted
    if (arr[mid] <= arr[start2]) {
        return;
    }

    // Two pointers to maintain start
    // of both arrays to merge
    while (start <= mid && start2 <= end) {

        // If element 1 is in right place
        if (arr[start] <= arr[start2]) {
            start++;
        }
        else {
            int value = arr[start2];
            int index = start2;

            // Shift all the elements between element 1
            // element 2, right by 1.
            while (index != start) {
                arr[index] = arr[index - 1];
                index--;
            }
            arr[start] = value;

            // Update all the pointers
            start++;
            mid++;
            start2++;
        }
    }
}

/* l is for left index and r is right index of the
   sub-array of arr to be sorted */
void mergeSort(int arr[], int l, int r)
{
    if (l < r) {

        // Same as (l + r) / 2, but avoids overflow
        // for large l and r
        int m = l + (r - l) / 2;

        // Sort first and second halves
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);

        merge(arr, l, m, r);
    }
}

/* UTILITY FUNCTIONS */
/* Function to print an array */
void printArray(int A[], int size)
{
    int i;
    for (i = 0; i < size; i++)
        cout <<" "<< A[i];
    cout <<"\n";
}

/* Driver program to test above functions */
int main()
{
    int arr[] = { 12, 11, 13, 5, 6, 7 };
    int arr_size = sizeof(arr) / sizeof(arr[0]);

    mergeSort(arr, 0, arr_size - 1);

    printArray(arr, arr_size);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C++ program in-place Merge Sort
#include <stdio.h>

// Merges two subarrays of arr[].
// First subarray is arr[l..m]
// Second subarray is arr[m+1..r]
// Inplace Implementation
void merge(int arr[], int start, int mid, int end)
{
    int start2 = mid + 1;

    // If the direct merge is already sorted
    if (arr[mid] <= arr[start2]) {
        return;
    }

    // Two pointers to maintain start
    // of both arrays to merge
    while (start <= mid && start2 <= end) {

        // If element 1 is in right place
        if (arr[start] <= arr[start2]) {
            start++;
        }
        else {
            int value = arr[start2];
            int index = start2;

            // Shift all the elements between element 1
            // element 2, right by 1.
            while (index != start) {
                arr[index] = arr[index - 1];
                index--;
            }
            arr[start] = value;

            // Update all the pointers
            start++;
            mid++;
            start2++;
        }
    }
}

/* l is for left index and r is right index of the
   sub-array of arr to be sorted */
void mergeSort(int arr[], int l, int r)
{
    if (l < r) {

        // Same as (l + r) / 2, but avoids overflow
        // for large l and r
        int m = l + (r - l) / 2;

        // Sort first and second halves
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);

        merge(arr, l, m, r);
    }
}

/* UTILITY FUNCTIONS */
/* Function to print an array */
void printArray(int A[], int size)
{
    int i;
    for (i = 0; i < size; i++)
        printf("%d ", A[i]);
    printf("\n");
}

/* Driver program to test above functions */
int main()
{
    int arr[] = { 12, 11, 13, 5, 6, 7 };
    int arr_size = sizeof(arr) / sizeof(arr[0]);

    mergeSort(arr, 0, arr_size - 1);

    printArray(arr, arr_size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program in-place Merge Sort

public class GFG {

    // Merges two subarrays of arr[].
    // First subarray is arr[l..m]
    // Second subarray is arr[m+1..r]
    // Inplace Implementation
    static void merge(int arr[], int start, int mid,
                      int end)
    {
        int start2 = mid + 1;

        // If the direct merge is already sorted
        if (arr[mid] <= arr[start2]) {
            return;
        }

        // Two pointers to maintain start
        // of both arrays to merge
        while (start <= mid && start2 <= end) {

            // If element 1 is in right place
            if (arr[start] <= arr[start2]) {
                start++;
            }
            else {
                int value = arr[start2];
                int index = start2;

                // Shift all the elements between element 1
                // element 2, right by 1.
                while (index != start) {
                    arr[index] = arr[index - 1];
                    index--;
                }
                arr[start] = value;

                // Update all the pointers
                start++;
                mid++;
                start2++;
            }
        }
    }

    /* l is for left index and r is right index of the
       sub-array of arr to be sorted */
    static void mergeSort(int arr[], int l, int r)
    {
        if (l < r) {

            // Same as (l + r) / 2, but avoids overflow
            // for large l and r
            int m = l + (r - l) / 2;

            // Sort first and second halves
            mergeSort(arr, l, m);
            mergeSort(arr, m + 1, r);

            merge(arr, l, m, r);
        }
    }

    /* UTILITY FUNCTIONS */
    /* Function to print an array */
    static void printArray(int A[], int size)
    {
        int i;
        for (i = 0; i < size; i++)
            System.out.print(A[i] + " ");
        System.out.println();
    }

    /* Driver program to test above functions */
    public static void main(String[] args)
    {
        int arr[] = { 12, 11, 13, 5, 6, 7 };
        int arr_size = arr.length;

        mergeSort(arr, 0, arr_size - 1);
        printArray(arr, arr_size);
    }
    // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python program in-place Merge Sort

# Merges two subarrays of arr.
# First subarray is arr[l..m]
# Second subarray is arr[m+1..r]
# Inplace Implementation

def merge(arr, start, mid, end):
    start2 = mid + 1

    # If the direct merge is already sorted
    if (arr[mid] <= arr[start2]):
        return

    # Two pointers to maintain start
    # of both arrays to merge
    while (start <= mid and start2 <= end):

        # If element 1 is in right place
        if (arr[start] <= arr[start2]):
            start += 1
        else:
            value = arr[start2]
            index = start2

            # Shift all the elements between element 1
            # element 2, right by 1.
            while (index != start):
                arr[index] = arr[index - 1]
                index -= 1

            arr[start] = value

            # Update all the pointers
            start += 1
            mid += 1
            start2 += 1

'''
* l is for left index and r is right index of
the sub-array of arr to be sorted
'''

def mergeSort(arr, l, r):
    if (l < r):

        # Same as (l + r) / 2, but avoids overflow
        # for large l and r
        m = l + (r - l) // 2

        # Sort first and second halves
        mergeSort(arr, l, m)
        mergeSort(arr, m + 1, r)

        merge(arr, l, m, r)

''' UTILITY FUNCTIONS '''
''' Function to pran array '''

def printArray(A, size):

    for i in range(size):
        print(A[i], end=" ")
    print()

''' Driver program to test above functions '''
if __name__ == '__main__':
    arr = [12, 11, 13, 5, 6, 7]
    arr_size = len(arr)

    mergeSort(arr, 0, arr_size - 1)
    printArray(arr, arr_size)

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program in-place Merge Sort
// sum.
using System;

class GFG {

    // Merges two subarrays of arr[].
    // First subarray is arr[l..m]
    // Second subarray is arr[m+1..r]
    // Inplace Implementation
    static void merge(int[] arr, int start, int mid,
                      int end)
    {
        int start2 = mid + 1;

        // If the direct merge is already sorted
        if (arr[mid] <= arr[start2]) {
            return;
        }

        // Two pointers to maintain start
        // of both arrays to merge
        while (start <= mid && start2 <= end) {

            // If element 1 is in right place
            if (arr[start] <= arr[start2]) {
                start++;
            }
            else {
                int value = arr[start2];
                int index = start2;

                // Shift all the elements between element 1
                // element 2, right by 1.
                while (index != start) {
                    arr[index] = arr[index - 1];
                    index--;
                }
                arr[start] = value;

                // Update all the pointers
                start++;
                mid++;
                start2++;
            }
        }
    }

    /* l is for left index and r is right index of the
    sub-array of arr to be sorted */
    static void mergeSort(int[] arr, int l, int r)
    {
        if (l < r) {

            // Same as (l + r) / 2, but avoids overflow
            // for large l and r
            int m = l + (r - l) / 2;

            // Sort first and second halves
            mergeSort(arr, l, m);
            mergeSort(arr, m + 1, r);

            merge(arr, l, m, r);
        }
    }

    /* UTILITY FUNCTIONS */
    /* Function to print an array */
    static void printArray(int[] A, int size)
    {
        int i;
        for (i = 0; i < size; i++)
            Console.Write(A[i] + " ");
        Console.WriteLine();
    }

    /* Driver code */
    public static void Main(String[] args)
    {
        int[] arr = { 12, 11, 13, 5, 6, 7 };
        int arr_size = arr.Length;

        mergeSort(arr, 0, arr_size - 1);
        printArray(arr, arr_size);
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program in-place Merge Sort

// Merges two subarrays of arr[].
// First subarray is arr[l..m]
// Second subarray is arr[m+1..r]
// Inplace Implementation
function merge(arr, start, mid, end)
{
    let start2 = mid + 1;

    // If the direct merge is already sorted
    if (arr[mid] <= arr[start2])
    {
        return;
    }

    // Two pointers to maintain start
    // of both arrays to merge
    while (start <= mid && start2 <= end)
    {

        // If element 1 is in right place
        if (arr[start] <= arr[start2])
        {
            start++;
        }
        else
        {
            let value = arr[start2];
            let index = start2;

            // Shift all the elements between element 1
            // element 2, right by 1.
            while (index != start)
            {
                arr[index] = arr[index - 1];
                index--;
            }
            arr[start] = value;

            // Update all the pointers
            start++;
            mid++;
            start2++;
        }
    }
}

/* l is for left index and r is right index
of the sub-array of arr to be sorted */
function mergeSort(arr, l, r)
{
    if (l < r)
    {

        // Same as (l + r) / 2, but avoids overflow
        // for large l and r
        let m = l + Math.floor((r - l) / 2);

        // Sort first and second halves
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);

        merge(arr, l, m, r);
    }
}

/* UTILITY FUNCTIONS */
/* Function to print an array */
function printArray(A, size)
{
    let i;
    for(i = 0; i < size; i++)
        document.write(A[i] + " ");

    document.write("<br>");
}

// Driver code
let arr = [ 12, 11, 13, 5, 6, 7 ];
let arr_size = arr.length;

mergeSort(arr, 0, arr_size - 1);
printArray(arr, arr_size);

// This code is contributed by rag2127

</script>
```

**Output**

```
5 6 7 11 12 13 
```

注:上述方法的[时间复杂度](http://penguin.ewu.edu/cscd300/Topic/AdvSorting/MergeSorts/InPlace.html#Top)为 O(n <sup>2</sup> * log(n))，因为合并为 O(n <sup>2</sup> )。[标准合并排序](https://www.geeksforgeeks.org/merge-sort/)时间复杂度较小，O(n Log n)。

**方法 2:** 思路:我们开始比较相距较远而不是相邻的元素。基本上我们是用 shell 排序来[合并两个排序后的数组，有 O(1)个额外的空间](https://www.geeksforgeeks.org/efficiently-merging-two-sorted-arrays-with-o1-extra-space/)。

mergeSort():

*   计算中间两个将阵列分成两半(左子阵列和右子阵列)
*   递归调用左子数组和右子数组上的合并排序来对它们进行排序
*   调用 merge 函数合并左子数组和右子数组

merge():

*   对于每个通道，我们计算间隙，并比较间隙右侧的元素。
*   以 n/2 的上限值启动间隙，其中 n 是左右子阵列的组合长度。
*   每通过一次，间隙减小到间隙/2 的上限。
*   拿一个指针 I 来传递数组。
*   如果第(i+gap)个元素小于第(或大于按降序排序时)个元素，则交换第(i+gap)个和第(I+gap)个元素。
*   当(i+gap)达到 n 时停止。

> **输入:** 10、30、14、11、16、7、28
> 
> 注意:假设左右子阵列已经排序，因此我们正在合并排序的子阵列[10，14，30]和[7，11，16，28]
> 
> 开始
> 
> 间隙= n/2 的上限= 7/2 = 4
> 
> [此间隙适用于整个合并数组]
> 
> **10** ，14，30，7， **11** ，16，28
> 
> 10、 **14** ，30、7、11、 **16** ，28
> 
> 10、14、 **30** 、7、11、16、 **28**
> 
> 10, 14, 28, 7, 11, 16, 30
> 
> 间隙= 4/2 的上限= 2
> 
> **10** ，14， **28** ，7，11，16，30
> 
> 10、 **14** 、28、 **7** 、11、16、30
> 
> 10，7， **28** ，14， **11** ，16，30
> 
> 10，7，11， **14** ，28， **16** ，30
> 
> 10、7、11、14、 **28** 、16、 **30**
> 
> 间隙= 2/2 = 1 的上限
> 
> **10** 、 **7** 、11、14、28、16、30
> 
> 7、 **10** 、 **11** 、14、28、16、30
> 
> 7、10、 **11** 、 **14** 、28、16、30
> 
> 7、10、11、 **14** 、 **28** 、16、30
> 
> 7、10、11、14、 **28** 、 **16** ，30
> 
> 7、10、11、14、16、 **28** 、 **30**
> 
> **输出:** 7、10、11、14、16、28、30

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Calculating next gap
int nextGap(int gap)
{
    if (gap <= 1)
        return 0;

    return (int)ceil(gap / 2.0);
}

// Function for swapping
void swap(int nums[], int i, int j)
{
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}

// Merging the subarrays using shell sorting
// Time Complexity: O(nlog n)
// Space Complexity: O(1)
void inPlaceMerge(int nums[], int start,
                              int end)
{
    int gap = end - start + 1;

    for(gap = nextGap(gap);
        gap > 0; gap = nextGap(gap))
    {
        for(int i = start; i + gap <= end; i++)
        {
            int j = i + gap;
            if (nums[i] > nums[j])
                swap(nums, i, j);
        }
    }
}

// merge sort makes log n recursive calls
// and each time calls merge()
// which takes nlog n steps
// Time Complexity: O(n*log n + 2((n/2)*log(n/2)) +
// 4((n/4)*log(n/4)) +.....+ 1)
// Time Complexity: O(logn*(n*log n))
// i.e. O(n*(logn)^2)
// Space Complexity: O(1)
void mergeSort(int nums[], int s, int e)
{
    if (s == e)
        return;

    // Calculating mid to slice the
    // array in two halves
    int mid = (s + e) / 2;

    // Recursive calls to sort left
    // and right subarrays
    mergeSort(nums, s, mid);
    mergeSort(nums, mid + 1, e);

    inPlaceMerge(nums, s, e);
}

// Driver Code
int main()
{
    int nums[] = { 12, 11, 13, 5, 6, 7 };
    int nums_size = sizeof(nums) / sizeof(nums[0]);

    mergeSort(nums, 0, nums_size-1);

    for(int i = 0; i < nums_size; i++)
    {
        cout << nums[i] << " ";
    }
    return 0;
}

// This code is contributed by adityapande88
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class InPlaceMerge {

    // Calculating next gap
    private static int nextGap(int gap)
    {
        if (gap <= 1)
            return 0;
        return (int)Math.ceil(gap / 2.0);
    }

    // Function for swapping
    private static void swap(int[] nums, int i, int j)
    {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    // Merging the subarrays using shell sorting
    // Time Complexity: O(nlog n)
    // Space Complexity: O(1)
    private static void inPlaceMerge(int[] nums, int start,
                                     int end)
    {
        int gap = end - start + 1;
        for (gap = nextGap(gap); gap > 0;
             gap = nextGap(gap)) {
            for (int i = start; i + gap <= end; i++) {
                int j = i + gap;
                if (nums[i] > nums[j])
                    swap(nums, i, j);
            }
        }
    }

    // merge sort makes log n recursive calls
    // and each time calls merge()
    // which takes nlog n steps
    // Time Complexity: O(n*log n + 2((n/2)*log(n/2)) +
    // 4((n/4)*log(n/4)) +.....+ 1)
    // Time Complexity: O(logn*(n*log n))
    // i.e. O(n*(logn)^2)
    // Space Complexity: O(1)
    private static void mergeSort(int[] nums, int s, int e)
    {
        if (s == e)
            return;

        // Calculating mid to slice the
        // array in two halves
        int mid = (s + e) / 2;

        // Recursive calls to sort left
        // and right subarrays
        mergeSort(nums, s, mid);
        mergeSort(nums, mid + 1, e);
        inPlaceMerge(nums, s, e);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] nums = new int[] { 12, 11, 13, 5, 6, 7 };
        mergeSort(nums, 0, nums.length - 1);
        System.out.println(Arrays.toString(nums));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math  

# Calculating next gap
def nextGap(gap):

    if gap <= 1:
        return 0

    return int(math.ceil(gap / 2))

# Function for swapping
def swap(nums, i, j):

    temp = nums[i]
    nums[i] = nums[j]
    nums[j] = temp

# Merging the subarrays using shell sorting
# Time Complexity: O(nlog n)
# Space Complexity: O(1)
def inPlaceMerge(nums,start, end):

    gap = end - start + 1
    gap = nextGap(gap)

    while gap > 0:
        i = start
        while (i + gap) <= end:
            j = i + gap

            if nums[i] > nums[j]:
                swap(nums, i, j)

            i += 1

        gap = nextGap(gap)

# merge sort makes log n recursive calls
# and each time calls merge()
# which takes nlog n steps
# Time Complexity: O(n*log n + 2((n/2)*log(n/2)) +
# 4((n/4)*log(n/4)) +.....+ 1)
# Time Complexity: O(logn*(n*log n))
# i.e. O(n*(logn)^2)
# Space Complexity: O(1)
def mergeSort(nums, s, e):

    if s == e:
        return

    # Calculating mid to slice the
    # array in two halves
    mid = (s + e) // 2

    # Recursive calls to sort left
    # and right subarrays
    mergeSort(nums, s, mid)
    mergeSort(nums, mid + 1, e)

    inPlaceMerge(nums, s, e)

# UTILITY FUNCTIONS
# Function to pran array
def printArray(A, size):

    for i in range(size):
        print(A[i], end = " ")

    print()

# Driver Code
if __name__ == '__main__':

    arr = [ 12, 11, 13, 5, 6, 7 ]
    arr_size = len(arr)

    mergeSort(arr, 0, arr_size - 1)
    printArray(arr, arr_size)

# This code is contributed by adityapande88
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Calculating next gap
function nextGap(gap)
{
    if (gap <= 1)
            return 0;
        return Math.floor(Math.ceil(gap / 2.0));
}

// Function for swapping
function swap(nums,i,j)
{
    let temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
}

// Merging the subarrays using shell sorting
    // Time Complexity: O(nlog n)
    // Space Complexity: O(1)
function inPlaceMerge(nums,start,end)
{
    let gap = end - start + 1;
        for (gap = nextGap(gap); gap > 0;
             gap = nextGap(gap)) {
            for (let i = start; i + gap <= end; i++) {
                let j = i + gap;
                if (nums[i] > nums[j])
                    swap(nums, i, j);
            }
        }
}

// merge sort makes log n recursive calls
    // and each time calls merge()
    // which takes nlog n steps
    // Time Complexity: O(n*log n + 2((n/2)*log(n/2)) +
    // 4((n/4)*log(n/4)) +.....+ 1)
    // Time Complexity: O(logn*(n*log n))
    // i.e. O(n*(logn)^2)
    // Space Complexity: O(1)
function mergeSort(nums,s,e)
{
    if (s == e)
            return;

        // Calculating mid to slice the
        // array in two halves
        let mid = Math.floor((s + e) / 2);

        // Recursive calls to sort left
        // and right subarrays
        mergeSort(nums, s, mid);
        mergeSort(nums, mid + 1, e);
        inPlaceMerge(nums, s, e);
}

// Driver Code
let nums=[12, 11, 13, 5, 6, 7 ];
mergeSort(nums, 0, nums.length - 1);
document.write((nums).join(" "));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
5 6 7 11 12 13 
```

**时间复杂度:** O(log n*nlog n)

**注意:** mergeSort 方法进行 n 次 log 递归调用，每次调用 merge，合并 2 个排序后的子数组需要 n 次 log n

**方法 3:** 这里我们使用下面的技巧:

```
Suppose we have a number A and we want to  
convert it to a number B and there is also a  
constraint that we can recover number A any  
time without using other variable.To achieve  
this we chose a number N which is greater  
than both numbers and add B*N in A.
so A --> A+B*N

To get number B out of (A+B*N)  
we divide (A+B*N) by N (A+B*N)/N = B.

To get number A out of (A+B*N)  
we take modulo with N (A+B*N)%N = A.

-> In short by taking modulo  
we get old number back and taking divide  
we new number.
```

**mergeSort():**

*   计算中间两个将阵列分成两半(左子阵列和右子阵列)
*   递归调用左子数组和右子数组上的合并排序来对它们进行排序
*   调用 merge 函数合并左子数组和右子数组

**合并():**

*   我们首先找到两个子阵列的最大元素，并将其递增 1，以避免在模运算过程中 0 和最大元素的冲突。
*   想法是从同时开始遍历两个子阵列。一个从 l 开始到 m，另一个从 m+1 开始到 r。所以，我们将初始化三个指针，比如 I，j，k
*   我将从 l 移动到 m；j 将从 m+1 移动到 r；k 将从 l 移动到 r。
*   现在通过添加 min(a[i]，a[j])*maximum_element 来更新值 a[k]。
*   然后也更新那些留在两个子数组中的元素。
*   更新完所有元素后，用 maximum_element 除所有元素，这样我们就可以得到更新后的数组。

下面是上述方法的实现:

## C++

```
// C++ program in-place Merge Sort
#include <bits/stdc++.h>
using namespace std;

// Merges two subarrays of arr[].
// First subarray is arr[l..m]
// Second subarray is arr[m+1..r]
// Inplace Implementation
void mergeInPlace(int a[], int l, int m, int r)
{
    // increment the maximum_element by one to avoid
    // collision of 0 and maximum element of array in modulo
    // operation
    int mx = max(a[m], a[r]) + 1;

    int i = l, j = m + 1, k = l;
    while (i <= m && j <= r && k <= r) {

        // recover back original element to compare
        int e1 = a[i] % mx;
        int e2 = a[j] % mx;
        if (e1 <= e2) {
            a[k] += (e1 * mx);
            i++;
            k++;
        }
        else {
            a[k] += (e2 * mx);
            j++;
            k++;
        }
    }

    // process those elements which are left in the array
    while (i <= m) {
        int el = a[i] % mx;
        a[k] += (el * mx);
        i++;
        k++;
    }

    while (j <= r) {
        int el = a[j] % mx;
        a[k] += (el * mx);
        j++;
        k++;
    }

    // finally update elements by dividing with maximum
    // element
    for (int i = l; i <= r; i++)
        a[i] /= mx;
}

/* l is for left index and r is right index of the
   sub-array of arr to be sorted */
void mergeSort(int arr[], int l, int r)
{
    if (l < r) {

        // Same as (l + r) / 2, but avoids overflow
        // for large l and r
        int m = l + (r - l) / 2;

        // Sort first and second halves
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
        mergeInPlace(arr, l, m, r);
    }
}

// Driver Code
int main()
{
    int nums[] = { 12, 11, 13, 5, 6, 7 };
    int nums_size = sizeof(nums) / sizeof(nums[0]);

    mergeSort(nums, 0, nums_size - 1);

    for (int i = 0; i < nums_size; i++) {
        cout << nums[i] << " ";
    }
    return 0;
}

// This code is contributed by soham11806959
```

**Output**

```
5 6 7 11 12 13 
```

**时间复杂度:**O(n log n)
T3】注:上述方法的时间复杂度为 O(n2)，因为 merge 为 O(n)。标准合并排序的时间复杂度为 O(n ^ log n)。

**方法 4** :这里我们使用以下技术来执行就地合并

```
Given 2 adjacent sorted sub-arrays within an array (hereafter
named A and B for convenience), appreciate that we can swap
some of the last portion of A with an equal number of elements
from the start of B, such that after the exchange, all of the
elements in A are less than or equal to any element in B.

After this exchange, this leaves with the A containing 2 sorted
sub-arrays, being the first original portion of A, and the first
original portion of B, and sub-array B now containing 2 sorted
sub-arrays, being the final original portion of A followed by
the final original portion of B

We can now recursively call the merge operation with the 2
sub-arrays of A, followed by recursively calling the merge
operation with the 2 sub-arrays of B

We stop the recursion when either A or B are empty, or when
either sub-array is small enough to efficiently merge into
the other sub-array using insertion sort. 
```

上面的过程自然有助于就地合并排序的以下实现。

**合并():**

*   此后，为了方便起见，我们将第一子阵列称为 A，第二子阵列称为 B
*   如果 A 或 B 是空的，或者如果第一个元素 B 不小于 A 的最后一个元素，那么我们就完成了
*   如果 A 的长度足够小，并且它的长度小于 B 的长度，那么使用插入排序将 A 合并到 B 中并返回
*   如果 B 的长度足够小，那么使用插入排序将 B 合并成 A 并返回
*   找到 A 中我们可以用 B 的第一部分交换 A 的剩余部分的位置，这样 A 中的所有<u>元素都小于或等于 B 中的任何元素</u>
*   执行甲和乙之间的交换
*   递归调用现在位于 A 中的 2 个排序子数组上的 **merge()**
*   递归调用现在位于 B 中的 2 个排序子数组上的 **merge()**

**merge_sort():**

*   将阵列分成两半(左子阵列和右子阵列)
*   递归调用左子数组和右子数组上的 **merge_sort()** 进行排序
*   调用 merge 函数合并左子数组和右子数组

## C++

```
// Merge In Place in C++

#include <iostream>
using namespace std;

#define __INSERT_THRESH 5
#define __swap(x, y) (t = *(x), *(x) = *(y), *(y) = t)

// Both sorted sub-arrays must be adjacent in 'a'
// 'an' is the length of the first sorted section in 'a'
// 'bn' is the length of the second sorted section in 'a'
static void merge(int* a, size_t an, size_t bn)
{
    int *b = a + an, *e = b + bn, *s, t;

    // Return right now if we're done
    if (an == 0 || bn == 0 || !(*b < *(b - 1)))
        return;

    // Do insertion sort to merge if size of sub-arrays are
    // small enough
    if (an < __INSERT_THRESH && an <= bn) {
        for (int *p = b, *v; p > a;
             p--) // Insert Sort A into B
            for (v = p, s = p - 1; v < e && *v < *s;
                 s = v, v++)
                __swap(s, v);
        return;
    }

    if (bn < __INSERT_THRESH) {
        for (int *p = b, *v; p < e;
             p++) // Insert Sort B into A
            for (s = p, v = p - 1; s > a && *s < *v;
                 s = v, v--)
                __swap(s, v);
        return;
    }

    // Find the pivot points.  Basically this is just
    // finding the point in 'a' where we can swap in the
    // first part of 'b' such that after the swap the last
    // element in 'a' will be less than or equal to the
    // least element in 'b'
    int *pa = a, *pb = b;

    for (s = a; s < b && pb < e; s++)
        if (*pb < *pa)
            pb++;
        else
            pa++;
    pa += b - s;

    // Swap first part of b with last part of a
    for (int *la = pa, *fb = b; la < b; la++, fb++)
        __swap(la, fb);

    // Now merge the two sub-array pairings
    merge(a, pa - a, pb - b);
    merge(b, pb - b, e - pb);
} // merge_array_inplace

#undef __swap
#undef __INSERT_THRESH

// Merge Sort Implementation
void merge_sort(int* a, size_t n)
{
    size_t m = (n + 1) / 2;

    // Sort first and second halves
    if (m > 1)
        merge_sort(a, m);

    if (n - m > 1)
        merge_sort(a + m, n - m);

    // Now merge the two sorted sub-arrays together
    merge(a, m, n - m);
}

// Function to print an array
void print_array(int a[], size_t n)
{
    if (n > 0) {
        cout <<" "<< a[0];
        for (size_t i = 1; i < n; i++)
            cout <<" "<< a[i];
    }
    cout <<"\n";
}

// Driver program to test sort utility
int main()
{
    int a[] = { 3, 16, 5, 14, 8,  10, 7, 15,
                1, 13, 4, 9,  12, 11, 6, 2 };
    size_t n = sizeof(a) / sizeof(a[0]);

    merge_sort(a, n);

    print_array(a, n);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
//                      Merge In Place in C

#include <stddef.h>
#include <stdio.h>

#define __INSERT_THRESH 5
#define __swap(x, y) (t = *(x), *(x) = *(y), *(y) = t)

// Both sorted sub-arrays must be adjacent in 'a'
// 'an' is the length of the first sorted section in 'a'
// 'bn' is the length of the second sorted section in 'a'
static void merge(int* a, size_t an, size_t bn)
{
    int *b = a + an, *e = b + bn, *s, t;

    // Return right now if we're done
    if (an == 0 || bn == 0 || !(*b < *(b - 1)))
        return;

    // Do insertion sort to merge if size of sub-arrays are
    // small enough
    if (an < __INSERT_THRESH && an <= bn) {
        for (int *p = b, *v; p > a;
             p--) // Insert Sort A into B
            for (v = p, s = p - 1; v < e && *v < *s;
                 s = v, v++)
                __swap(s, v);
        return;
    }

    if (bn < __INSERT_THRESH) {
        for (int *p = b, *v; p < e;
             p++) // Insert Sort B into A
            for (s = p, v = p - 1; s > a && *s < *v;
                 s = v, v--)
                __swap(s, v);
        return;
    }

    // Find the pivot points.  Basically this is just
    // finding the point in 'a' where we can swap in the
    // first part of 'b' such that after the swap the last
    // element in 'a' will be less than or equal to the
    // least element in 'b'
    int *pa = a, *pb = b;

    for (s = a; s < b && pb < e; s++)
        if (*pb < *pa)
            pb++;
        else
            pa++;
    pa += b - s;

    // Swap first part of b with last part of a
    for (int *la = pa, *fb = b; la < b; la++, fb++)
        __swap(la, fb);

    // Now merge the two sub-array pairings
    merge(a, pa - a, pb - b);
    merge(b, pb - b, e - pb);
} // merge_array_inplace

#undef __swap
#undef __INSERT_THRESH

// Merge Sort Implementation
void merge_sort(int* a, size_t n)
{
    size_t m = (n + 1) / 2;

    // Sort first and second halves
    if (m > 1)
        merge_sort(a, m);

    if (n - m > 1)
        merge_sort(a + m, n - m);

    // Now merge the two sorted sub-arrays together
    merge(a, m, n - m);
}

// Function to print an array
void print_array(int a[], size_t n)
{
    if (n > 0) {
        printf("%d", a[0]);
        for (size_t i = 1; i < n; i++)
            printf(" %d", a[i]);
    }
    printf("\n");
}

// Driver program to test sort utiliyy
int main()
{
    int a[] = { 3, 16, 5, 14, 8,  10, 7, 15,
                1, 13, 4, 9,  12, 11, 6, 2 };
    size_t n = sizeof(a) / sizeof(a[0]);

    merge_sort(a, n);

    print_array(a, n);
    return 0;
}

// Author: Stew Forster (stew675@gmail.com)     Date: 29
// July 2021
```

**Output**

```
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16
```

**merge()的时间复杂度:** : *最坏情况:* O(n^2，*平均:*o(n log n)*最佳:* O(1)

**merge _ sort()**函数的时间复杂度:*整体来说:* O(log n)单独对于递归来说，由于总是将数组平均分为 2

**时间复杂度** **merge_sort()** 整体:*最差情况:* O(n^2 对数 n)*平均:* O(n(对数 n)^2)*最佳:* O(对数 n)

最坏的情况发生在 **merge()** 内的每个子阵列交换只导致 *_INSERT_THRESH-1* 元素被交换的时候