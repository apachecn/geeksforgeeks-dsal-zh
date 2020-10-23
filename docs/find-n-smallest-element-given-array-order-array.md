# 按原始顺序打印给定数组中的`n`个最小元素

> 原文： [https://www.geeksforgeeks.org/find-n-smallest-element-given-array-order-array/](https://www.geeksforgeeks.org/find-n-smallest-element-given-array-order-array/)

我们给定了一个由`m`个元素组成的数组，我们需要从该数组中找到`n`个最小的元素，但它们的顺序必须与给定数组中的元素相同。

**示例**：

```
Input : arr[] = {4, 2, 6, 1, 5}, 
        n = 3
Output : 4 2 1
Explanation : 
1, 2 and 4 are 3 smallest numbers and
4 2 1 is their order in given array.

Input : arr[] = {4, 12, 16, 21, 25},
        n = 3
Output : 4 12 16
Explanation : 
4, 12 and 16 are 3 smallest numbers and 
4 12 16 is their order in given array.

```



制作原始数组的副本，然后对副本数组进行排序。 对副本数组排序后，保存所有`n`个最小的数字。 此外，对于原始数组中的每个元素，检查它是否存在于`n`个最小的数字中，如果它存在于`n`个最小的数组中，则将其打印出来，否则向前移动。

*   创建`copy_arr[]`

*   排序`copy_arr`

*   对于`arr []`中的所有元素：

    *   在`copy_arr`的`n`个最小元素中找到`arr[i]`

    *   如果找到，则打印元素

下面是上述方法的实现：

## C++ 

```cpp

// CPP for printing smallest n number in order 
#include <bits/stdc++.h> 
using namespace std; 

// Function to print smallest n numbers 
void printSmall(int arr[], int asize, int n) 
{ 
    // Make copy of array 
    vector<int> copy_arr(arr, arr + asize); 

    // Sort copy array 
    sort(copy_arr.begin(), copy_arr.begin() + asize); 

    // For each arr[i] find whether 
    // it is a part of n-smallest 
    // with binary search 
    for (int i = 0; i < asize; ++i) 
        if (binary_search(copy_arr.begin(),  
                copy_arr.begin() + n, arr[i])) 
            cout << arr[i] << " "; 
} 

// Driver program 
int main() 
{ 
    int arr[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 }; 
    int asize = sizeof(arr) / sizeof(arr[0]);     
    int n = 5; 
    printSmall(arr, asize, n); 
    return 0; 
} 

```

## Java

```java
// Java for printing smallest n number in order 
import java.util.*; 
  
class GFG  
{ 
  
  
// Function to print smallest n numbers 
static void printSmall(int arr[], int asize, int n) 
{ 
    // Make copy of array 
    int []copy_arr = Arrays.copyOf(arr,asize); 
  
    // Sort copy array 
    Arrays.sort(copy_arr); 
  
    // For each arr[i] find whether 
    // it is a part of n-smallest 
    // with binary search 
    for (int i = 0; i < asize; ++i) 
    { 
        if (Arrays.binarySearch(copy_arr,0,n, arr[i])>-1) 
            System.out.print(arr[i] + " "); 
    } 
} 
  
// Driver code 
public static void main(String[] args)  
{ 
    int arr[] = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 }; 
    int asize = arr.length;  
    int n = 5; 
    printSmall(arr, asize, n); 
} 
} 
  
// This code is contributed by Princi Singh
```

## Python3

```py
# Python3 for printing smallest n number in order 
  
# Function for binary_search 
def binary_search(arr, low, high, ele): 
    while low < high: 
        mid = (low + high) // 2
        if arr[mid] == ele: 
            return mid 
        elif arr[mid] > ele: 
            high = mid 
        else: 
            low = mid + 1
    return -1
  
# Function to print smallest n numbers 
def printSmall(arr, asize, n): 
  
    # Make copy of array 
    copy_arr = arr.copy() 
  
    # Sort copy array 
    copy_arr.sort() 
  
    # For each arr[i] find whether 
    # it is a part of n-smallest 
    # with binary search 
    for i in range(asize): 
        if binary_search(copy_arr, low = 0,  
                         high = n, ele = arr[i]) > -1: 
            print(arr[i], end = " ") 
  
# Driver Code 
if __name__ == "__main__": 
    arr = [1, 5, 8, 9, 6, 7, 3, 4, 2, 0] 
    asize = len(arr) 
    n = 5
    printSmall(arr, asize, n) 
  
# This code is conributed by 
# sanjeev2552
```

## C#

```cs
// C# for printing smallest n number in order 
using System;      
  
class GFG  
{ 
  
  
// Function to print smallest n numbers 
static void printSmall(int []arr, int asize, int n) 
{ 
    // Make copy of array 
    int []copy_arr = new int[asize]; 
    Array.Copy(arr, copy_arr, asize); 
  
    // Sort copy array 
    Array.Sort(copy_arr); 
  
    // For each arr[i] find whether 
    // it is a part of n-smallest 
    // with binary search 
    for (int i = 0; i < asize; ++i) 
    { 
        if (Array.BinarySearch(copy_arr, 0, n, arr[i])>-1) 
            Console.Write(arr[i] + " "); 
    } 
} 
  
// Driver code 
public static void Main(String[] args)  
{ 
    int []arr = { 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 }; 
    int asize = arr.Length;  
    int n = 5; 
    printSmall(arr, asize, n); 
} 
} 
  
// This code has been contributed by 29AjayKumar
```

输出：

```
1 3 4 2 0 
```

为了复制数组，我们需要`O(n)`的空间复杂度，然后为了排序，我们需要`O(n log n)`的复杂度。 进一步，对于`arr[]`中的每个元素，我们都在`copy_arr[]`中执行搜索，这将导致`O(n)`进行线性搜索，但是我们可以通过应用二进制搜索对其进行改进，因此我们的整体时间复杂度将为`O(n log n)`。