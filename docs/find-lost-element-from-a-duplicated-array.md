# 从重复的数组中查找丢失的元素

> 原文： [https://www.geeksforgeeks.org/find-lost-element-from-a-duplicated-array/](https://www.geeksforgeeks.org/find-lost-element-from-a-duplicated-array/)

给定两个数组，除了一个元素外，它们彼此重复，也就是说，其中一个元素丢失了，我们需要找到该元素。

**示例**：

```
Input:  arr1[] = {1, 4, 5, 7, 9}
        arr2[] = {4, 5, 7, 9}
Output: 1
1 is missing from second array.

Input: arr1[] = {2, 3, 4, 5}
       arr2[] = {2, 3, 4, 5, 6}
Output: 6
6 is missing from first array.
```



一种**简单解决方案**是遍历数组并逐元素检查元素，并在发现不匹配项时标记缺少的元素，但是此解决方案需要整个数组长度的线性时间。

另一种**有效解决方案**基于[二分搜索](http://geeksquiz.com/binary-search/)方法。 算法步骤如下：

1.  在更大的数组中开始二分搜索，并获得`(lo + hi) / 2`的中间值。

2.  如果两个数组的值相同，则缺少的元素必须在右侧，因此将`lo`设置为`mid`。

3.  否则将`hi`设置为`mid`，因为如果`mid`元素不相等，则缺少的元素必须位于较大数组的左侧。

4.  对于单元素和零元素数组，特殊情况将分别处理，单元素本身将是缺少的元素。

    如果第一个元素本身不相等，则该元素将成为丢失的元素。

以下是上述步骤的实现：

## C++ 

```cpp

// C++ program to find missing element from same 
// arrays (except one missing element) 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find missing element based on binary 
// search approach.  arr1[] is of larger size and 
// N is size of it.  arr1[] and arr2[] are assumed 
// to be in same order. 
int findMissingUtil(int arr1[], int arr2[], int N) 
{ 
    // special case, for only element which is 
    // missing in second array 
    if (N == 1) 
        return arr1[0]; 

    // special case, for first element missing 
    if (arr1[0] != arr2[0]) 
        return arr1[0]; 

    // Initialize current corner points 
    int lo = 0,  hi = N - 1; 

    // loop until lo < hi 
    while (lo < hi) 
    { 
        int mid = (lo + hi) / 2; 

        // If element at mid indices are equal 
        // then go to right subarray 
        if (arr1[mid] == arr2[mid]) 
            lo = mid; 
        else
            hi = mid; 

        // if lo, hi becomes contiguous,  break 
        if (lo == hi - 1) 
            break; 
    } 

    // missing element will be at hi index of 
    // bigger array 
    return arr1[hi]; 
} 

// This function mainly does basic error checking 
// and calls findMissingUtil 
void findMissing(int arr1[], int arr2[], int M, int N) 
{ 
    if (N == M-1) 
        cout << "Missing Element is "
        << findMissingUtil(arr1, arr2, M) << endl; 
    else if (M == N-1) 
        cout << "Missing Element is "
        << findMissingUtil(arr2, arr1, N) << endl; 
    else
        cout << "Invalid Input"; 
} 

// Driver Code 
int main() 
{ 
    int arr1[] = {1, 4, 5, 7, 9}; 
    int arr2[] = {4, 5, 7, 9}; 

    int M = sizeof(arr1) / sizeof(int); 
    int N = sizeof(arr2) / sizeof(int); 

    findMissing(arr1, arr2, M, N); 

    return 0; 
} 

```

## Java

```java
// Java program to find missing element 
// from same arrays 
// (except one missing element) 
  
import java.io.*; 
class MissingNumber { 
  
    /* Function to find missing element based 
     on binary search approach. arr1[] is of 
     larger size and N is size of it.arr1[] and  
     arr2[] are assumed to be in same order. */
    int findMissingUtil(int arr1[], int arr2[], 
                        int N) 
    { 
        // special case, for only element 
        // which is missing in second array 
        if (N == 1) 
            return arr1[0]; 
  
        // special case, for first 
        // element missing 
        if (arr1[0] != arr2[0]) 
            return arr1[0]; 
  
        // Initialize current corner points 
        int lo = 0, hi = N - 1; 
  
        // loop until lo < hi 
        while (lo < hi) { 
            int mid = (lo + hi) / 2; 
  
            // If element at mid indices are 
            // equal then go to right subarray 
            if (arr1[mid] == arr2[mid]) 
                lo = mid; 
            else
                hi = mid; 
  
            // if lo, hi becomes  
            // contiguous, break 
            if (lo == hi - 1) 
                break; 
        } 
  
        // missing element will be at hi  
        // index of bigger array 
        return arr1[hi]; 
    } 
  
    // This function mainly does basic error 
    // checking and calls findMissingUtil 
    void findMissing(int arr1[], int arr2[],  
                              int M, int N) 
    { 
        if (N == M - 1) 
        System.out.println("Missing Element is "
        + findMissingUtil(arr1, arr2, M) + "\n"); 
        else if (M == N - 1) 
        System.out.println("Missing Element is "
        + findMissingUtil(arr2, arr1, N) + "\n"); 
        else
        System.out.println("Invalid Input"); 
    } 
  
    // Driver Code 
    public static void main(String args[]) 
    { 
        MissingNumber obj = new MissingNumber(); 
        int arr1[] = { 1, 4, 5, 7, 9 }; 
        int arr2[] = { 4, 5, 7, 9 }; 
        int M = arr1.length; 
        int N = arr2.length; 
        obj.findMissing(arr1, arr2, M, N); 
    } 
} 
  
// This code is contributed by Anshika Goyal.
```

## Python3

```py
# Python3 program to find missing 
# element from same arrays  
# (except one missing element) 
  
# Function to find missing element based 
# on binary search approach. arr1[] is  
# of larger size and N is size of it.  
# arr1[] and arr2[] are assumed 
# to be in same order. 
def findMissingUtil(arr1, arr2, N): 
  
    # special case, for only element  
    # which is missing in second array 
    if N == 1: 
        return arr1[0]; 
  
    # special case, for first 
    # element missing 
    if arr1[0] != arr2[0]: 
        return arr1[0] 
  
    # Initialize current corner points 
    lo = 0
    hi = N - 1
      
    # loop until lo < hi 
    while (lo < hi): 
      
        mid = (lo + hi) / 2
  
        # If element at mid indices 
        # are equal then go to  
        # right subarray 
        if arr1[mid] == arr2[mid]: 
            lo = mid 
        else: 
            hi = mid 
  
        # if lo, hi becomes  
        # contiguous, break 
        if lo == hi - 1: 
            break
      
    # missing element will be at 
    # hi index of bigger array 
    return arr1[hi] 
  
# This function mainly does basic 
# error checking and calls  
# findMissingUtil 
def findMissing(arr1, arr2, M, N): 
  
    if N == M-1: 
        print("Missing Element is", 
            findMissingUtil(arr1, arr2, M)) 
    elif M == N-1: 
        print("Missing Element is", 
            findMissingUtil(arr2, arr1, N)) 
    else: 
        print("Invalid Input") 
  
# Driver Code 
arr1 = [1, 4, 5, 7, 9] 
arr2 = [4, 5, 7, 9] 
M = len(arr1) 
N = len(arr2) 
findMissing(arr1, arr2, M, N) 
  
# This code is contributed by Smitha Dinesh Semwal
```

## C#

```cs
// C# program to find missing element from  
// same arrays (except one missing element) 
using System; 
  
class GFG { 
  
    /* Function to find missing element based 
    on binary search approach. arr1[] is of 
    larger size and N is size of it.arr1[] and  
    arr2[] are assumed to be in same order. */
    static int findMissingUtil(int []arr1,  
                            int []arr2, int N) 
    { 
          
        // special case, for only element 
        // which is missing in second array 
        if (N == 1) 
            return arr1[0]; 
  
        // special case, for first 
        // element missing 
        if (arr1[0] != arr2[0]) 
            return arr1[0]; 
  
        // Initialize current corner points 
        int lo = 0, hi = N - 1; 
  
        // loop until lo < hi 
        while (lo < hi) { 
            int mid = (lo + hi) / 2; 
  
            // If element at mid indices are 
            // equal then go to right subarray 
            if (arr1[mid] == arr2[mid]) 
                lo = mid; 
            else
                hi = mid; 
  
            // if lo, hi becomes  
            // contiguous, break 
            if (lo == hi - 1) 
                break; 
        } 
  
        // missing element will be at hi  
        // index of bigger array 
        return arr1[hi]; 
    } 
  
    // This function mainly does basic error 
    // checking and calls findMissingUtil 
    static void findMissing(int []arr1, int []arr2,  
                            int M, int N) 
    { 
        if (N == M - 1) 
            Console.WriteLine("Missing Element is "
            + findMissingUtil(arr1, arr2, M) + "\n"); 
        else if (M == N - 1) 
            Console.WriteLine("Missing Element is "
            + findMissingUtil(arr2, arr1, N) + "\n"); 
        else
            Console.WriteLine("Invalid Input"); 
    } 
  
    // Driver Code 
    public static void Main() 
    { 
        int []arr1 = { 1, 4, 5, 7, 9 }; 
        int []arr2 = { 4, 5, 7, 9 }; 
        int M = arr1.Length; 
        int N = arr2.Length; 
        findMissing(arr1, arr2, M, N); 
    } 
} 
  
// This code is contributed by anuj_67.
```

## PHP

```php
<?php 
// PHP program to find missing  
// element from same arrays  
// (except one missing element) 
  
// Function to find missing  
// element based on binary 
// search approach. arr1[]  
// is of larger size and 
// N is size of it. arr1[] 
// and arr2[] are assumed 
// to be in same order. 
function findMissingUtil($arr1, $arr2, $N) 
{ 
      
    // special case, for only  
    // element which is 
    // missing in second array 
    if ($N == 1) 
        return $arr1[0]; 
  
    // special case, for first 
    // element missing 
    if ($arr1[0] != $arr2[0]) 
        return $arr1[0]; 
  
    // Initialize current  
    // corner points 
    $lo = 0; 
    $hi = $N - 1; 
  
    // loop until lo < hi 
    while ($lo < $hi) 
    { 
        $mid = ($lo + $hi) / 2; 
  
        // If element at mid indices are  
        // equal then go to right subarray 
        if ($arr1[$mid] == $arr2[$mid]) 
            $lo = $mid; 
        else
            $hi = $mid; 
  
        // if lo, hi becomes  
        // contiguous, break 
        if ($lo == $hi - 1) 
            break; 
    } 
  
    // missing element will be  
    // at hi index of 
    // bigger array 
    return $arr1[$hi]; 
} 
  
// This function mainly  
// does basic error checking 
// and calls findMissingUtil 
function findMissing($arr1, $arr2,  
                           $M, $N) 
{ 
    if ($N == $M - 1) 
        echo "Missing Element is "
             , findMissingUtil($arr1,  
                         $arr2, $M) ; 
    else if ($M == $N - 1) 
        echo "Missing Element is "
             , findMissingUtil($arr2,  
                           $arr1, $N); 
    else
        echo "Invalid Input"; 
} 
  
    // Driver Code 
    $arr1 = array(1, 4, 5, 7, 9); 
    $arr2 = array(4, 5, 7, 9); 
    $M = count($arr1); 
    $N = count($arr2); 
    findMissing($arr1, $arr2, $M, $N); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
Missing Element is 1
```
