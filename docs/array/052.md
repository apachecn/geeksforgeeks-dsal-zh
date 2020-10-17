# 最长的双子序列 | DP-15

> 原文： [https://www.geeksforgeeks.org/dynamic-programming-set-15-longest-bitonic-subsequence/](https://www.geeksforgeeks.org/dynamic-programming-set-15-longest-bitonic-subsequence/)

给定包含`n`个正整数的数组`arr[0…n-1]`，如果`arr[]`的[子序列](http://en.wikipedia.org/wiki/Subsequence)先增大然后减小，则称为 Bitonic。 编写一个将数组作为参数并返回最长双子序列的长度的函数。

按升序排序的序列被视为 Bitonic，而其递减部分为空。 类似地，降序序列被视为 Bitonic，而升序部分为空。

**示例**：

```
Input arr[] = {1, 11, 2, 10, 4, 5, 2, 1};
Output: 6 (A Longest Bitonic Subsequence of length 6 is 1, 2, 10, 4, 2, 1)

Input arr[] = {12, 11, 40, 5, 3, 1}
Output: 5 (A Longest Bitonic Subsequence of length 5 is 12, 11, 5, 3, 1)

Input arr[] = {80, 60, 30, 40, 20, 10}
Output: 5 (A Longest Bitonic Subsequence of length 5 is 80, 60, 30, 20, 10)

```

资料来源：Microsoft 面试问题。



**解决方案**：

此问题是标准[最长子序列（LIS）问题](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的变体。 令输入数组为长度为`n`的`arr[]`。 我们需要使用 [LIS 问题](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的动态规划解决方案构造两个数组`lis[]`和`lds[]`。 `lis[i]`存储以`arr[i]`结尾的最长增加子序列的长度。 `lds[i]`存储从`arr[i]`开始的最长递减子序列的长度。 最后，我们需要返回`lis[i] + lds[i] – 1`的最大值，其中`i`从 0 到`n-1`。

以下是上述动态规划解决方案的实现。

## C++ 

```cpp

/* Dynamic Programming implementation of longest bitonic subsequence problem */
#include<stdio.h> 
#include<stdlib.h> 

/* lbs() returns the length of the Longest Bitonic Subsequence in 
    arr[] of size n. The function mainly creates two temporary arrays 
    lis[] and lds[] and returns the maximum lis[i] + lds[i] - 1\. 

    lis[i] ==> Longest Increasing subsequence ending with arr[i] 
    lds[i] ==> Longest decreasing subsequence starting with arr[i] 
*/
int lbs( int arr[], int n ) 
{ 
   int i, j; 

   /* Allocate memory for LIS[] and initialize LIS values as 1 for 
      all indexes */
   int *lis = new int[n]; 
   for (i = 0; i < n; i++) 
      lis[i] = 1; 

   /* Compute LIS values from left to right */
   for (i = 1; i < n; i++) 
      for (j = 0; j < i; j++) 
         if (arr[i] > arr[j] && lis[i] < lis[j] + 1) 
            lis[i] = lis[j] + 1; 

   /* Allocate memory for lds and initialize LDS values for 
      all indexes */
   int *lds = new int [n]; 
   for (i = 0; i < n; i++) 
      lds[i] = 1; 

   /* Compute LDS values from right to left */
   for (i = n-2; i >= 0; i--) 
      for (j = n-1; j > i; j--) 
         if (arr[i] > arr[j] && lds[i] < lds[j] + 1) 
            lds[i] = lds[j] + 1; 

   /* Return the maximum value of lis[i] + lds[i] - 1*/
   int max = lis[0] + lds[0] - 1; 
   for (i = 1; i < n; i++) 
     if (lis[i] + lds[i] - 1 > max) 
         max = lis[i] + lds[i] - 1; 
   return max; 
} 

/* Driver program to test above function */
int main() 
{ 
  int arr[] = {0, 8, 4, 12, 2, 10, 6, 14, 1, 9, 5, 
              13, 3, 11, 7, 15}; 
  int n = sizeof(arr)/sizeof(arr[0]); 
  printf("Length of LBS is %d\n", lbs( arr, n ) ); 
  return 0; 
} 

```

## Java

```java
/* Dynamic Programming implementation in Java for longest bitonic 
   subsequence problem */
import java.util.*; 
import java.lang.*; 
import java.io.*; 
  
class LBS 
{ 
    /* lbs() returns the length of the Longest Bitonic Subsequence in 
    arr[] of size n. The function mainly creates two temporary arrays 
    lis[] and lds[] and returns the maximum lis[i] + lds[i] - 1. 
  
    lis[i] ==> Longest Increasing subsequence ending with arr[i] 
    lds[i] ==> Longest decreasing subsequence starting with arr[i] 
    */
    static int lbs( int arr[], int n ) 
    { 
        int i, j; 
  
        /* Allocate memory for LIS[] and initialize LIS values as 1 for 
            all indexes */
        int[] lis = new int[n]; 
        for (i = 0; i < n; i++) 
            lis[i] = 1; 
  
        /* Compute LIS values from left to right */
        for (i = 1; i < n; i++) 
            for (j = 0; j < i; j++) 
                if (arr[i] > arr[j] && lis[i] < lis[j] + 1) 
                    lis[i] = lis[j] + 1; 
  
        /* Allocate memory for lds and initialize LDS values for 
            all indexes */
        int[] lds = new int [n]; 
        for (i = 0; i < n; i++) 
            lds[i] = 1; 
  
        /* Compute LDS values from right to left */
        for (i = n-2; i >= 0; i--) 
            for (j = n-1; j > i; j--) 
                if (arr[i] > arr[j] && lds[i] < lds[j] + 1) 
                    lds[i] = lds[j] + 1; 
  
  
        /* Return the maximum value of lis[i] + lds[i] - 1*/
        int max = lis[0] + lds[0] - 1; 
        for (i = 1; i < n; i++) 
            if (lis[i] + lds[i] - 1 > max) 
                max = lis[i] + lds[i] - 1; 
  
        return max; 
    } 
  
    public static void main (String[] args) 
    { 
        int arr[] = {0, 8, 4, 12, 2, 10, 6, 14, 1, 9, 5, 
                    13, 3, 11, 7, 15}; 
        int n = arr.length; 
        System.out.println("Length of LBS is "+ lbs( arr, n )); 
    } 
} 
```

## Python

```py
# Dynamic Programming implementation of longest bitonic subsequence problem 
""" 
lbs() returns the length of the Longest Bitonic Subsequence in 
arr[] of size n. The function mainly creates two temporary arrays 
lis[] and lds[] and returns the maximum lis[i] + lds[i] - 1. 
  
lis[i] ==> Longest Increasing subsequence ending with arr[i] 
lds[i] ==> Longest decreasing subsequence starting with arr[i] 
"""
  
def lbs(arr): 
    n = len(arr) 
  
  
    # allocate memory for LIS[] and initialize LIS values as 1 
    # for all indexes 
    lis = [1 for i in range(n+1)] 
  
    # Compute LIS values from left to right 
    for i in range(1 , n): 
        for j in range(0 , i): 
            if ((arr[i] > arr[j]) and (lis[i] < lis[j] +1)): 
                lis[i] = lis[j] + 1
  
    # allocate memory for LDS and initialize LDS values for 
    # all indexes 
    lds = [1 for i in range(n+1)] 
      
    # Compute LDS values from right to left 
    for i in reversed(range(n-1)): #loop from n-2 downto 0 
        for j in reversed(range(i-1 ,n)): #loop from n-1 downto i-1 
            if(arr[i] > arr[j] and lds[i] < lds[j] + 1): 
                lds[i] = lds[j] + 1 
  
  
    # Return the maximum value of (lis[i] + lds[i] - 1) 
    maximum = lis[0] + lds[0] - 1
    for i in range(1 , n): 
        maximum = max((lis[i] + lds[i]-1), maximum) 
      
    return maximum 
  
# Driver program to test the above function 
arr =  [0 , 8 , 4, 12, 2, 10 , 6 , 14 , 1 , 9 , 5 , 13, 
        3, 11 , 7 , 15] 
print "Length of LBS is",lbs(arr) 
  
# This code is contributed by Nikhil Kumar Singh(nickzuck_007) 
```

## C#

```cs
/* Dynamic Programming implementation in  
   C# for longest bitonic subsequence problem */
using System; 
  
class LBS { 
      
    /* lbs() returns the length of the Longest Bitonic Subsequence in 
    arr[] of size n. The function mainly creates two temporary arrays 
    lis[] and lds[] and returns the maximum lis[i] + lds[i] - 1. 
  
    lis[i] ==> Longest Increasing subsequence ending with arr[i] 
    lds[i] ==> Longest decreasing subsequence starting with arr[i] 
    */
    static int lbs(int[] arr, int n) 
    { 
        int i, j; 
  
        /* Allocate memory for LIS[] and initialize  
           LIS values as 1 for all indexes */
        int[] lis = new int[n]; 
        for (i = 0; i < n; i++) 
            lis[i] = 1; 
  
        /* Compute LIS values from left to right */
        for (i = 1; i < n; i++) 
            for (j = 0; j < i; j++) 
                if (arr[i] > arr[j] && lis[i] < lis[j] + 1) 
                    lis[i] = lis[j] + 1; 
  
        /* Allocate memory for lds and initialize LDS values for 
            all indexes */
        int[] lds = new int[n]; 
        for (i = 0; i < n; i++) 
            lds[i] = 1; 
  
        /* Compute LDS values from right to left */
        for (i = n - 2; i >= 0; i--) 
            for (j = n - 1; j > i; j--) 
                if (arr[i] > arr[j] && lds[i] < lds[j] + 1) 
                    lds[i] = lds[j] + 1; 
  
        /* Return the maximum value of lis[i] + lds[i] - 1*/
        int max = lis[0] + lds[0] - 1; 
        for (i = 1; i < n; i++) 
            if (lis[i] + lds[i] - 1 > max) 
                max = lis[i] + lds[i] - 1; 
  
        return max; 
    } 
      
    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 0, 8, 4, 12, 2, 10, 6, 14, 1, 9, 5, 
                                      13, 3, 11, 7, 15 }; 
        int n = arr.Length; 
        Console.WriteLine("Length of LBS is " + lbs(arr, n)); 
    } 
} 
  
// This code is contributed by vt_m. 
```

## PHP

```php
<?php  
// Dynamic Programming implementation 
// of longest bitonic subsequence problem  
  
/* lbs() returns the length of the Longest  
   Bitonic Subsequence in arr[] of size n.  
   The function mainly creates two temporary  
   arrays lis[] and lds[] and returns the  
   maximum lis[i] + lds[i] - 1. 
  
   lis[i] ==> Longest Increasing subsequence 
              ending with arr[i] 
   lds[i] ==> Longest decreasing subsequence  
              starting with arr[i] 
*/
function lbs(&$arr, $n) 
{ 
  
    /* Allocate memory for LIS[] and initialize  
       LIS values as 1 for all indexes */
    $lis = array_fill(0, $n, NULL); 
    for ($i = 0; $i < $n; $i++) 
        $lis[$i] = 1; 
      
    /* Compute LIS values from left to right */
    for ($i = 1; $i < $n; $i++) 
        for ($j = 0; $j < $i; $j++) 
            if ($arr[$i] > $arr[$j] &&  
                $lis[$i] < $lis[$j] + 1) 
                $lis[$i] = $lis[$j] + 1; 
      
    /* Allocate memory for lds and initialize  
       LDS values for all indexes */
    $lds = array_fill(0, $n, NULL); 
    for ($i = 0; $i < $n; $i++) 
        $lds[$i] = 1; 
      
    /* Compute LDS values from right to left */
    for ($i = $n - 2; $i >= 0; $i--) 
        for ($j = $n - 1; $j > $i; $j--) 
            if ($arr[$i] > $arr[$j] &&  
                $lds[$i] < $lds[$j] + 1) 
                $lds[$i] = $lds[$j] + 1; 
      
    /* Return the maximum value of  
       lis[i] + lds[i] - 1*/
    $max = $lis[0] + $lds[0] - 1; 
    for ($i = 1; $i < $n; $i++) 
        if ($lis[$i] + $lds[$i] - 1 > $max) 
            $max = $lis[$i] + $lds[$i] - 1; 
    return $max; 
} 
  
// Driver Code 
$arr = array(0, 8, 4, 12, 2, 10, 6, 14,  
             1, 9, 5, 13, 3, 11, 7, 15); 
$n = sizeof($arr); 
echo "Length of LBS is " . lbs( $arr, $n ); 
  
// This code is contributed by ita_c 
?> 
```

输出：

```
Length of LBS is 7
```

时间复杂度：`O(n ^ 2)`。

辅助空间：`O(n)`。