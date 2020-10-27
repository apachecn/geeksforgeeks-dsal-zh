# 用恒定的额外空间重新排列正数和负数

> 原文： [https://www.geeksforgeeks.org/rearrange-positive-and-negative-numbers/](https://www.geeksforgeeks.org/rearrange-positive-and-negative-numbers/)

给定一个正负数组，将它们排列成使所有负整数出现在数组中的所有正整数之前，而无需使用任何其他数据结构（例如哈希表，数组等）。出现的顺序应保持。

**示例**：

```
Input:  [12 11 -13 -5 6 -7 5 -3 -6]
Output: [-13 -5 -7 -3 -6 12 11 6 5]

```



一个简单的解决方案是使用另一个数组。 我们将原始数组的所有元素复制到新数组。 然后，我们遍历新数组，并将所有负数和正数元素一一复制回原始数组。 在中讨论了这种方法。 这种方法的问题在于它使用辅助数组，并且我们不允许使用任何数据结构来解决此问题。

一种不使用任何数据结构的方法是使用快排的使用分区过程。 想法是将 0 视为枢轴并围绕其划分数组。 这种方法的问题在于它会更改元素的相对顺序。 在中讨论了类似的分区过程。

现在，让我们讨论一些不使用任何其他数据结构并保留元素相对顺序的方法。

**方法 1：修改插入排序**：

我们可以修改[插入排序](http://geeksquiz.com/insertion-sort/)来解决此问题。

算法–

```
Loop from i = 1 to n - 1.
  a) If the current element is positive, do nothing.
  b) If the current element arr[i] is negative, we 
     insert it into sequence arr[0..i-1] such that 
     all positive elements in arr[0..i-1] are shifted 
     one position to their right and arr[i] is inserted
     at index of first positive element.

```

下面是实现–

## C++ 

```cpp

// C++ program to Rearrange positive and negative 
// numbers in a array 
#include <stdio.h> 

// A utility function to print an array of size n 
void printArray(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) 
        printf("%d ", arr[i]); 
    printf("\n"); 
} 

// Function to Rearrange positive and negative 
// numbers in a array 
void RearrangePosNeg(int arr[], int n) 
{ 
    int key, j; 
    for (int i = 1; i < n; i++) { 
        key = arr[i]; 

        // if current element is positive 
        // do nothing 
        if (key > 0) 
            continue; 

        /* if current element is negative, 
        shift positive elements of arr[0..i-1], 
        to one position to their right */
        j = i - 1; 
        while (j >= 0 && arr[j] > 0) { 
            arr[j + 1] = arr[j]; 
            j = j - 1; 
        } 

        // Put negative element at its right position 
        arr[j + 1] = key; 
    } 
} 

/* Driver program to test above functions */
int main() 
{ 
    int arr[] = { -12, 11, -13, -5, 6, -7, 5, -3, -6 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    RearrangePosNeg(arr, n); 
    printArray(arr, n); 

    return 0; 
} 

```

## Java

```java
// Java program to Rearrange positive 
// and negative numbers in a array 
import java.io.*; 
  
class GFG { 
    // A utility function to print 
    // an array of size n 
    static void printArray(int arr[], int n) 
    { 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 
        System.out.println(); 
    } 
  
    // Function to Rearrange positive and negative 
    // numbers in a array 
    static void RearrangePosNeg(int arr[], int n) 
    { 
        int key, j; 
        for (int i = 1; i < n; i++) { 
            key = arr[i]; 
  
            // if current element is positive 
            // do nothing 
            if (key > 0) 
                continue; 
  
            /* if current element is negative, 
            shift positive elements of arr[0..i-1], 
            to one position to their right */
            j = i - 1; 
            while (j >= 0 && arr[j] > 0) { 
                arr[j + 1] = arr[j]; 
                j = j - 1; 
            } 
  
            // Put negative element at its right position 
            arr[j + 1] = key; 
        } 
    } 
  
    // Driver program 
    public static void main(String[] args) 
    { 
        int arr[] = { -12, 11, -13, -5, 6, -7, 5, -3, -6 }; 
        int n = arr.length; 
        RearrangePosNeg(arr, n); 
        printArray(arr, n); 
    } 
} 
  
// This code is contributed by vt_m. 
```

## Python 3

```py
# Python 3 program to Rearrange positive  
# and negative numbers in a array 
  
# A utility function to print  
# an array of size n 
def printArray(arr, n): 
    for i in range(n): 
        print(arr[i], end = " ") 
    print() 
  
# Function to Rearrange positive  
# and negative numbers in a array 
def RearrangePosNeg(arr, n): 
  
    for i in range(1, n): 
        key = arr[i] 
  
        # if current element is positive 
        # do nothing 
        if (key > 0): 
            continue
  
        ''' if current element is negative, 
        shift positive elements of arr[0..i-1], 
        to one position to their right '''
        j = i - 1
        while (j >= 0 and arr[j] > 0): 
            arr[j + 1] = arr[j] 
            j = j - 1
  
        # Put negative element at its  
        # right position 
        arr[j + 1] = key 
  
# Driver Code 
if __name__ == "__main__": 
    arr = [ -12, 11, -13, -5,  
            6, -7, 5, -3, -6 ] 
    n = len(arr) 
  
    RearrangePosNeg(arr, n) 
    printArray(arr, n) 
  
# This code is contributed 
# by ChitraNayal 
```

## C#

```cs
// C# program to Rearrange positive 
// and negative numbers in a array 
using System; 
  
class GFG { 
  
    // A utility function to print 
    // an array of size n 
    static void printArray(int[] arr, int n) 
    { 
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i] + " "); 
        Console.WriteLine(); 
    } 
  
    // Function to Rearrange positive and negative 
    // numbers in a array 
    static void RearrangePosNeg(int[] arr, int n) 
    { 
        int key, j; 
        for (int i = 1; i < n; i++) { 
            key = arr[i]; 
  
            // if current element is positive 
            // do nothing 
            if (key > 0) 
                continue; 
  
            /* if current element is negative, 
            shift positive elements of arr[0..i-1], 
            to one position to their right */
            j = i - 1; 
            while (j >= 0 && arr[j] > 0) { 
                arr[j + 1] = arr[j]; 
                j = j - 1; 
            } 
  
            // Put negative element at its right position 
            arr[j + 1] = key; 
        } 
    } 
  
    // Driver program 
    public static void Main() 
    { 
        int[] arr = { -12, 11, -13, -5, 6, 
                      -7, 5, -3, -6 }; 
        int n = arr.Length; 
        RearrangePosNeg(arr, n); 
        printArray(arr, n); 
    } 
} 
  
// This code is contributed by vt_m. 
```

## PHP

```php
<?php 
// PHP program to Rearrange positive  
// and negative numbers in a array 
// A utility function to print  
// an array of size n 
function printArray($arr, $n) 
{ 
    for ($i = 0; $i < $n; $i++) 
        echo($arr[$i] . " "); 
} 
  
// Function to Rearrange positive and negative 
// numbers in a array 
function RearrangePosNeg(&$arr, $n) 
{ 
    $key; $j; 
    for($i = 1; $i < $n; $i++) 
    { 
        $key = $arr[$i]; 
  
        // if current element is positive 
        // do nothing 
        if ($key > 0) 
            continue; 
  
        /* if current element is negative, 
        shift positive elements of arr[0..i-1], 
        to one position to their right */
        $j = $i - 1; 
        while ($j >= 0 && $arr[$j] > 0) 
        { 
            $arr[$j + 1] = $arr[$j]; 
            $j = $j - 1; 
        } 
  
        // Put negative element at its right position 
        $arr[$j + 1] = $key; 
    } 
} 
  
// Driver program  
{ 
    $arr = array( -12, 11, -13, -5, 6, -7, 5, -3, -6 ); 
    $n = sizeof($arr); 
    RearrangePosNeg($arr, $n); 
    printArray($arr, $n); 
  
} 
  
// This code is contributed by Code_Mech. 
```

输出：

```
-12 -13 -5 -7 -3 -6 11 6 5
```

上述解决方案的时间复杂度为`O(n ^ 2)`，辅助空间为`O(1)`。 我们保持了外观顺序，没有使用任何其他数据结构。

方法 2 - 优化合并排序：

可以修改标准合并排序算法的合并方法来解决此问题。 合并左右两个排序的半部分时，我们需要以这样的方式合并：先复制左和右子数组的负部分，然后再复制左和右子数组的正部分。

以下是该想法的实现：

## C++

```cpp
// C++ program to Rearrange positive and negative 
// numbers in a array 
#include <iostream> 
using namespace std; 
  
/* Function to print an array */
void printArray(int A[], int size) 
{ 
    for (int i = 0; i < size; i++) 
        cout << A[i] << " "; 
    cout << endl; 
} 
  
// Merges two subarrays of arr[]. 
// First subarray is arr[l..m] 
// Second subarray is arr[m+1..r] 
void merge(int arr[], int l, int m, int r) 
{ 
    int i, j, k; 
    int n1 = m - l + 1; 
    int n2 = r - m; 
  
    /* create temp arrays */
    int L[n1], R[n2]; 
  
    /* Copy data to temp arrays L[] and R[] */
    for (i = 0; i < n1; i++) 
        L[i] = arr[l + i]; 
    for (j = 0; j < n2; j++) 
        R[j] = arr[m + 1 + j]; 
  
    /* Merge the temp arrays back into arr[l..r]*/
    i = 0; // Initial index of first subarray 
    j = 0; // Initial index of second subarray 
    k = l; // Initial index of merged subarray 
  
    // Note the order of appearance of elements should 
    // be maintained - we copy elements of left subarray 
    // first followed by that of right subarray 
  
    // copy negative elements of left subarray 
    while (i < n1 && L[i] < 0) 
        arr[k++] = L[i++]; 
  
    // copy negative elements of right subarray 
    while (j < n2 && R[j] < 0) 
        arr[k++] = R[j++]; 
  
    // copy positive elements of left subarray 
    while (i < n1) 
        arr[k++] = L[i++]; 
  
    // copy positive elements of right subarray 
    while (j < n2) 
        arr[k++] = R[j++]; 
} 
  
// Function to Rearrange positive and negative 
// numbers in a array 
void RearrangePosNeg(int arr[], int l, int r) 
{ 
    if (l < r) { 
        // Same as (l + r)/2, but avoids overflow for 
        // large l and h 
        int m = l + (r - l) / 2; 
  
        // Sort first and second halves 
        RearrangePosNeg(arr, l, m); 
        RearrangePosNeg(arr, m + 1, r); 
  
        merge(arr, l, m, r); 
    } 
} 
  
/* Driver program to test above functions */
int main() 
{ 
    int arr[] = { -12, 11, -13, -5, 6, -7, 5, -3, -6 }; 
    int arr_size = sizeof(arr) / sizeof(arr[0]); 
  
    RearrangePosNeg(arr, 0, arr_size - 1); 
  
    printArray(arr, arr_size); 
  
    return 0; 
} 
```

## Java

```java
// Java program to Rearrange positive 
// and negative numbers in a array 
import java.io.*; 
  
class GFG { 
    /* Function to print an array */
    static void printArray(int A[], int size) 
    { 
        for (int i = 0; i < size; i++) 
            System.out.print(A[i] + " "); 
        System.out.println(); 
    } 
  
    // Merges two subarrays of arr[]. 
    // First subarray is arr[l..m] 
    // Second subarray is arr[m+1..r] 
    static void merge(int arr[], int l, int m, int r) 
    { 
        int i, j, k; 
        int n1 = m - l + 1; 
        int n2 = r - m; 
  
        /* create temp arrays */
        int L[] = new int[n1]; 
        int R[] = new int[n2]; 
  
        /* Copy data to temp arrays L[] and R[] */
        for (i = 0; i < n1; i++) 
            L[i] = arr[l + i]; 
        for (j = 0; j < n2; j++) 
            R[j] = arr[m + 1 + j]; 
  
        /* Merge the temp arrays back into arr[l..r]*/
        // Initial index of first subarray 
        i = 0; 
  
        // Initial index of second subarray 
        j = 0; 
  
        // Initial index of merged subarray 
        k = l; 
  
        // Note the order of appearance of elements should 
        // be maintained - we copy elements of left subarray 
        // first followed by that of right subarray 
  
        // copy negative elements of left subarray 
        while (i < n1 && L[i] < 0) 
            arr[k++] = L[i++]; 
  
        // copy negative elements of right subarray 
        while (j < n2 && R[j] < 0) 
            arr[k++] = R[j++]; 
  
        // copy positive elements of left subarray 
        while (i < n1) 
            arr[k++] = L[i++]; 
  
        // copy positive elements of right subarray 
        while (j < n2) 
            arr[k++] = R[j++]; 
    } 
  
    // Function to Rearrange positive and negative 
    // numbers in a array 
    static void RearrangePosNeg(int arr[], int l, int r) 
    { 
        if (l < r) { 
            // Same as (l + r)/2, but avoids overflow for 
            // large l and h 
            int m = l + (r - l) / 2; 
  
            // Sort first and second halves 
            RearrangePosNeg(arr, l, m); 
            RearrangePosNeg(arr, m + 1, r); 
  
            merge(arr, l, m, r); 
        } 
    } 
  
    // Driver program 
    public static void main(String[] args) 
    { 
        int arr[] = { -12, 11, -13, -5, 6, -7, 5, -3, -6 }; 
        int arr_size = arr.length; 
        RearrangePosNeg(arr, 0, arr_size - 1); 
        printArray(arr, arr_size); 
    } 
} 
  
// This code is contributed by vt_m. 
```

## Python3

```py
# Python3 program to Rearrange positive  
# and negative numbers in a array 
  
# Function to pran array 
def printArray(A, size): 
  
    for i in range(size): 
        print(A[i], end = " ") 
    print()  
  
# Merges two subarrays of arr[]. 
# First subarray is arr[l..m] 
# Second subarray is arr[m + 1..r] 
def merge(arr, l, m, r): 
    i, j, k = 0, 0, 0
    n1 = m - l + 1
    n2 = r - m 
  
    # create temp arrays */ 
    L = [arr[l + i] for i in range(n1)] 
    R = [arr[m + 1 + j] for j in range(n2)] 
  
    # Merge the temp arrays back into arr[l..r]*/ 
    i = 0 # Initial index of first subarray 
    j = 0 # Initial index of second subarray 
    k = l # Initial index of merged subarray 
  
    # Note the order of appearance of elements  
    # should be maintained - we copy elements  
    # of left subarray first followed by that  
    # of right subarray 
  
    # copy negative elements of left subarray 
    while (i < n1 and L[i] < 0): 
        arr[k] = L[i] 
        k += 1
        i += 1
  
    # copy negative elements of right subarray 
    while (j < n2 and R[j] < 0): 
        arr[k] = R[j] 
        k += 1
        j += 1
  
    # copy positive elements of left subarray 
    while (i < n1): 
        arr[k] = L[i] 
        k += 1
        i += 1
  
    # copy positive elements of right subarray 
    while (j < n2): 
        arr[k] = R[j] 
        k += 1
        j += 1
  
# Function to Rearrange positive and  
# negative numbers in a array 
def RearrangePosNeg(arr, l, r): 
  
    if(l < r): 
          
        # Same as (l + r)/2, but avoids  
        # overflow for large l and h 
        m = l + (r - l) // 2
  
        # Sort first and second halves 
        RearrangePosNeg(arr, l, m) 
        RearrangePosNeg(arr, m + 1, r) 
  
        merge(arr, l, m, r) 
      
# Driver Code 
arr = [ -12, 11, -13, -5,  
        6, -7, 5, -3, -6 ] 
arr_size = len(arr) 
  
RearrangePosNeg(arr, 0, arr_size - 1) 
  
printArray(arr, arr_size) 
  
# This code is contributed by 
# mohit kumar 29 
```

## C#

```cs
// C# program to Rearrange positive 
// and negative numbers in a array 
using System; 
  
class GFG { 
  
    /* Function to print an array */
    static void printArray(int[] A, int size) 
    { 
        for (int i = 0; i < size; i++) 
            Console.Write(A[i] + " "); 
        Console.WriteLine(); 
    } 
  
    // Merges two subarrays of arr[]. 
    // First subarray is arr[l..m] 
    // Second subarray is arr[m+1..r] 
    static void merge(int[] arr, int l, int m, int r) 
    { 
        int i, j, k; 
        int n1 = m - l + 1; 
        int n2 = r - m; 
  
        /* create temp arrays */
        int[] L = new int[n1]; 
        int[] R = new int[n2]; 
  
        /* Copy data to temp arrays L[] and R[] */
        for (i = 0; i < n1; i++) 
            L[i] = arr[l + i]; 
        for (j = 0; j < n2; j++) 
            R[j] = arr[m + 1 + j]; 
  
        /* Merge the temp arrays back into arr[l..r]*/
        // Initial index of first subarray 
        i = 0; 
  
        // Initial index of second subarray 
        j = 0; 
  
        // Initial index of merged subarray 
        k = l; 
  
        // Note the order of appearance of elements should 
        // be maintained - we copy elements of left subarray 
        // first followed by that of right subarray 
  
        // copy negative elements of left subarray 
        while (i < n1 && L[i] < 0) 
            arr[k++] = L[i++]; 
  
        // copy negative elements of right subarray 
        while (j < n2 && R[j] < 0) 
            arr[k++] = R[j++]; 
  
        // copy positive elements of left subarray 
        while (i < n1) 
            arr[k++] = L[i++]; 
  
        // copy positive elements of right subarray 
        while (j < n2) 
            arr[k++] = R[j++]; 
    } 
  
    // Function to Rearrange positive and negative 
    // numbers in a array 
    static void RearrangePosNeg(int[] arr, int l, int r) 
    { 
        if (l < r) { 
  
            // Same as (l + r)/2, but avoids overflow for 
            // large l and h 
            int m = l + (r - l) / 2; 
  
            // Sort first and second halves 
            RearrangePosNeg(arr, l, m); 
            RearrangePosNeg(arr, m + 1, r); 
  
            merge(arr, l, m, r); 
        } 
    } 
  
    // Driver program 
    public static void Main() 
    { 
        int[] arr = { -12, 11, -13, -5, 6, -7, 5, -3, -6 }; 
        int arr_size = arr.Length; 
        RearrangePosNeg(arr, 0, arr_size - 1); 
        printArray(arr, arr_size); 
    } 
} 
  
// This code is contributed by vt_m. 
```

输出：

```
-12 -13 -5 -7 -3 -6 11 6 5
```

上述解决方案的时间复杂度为`O（n log n）`。 这种方法的问题是我们正在使用辅助数组进行合并，但不允许使用任何数据结构来解决此问题。 我们可以在不使用任何数据结构的情况下进行原地合并。 这个想法来自这里。

令`Ln`和`Lp`分别表示左子数组的负部分和正部分。 类似地，`Rn`和`Rp`分别表示右子数组的负和正部分。

以下是在不使用多余空间的情况下将`[Ln Lp Rn Rp]`转换为`[Ln Rn Lp Rp]`的步骤。

1.  反转`Lp`和`Rn`。 我们得到`[Lp] -> [Lp']`和`[Rn] -> [Rn']`：`[Ln Lp Rn Rp] -> [Ln Lp’ Rn’ Rp]`。

2.  反转`[Lp’ Rn’]`。 我们得到`[Rn Lp]`，`[Ln Lp’ Rn’ Rp] -> [Ln Rn Lp Rp]`。

以下是上述想法的实现：

## C++

```cpp
// C++ program to Rearrange positive and negative 
// numbers in a array 
#include <bits/stdc++.h> 
using namespace std; 
  
/* Function to print an array */
void printArray(int A[], int size) 
{ 
    for (int i = 0; i < size; i++) 
        cout << A[i] << " "; 
    cout << endl; 
} 
  
/* Function to reverse an array. An array can be 
reversed in O(n) time and O(1) space. */
void reverse(int arr[], int l, int r) 
{ 
    if (l < r) { 
        swap(arr[l], arr[r]); 
        reverse(arr, ++l, --r); 
    } 
} 
  
// Merges two subarrays of arr[]. 
// First subarray is arr[l..m] 
// Second subarray is arr[m+1..r] 
void merge(int arr[], int l, int m, int r) 
{ 
    int i = l; // Initial index of 1st subarray 
    int j = m + 1; // Initial index of IInd 
  
    while (i <= m && arr[i] < 0) 
        i++; 
  
    // arr[i..m] is positive 
  
    while (j <= r && arr[j] < 0) 
        j++; 
  
    // arr[j..r] is positive 
  
    // reverse positive part of left sub-array (arr[i..m]) 
    reverse(arr, i, m); 
  
    // reverse negative part of right sub-array (arr[m+1..j-1]) 
    reverse(arr, m + 1, j - 1); 
  
    // reverse arr[i..j-1] 
    reverse(arr, i, j - 1); 
} 
  
// Function to Rearrange positive and negative 
// numbers in a array 
void RearrangePosNeg(int arr[], int l, int r) 
{ 
    if (l < r) { 
        // Same as (l+r)/2, but avoids overflow for 
        // large l and h 
        int m = l + (r - l) / 2; 
  
        // Sort first and second halves 
        RearrangePosNeg(arr, l, m); 
        RearrangePosNeg(arr, m + 1, r); 
  
        merge(arr, l, m, r); 
    } 
} 
  
/* Driver program to test above functions */
int main() 
{ 
    int arr[] = { -12, 11, -13, -5, 6, -7, 5, -3, -6 }; 
    int arr_size = sizeof(arr) / sizeof(arr[0]); 
  
    RearrangePosNeg(arr, 0, arr_size - 1); 
  
    printArray(arr, arr_size); 
  
    return 0; 
} 
```

## Java

```java
// Java program to Rearrange positive and negative 
// numbers in a array 
class GFG { 
  
    /* Function to print an array */
    static void printArray(int A[], int size) 
    { 
        for (int i = 0; i < size; i++) 
            System.out.print(A[i] + " "); 
        System.out.println(""); 
        ; 
    } 
  
    /* Function to reverse an array. An array can be 
reversed in O(n) time and O(1) space. */
    static void reverse(int arr[], int l, int r) 
    { 
        if (l < r) { 
            arr = swap(arr, l, r); 
            reverse(arr, ++l, --r); 
        } 
    } 
  
    // Merges two subarrays of arr[]. 
    // First subarray is arr[l..m] 
    // Second subarray is arr[m+1..r] 
    static void merge(int arr[], int l, int m, int r) 
    { 
        int i = l; // Initial index of 1st subarray 
        int j = m + 1; // Initial index of IInd 
  
        while (i <= m && arr[i] < 0) 
            i++; 
  
        // arr[i..m] is positive 
  
        while (j <= r && arr[j] < 0) 
            j++; 
  
        // arr[j..r] is positive 
  
        // reverse positive part of 
        // left sub-array (arr[i..m]) 
        reverse(arr, i, m); 
  
        // reverse negative part of 
        // right sub-array (arr[m+1..j-1]) 
        reverse(arr, m + 1, j - 1); 
  
        // reverse arr[i..j-1] 
        reverse(arr, i, j - 1); 
    } 
  
    // Function to Rearrange positive and negative 
    // numbers in a array 
    static void RearrangePosNeg(int arr[], int l, int r) 
    { 
        if (l < r) { 
            // Same as (l+r)/2, but avoids overflow for 
            // large l and h 
            int m = l + (r - l) / 2; 
  
            // Sort first and second halves 
            RearrangePosNeg(arr, l, m); 
            RearrangePosNeg(arr, m + 1, r); 
  
            merge(arr, l, m, r); 
        } 
    } 
    static int[] swap(int[] arr, int i, int j) 
    { 
        int temp = arr[i]; 
        arr[i] = arr[j]; 
        arr[j] = temp; 
        return arr; 
    } 
  
    /* Driver code*/
    public static void main(String[] args) 
    { 
        int arr[] = { -12, 11, -13, -5, 6, -7, 5, -3, -6 }; 
        int arr_size = arr.length; 
  
        RearrangePosNeg(arr, 0, arr_size - 1); 
  
        printArray(arr, arr_size); 
    } 
} 
  
// This code has been contributed by 29AjayKumar 
```

## Python3

```py
# Python3 program to Rearrange positive  
# and negative numbers in an array  
  
# Function to print an array  
def printArray(A, size):  
  
    for i in range(0, size):  
        print(A[i], end = " ")  
    print() 
  
# Function to reverse an array. An array can  
# be reversed in O(n) time and O(1) space. 
def reverse(arr, l, r):  
  
    if l < r: 
      
        arr[l], arr[r] = arr[r], arr[l] 
        l, r = l + 1, r - 1
        reverse(arr, l, r)  
      
# Merges two subarrays of arr[].  
# First subarray is arr[l..m]  
# Second subarray is arr[m + 1..r]  
def merge(arr, l, m, r):  
  
    i = l # Initial index of 1st subarray  
    j = m + 1 # Initial index of IInd  
  
    while i <= m and arr[i] < 0:  
        i += 1
  
    # arr[i..m] is positive  
  
    while j <= r and arr[j] < 0:  
        j += 1
  
    # arr[j..r] is positive  
  
    # reverse positive part of left 
    # sub-array (arr[i..m])  
    reverse(arr, i, m)  
  
    # reverse negative part of right  
    # sub-array (arr[m + 1..j-1])  
    reverse(arr, m + 1, j - 1)  
  
    # reverse arr[i..j-1]  
    reverse(arr, i, j - 1)  
  
# Function to Rearrange positive  
# and negative numbers in a array  
def RearrangePosNeg(arr, l, r):  
  
    if l < r: 
      
        # Same as (l + r)/2, but avoids  
        # overflow for large l and h  
        m = l + (r - l) // 2
  
        # Sort first and second halves  
        RearrangePosNeg(arr, l, m)  
        RearrangePosNeg(arr, m + 1, r)  
  
        merge(arr, l, m, r)  
  
# Driver Code 
if __name__ == "__main__":  
  
    arr = [-12, 11, -13, -5, 6, -7, 5, -3, -6]  
    arr_size = len(arr)  
  
    RearrangePosNeg(arr, 0, arr_size - 1)  
  
    printArray(arr, arr_size)  
  
# This code is contributed by Rituraj Jain 
```

## C#

```cs
// C# program to Rearrange positive and negative 
// numbers in a array 
using System; 
  
class GFG { 
  
    /* Function to print an array */
    static void printArray(int[] A, int size) 
    { 
        for (int i = 0; i < size; i++) 
            Console.Write(A[i] + " "); 
        Console.WriteLine(""); 
        ; 
    } 
  
    /* Function to reverse an array. An array can be 
reversed in O(n) time and O(1) space. */
    static void reverse(int[] arr, int l, int r) 
    { 
        if (l < r) { 
            arr = swap(arr, l, r); 
            reverse(arr, ++l, --r); 
        } 
    } 
  
    // Merges two subarrays of arr[]. 
    // First subarray is arr[l..m] 
    // Second subarray is arr[m+1..r] 
    static void merge(int[] arr, int l, int m, int r) 
    { 
        int i = l; // Initial index of 1st subarray 
        int j = m + 1; // Initial index of IInd 
  
        while (i <= m && arr[i] < 0) 
            i++; 
  
        // arr[i..m] is positive 
  
        while (j <= r && arr[j] < 0) 
            j++; 
  
        // arr[j..r] is positive 
  
        // reverse positive part of 
        // left sub-array (arr[i..m]) 
        reverse(arr, i, m); 
  
        // reverse negative part of 
        // right sub-array (arr[m+1..j-1]) 
        reverse(arr, m + 1, j - 1); 
  
        // reverse arr[i..j-1] 
        reverse(arr, i, j - 1); 
    } 
  
    // Function to Rearrange positive and negative 
    // numbers in a array 
    static void RearrangePosNeg(int[] arr, int l, int r) 
    { 
        if (l < r) { 
            // Same as (l+r)/2, but avoids overflow for 
            // large l and h 
            int m = l + (r - l) / 2; 
  
            // Sort first and second halves 
            RearrangePosNeg(arr, l, m); 
            RearrangePosNeg(arr, m + 1, r); 
  
            merge(arr, l, m, r); 
        } 
    } 
    static int[] swap(int[] arr, int i, int j) 
    { 
        int temp = arr[i]; 
        arr[i] = arr[j]; 
        arr[j] = temp; 
        return arr; 
    } 
  
    /* Driver code*/
    public static void Main() 
    { 
        int[] arr = { -12, 11, -13, -5, 6, -7, 5, -3, -6 }; 
        int arr_size = arr.Length; 
  
        RearrangePosNeg(arr, 0, arr_size - 1); 
  
        printArray(arr, arr_size); 
    } 
} 
  
/* This code contributed by PrinciRaj1992 */
```

输出：

```
-12 -13 -5 -7 -3 -6 11 6 5
```

上述解决方案的时间复杂度是`O(n log n)`，`O(Log n)`用于递归调用的空间，并且没有其他数据结构。