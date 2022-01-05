# 存储重复的键值对，并按键对键值对进行排序

> 原文:[https://www . geeksforgeeks . org/store-复制-键-值-对-键-值-对-键-值-对-排序/](https://www.geeksforgeeks.org/store-duplicate-keys-values-pair-and-sort-the-key-value-pair-by-key/)

给定包含重复键和值的 **N** 键-值对，任务是存储这些对并按键对这些对进行排序。

**示例:**

> **输入:**
> N : 10
> 键:5 1 4 6 8 0 6 5 5
> 值:0 1 2 3 4 5 6 7 8 9
> **输出:**
> 键:0 1 4 5 5 5 6 6 6 8
> 值:5 1 2 0 8 9 3 6 7 4
> **解释:**
> 我们给出了 10 个包含重复键和值的键、值对。
> 键值对是{(5，0)，(1，1)，(4，2)，(6，3)，(8，4)，(0，5)，(6，6)，
> (6，7)，(5，8)，(5，9)}我们想存储这些键值对，并按键对这些
> 键值对进行排序。所以，期望的输出是{(0，5)，(1，1)，(4，2)，(5，0)，
> (5，8)，(5，9)，(6，3)，(6，6)，(6，7)，(8，4)}。因为排序后的
> 键递增顺序是{0，1，4，5，5，5，6，6，6，8}。

**方法:**
为了解决上面提到的问题，我们可以使用单独的数组来存储键和值，然后我们可以简单地通过**合并排序算法**来排序键。我们可以使用任何排序算法，但 Mergesort 是最快的标准排序算法，并行地，我们可以对值数组执行与对键执行的操作相同的操作，以便键-值对在两个数组上保持相同的索引。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Store duplicate
// keys-values pair and sort the
// key-value pair by key
import java.util.*;
import java.lang.*;
import java.io.*;

class Solution {

    // Merges two subarrays of arr[].
    // First subarray is arr[l..m]
    // Second subarray is arr[m+1..r]
    void merge(int arrk[], int l, int m,
            int r, int arrv[])
    {
        // Sizes of two subarrays
        // that are to be merged
        int n1 = m - l + 1;
        int n2 = r - m;

        /* Create temporary arrays */
        int L[] = new int[n1];
        int R[] = new int[n2];
        int Lk[] = new int[n1];
        int Rk[] = new int[n2];

        /* Copy data to temporary arrays */
        for (int i = 0; i < n1; ++i) {
            L[i] = arrk[l + i];
            Lk[i] = arrv[l + i];
        }
        for (int j = 0; j < n2; ++j) {
            R[j] = arrk[m + 1 + j];
            Rk[j] = arrv[m + 1 + j];
        }

        // Initial indexes of
        // first and second subarrays
        int i = 0, j = 0;

        int k = l;

        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arrk[k] = L[i];
                arrv[k] = Lk[i];

                i++;
            }
            else {
                arrk[k] = R[j];
                arrv[k] = Rk[j];

                j++;
            }

            k++;
        }

        /* Copy remaining elements of L[] if any */
        while (i < n1) {
            arrk[k] = L[i];
            arrv[k] = Lk[i];

            i++;
            k++;
        }

        /* Copy remaining elements of R[] if any */
        while (j < n2) {
            arrk[k] = R[j];
            arrv[k] = Rk[j];

            j++;
            k++;
        }
    }

    // Function that sorts arr[l..r] using merge()
    void sort(int arrk[], int l, int r, int arrv[])
    {
        if (l < r) {
            // Find the middle point
            int m = (l + r) / 2;

            // Sort first and second halves
            sort(arrk, l, m, arrv);
            sort(arrk, m + 1, r, arrv);

            // Merge the sorted halves
            merge(arrk, l, m, r, arrv);
        }
    }

    /* Function to print array of size n */
    static void printArray(int arr[])
    {
        int n = arr.length;

        for (int i = 0; i < n; ++i)

            System.out.print(arr[i] + " ");

        System.out.println();
    }

    // Driver code
    public static void main(String[] args)
                    throws java.lang.Exception
    {

        // Size of Array
        int n = 10;

        // array of keys
        int[] arrk = { 5, 1, 4, 6, 8, 0,
                                    6, 6, 5, 5 };

        // array of values
        int[] arrv = { 0, 1, 2, 3, 4, 5,
                                    6, 7, 8, 9 };

        Solution ob = new Solution();

        ob.sort(arrk, 0, n - 1, arrv);

        System.out.print("Keys: ");
        printArray(arrk);

        System.out.println();

        System.out.print("Values: ");
        printArray(arrv);
    }
}
```

## 蟒蛇 3

```
# Python program to Store duplicate
# keys-values pair and sort the
# key-value pair by key

# Merges two subarrays of arr[].
# First subarray is arr[l..m]
# Second subarray is arr[m+1..r]
def merge(arrk, l, m, r, arrv):

    # Sizes of two subarrays
    # that are to be merged
    n1 = m - l + 1;
    n2 = r - m;

    #Create temporary arrays
    L = [0]*n1
    R = [0]*n2
    Lk = [0]*n1
    Rk = [0]*n2

    #Copy data to temporary arrays
    for i in range(n1):
        L[i] = arrk[l + i];
        Lk[i] = arrv[l + i];

    for j in range(n2):
        R[j] = arrk[m + 1 + j];
        Rk[j] = arrv[m + 1 + j];

    # Initial indexes of
    # first and second subarrays   
    a = 0
    b = 0   
    k = l

    while(a < n1 and b < n2):
        if (L[a] <= R[b]):       
            arrk[k] = L[a];
            arrv[k] = Lk[a];

            a += 1;

        else:

            arrk[k] = R[b];
            arrv[k] = Rk[b];
            b += 1;       
        k += 1;

    # Copy remaining elements of L[] if any
    while (a < n1):
        arrk[k] = L[a];
        arrv[k] = Lk[a];

        a += 1;
        k += 1;

    # Copy remaining elements of R[] if any   
    while (b < n2):
        arrk[k] = R[b];
        arrv[k] = Rk[b];

        b += 1;
        k += 1;

# Function that sorts arr[l..r] using merge()
def sort(arrk, l, r, arrv):
    if (l < r):

        # Find the middle point
        m = (l + r) // 2;

        # Sort first and second halves
        sort(arrk, l, m, arrv);
        sort(arrk, m + 1, r, arrv);

        # Merge the sorted halves
        merge(arrk, l, m, r, arrv);

# Function to print array of size n       
def printArray(arr):

    n = len(arr)

    for i in range(n):
        print(arr[i], end = " ")

    print()

#  Driver code

# Size of Array
n = 10;

# array of keys
arrk = [5, 1, 4, 6, 8,
                   0, 6, 6, 5, 5 ]

# array of values                  
arrv = [0, 1, 2, 3, 4,
                   5, 6, 7, 8, 9]

sort(arrk, 0, n - 1, arrv)
print("Keys: ", end = '')
printArray(arrk);
print()
print("Values: ", end = "")
printArray(arrv);

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to Store duplicate
// keys-values pair and sort the
// key-value pair by key
using System;

class Solution{

// Merges two subarrays of arr[].
// First subarray is arr[l..m]
// Second subarray is arr[m+1..r]
void merge(int []arrk, int l, int m,
           int r, int []arrv)
{

    // Sizes of two subarrays
    // that are to be merged
    int n1 = m - l + 1;
    int n2 = r - m;

    // Create temporary arrays
    int []L = new int[n1];
    int []R = new int[n2];
    int []Lk = new int[n1];
    int []Rk = new int[n2];

    // Copy data to temporary arrays
    for(int i = 0; i < n1; ++i)
    {
        L[i] = arrk[l + i];
        Lk[i] = arrv[l + i];
    }
    for(int j = 0; j < n2; ++j)
    {
        R[j] = arrk[m + 1 + j];
        Rk[j] = arrv[m + 1 + j];
    }

    // Initial indexes of
    // first and second subarrays
    int a = 0 , b = 0;

    int k = l;

    while (a < n1 && b < n2)
    {
        if (L[a] <= R[b])
        {
            arrk[k] = L[a];
            arrv[k] = Lk[a];

            a++;
        }
        else
        {
            arrk[k] = R[b];
            arrv[k] = Rk[b];

            b++;
        }
        k++;
    }

    // Copy remaining elements of L[] if any
    while (a < n1)
    {
        arrk[k] = L[a];
        arrv[k] = Lk[a];

        a++;
        k++;
    }

    // Copy remaining elements of R[] if any
    while (b < n2)
    {
        arrk[k] = R[b];
        arrv[k] = Rk[b];

        b++;
        k++;
    }
}

// Function that sorts arr[l..r] using merge()
void sort(int []arrk, int l, int r, int []arrv)
{
    if (l < r)
    {

        // Find the middle point
        int m = (l + r) / 2;

        // Sort first and second halves
        sort(arrk, l, m, arrv);
        sort(arrk, m + 1, r, arrv);

        // Merge the sorted halves
        merge(arrk, l, m, r, arrv);
    }
}

// Function to print array of size n
static void printArray(int []arr)
{
    int n = arr.Length;

    for(int i = 0; i < n; ++i)
        Console.Write(arr[i] + " ");

    Console.WriteLine();
}

// Driver code
public static void Main(string[] args)
{

    // Size of Array
    int n = 10;

    // array of keys
    int[] arrk = { 5, 1, 4, 6, 8,
                   0, 6, 6, 5, 5 };

    // array of values
    int[] arrv = { 0, 1, 2, 3, 4,
                   5, 6, 7, 8, 9 };

    Solution ob = new Solution();

    ob.sort(arrk, 0, n - 1, arrv);

    Console.Write("Keys: ");
    printArray(arrk);

    Console.WriteLine();

    Console.Write("Values: ");
    printArray(arrv);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program to Store duplicate
// keys-values pair and sort the
// key-value pair by key

// Merges two subarrays of arr[].
// First subarray is arr[l..m]
// Second subarray is arr[m+1..r]
function merge(arrk, l, m, r, arrv)
{
    // Sizes of two subarrays
    // that are to be merged
    var n1 = m - l + 1;
    var n2 = r - m;

    /* Create temporary arrays */
    var L = Array(n1).fill(0);
    var R = Array(n2).fill(0);
    var Lk = Array(n1).fill(0);
    var Rk = Array(n2).fill(0);

    /* Copy data to temporary arrays */
    for (var i = 0; i < n1; ++i) {
        L[i] = arrk[l + i];
        Lk[i] = arrv[l + i];
    }
    for (var j = 0; j < n2; ++j) {
        R[j] = arrk[m + 1 + j];
        Rk[j] = arrv[m + 1 + j];
    }
    // Initial indexes of
    // first and second subarrays
    var i = 0, j = 0;
    var k = l;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arrk[k] = L[i];
            arrv[k] = Lk[i];
            i++;
        }
        else {
            arrk[k] = R[j];
            arrv[k] = Rk[j];
            j++;
        }
        k++;
    }
    /* Copy remaining elements of L[] if any */
    while (i < n1) {
        arrk[k] = L[i];
        arrv[k] = Lk[i];
        i++;
        k++;
    }
    /* Copy remaining elements of R[] if any */
    while (j < n2) {
        arrk[k] = R[j];
        arrv[k] = Rk[j];
        j++;
        k++;
    }
}
// Function that sorts arr[l..r] using merge()
function sort(arrk, l, r, arrv)
{
    if (l < r) {
        // Find the middle point
        var m = parseInt((l + r) / 2);
        // Sort first and second halves
        sort(arrk, l, m, arrv);
        sort(arrk, m + 1, r, arrv);
        // Merge the sorted halves
        merge(arrk, l, m, r, arrv);
    }
}
/* Function to print array of size n */
function printArray(arr)
{
    var n = arr.length;
    for (var i = 0; i < n; ++i)
        document.write(arr[i] + " ");
    document.write("<br>");
}
// Driver code

// Size of Array
var n = 10;
// array of keys
var arrk = [ 5, 1, 4, 6, 8, 0, 6, 6, 5, 5 ]
// array of values
var arrv = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
sort(arrk, 0, n - 1, arrv);
document.write("Keys: ");
printArray(arrk);
document.write("<br>");
document.write("Values: ");
printArray(arrv);

</script>
```

**Output:** 

```
Keys: 0 1 4 5 5 5 6 6 6 8 

Values: 5 1 2 0 8 9 3 6 7 4
```

**时间复杂度:** O(N*logN)