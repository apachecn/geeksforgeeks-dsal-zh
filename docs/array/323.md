# 排序数组中的最后一个重复元素

> 原文： [https://www.geeksforgeeks.org/last-duplicate-element-sorted-array/](https://www.geeksforgeeks.org/last-duplicate-element-sorted-array/)

我们有一个包含重复元素的排序数组，我们必须找到最后一个重复元素的索引并打印它的索引，还要打印重复元素。 如果找不到这样的元素，则打印一条消息。

示例：

```
Input : arr[] = {1, 5, 5, 6, 6, 7}
Output :
Last index: 4
Last duplicate item: 6

Input : arr[] = {1, 2, 3, 4, 5}
Output : No duplicate found

```



我们只需以相反的顺序遍历数组，然后比较当前元素和上一个元素。 如果找到匹配项，则打印索引和重复元素。 由于这是排序数组，它将是最后一个重复项。 如果找不到此类元素，我们将为其打印消息。

```
1- for i = n-1 to 0
     if (arr[i] == arr[i-1])
        Print current element and its index.
        Return
2- If no such element found print a message 
   of no duplicate found.

```

## C++ 

```cpp

// To print last duplicate element and its 
// index in a sorted array 
#include <bits/stdc++.h> 

void dupLastIndex(int arr[], int n) { 

  // if array is null or size is less  
  // than equal to 0 return 
  if (arr == NULL || n <= 0)  
    return; 

  // compare elements and return last 
  // duplicate and its index 
  for (int i = n - 1; i > 0; i--) { 
    if (arr[i] == arr[i - 1]) { 
      printf("Last index: %d\nLast " 
            "duplicate item: %d\n", i, arr[i]); 
      return; 
    } 
  } 

  // If we reach here, then no duplicate 
  // found. 
  printf("no duplicate found"); 
} 

int main() { 
  int arr[] = {1, 5, 5, 6, 6, 7, 9}; 
  int n = sizeof(arr) / sizeof(int); 
  dupLastIndex(arr, n); 
  return 0; 
} 

```

## Java

```java

// Java code to print last duplicate element  
// and its index in a sorted array 
import java.io.*; 

class GFG 
{ 
    static void dupLastIndex(int arr[], int n)  
    { 
        // if array is null or size is less  
        // than equal to 0 return 
        if (arr == null || n <= 0)  
            return; 

        // compare elements and return last 
        // duplicate and its index 
        for (int i = n - 1; i > 0; i--)  
        { 
            if (arr[i] == arr[i - 1])  
            { 
            System.out.println("Last index:" + i); 
            System.out.println("Last duplicate item: "
                              + arr[i]); 
            return; 
            } 
        } 

        // If we reach here, then no duplicate 
        // found. 
        System.out.print("no duplicate found"); 
    } 

    // Driver code  
    public static void main (String[] args)  
    { 
        int arr[] = {1, 5, 5, 6, 6, 7, 9}; 
        int n = arr.length; 
        dupLastIndex(arr, n); 

    } 
} 

// This code is contributed by vt_m 

```

## Python3

```py

# Python3 code to print last duplicate  
# element and its index in a sorted array 

def dupLastIndex(arr, n):  

    # if array is null or size is less  
    # than equal to 0 return 
    if (arr == None or n <= 0):  
        return

    # compare elements and return last 
    # duplicate and its index 
    for i in range(n - 1, 0, -1):  

        if (arr[i] == arr[i - 1]):  
            print("Last index:", i, "\nLast", 
                     "duplicate item:",arr[i]) 
            return

    # If we reach here, then no duplicate 
    # found. 
    print("no duplicate found") 

arr = [1, 5, 5, 6, 6, 7, 9] 
n = len(arr)  
dupLastIndex(arr, n) 

# This code is contributed by  
# Smitha Dinesh Semwal 

```

## C# 

```cs

// C# code to print last duplicate element  
// and its index in a sorted array 
using System; 

class GFG { 

    static void dupLastIndex(int []arr, int n)  
    { 

        // if array is null or size is less  
        // than equal to 0 return 
        if (arr == null || n <= 0)  
            return; 

        // compare elements and return last 
        // duplicate and its index 
        for (int i = n - 1; i > 0; i--)  
        { 
            if (arr[i] == arr[i - 1])  
            { 
                Console.WriteLine("Last index:" + i); 
                Console.WriteLine("Last duplicate item: "
                                + arr[i]); 
                return; 
            } 
        } 

        // If we reach here, then no duplicate 
        // found. 
        Console.WriteLine("no duplicate found"); 
    } 

    // Driver code  
    public static void Main ()  
    { 
        int []arr = {1, 5, 5, 6, 6, 7, 9}; 
        int n = arr.Length; 

        dupLastIndex(arr, n); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP program to print last  
// duplicate element and its 
// index in a sorted array 

function dupLastIndex($arr, $n) 
{ 

    // if array is null or size is less  
    // than equal to 0 return 
    if ($arr == null or $n <= 0)  
        return; 

    // compare elements and return last 
    // duplicate and its index 
    for ( $i = $n - 1; $i > 0; $i--) 
    { 
        if ($arr[$i] == $arr[$i - 1]) 
        { 
            echo "Last index:", $i , "\n"; 
            echo "Last duplicate item:", $arr[$i]; 
            return; 
    } 
} 

    // If we reach here, then 
    // no duplicate found. 
    echo "no duplicate found"; 
} 

// Driver Code 
$arr = array(1, 5, 5, 6, 6, 7, 9); 
$n = count($arr); 
dupLastIndex($arr, $n); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
Last index: 4
Last duplicate item: 6

```



* * *

* * *



