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