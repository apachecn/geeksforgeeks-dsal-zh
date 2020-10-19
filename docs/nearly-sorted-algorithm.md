# 对几乎排序（或`K`排序）的数组进行排序

> 原文： [https://www.geeksforgeeks.org/nearly-sorted-algorithm/](https://www.geeksforgeeks.org/nearly-sorted-algorithm/)

给定`n`个元素的数组，其中每个元素距离其目标位置最多`k`个，设计一种算法，以`O(n log k)`时间排序。 例如，让我们考虑`k`为 2，在排序数组中索引 7 处的元素可以在给定数组中索引 5、6、7、8、9 处。

**示例**：

```
Input : arr[] = {6, 5, 3, 2, 8, 10, 9}
            k = 3 
Output : arr[] = {2, 3, 5, 6, 8, 9, 10}

Input : arr[] = {10, 9, 8, 7, 4, 70, 60, 50}
         k = 4
Output : arr[] = {4, 7, 8, 9, 10, 50, 60, 70}

```



我们可以**使用插入排序**对元素进行有效排序。 以下是标准插入排序的 C 代码。

## C

```c

/* Function to sort an array using insertion sort*/
void insertionSort(int A[], int size) 
{ 
   int i, key, j; 
   for (i = 1; i < size; i++) 
   { 
       key = A[i]; 
       j = i-1; 

       /* Move elements of A[0..i-1], that are greater than key, to one  
          position ahead of their current position. 
          This loop will run at most k times */
       while (j >= 0 && A[j] > key) 
       { 
           A[j+1] = A[j]; 
           j = j-1; 
       } 
       A[j+1] = key; 
   } 
} 

```

## Java

```
/* Function to sort an array using insertion sort*/
static void insertionSort(int A[], int size)  
{  
int i, key, j;  
for (i = 1; i < size; i++)  
{  
    key = A[i];  
    j = i-1;  
  
    /* Move elements of A[0..i-1], that are greater than key, to one  
        position ahead of their current position.  
        This loop will run at most k times */
    while (j >= 0 && A[j] > key)  
    {  
        A[j+1] = A[j];  
        j = j-1;  
    }  
    A[j+1] = key;  
}  
}
```

## Python3

```
# Function to sort an array using 
# insertion sort 
def insertionSort(A, size): 
i, key, j = 0, 0, 0
for i in range(size): 
    key = A[i]  
    j = i-1
  
    # Move elements of A[0..i-1], that are  
    # greater than key, to one position  
    # ahead of their current position.  
    # This loop will run at most k times  
    while j >= 0 and A[j] > key: 
        A[j + 1] = A[j]  
        j = j - 1
    A[j + 1] = key
```

## C#

```
/* C# Function to sort an array using insertion sort*/
static void insertionSort(int A[], int size)  
{  
    int i, key, j;  
        for (i = 1; i < size; i++)  
        {  
            key = A[i];  
            j = i-1;  
  
    /* Move elements of A[0..i-1], that are greater than key, to one  
        position ahead of their current position.  
        This loop will run at most k times */
    while (j >= 0 && A[j] > key)  
    {  
        A[j+1] = A[j];  
        j = j-1;  
    }  
    A[j+1] = key;  
}  
}
```

内循环最多运行k次。 要将每个元素移到正确的位置，最多需要移动`k`个元素。 因此总体复杂度将为`O(nk)`。

我们可以借助堆数据结构更有效地对此类数组进行排序。 以下是使用堆的详细过程。

1.  使用前`k + 1`个元素创建大小为`k + 1`的最小堆。 这将花费`O(k)`时间（[请参阅此 GFact](https://www.geeksforgeeks.org/time-complexity-of-building-a-heap/)）。
2.  一步一步地从堆中删除`min`元素，将其放入结果数组，然后从其余元素中向堆中添加一个新元素。

删除元素并将新元素添加到最小堆将花费`Logk`时间。 因此总体复杂度将为`O(k + (n-k) * logK)`。

## C++

```
// A STL based C++ program to sort a nearly sorted array. 
#include <bits/stdc++.h> 
using namespace std; 
   
// Given an array of size n, where every element 
// is k away from its target position, sorts the 
// array in O(nLogk) time. 
int sortK(int arr[], int n, int k) 
{ 
    // Insert first k+1 items in a priority queue (or min heap) 
    //(A O(k) operation). We assume, k < n. 
    priority_queue<int, vector<int>, greater<int> > pq(arr, arr + k + 1); 
   
    // i is index for remaining elements in arr[] and index 
    // is target index of for current minimum element in 
    // Min Heapm 'hp'. 
    int index = 0; 
    for (int i = k + 1; i < n; i++) { 
        arr[index++] = pq.top(); 
        pq.pop(); 
        pq.push(arr[i]); 
    } 
   
    while (pq.empty() == false) { 
        arr[index++] = pq.top(); 
        pq.pop(); 
    } 
} 
   
// A utility function to print array elements 
void printArray(int arr[], int size) 
{ 
    for (int i = 0; i < size; i++) 
        cout << arr[i] << " "; 
    cout << endl; 
} 
   
// Driver program to test above functions 
int main() 
{ 
    int k = 3; 
    int arr[] = { 2, 6, 3, 12, 56, 8 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    sortK(arr, n, k); 
   
    cout << "Following is sorted array" << endl; 
    printArray(arr, n); 
   
    return 0; 
}
```

## Java

```
// A java program to sort a nearly sorted array 
import java.util.Iterator; 
import java.util.PriorityQueue; 
  
class GFG  
{ 
    private static void kSort(int[] arr, int n, int k)  
    { 
  
        // min heap 
        PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(); 
  
        // add first k + 1 items to the min heap 
        for(int i = 0; i < k + 1; i++) 
        { 
            priorityQueue.add(arr[i]); 
        } 
  
        int index = 0; 
        for(int i = k + 1; i < n; i++)  
        { 
            arr[index++] = priorityQueue.peek(); 
            priorityQueue.poll(); 
            priorityQueue.add(arr[i]); 
        } 
  
        Iterator<Integer> itr = priorityQueue.iterator(); 
  
        while(itr.hasNext())  
        { 
            arr[index++] = priorityQueue.peek(); 
            priorityQueue.poll(); 
        } 
  
    } 
  
    // A utility function to print the array 
    private static void printArray(int[] arr, int n)  
    { 
        for(int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 
    } 
  
    // Driver Code 
    public static void main(String[] args)  
    { 
        int k = 3; 
        int arr[] = { 2, 6, 3, 12, 56, 8 }; 
        int n = arr.length; 
        kSort(arr, n, k); 
        System.out.println("Following is sorted array"); 
        printArray(arr, n); 
    } 
} 
  
// This code is contributed by  
// Manpreet Singh(manpreetsngh294)
```

## Python3

```
# A Python3 program to sort a 
# nearly sorted array. 
  
from heapq import heappop, heappush, heapify 
  
  
# A utility function to print  
# array elements 
def print_array(arr: list): 
    for elem in arr: 
        print(elem, end = ' ') 
  
# Given an array of size n, where every   
# element is k away from its target  
# position, sorts the array in O(nLogk) time. 
def sort_k(arr: list, n: int, k: int): 
    """ 
    :param arr: input array 
    :param n: length of the array 
    :param k: max distance, which every  
     element is away from its target position. 
    :return: None 
    """
    # List of first k+1 items 
    heap = arr[:k + 1] 
  
    # using heapify to convert list  
    # into heap(or min heap) 
    heapify(heap) 
  
    # "rem_elmnts_index" is index for remaining  
    # elements in arr and "target_index" is  
    # target index of for current minimum element  
    # in Min Heap "heap". 
    target_index = 0
    for rem_elmnts_index in range(k + 1, n): 
        arr[target_index] = heappop(heap) 
        heappush(heap, arr[rem_elmnts_index]) 
        target_index += 1
  
    while heap: 
        arr[target_index] = heappop(heap) 
        target_index += 1
  
# Driver Code 
k = 3
arr = [2, 6, 3, 12, 56, 8] 
n = len(arr) 
sort_k(arr, n, k) 
  
print('Following is sorted array') 
print_array(arr) 
  
# This code is contributed by  
# Veerat Beri(viratberi)
```

输出：

```
Following is sorted array
2 3 6 8 12 56
```

基于最小堆的方法需要`O(nLogk)`时间，并使用`O(k)`辅助空间。

我们还可以使用平衡二进制搜索树而不是堆来存储`K + 1`个元素。 平衡 BST 上的插入和删除操作也需要`O(Logk)`时间。 因此，基于平衡 BST 的方法也将花费`O(nLogk)`时间，但是堆最小化方法似乎更有效，因为最小元素始终是根。 此外，堆不需要额外的空间来放置左右指针。

