# 在线性时间内找到大小为 3 的排序子序列

> 原文： [https://www.geeksforgeeks.org/find-a-sorted-subsequence-of-size-3-in-linear-time/](https://www.geeksforgeeks.org/find-a-sorted-subsequence-of-size-3-in-linear-time/)

给定`n`个整数的数组，请找到 3 个元素，以便在`0(n)`时间内`a[i] < a[j] < a[k]`和`i < j < k`。 如果有多个这样的三元组，请打印其中的任何一个。

**示例**：

```
Input: arr[] = {12, 11, 10, 5, 6, 2, 30}
Output: 5, 6, 30
Explanation: As 5 < 6 < 30, and they 
appear in the same sequence in the array 

Input: arr[] = {1, 2, 3, 4}
Output: 1, 2, 3 OR 1, 2, 4 OR 2, 3, 4
Explanation: As the array is sorted, for every i, j, k,
where i < j < k, arr[i] < arr[j] < arr[k] 

Input: arr[] = {4, 3, 2, 1}
Output: No such triplet exists.

```



**提示**：使用辅助空间。

**解决方案**：因此，主要动机是找到一个元素，该元素的元素在数组的左侧小于其自身，而元素的大小大于在数组的右侧，如果有这样的元素的话，存在一个满足标准的三元组。

**方法**：这可以通过非常简单的方式解决。 要查找数组左侧的元素小于其自身的元素，请在从起始索引即（0）开始遍历数组时检查该元素是否为最小元素，并检查在它的右侧是否存在大于它本身的元素，从该数组的末尾遍历（`n-1`）时，检查该元素是否为最大元素。 如果该元素不是从 0 到该索引的最小元素，则它的左侧小于其自身的元素；类似地，如果该元素不是从该索引到最后一个索引的最大元素，则它的右侧的元素更大。

**算法**：

1.  创建一个较小的辅助数组`[0..n-1]`。 `small[i]`存储小于`arr[i]`且在左侧的数字的索引。 如果没有这样的元素，则数组包含 -1。

2.  创建另一个更大`[0..n-1]`的辅助数组。 `Greater[i]`存储大于`arr[i]`且位于`arr[i]`右侧的数字的索引。 如果没有这样的元素，则数组包含 -1。

3.  最后遍历`smaller[]`和`biger[]`，并找到索引`[i]`，其中`smaller[i]`和`Greater[i]`都不等于 -1。

## C++ 

```cpp

// C++ program to find a sorted 
// sub-sequence of size 3 
#include <bits/stdc++.h> 
using namespace std; 

// A function to fund a sorted 
// sub-sequence of size 3 
void find3Numbers(int arr[], int n) 
{ 
    // Index of maximum element 
    // from right side 
    int max = n - 1; 

    // Index of minimum element 
    // from left side 
    int min = 0; 
    int i; 

    // Create an array that will store 
    // index of a smaller element on left side. 
    // If there is no smaller element on left 
    // side, then smaller[i] will be -1\. 
    int* smaller = new int[n]; 

    // first entry will always be -1 
    smaller[0] = -1; 
    for (i = 1; i < n; i++) { 
        if (arr[i] <= arr[min]) { 
            min = i; 
            smaller[i] = -1; 
        } 
        else
            smaller[i] = min; 
    } 

    // Create another array that will 
    // store index of a greater element 
    // on right side. If there is no greater 
    // element on right side, then 
    // greater[i] will be -1\. 
    int* greater = new int[n]; 

    // last entry will always be -1 
    greater[n - 1] = -1; 
    for (i = n - 2; i >= 0; i--) { 
        if (arr[i] >= arr[max]) { 
            max = i; 
            greater[i] = -1; 
        } 
        else
            greater[i] = max; 
    } 

    // Now find a number which has both 
    // a greater number on right side and 
    // smaller number on left side 
    for (i = 0; i < n; i++) { 
        if (smaller[i] != -1 && greater[i] != -1) { 
            cout << arr[smaller[i]] 
                 << " " << arr[i] << " "
                 << arr[greater[i]]; 
            return; 
        } 
    } 

    // If we reach number, then there are 
    // no such 3 numbers 
    cout << "No such triplet found"; 

    // Free the dynamically allocated memory 
    // to avoid memory leak 
    delete[] smaller; 
    delete[] greater; 

    return; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 12, 11, 10, 5, 6, 2, 30 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    find3Numbers(arr, n); 
    return 0; 
    a greater number on 
} 

// This is code is contributed by rathbhupendra 

```

## C

```c

// C program to find a sorted 
// sub-sequence of size 3 
#include <stdio.h> 

// A function to fund a sorted 
// sub-sequence of size 3 
void find3Numbers(int arr[], int n) 
{ 
    // Index of maximum element 
    // from right side 
    int max = n - 1; 

    // Index of minimum element 
    // from left side 
    int min = 0; 
    int i; 

    // Create an array that will store 
    // index of a smaller element on left side. 
    // If there is no smaller element on left side, 
    // then smaller[i] will be -1\. 
    int* smaller = new int[n]; 

    // first entry will always be -1 
    smaller[0] = -1; 
    for (i = 1; i < n; i++) { 
        if (arr[i] <= arr[min]) { 
            min = i; 
            smaller[i] = -1; 
        } 
        else
            smaller[i] = min; 
    } 

    // Create another array that will 
    // store index of a greater element 
    // on right side. If there is no greater 
    // element on right side, then 
    // greater[i] will be -1\. 
    int* greater = new int[n]; 

    // last entry will always be -1 
    greater[n - 1] = -1; 
    for (i = n - 2; i >= 0; i--) { 
        if (arr[i] >= arr[max]) { 
            max = i; 
            greater[i] = -1; 
        } 
        else
            greater[i] = max; 
    } 

    // Now find a number which has 
    // both a greater number on right 
    // side and smaller number on left side 
    for (i = 0; i < n; i++) { 
        if (smaller[i] != -1 && greater[i] != -1) { 
            printf("%d %d %d", arr[smaller[i]], 
                   arr[i], arr[greater[i]]); 
            return; 
        } 
    } 

    // If we reach number, then 
    // there are no such 3 numbers 
    printf("No such triplet found"); 

    // Free the dynamically allocated memory 
    // to avoid memory leak 
    delete[] smaller; 
    delete[] greater; 

    return; 
} 

// Driver program to test above function 
int main() 
{ 
    int arr[] = { 12, 11, 10, 5, 6, 2, 30 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    find3Numbers(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find a sorted 
// sub-sequence of size 3 
import java.io.*; 

class SortedSubsequence { 
    // A function to find a sorted 
    // sub-sequence of size 3 
    static void find3Numbers(int arr[]) 
    { 
        int n = arr.length; 

        // Index of maximum element 
        // from right side 
        int max = n - 1; 

        // Index of minimum element 
        // from left side 
        int min = 0; 
        int i; 

        // Create an array that will store 
        // index of a smaller element on left side. 
        // If there is no smaller element on left 
        // side, then smaller[i] will be -1\. 
        int[] smaller = new int[n]; 

        // first entry will always be -1 
        smaller[0] = -1; 
        for (i = 1; i < n; i++) { 
            if (arr[i] <= arr[min]) { 
                min = i; 
                smaller[i] = -1; 
            } 
            else
                smaller[i] = min; 
        } 

        // Create another array that will 
        // store index of a greater element 
        // on right side. If there is no greater 
        // element on right side, then greater[i] 
        // will be -1\. 
        int[] greater = new int[n]; 

        // last entry will always be -1 
        greater[n - 1] = -1; 
        for (i = n - 2; i >= 0; i--) { 
            if (arr[i] >= arr[max]) { 
                max = i; 
                greater[i] = -1; 
            } 
            else
                greater[i] = max; 
        } 

        // Now find a number which has 
        // both greater number on right 
        // side and smaller number on left side 
        for (i = 0; i < n; i++) { 
            if ( 
                smaller[i] != -1 && greater[i] != -1) { 
                System.out.print( 
                    arr[smaller[i]] + " " + arr[i] 
                    + " " + arr[greater[i]]); 
                return; 
            } 
        } 

        // If we reach number, then there 
        // are no such 3 numbers 
        System.out.println("No such triplet found"); 
        return; 
    } 

    public static void main(String[] args) 
    { 
        int arr[] = { 12, 11, 10, 5, 6, 2, 30 }; 
        find3Numbers(arr); 
    } 
} 
/* This code is contributed by Devesh Agrawal*/

```

## Python

```py

# Python program to fund a sorted 
# sub-sequence of size 3 

def find3numbers(arr): 
    n = len(arr) 

# Index of maximum element from right side 
    max = n-1

# Index of minimum element from left side  
    min = 0

    # Create an array that will store  
    # index of a smaller element on left side.  
    # If there is no smaller element on left side, 
# then smaller[i] will be -1\. 
    smaller = [0]*10000
    smaller[0] = -1
    for i in range(1, n): 
        if (arr[i] <= arr[min]): 
            min = i 
            smaller[i] = -1
        else: 
            smaller[i] = min

    # Create another array that will  
    # store index of a greater element  
    # on right side. If there is no greater  
# element on right side, then greater[i]  
# will be -1\. 
    greater = [0]*10000
    greater[n-1] = -1

    for i in range(n-2, -1, -1): 
        if (arr[i] >= arr[max]): 
            max = i 
            greater[i] = -1

        else: 
            greater[i] = max

    # Now find a number which has  
    # both a greater number on right  
# side and smaller number on left side 
    for i in range(0, n): 
        if smaller[i] != -1 and greater[i] != -1: 
            print arr[smaller[i]], arr[i], arr[greater[i]] 
            return

    # If we reach here, then there are no such 3 numbers 
    print "No triplet found"
    return

# Driver function to test above function 
arr = [12, 11, 10, 5, 6, 2, 30] 
find3numbers(arr) 

# This code is contributed by Devesh Agrawal 

```

## C# 

```cs

// C# program to find a sorted 
// subsequence of size 3 
using System; 

class SortedSubsequence { 

    // A function to find a sorted 
    // subsequence of size 3 
    static void find3Numbers(int[] arr) 
    { 
        int n = arr.Length; 

        // Index of maximum element from right side 
        int max = n - 1; 

        // Index of minimum element from left side 
        int min = 0; 
        int i; 

        // Create an array that will store index 
        // of a smaller element on left side. 
        // If there is no smaller element 
        // on left side, then smaller[i] will be -1\. 
        int[] smaller = new int[n]; 

        // first entry will always be -1 
        smaller[0] = -1; 
        for (i = 1; i < n; i++) { 
            if (arr[i] <= arr[min]) { 
                min = i; 
                smaller[i] = -1; 
            } 
            else
                smaller[i] = min; 
        } 

        // Create another array that will store 
        // index of a greater element on right side. 
        // If there is no greater element on 
        // right side, then greater[i] will be -1\. 
        int[] greater = new int[n]; 

        // last entry will always be -1 
        greater[n - 1] = -1; 
        for (i = n - 2; i >= 0; i--) { 
            if (arr[i] >= arr[max]) { 
                max = i; 
                greater[i] = -1; 
            } 
            else
                greater[i] = max; 
        } 

        // Now find a number which has 
        // both a greater number on right side 
        // and smaller number on left side 
        for (i = 0; i < n; i++) { 
            if (smaller[i] != -1 && greater[i] != -1) { 
                Console.Write( 
                    arr[smaller[i]] + " " + arr[i] 
                    + " " + arr[greater[i]]); 
                return; 
            } 
        } 

        // If we reach number, then there 
        // are no such 3 numbers 
        Console.Write("No such triplet found"); 
        return; 
    } 

    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 12, 11, 10, 5, 6, 2, 30 }; 
        find3Numbers(arr); 
    } 
} 

/* This code is contributed by vt_m*/

```

## PHP

```php

<?php  
// PHP program to find a sorted  
// subsequence of size 3 

// A function to fund a sorted 
// subsequence of size 3 
function find3Numbers(&$arr, $n) 
{ 
    // Index of maximum element from right side 
    $max = $n - 1; 

    // Index of minimum element from left side  
    $min = 0;  

    // Create an array that will store  
    // index of a smaller element on 
    // left side. If there is no smaller  
    // element on left side, then  
    // smaller[i] will be -1\. 
    $smaller = array_fill(0, $n, NULL); 
    $smaller[0] = -1; // first entry will 
                      // always be -1 
    for ($i = 1; $i < $n; $i++) 
    { 
        if ($arr[$i] <= $arr[$min]) 
        { 
            $min = $i; 
            $smaller[$i] = -1; 
        } 
        else
            $smaller[$i] = $min; 
    } 

    // Create another array that will  
    // store index of a greater element  
    // on right side. If there is no  
    // greater element on right side,  
    // then greater[i] will be -1\. 
    $greater = array_fill(0, $n, NULL); 

    // last entry will always be -1 
    $greater[$n - 1] = -1;  
    for ($i = $n - 2; $i >= 0; $i--) 
    { 
        if ($arr[$i] >= $arr[$max]) 
        { 
            $max = $i; 
            $greater[$i] = -1; 
        } 
        else
            $greater[$i] = $max; 
    } 

    // Now find a number which has both  
    // a greater number on right side  
    // and smaller number on left side 
    for ($i = 0; $i < $n; $i++) 
    { 
        if ($smaller[$i] != -1 &&  
            $greater[$i] != -1) 
        { 
            echo $arr[$smaller[$i]]." ". 
                      $arr[$i] . " " .  
                      $arr[$greater[$i]]; 
            return; 
        } 
    } 

    // If we reach number, then there 
    // are no such 3 numbers 
    printf("No such triplet found"); 

    return; 
} 

// Driver Code 
$arr = array(12, 11, 10, 5, 6, 2, 30); 
$n = sizeof($arr); 
find3Numbers($arr, $n); 

// This code is contributed  
// by ChitraNayal 
?> 

```

**输出**：

```
5 6 30

```

**复杂度分析**：

*   **时间复杂度**：`O(n)`。 由于数组仅传播一次，并且没有嵌套循环，因此时间复杂度将约为`n`。

*   **辅助空间**：`O(n)`。 由于需要两个额外的数组来存储前一个较小元素和下一个较大元素的索引，因此所需空间也将为`n`。

**参考**： [如何在线性时间中按数组的递增顺序和索引找到 3 个数字](http://stackoverflow.com/questions/10008118/how-to-find-3-numbers-in-increasing-order-and-increasing-indices-in-an-array-in)

**练习**：

1.  找到大小为 3 的子序列，使得`arr[i] arr[k]`。

2.  在线性时间内找到大小为 4 的排序子序列。

