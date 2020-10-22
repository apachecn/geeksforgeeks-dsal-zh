# 数组中的`k`个最大（或最小）元素 | 新增最小堆方法

> 原文： [https://www.geeksforgeeks.org/k-largestor-smallest-elements-in-an-array/](https://www.geeksforgeeks.org/k-largestor-smallest-elements-in-an-array/)

**问题**：编写一个有效的程序来打印数组中`k`个最大的元素。 数组中的元素可以按任何顺序排列。

例如，如果给定的数组为`[1, 23, 12, 9, 30, 2, 50]`，并且要求您输入最大的 3 个元素，即`k = 3`，则程序应输出 50、30 和 23。



 **方法 1（使用冒泡`k`次）**：

 

感谢 Shailendra 提出了这种方法。

1.  修改[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)，最多可运行`k`次外部循环。

2.  打印在步骤 1 中获得的数组的最后`k`个元素。

时间复杂度：`O(nk)`。

像冒泡排序一样，其他排序算法（例如[选择排序](http://en.wikipedia.org/wiki/Selection_sort)）也可以修改以获取`k`个最大元素。

**方法 2（使用临时数组）**：

来自`arr[0..n-1]`的`K`个最大元素：

1.  将前`k`个元素存储在临时数组`temp[0..k-1]`中。

2.  在`temp[]`中找到最小的元素，让最小的元素为`min`。

3.  对于`arr[k]`至`arr[n-1]`中的每个元素`x`（`O(n-k)`），

    1.  如果`x`大于最小值，则从`temp[]`中删除`min`并插入`x`。

    2.  然后，从`temp[]`确定新的`min`（`O(k)`）。

4.  打印`temp[]`的最后`k`个元素。

时间复杂度：`O((n-k) * k)`。 如果我们要对输出进行排序，则`O((n-k) * k + klogk)`。

感谢 nesamani1822 建议使用此方法。

**方法 3（使用排序）**：

1.  在`O(nLogn)`中按降序对元素进行排序。

2.  打印已排序数组`O(k)`的前`k`个数字。

以下是以上的实现。

## C++ 

```cpp

// C++ code for k largest elements in an array 
#include <bits/stdc++.h> 
using namespace std; 

void kLargest(int arr[], int n, int k) 
{ 
    // Sort the given array arr in reverse 
    // order. 
    sort(arr, arr + n, greater<int>()); 

    // Print the first kth largest elements 
    for (int i = 0; i < k; i++) 
        cout << arr[i] << " "; 
} 

// driver program 
int main() 
{ 
    int arr[] = { 1, 23, 12, 9, 30, 2, 50 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int k = 3; 
    kLargest(arr, n, k); 
} 

// This article is contributed by Chhavi 

```

## Java

```java
// Java code for k largest elements in an array 
import java.util.Arrays; 
import java.util.Collections; 
  
class GFG { 
    public static void kLargest(Integer[] arr, int k) 
    { 
        // Sort the given array arr in reverse order 
        // This method doesn't work with primitive data 
        // types. So, instead of int, Integer type 
        // array will be used 
        Arrays.sort(arr, Collections.reverseOrder()); 
  
        // Print the first kth largest elements 
        for (int i = 0; i < k; i++) 
            System.out.print(arr[i] + " "); 
    } 
  
    public static void main(String[] args) 
    { 
        Integer arr[] = new Integer[] { 1, 23, 12, 9, 
                                        30, 2, 50 }; 
        int k = 3; 
        kLargest(arr, k); 
    } 
} 
// This code is contributed by Kamal Rawal
```

## Python

```py
''' Python3 code for k largest elements in an array'''
  
def kLargest(arr, k): 
    # Sort the given array arr in reverse  
    # order. 
    arr.sort(reverse = True) 
    # Print the first kth largest elements 
    for i in range(k): 
        print (arr[i], end =" ")  
  
# Driver program 
arr = [1, 23, 12, 9, 30, 2, 50] 
# n = len(arr) 
k = 3
kLargest(arr, k) 
  
# This code is contributed by shreyanshi_arun. 
```

## C#

```cs
// C# code for k largest elements in an array 
using System; 
  
class GFG { 
    public static void kLargest(int[] arr, int k) 
    { 
        // Sort the given array arr in reverse order 
        // This method doesn't work with primitive data 
        // types. So, instead of int, Integer type 
        // array will be used 
        Array.Sort(arr); 
        Array.Reverse(arr); 
  
        // Print the first kth largest elements 
        for (int i = 0; i < k; i++) 
            Console.Write(arr[i] + " "); 
    } 
  
    // Driver code 
    public static void Main(String[] args) 
    { 
        int[] arr = new int[] { 1, 23, 12, 9, 
                                30, 2, 50 }; 
        int k = 3; 
        kLargest(arr, k); 
    } 
} 
  
// This code contributed by Rajput-Ji 
```

## PHP

```php
<?php  
// PHP code for k largest  
// elements in an array 
  
function kLargest(&$arr, $n, $k) 
{ 
    // Sort the given array arr  
    // in reverse order. 
    rsort($arr); 
  
    // Print the first kth  
    // largest elements 
    for ($i = 0; $i < $k; $i++) 
        echo $arr[$i] . " "; 
} 
  
// Driver Code 
$arr = array(1, 23, 12, 9,  
                30, 2, 50); 
$n = sizeof($arr); 
$k = 3; 
kLargest($arr, $n, $k); 
  
// This code is contributed  
// by ChitraNayal 
?> 
```

输出：

```
50 30 23 
```

时间复杂度：`O(nlogn)`。

方法 4（使用最大堆）：

1.  在`O(n)`中建立一个最大堆树
2.  使用提取最大k次从最大堆`O(klogn)`中获取`k`个最大元素

时间复杂度：`O(n + klogn)`。

方法 5（使用奇数统计）：

1.  使用顺序统计算法找到第k个最大元素。请参阅最坏情况线性时间`O(n)`中的主题选择
2.  使用`QuickSort`分区算法对第`k`个最大数`O(n)`进行分区。
3.  对`k-1`个元素（大于第k​​个最大元素的元素）进行排序，`O(kLogk)`。仅当需要排序的输出时才需要此步骤。

时间复杂度：如果不需要排序输出，则为`O(n)`，否则为`O(n + kLogk)`。

感谢 Shilpi 建议前两种方法。

方法 6（使用最小堆）：

此方法主要是方法1的优化。请使用最小堆，而不要使用`temp[]`数组。

1.  建立给定数组的前`k`个元素（`arr[0]`至`arr[k-1]`）的最小堆`MH`，`O(k)`。

2.  对于每个元素，在第`k`个元素（`arr[k]`至`arr[n-1]`）之后，将其与`MH`的根进行比较。
    
    +   如果元素大于根，则将其设为根并为`MH`调用`heapify`。
    +   否则忽略它。

    步骤 2 为`O((n-k) * logk)`。

3.  最后，`MH`具有`k`个最大元素，而`MH`的根是第`k`个最大元素。

时间复杂度：`O(k + (n-k) Logk)`，无排序输出。如果需要排序的输出，则`O(k + (n-k) Logk + kLogk)`。

所有上述方法也可以用于找到第`k`个最大（或最小）元素。

## C++

```cpp
#include <iostream> 
using namespace std; 
  
// Swap function to interchange 
// the value of variables x and y 
int swap(int& x, int& y) 
{ 
    int temp = x; 
    x = y; 
    y = temp; 
} 
  
// Min Heap Class 
// arr holds reference to an integer  
// array size indicate the number of 
// elements in Min Heap 
class MinHeap { 
  
    int size; 
    int* arr; 
  
public: 
    // Constructor to initialize the size and arr 
    MinHeap(int size, int input[]); 
  
    // Min Heapify function, that assumes that 
    // 2*i+1 and 2*i+2 are min heap and fix the 
    // heap property for i. 
    void heapify(int i); 
  
    // Build the min heap, by calling heapify 
    // for all non-leaf nodes. 
    void buildHeap(); 
}; 
  
// Constructor to initialize data 
// members and creating mean heap 
MinHeap::MinHeap(int size, int input[]) 
{ 
    // Initializing arr and size 
  
    this->size = size; 
    this->arr = input; 
  
    // Building the Min Heap 
    buildHeap(); 
} 
  
// Min Heapify function, that assumes 
// 2*i+1 and 2*i+2 are min heap and  
// fix min heap property for i 
  
void MinHeap::heapify(int i) 
{ 
    // If Leaf Node, Simply return 
    if (i >= size / 2) 
        return; 
  
    // variable to store the smallest element 
    // index out of i, 2*i+1 and 2*i+2 
    int smallest; 
  
    // Index of left node 
    int left = 2 * i + 1; 
  
    // Index of right node 
    int right = 2 * i + 2; 
  
    // Select minimum from left node and  
    // current node i, and store the minimum 
    // index in smallest variable 
    smallest = arr[left] < arr[i] ? left : i; 
  
    // If right child exist, compare and 
    // update the smallest variable 
    if (right < size) 
        smallest = arr[right] < arr[smallest] 
                             ? right : smallest; 
  
    // If Node i violates the min heap  
    // property, swap  current node i with 
    // smallest to fix the min-heap property  
    // and recursively call heapify for node smallest. 
    if (smallest != i) { 
        swap(arr[i], arr[smallest]); 
        heapify(smallest); 
    } 
} 
  
// Build Min Heap 
void MinHeap::buildHeap() 
{ 
    // Calling Heapify for all non leaf nodes 
    for (int i = size / 2 - 1; i >= 0; i--) { 
        heapify(i); 
    } 
} 
  
void FirstKelements(int arr[],int size,int k){ 
    // Creating Min Heap for given 
    // array with only k elements 
    MinHeap* m = new MinHeap(k, arr); 
  
    // Loop For each element in array 
    // after the kth element 
    for (int i = k; i < size; i++) { 
  
        // if current element is smaller  
        // than minimum element, do nothing  
        // and continue to next element 
        if (arr[0] > arr[i]) 
            continue; 
  
        // Otherwise Change minimum element to  
        // current element, and call heapify to 
        // restore the heap property 
        else { 
            arr[0] = arr[i]; 
            m->heapify(0); 
        } 
    } 
    // Now min heap contains k maximum 
    // elements, Iterate and print 
    for (int i = 0; i < k; i++) { 
        cout << arr[i] << " "; 
    } 
} 
// Driver Program 
int main() 
{ 
  
    int arr[] = { 11, 3, 2, 1, 15, 5, 4, 
                           45, 88, 96, 50, 45 }; 
  
    int size = sizeof(arr) / sizeof(arr[0]); 
  
    // Size of Min Heap 
    int k = 3; 
  
    FirstKelements(arr,size,k); 
  
    return 0; 
} 
// This code is contributed by Ankur Goel 
```

输出：

```
50 88 96
```

参考：

<http://en.wikipedia.org/wiki/Selection_algorithm>