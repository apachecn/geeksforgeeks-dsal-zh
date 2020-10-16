# 两个排序数组的并集和交集

> 原文： [https://www.geeksforgeeks.org/union-and-intersection-of-two-sorted-arrays-2/](https://www.geeksforgeeks.org/union-and-intersection-of-two-sorted-arrays-2/)

给定两个排序的数组，找到它们的并集和交集。

**示例**：

```
Input : arr1[] = {1, 3, 4, 5, 7}
        arr2[] = {2, 3, 5, 6} 
Output : Union : {1, 2, 3, 4, 5, 6, 7} 
         Intersection : {3, 5}

Input : arr1[] = {2, 5, 6}
        arr2[] = {4, 6, 8, 10} 
Output : Union : {2, 4, 5, 6, 8, 10} 
         Intersection : {6}

```

[](https://practice.geeksforgeeks.org/problem-page.php?pid=537)

## 强烈建议您在继续解决方案之前，单击这里进行练习。

**数组`arr1[]`和`arr2[]`的并集**：

要查找两个排序数组的并集，请遵循以下合并过程：

1.  使用两个索引变量`i`和`j`，初始值`i = 0`，`j = 0`。

2.  如果`arr1[i]`小于`arr2[j]`，则打印`arr1[i]`并递增`i`。

3.  如果`arr1[i]`大于`arr2[j]`，则打印`arr2[j]`并递增`j`。

4.  如果两者相同，则打印其中的任何一个并递增`i`和`j`。

5.  打印较大数组的其余元素。

下面是上述方法的实现：

## C++ 

```cpp

// C++ program to find union of 
// two sorted arrays 
#include <bits/stdc++.h> 
using namespace std; 

/* Function prints union of arr1[] and arr2[] 
   m is the number of elements in arr1[] 
   n is the number of elements in arr2[] */
int printUnion(int arr1[], int arr2[], int m, int n) 
{ 
  int i = 0, j = 0; 
  while (i < m && j < n) 
  { 
    if (arr1[i] < arr2[j]) 
       cout << arr1[i++] << " "; 

    else if (arr2[j] < arr1[i]) 
       cout << arr2[j++] << " "; 

    else
    { 
       cout << arr2[j++] << " "; 
       i++; 
    } 
  } 

  /* Print remaining elements of the larger array */
  while(i < m) 
     cout << arr1[i++] << " "; 

  while(j < n) 
    cout << arr2[j++] << " "; 
} 

/* Driver program to test above function */
int main() 
{ 
  int arr1[] = {1, 2, 4, 5, 6}; 
  int arr2[] = {2, 3, 5, 7}; 

  int m = sizeof(arr1)/sizeof(arr1[0]); 
  int n = sizeof(arr2)/sizeof(arr2[0]); 

  // Function calling 
  printUnion(arr1, arr2, m, n); 

  return 0; 
} 

```