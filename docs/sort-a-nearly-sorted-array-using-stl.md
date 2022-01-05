# 使用 STL

对接近排序的数组进行排序

> 原文:[https://www . geesforgeks . org/sort-a-近排序-array-using-stl/](https://www.geeksforgeeks.org/sort-a-nearly-sorted-array-using-stl/)

给定一个由 n 个元素组成的数组，其中每个元素离它的目标位置最多 k，设计一个在 O(n log k)时间内排序的算法。例如，让我们考虑 k 是 2，排序数组中索引 7 处的元素可以位于给定数组中的索引 5、6、7、8、9 处。可以假设 k < n。

**例:**

```
Input: arr[] = {6, 5, 3, 2, 8, 10, 9}, 
       k = 3
Output: arr[] = {2, 3, 5, 6, 8, 9, 10}

Input: arr[] = {10, 9, 8, 7, 4, 70, 60, 50}, 
       k = 4
Output: arr[] = {4, 7, 8, 9, 10, 50, 60, 70}
```

**<u>简单方法:</u>** 基本解决方案是使用任何标准排序算法对数组进行排序。

## CPP14

```
// A STL based C++ program to
// sort a nearly sorted array.
#include <bits/stdc++.h>
using namespace std;

// Given an array of size n,
// where every element
// is k away from its target
// position, sorts the
// array in O(n Log n) time.
int sortK(int arr[], int n, int k)
{
    // Sort the array using
    // inbuilt function
    sort(arr, arr + n);
}

// An utility function to print
// array elements
void printArray(
    int arr[], int size)
{
    for (int i = 0; i < size; i++)
        cout << arr[i] << " ";
    cout << endl;
}

// Driver program to test
// above functions
int main()
{
    int k = 3;
    int arr[] = { 2, 6, 3, 12, 56, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    sortK(arr, n, k);

    cout << "Following is sorted array\n";
    printArray(arr, n);

    return 0;
}
```

## Java

```
// A STL based Java program to
// sort a nearly sorted array.
import java.util.*;
public class GFG
{

  // Given an array of size n,
  // where every element
  // is k away from its target
  // position, sorts the
  // array in O(n Log n) time.
  static void sortK(int[] arr, int n, int k)
  {

    // Sort the array using
    // inbuilt function
    Arrays.sort(arr);
  }

  // An utility function to print
  // array elements
  static void printArray(
    int[] arr, int size)
  {
    for (int i = 0; i < size; i++)
      System.out.print(arr[i] + " ");
    System.out.println();
  }

  // Driver code
  public static void main(String[] args)
  {
    int k = 3;
    int[] arr = { 2, 6, 3, 12, 56, 8 };
    int n = arr.length;
    sortK(arr, n, k);

    System.out.println("Following is sorted array");
    printArray(arr, n);
  }
}

// This code is contributed by divyesh072019.
```

## python 3

```
# A STL based Java program to
# sort a nearly sorted array.

# Given an array of size n,
# where every element
# is k away from its target
# position, sorts the
# array in O(n Log n) time.
def sortK(arr, n, k):

    # Sort the array using
    # inbuilt function
    arr.sort()

# An utility function to print
# array elements
def printArray(arr, size):
    for i in range(size):
        print(arr[i], end = " ")
    print()

# Driver code
k = 3
arr = [ 2, 6, 3, 12, 56, 8]
n = len(arr)
sortK(arr, n, k)
print("Following is sorted array")
printArray(arr, n)

# This code is contributed by avanitrachhadiya2155
```

## c#

```
// A STL based C# program to
// sort a nearly sorted array.
using System;
class GFG
{

    // Given an array of size n,
    // where every element
    // is k away from its target
    // position, sorts the
    // array in O(n Log n) time.
    static void sortK(int[] arr, int n, int k)
    {

        // Sort the array using
        // inbuilt function
        Array.Sort(arr);
    }

    // An utility function to print
    // array elements
    static void printArray(
        int[] arr, int size)
    {
        for (int i = 0; i < size; i++)
            Console.Write(arr[i] + " ");
        Console.WriteLine();
    }

  // Driver code
  static void Main()
  {
    int k = 3;
    int[] arr = { 2, 6, 3, 12, 56, 8 };
    int n = arr.Length;
    sortK(arr, n, k);

    Console.WriteLine("Following is sorted array");
    printArray(arr, n);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## Javascript

```
<script>
// A STL based Javascript program to
// sort a nearly sorted array.

// Given an array of size n,
// where every element
// is k away from its target
// position, sorts the
// array in O(n Log n) time.
function sortK(arr,n,k)
{
    // Sort the array using
    // inbuilt function
    (arr).sort(function(a,b){return a-b;});
}

// An utility function to print
// array elements
function printArray(arr,size)
{
    for (let i = 0; i < size; i++)
      document.write(arr[i] + " ");
    document.write("<br>");
}

// Driver code
let k = 3;
let arr=[ 2, 6, 3, 12, 56, 8 ];
let n = arr.length;
sortK(arr, n, k);
document.write("Following is sorted array<br>");
printArray(arr, n);

// This code is contributed by ab2127
</script>
```

**输出:**

```
Following is sorted arrayn2 3 6 8 12 56
```