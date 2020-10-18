# 在旋转排序后的数组中找到旋转计数

> 原文： [https://www.geeksforgeeks.org/find-rotation-count-rotated-sorted-array/](https://www.geeksforgeeks.org/find-rotation-count-rotated-sorted-array/)

考虑以递增顺序排序的一组不同数字。 数组（顺时针）旋转了`k`次。 给定这样一个数组，找到`k`的值。

**示例**：

```
Input : arr[] = {15, 18, 2, 3, 6, 12}
Output: 2
Explanation : Initial array must be {2, 3,
6, 12, 15, 18}. We get the given array after 
rotating the initial array twice.

Input : arr[] = {7, 9, 11, 12, 5}
Output: 4

Input: arr[] = {7, 9, 11, 12, 15};
Output: 0

```



**方法 1（使用[线性搜索](http://quiz.geeksforgeeks.org/linear-search/)）**：

如果仔细研究示例，我们会发现转数等于最小元素的索引。 一个简单的线性解决方案是找到最小元素并返回其索引。 以下是该想法的 C++ 实现。

## C++ 

```cpp

// C++ program to find number of rotations 
// in a sorted and rotated array. 
#include<bits/stdc++.h> 
using namespace std; 

// Returns count of rotations for an array which 
// is first sorted in ascending order, then rotated 
int countRotations(int arr[], int n) 
{ 
    // We basically find index of minimum 
    // element 
    int min = arr[0], min_index; 
    for (int i=0; i<n; i++) 
    { 
        if (min > arr[i]) 
        { 
            min = arr[i]; 
            min_index = i; 
        } 
    } 
    return min_index; 
} 

// Driver code 
int main() 
{ 
    int arr[] = {15, 18, 2, 3, 6, 12}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << countRotations(arr, n); 
    return 0; 
} 

```

## Java

```java
// Java program to find number of  
// rotations in a sorted and rotated 
// array. 
import java.util.*; 
import java.lang.*; 
import java.io.*; 
  
class LinearSearch 
{ 
    // Returns count of rotations for an  
    // array which is first sorted in  
    // ascending order, then rotated 
    static int countRotations(int arr[], int n) 
    { 
        // We basically find index of minimum 
        // element 
        int min = arr[0], min_index = -1; 
        for (int i = 0; i < n; i++) 
        { 
            if (min > arr[i]) 
            { 
                min = arr[i]; 
                min_index = i; 
            } 
        }  
        return min_index; 
    } 
  
    // Driver program to test above functions 
    public static void main (String[] args)  
    { 
        int arr[] = {15, 18, 2, 3, 6, 12}; 
        int n = arr.length; 
      
        System.out.println(countRotations(arr, n)); 
    } 
} 
// This code is contributed by Chhavi 
```

## Python3

```py
# Python3 program to find number 
# of rotations in a sorted and 
# rotated array. 
  
# Returns count of rotations for 
# an array which is first sorted 
# in ascending order, then rotated 
def countRotations(arr, n): 
  
    # We basically find index 
    # of minimum element 
    min = arr[0] 
    for i in range(0, n): 
      
        if (min > arr[i]): 
          
            min = arr[i] 
            min_index = i 
          
    return min_index; 
  
  
# Driver code 
arr = [15, 18, 2, 3, 6, 12] 
n = len(arr) 
print(countRotations(arr, n)) 
  
# This code is contributed by Smitha Dinesh Semwal 
```

## C#

```cs
// c# program to find number of  
// rotations in a sorted and rotated 
// array. 
using System; 
  
class LinearSearch 
{ 
    // Returns count of rotations for an  
    // array which is first sorted in  
    // ascending order, then rotated 
    static int countRotations(int []arr, int n) 
    { 
        // We basically find index of minimum 
        // element 
        int min = arr[0], min_index = -1; 
        for (int i = 0; i < n; i++) 
        { 
            if (min > arr[i]) 
            { 
                min = arr[i]; 
                min_index = i; 
            } 
        }  
        return min_index; 
    } 
  
    // Driver program to test above functions 
    public static void Main ()  
    { 
        int []arr = {15, 18, 2, 3, 6, 12}; 
        int n = arr.Length; 
      
    Console.WriteLine(countRotations(arr, n)); 
    } 
} 
// This code is contributed by vt_m. 
PHP
<?php 
// PHP program to find number  
// of rotations in a sorted  
// and rotated array. 
  
// Returns count of rotations  
// for an array which is first  
// sorted in ascending order, 
// then rotated 
function countRotations($arr, $n) 
{ 
    // We basically find index  
    // of minimum element 
    $min = $arr[0]; 
    $min_index; 
    for ($i = 0; $i < $n; $i++) 
    { 
        if ($min > $arr[$i]) 
        { 
            $min = $arr[$i]; 
            $min_index = $i; 
        } 
    } 
    return $min_index; 
} 
  
// Driver code 
$arr = array(15, 18, 2,  
             3, 6, 12); 
$n = sizeof($arr); 
echo countRotations($arr, $n); 
  
// This code is contributed 
// by ajit 
?> 
```

输出：

```
2
```

时间复杂度：`O(n)`。

辅助空间：`O(1)`。

方法2（高效使用二分搜索）：

在这里我们也找到最小元素的索引，但是使用二分搜索。 这个想法基于以下事实：

最小元素是前一个大于它的唯一元素。 如果没有先前的元素，则没有旋转（第一个元素为最小）。 我们通过将此条件与第`mid-1`个和第`mid + 1`个元素进行比较来检查此条件。

如果最小元素不在中间（既不是`mid`也不是`mid + 1`），则最小元素位于左半部分或右半部分。

如果中间元素小于最后一个元素，则最小元素位于左半部分

其他最小元素位于右半部分。

下面是从此处获取的实现。

## C++

```cpp
// Binary Search based C++ program to find number 
// of rotations in a sorted and rotated array. 
#include<bits/stdc++.h> 
using namespace std; 
  
// Returns count of rotations for an array which 
// is first sorted in ascending order, then rotated 
int countRotations(int arr[], int low, int high) 
{ 
    // This condition is needed to handle the case 
    // when the array is not rotated at all 
    if (high < low) 
        return 0; 
  
    // If there is only one element left 
    if (high == low) 
        return low; 
  
    // Find mid 
    int mid = low + (high - low)/2; /*(low + high)/2;*/
  
    // Check if element (mid+1) is minimum element. 
    // Consider the cases like {3, 4, 5, 1, 2} 
    if (mid < high && arr[mid+1] < arr[mid]) 
       return (mid+1); 
  
    // Check if mid itself is minimum element 
    if (mid > low && arr[mid] < arr[mid - 1]) 
       return mid; 
  
    // Decide whether we need to go to left half or 
    // right half 
    if (arr[high] > arr[mid]) 
       return countRotations(arr, low, mid-1); 
  
    return countRotations(arr, mid+1, high); 
} 
  
// Driver code 
int main() 
{ 
    int arr[] = {15, 18, 2, 3, 6, 12}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << countRotations(arr, 0, n-1); 
    return 0; 
} 
```

## Java

```java
// Java program to find number of  
// rotations in a sorted and rotated 
// array. 
import java.util.*; 
import java.lang.*; 
import java.io.*; 
  
class BinarySearch 
{ 
    // Returns count of rotations for an array 
    // which is first sorted in ascending order, 
    // then rotated 
    static int countRotations(int arr[], int low, 
                                       int high) 
    { 
        // This condition is needed to handle  
        // the case when array is not rotated  
        // at all 
        if (high < low) 
            return 0; 
  
        // If there is only one element left 
        if (high == low) 
            return low; 
  
        // Find mid 
        // /*(low + high)/2;*/ 
        int mid = low + (high - low)/2;  
  
        // Check if element (mid+1) is minimum 
        // element. Consider the cases like 
        // {3, 4, 5, 1, 2} 
        if (mid < high && arr[mid+1] < arr[mid]) 
            return (mid + 1); 
  
        // Check if mid itself is minimum element 
        if (mid > low && arr[mid] < arr[mid - 1]) 
            return mid; 
  
        // Decide whether we need to go to left  
        // half or right half 
        if (arr[high] > arr[mid]) 
            return countRotations(arr, low, mid - 1); 
  
        return countRotations(arr, mid + 1, high); 
    } 
  
    // Driver program to test above functions 
    public static void main (String[] args)  
    { 
        int arr[] = {15, 18, 2, 3, 6, 12}; 
        int n = arr.length; 
          
        System.out.println(countRotations(arr, 0, n-1)); 
    } 
} 
// This code is contributed by Chhavi 
```

## Python3

```py
# Binary Search based Python3  
# program to find number of  
# rotations in a sorted and 
# rotated array. 
  
# Returns count of rotations for 
# an array which is first sorted  
# in ascending order, then rotated 
def countRotations(arr,low, high): 
  
    # This condition is needed to  
    # handle the case when array 
    # is not rotated at all 
    if (high < low): 
        return 0
  
    # If there is only one  
    # element left 
    if (high == low): 
        return low 
  
    # Find mid 
    # (low + high)/2  
    mid = low + (high - low)/2;  
    mid = int(mid) 
  
    # Check if element (mid+1) is 
    # minimum element. Consider  
    # the cases like {3, 4, 5, 1, 2} 
    if (mid < high and arr[mid+1] < arr[mid]): 
        return (mid+1) 
  
    # Check if mid itself is  
    # minimum element 
    if (mid > low and arr[mid] < arr[mid - 1]): 
        return mid 
  
    # Decide whether we need to go 
    # to left half or right half 
    if (arr[high] > arr[mid]): 
        return countRotations(arr, low, mid-1); 
  
    return countRotations(arr, mid+1, high) 
  
# Driver code 
arr = [15, 18, 2, 3, 6, 12] 
n = len(arr) 
print(countRotations(arr, 0, n-1))     
  
# This code is contributed by Smitha Dinesh Semwal 
```

## C#

```cs
// C# program to find number of  
// rotations in a sorted and rotated 
// array. 
using System; 
  
class BinarySearch 
{ 
    // Returns count of rotations for an array 
    // which is first sorted in ascending order, 
    // then rotated 
    static int countRotations(int []arr, int low, int high) 
    { 
        // This condition is needed to handle  
        // the case when array is not rotated  
        // at all 
        if (high < low) 
            return 0; 
  
        // If there is only one element left 
        if (high == low) 
            return low; 
  
        // Find mid 
        // /*(low + high)/2;*/ 
        int mid = low + (high - low)/2;  
  
        // Check if element (mid+1) is minimum 
        // element. Consider the cases like 
        // {3, 4, 5, 1, 2} 
        if (mid < high && arr[mid+1] < arr[mid]) 
            return (mid + 1); 
  
        // Check if mid itself is minimum element 
        if (mid > low && arr[mid] < arr[mid - 1]) 
            return mid; 
  
        // Decide whether we need to go to left  
        // half or right half 
        if (arr[high] > arr[mid]) 
            return countRotations(arr, low, mid - 1); 
  
        return countRotations(arr, mid + 1, high); 
    } 
  
    // Driver program to test above functions 
    public static void Main ()  
    { 
        int []arr = {15, 18, 2, 3, 6, 12}; 
        int n = arr.Length; 
          
    Console.WriteLine(countRotations(arr, 0, n-1)); 
    } 
} 
// This code is contributed by vt_m. 
```

## PHP

```php
<?php 
// Binary Search based PHP 
// program to find number 
// of rotations in a sorted 
// and rotated array. 
  
// Returns count of rotations 
// for an array which is  
// first sorted in ascending  
// order, then rotated 
function countRotations($arr,  
                        $low, $high) 
{ 
    // This condition is needed  
    // to handle the case when  
    // array is not rotated at all 
    if ($high < $low) 
        return 0; 
  
    // If there is only  
    // one element left 
    if ($high == $low) 
        return $low; 
  
    // Find mid 
    $mid = $low + ($high -  
                   $low) / 2;  
  
    // Check if element (mid+1) 
    // is minimum element. Consider 
    // the cases like {3, 4, 5, 1, 2} 
    if ($mid < $high &&  
        $arr[$mid + 1] < $arr[$mid]) 
    return (int)($mid + 1); 
  
    // Check if mid itself  
    // is minimum element 
    if ($mid > $low &&  
        $arr[$mid] < $arr[$mid - 1]) 
    return (int)($mid); 
  
    // Decide whether we need  
    // to go to left half or  
    // right half 
    if ($arr[$high] > $arr[$mid]) 
    return countRotations($arr, $low,  
                          $mid - 1); 
  
    return countRotations($arr,  
                          $mid + 1,  
                          $high); 
} 
  
// Driver code 
$arr = array(15, 18, 2, 3, 6, 12); 
$n = sizeof($arr); 
echo countRotations($arr, 0, $n - 1); 
  
// This code is contributed bu ajit 
?> 
```

输出：

```
2
```

时间复杂度：`O(Log n)`。

辅助空间：如果我们使用迭代二分搜索，则使用`O(1)`（读者可以参考[二分搜索文章](http://quiz.geeksforgeeks.org/binary-search/)中的迭代二分搜索）。