# 两个元素的和最接近零

> 原文： [https://www.geeksforgeeks.org/two-elements-whose-sum-is-closest-to-zero/](https://www.geeksforgeeks.org/two-elements-whose-sum-is-closest-to-zero/)

**问题**：给出了一个整数数组，包括`+ve`和`-ve`。 您需要找到两个元素，使它们的总和最接近零。

对于以下数组，程序应打印 -80 和 85。



**方法 1（简单）**：

对于每个元素，找到它与数组中每个其他元素的总和，并比较总和。 最后，返回最小值。

**实现**：

## C++ 

```cpp

# include <bits/stdc++.h> 
# include <stdlib.h> /* for abs() */ 
# include <math.h> 

using namespace std; 
void minAbsSumPair(int arr[], int arr_size) 
{ 
    int inv_count = 0; 
    int l, r, min_sum, sum, min_l, min_r; 

    /* Array should have at least 
       two elements*/
    if(arr_size < 2) 
    { 
        cout << "Invalid Input"; 
        return; 
    } 

    /* Initialization of values */
    min_l = 0; 
    min_r = 1; 
    min_sum = arr[0] + arr[1]; 

    for(l = 0; l < arr_size - 1; l++) 
    { 
        for(r = l + 1; r < arr_size; r++) 
        { 
        sum = arr[l] + arr[r]; 
        if(abs(min_sum) > abs(sum)) 
        { 
            min_sum = sum; 
            min_l = l; 
            min_r = r; 
        } 
        } 
    } 

    cout << "The two elements whose sum is minimum are "
         << arr[min_l] << " and " << arr[min_r]; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = {1, 60, -10, 70, -80, 85}; 
    minAbsSumPair(arr, 6); 
    return 0; 
} 

// This code is contributed 
// by Akanksha Rai(Abby_akku) 

```

## C

```c

# include <stdio.h> 
# include <stdlib.h> /* for abs() */ 
# include <math.h> 
void minAbsSumPair(int arr[], int arr_size) 
{ 
  int inv_count = 0; 
  int l, r, min_sum, sum, min_l, min_r; 

  /* Array should have at least two elements*/
  if(arr_size < 2) 
  { 
    printf("Invalid Input"); 
    return; 
  } 

  /* Initialization of values */
  min_l = 0; 
  min_r = 1; 
  min_sum = arr[0] + arr[1]; 

  for(l = 0; l < arr_size - 1; l++) 
  { 
    for(r = l+1; r < arr_size; r++) 
    { 
      sum = arr[l] + arr[r]; 
      if(abs(min_sum) > abs(sum)) 
      { 
        min_sum = sum; 
        min_l = l; 
        min_r = r; 
      } 
    } 
  } 

  printf(" The two elements whose sum is minimum are %d and %d", 
          arr[min_l], arr[min_r]); 
} 

/* Driver program to test above function */
int main() 
{ 
  int arr[] = {1, 60, -10, 70, -80, 85}; 
  minAbsSumPair(arr, 6); 
  getchar(); 
  return 0; 
} 

```

## Java

```java

import java.util.*; 
import java.lang.*; 
class Main 
{ 
    static void minAbsSumPair(int arr[], int arr_size) 
    { 
      int inv_count = 0; 
      int l, r, min_sum, sum, min_l, min_r; 

      /* Array should have at least two elements*/
      if(arr_size < 2) 
      { 
        System.out.println("Invalid Input"); 
        return; 
      } 

      /* Initialization of values */
      min_l = 0; 
      min_r = 1; 
      min_sum = arr[0] + arr[1]; 

      for(l = 0; l < arr_size - 1; l++) 
      { 
        for(r = l+1; r < arr_size; r++) 
        { 
          sum = arr[l] + arr[r]; 
          if(Math.abs(min_sum) > Math.abs(sum)) 
          { 
            min_sum = sum; 
            min_l = l; 
            min_r = r; 
          } 
        } 
      } 

      System.out.println(" The two elements whose "+ 
                              "sum is minimum are "+ 
                        arr[min_l]+ " and "+arr[min_r]); 
    } 

    // main function 
    public static void main (String[] args)  
    { 
        int arr[] = {1, 60, -10, 70, -80, 85}; 
        minAbsSumPair(arr, 6); 
    } 

} 

```

## Python3

```py

# Python3 code to find Two elements 
# whose sum is closest to zero 

def minAbsSumPair(arr,arr_size): 
    inv_count = 0

    # Array should have at least 
    # two elements 
    if arr_size < 2: 
        print("Invalid Input") 
        return

    # Initialization of values  
    min_l = 0
    min_r = 1
    min_sum = arr[0] + arr[1] 
    for l in range (0, arr_size - 1): 
        for r in range (l + 1, arr_size): 
            sum = arr[l] + arr[r]                  
            if abs(min_sum) > abs(sum):          
                min_sum = sum
                min_l = l 
                min_r = r 

    print("The two elements whose sum is minimum are",  
            arr[min_l], "and ", arr[min_r]) 

# Driver program to test above function  
arr = [1, 60, -10, 70, -80, 85] 

minAbsSumPair(arr, 6); 

# This code is contributed by Smitha Dinesh Semwal 

```

## C# 

```cs

// C# code to find Two elements 
// whose sum is closest to zero 
using System; 

class GFG 
{ 
static void minAbsSumPair(int []arr, 
                        int arr_size) 
    { 

    int l, r, min_sum, sum, min_l, min_r; 

    /* Array should have at least two elements*/
    if (arr_size < 2) 
    { 
        Console.Write("Invalid Input"); 
        return; 
    } 

    /* Initialization of values */
    min_l = 0; 
    min_r = 1; 
    min_sum = arr[0] + arr[1]; 

    for (l = 0; l < arr_size - 1; l++) 
    { 
        for (r = l+1; r < arr_size; r++) 
        { 
            sum = arr[l] + arr[r]; 
            if (Math.Abs(min_sum) > Math.Abs(sum)) 
            { 
                min_sum = sum; 
                min_l = l; 
                min_r = r; 
            } 
        } 
    } 

    Console.Write(" The two elements whose "+ 
                        "sum is minimum are "+ 
                    arr[min_l]+ " and "+arr[min_r]); 
    } 

    // main function 
    public static void Main ()  
    { 
        int []arr = {1, 60, -10, 70, -80, 85}; 

        minAbsSumPair(arr, 6); 
    } 

} 

// This code is contributed by Sam007 

```

## PHP

```php

<?php 
// PHP program to find the Two elements 
// whose sum is closest to zero 

function minAbsSumPair($arr, $arr_size) 
{ 
    $inv_count = 0; 

    /* Array should have at 
    least two elements*/
    if($arr_size < 2) 
    { 
        echo "Invalid Input"; 
        return; 
    } 

    /* Initialization of values */
    $min_l = 0; 
    $min_r = 1; 
    $min_sum = $arr[0] + $arr[1]; 

    for($l = 0; $l < $arr_size - 1; $l++) 
    { 
        for($r = $l+1; $r < $arr_size; $r++) 
        { 
        $sum = $arr[$l] + $arr[$r]; 
        if(abs($min_sum) > abs($sum)) 
        { 
            $min_sum = $sum; 
            $min_l = $l; 
            $min_r = $r; 
        } 
        } 
    } 

    echo "The two elements whose sum is minimum are "
            .$arr[$min_l]." and ". $arr[$min_r]; 

} 

// Driver Code 
$arr = array(1, 60, -10, 70, -80, 85); 
minAbsSumPair($arr, 6); 

// This code is contributed by Sam007 
?> 

```

**输出**：

```
The two elements whose sum is minimum are -80 and 85

```

**时间复杂度**：`O(n ^ 2)`。

**方法 2（使用排序）**：

感谢 baskin 建议这种方法。 我们建议阅读[这篇文章](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/)，以了解此方法的背景知识。

**算法**：

1.  对输入数组的所有元素进行排序。

2.  使用两个索引变量`l`和`r`分别从左端和右端遍历。 将`l`初始化为 0，将`r`初始化为`n-1`。

3.  `sum = a[l] + a[r]`。

4.  如果`sum`为`-ve`，则`l++`。

5.  如果`sum`为`+ve`，则`r–-`。

6.  跟踪绝对最低总数。

7.  当`l < r`重复步骤 3、4、5 和 6。

**实现**：

## C++

```
#include <bits/stdc++.h> 
using namespace std; 
  
void quickSort(int *, int, int);  
  
/* Function to print pair of elements 
   having minimum sum */
void minAbsSumPair(int arr[], int n)  
{  
          
    // Variables to keep track  
    // of current sum and minimum sum  
    int sum, min_sum = INT_MAX;  
      
    // left and right index variables  
    int l = 0, r = n-1;  
      
    // variable to keep track of  
    // the left and right pair for min_sum  
    int min_l = l, min_r = n-1;  
      
    /* Array should have at least two elements*/
    if(n < 2)  
    {  
        cout << "Invalid Input";  
        return;  
    }  
      
    /* Sort the elements */
    quickSort(arr, l, r);  
      
    while(l < r)  
    {  
        sum = arr[l] + arr[r];  
      
        /*If abs(sum) is less  
          then update the result items*/
        if(abs(sum) < abs(min_sum))  
        {  
            min_sum = sum;  
            min_l = l;  
            min_r = r;  
        }  
        if(sum < 0)  
            l++;  
        else
            r--;  
    }  
      
    cout << "The two elements whose sum is minimum are " 
         << arr[min_l] << " and " << arr[min_r];  
}  
  
// Driver Code 
int main()  
{  
    int arr[] = {1, 60, -10, 70, -80, 85};  
    int n = sizeof(arr) / sizeof(arr[0]);  
    minAbsSumPair(arr, n);  
    return 0;  
}  
  
/* FOLLOWING FUNCTIONS ARE ONLY FOR  
   SORTING PURPOSE */
void exchange(int *a, int *b)  
{  
    int temp;  
    temp = *a;  
    *a = *b;  
    *b = temp;  
}  
  
int partition(int arr[], int si, int ei)  
{  
    int x = arr[ei];  
    int i = (si - 1);  
    int j;  
      
    for (j = si; j <= ei - 1; j++)  
    {  
        if(arr[j] <= x)  
        {  
            i++;  
            exchange(&arr[i], &arr[j]);  
        }  
    }  
    exchange (&arr[i + 1], &arr[ei]);  
    return (i + 1);  
}  
  
/* Implementation of Quick Sort  
arr[] --> Array to be sorted  
si --> Starting index  
ei --> Ending index  
*/
void quickSort(int arr[], int si, int ei)  
{  
    int pi; /* Partitioning index */
    if(si < ei)  
    {  
        pi = partition(arr, si, ei);  
        quickSort(arr, si, pi - 1);  
        quickSort(arr, pi + 1, ei);  
    }  
}  
  
// This code is contributed by rathbhupendra
```

## C

```
# include <stdio.h> 
# include <math.h> 
# include <limits.h> 
  
void quickSort(int *, int, int); 
  
/* Function to print pair of elements having minimum sum */
void minAbsSumPair(int arr[], int n) 
{ 
  // Variables to keep track of current sum and minimum sum 
  int sum, min_sum = INT_MAX; 
  
  // left and right index variables 
  int l = 0, r = n-1; 
  
  // variable to keep track of the left and right pair for min_sum 
  int min_l = l, min_r = n-1; 
  
  /* Array should have at least two elements*/
  if(n < 2) 
  { 
    printf("Invalid Input"); 
    return; 
  } 
  
  /* Sort the elements */
  quickSort(arr, l, r); 
  
  while(l < r) 
  { 
    sum = arr[l] + arr[r]; 
  
    /*If abs(sum) is less then update the result items*/
    if(abs(sum) < abs(min_sum)) 
    { 
      min_sum = sum; 
      min_l = l; 
      min_r = r; 
    } 
    if(sum < 0) 
      l++; 
    else
      r--; 
  } 
  
  printf(" The two elements whose sum is minimum are %d and %d", 
          arr[min_l], arr[min_r]); 
} 
  
/* Driver program to test above function */
int main() 
{ 
  int arr[] = {1, 60, -10, 70, -80, 85}; 
  int n = sizeof(arr)/sizeof(arr[0]); 
  minAbsSumPair(arr, n); 
  getchar(); 
  return 0; 
} 
  
/* FOLLOWING FUNCTIONS ARE ONLY FOR SORTING 
    PURPOSE */
void exchange(int *a, int *b) 
{ 
  int temp; 
  temp = *a; 
  *a   = *b; 
  *b   = temp; 
} 
  
int partition(int arr[], int si, int ei) 
{ 
  int x = arr[ei]; 
  int i = (si - 1); 
  int j; 
  
  for (j = si; j <= ei - 1; j++) 
  { 
    if(arr[j] <= x) 
    { 
      i++; 
      exchange(&arr[i], &arr[j]); 
    } 
  } 
  
  exchange (&arr[i + 1], &arr[ei]); 
  return (i + 1); 
} 
  
/* Implementation of Quick Sort 
arr[] --> Array to be sorted 
si  --> Starting index 
ei  --> Ending index 
*/
void quickSort(int arr[], int si, int ei) 
{ 
  int pi;    /* Partitioning index */
  if(si < ei) 
  { 
    pi = partition(arr, si, ei); 
    quickSort(arr, si, pi - 1); 
    quickSort(arr, pi + 1, ei); 
  } 
}
```

## Java

```
import java.util.*; 
import java.lang.*; 
class Main 
{ 
    static void minAbsSumPair(int arr[], int n) 
    { 
      // Variables to keep track of current sum and minimum sum 
      int sum, min_sum = 999999; 
       
      // left and right index variables 
      int l = 0, r = n-1; 
       
      // variable to keep track of the left and right pair for min_sum 
      int min_l = l, min_r = n-1; 
       
      /* Array should have at least two elements*/
      if(n < 2) 
      { 
        System.out.println("Invalid Input"); 
        return; 
      } 
       
      /* Sort the elements */
      sort(arr, l, r); 
       
      while(l < r) 
      { 
        sum = arr[l] + arr[r]; 
       
        /*If abs(sum) is less then update the result items*/
        if(Math.abs(sum) < Math.abs(min_sum)) 
        { 
          min_sum = sum; 
          min_l = l; 
          min_r = r; 
        } 
        if(sum < 0) 
          l++; 
        else
          r--; 
      } 
       
        
      System.out.println(" The two elements whose "+ 
                              "sum is minimum are "+ 
                        arr[min_l]+ " and "+arr[min_r]); 
    } 
       
    // main function 
    public static void main (String[] args)  
    { 
        int arr[] = {1, 60, -10, 70, -80, 85}; 
        int n = arr.length; 
        minAbsSumPair(arr, n); 
    } 
      
    /* Functions for QuickSort */
      
    /* This function takes last element as pivot, 
       places the pivot element at its correct 
       position in sorted array, and places all 
       smaller (smaller than pivot) to left of 
       pivot and all greater elements to right 
       of pivot */
    static int partition(int arr[], int low, int high) 
    { 
        int pivot = arr[high];  
        int i = (low-1); // index of smaller element 
        for (int j=low; j<high; j++) 
        { 
            // If current element is smaller than or 
            // equal to pivot 
            if (arr[j] <= pivot) 
            { 
                i++; 
  
                // swap arr[i] and arr[j] 
                int temp = arr[i]; 
                arr[i] = arr[j]; 
                arr[j] = temp; 
            } 
        } 
  
        // swap arr[i+1] and arr[high] (or pivot) 
        int temp = arr[i+1]; 
        arr[i+1] = arr[high]; 
        arr[high] = temp; 
  
        return i+1; 
    } 
  
  
    /* The main function that implements QuickSort() 
      arr[] --> Array to be sorted, 
      low  --> Starting index, 
      high  --> Ending index */
    static void sort(int arr[], int low, int high) 
    { 
        if (low < high) 
        { 
            /* pi is partitioning index, arr[pi] is  
              now at right place */
            int pi = partition(arr, low, high); 
  
            // Recursively sort elements before 
            // partition and after partition 
            sort(arr, low, pi-1); 
            sort(arr, pi+1, high); 
        } 
    } 
}
```

## Python3

```
# Function to prpair of elements 
# having minimum sum */ 
  
# FOLLOWING FUNCTIONS ARE ONLY FOR 
# SORTING PURPOSE */ 
def partition(arr, si, ei): 
    x = arr[ei] 
    i = (si - 1) 
  
    for j in range(si,ei): 
        if(arr[j] <= x): 
            i += 1
            arr[i], arr[j] = arr[j], arr[i] 
    arr[i + 1], arr[ei] = arr[ei], arr[i + 1] 
    return (i + 1)  
  
# Implementation of Quick Sort 
# arr[] --> Array to be sorted 
# si --> Starting index 
# ei --> Ending index 
def quickSort(arr, si, ei): 
    pi = 0 # Partitioning index */ 
    if(si < ei): 
        pi = partition(arr, si, ei) 
        quickSort(arr, si, pi - 1) 
        quickSort(arr, pi + 1, ei) 
  
def minAbsSumPair(arr, n): 
  
    # Variables to keep track 
    # of current sum and minimum sum 
    sum, min_sum = 0, 10**9
  
    # left and right index variables 
    l = 0
    r = n - 1
  
    # variable to keep track of 
    # the left and right pair for min_sum 
    min_l = l 
    min_r = n - 1
  
    # Array should have at least two elements*/ 
    if(n < 2): 
        print("Invalid Input", end = "") 
        return
  
    # Sort the elements */ 
    quickSort(arr, l, r) 
  
    while(l < r): 
        sum = arr[l] + arr[r] 
  
        # If abs(sum) is less 
        # then update the result items 
        if(abs(sum) < abs(min_sum)): 
            min_sum = sum
            min_l = l 
            min_r = r 
        if(sum < 0): 
            l += 1
        else: 
            r -= 1
  
    print("The two elements whose sum is minimum are",  
                        arr[min_l], "and", arr[min_r]) 
  
# Driver Code 
arr = [1, 60, -10, 70, -80, 85]  
n = len(arr) 
minAbsSumPair(arr, n) 
  
# This code is contributed by mohit kumar 29
```

## C#

```
using System; 
  
class GFG 
{ 
    static void minAbsSumPair(int []arr ,int n) 
    { 
        // Variables to keep track  
        // of current sum and minimum sum 
        int sum, min_sum = 999999; 
          
        // left and right index variables 
        int l = 0, r = n-1; 
          
        // variable to keep track of the left 
        // and right pair for min_sum 
        int min_l = l, min_r = n-1; 
          
        /* Array should have at least two elements*/
        if (n < 2) 
        { 
            Console.Write("Invalid Input"); 
            return; 
        } 
          
        /* Sort the elements */
        sort(arr, l, r); 
          
        while(l < r) 
        { 
            sum = arr[l] + arr[r]; 
          
            /*If abs(sum) is less then update the result items*/
            if (Math.Abs(sum) < Math.Abs(min_sum)) 
            { 
                min_sum = sum; 
                min_l = l; 
                min_r = r; 
            } 
            if (sum < 0) 
                l++; 
            else
                r--; 
        } 
          
        Console.Write(" The two elements whose " +  
                                "sum is minimum are " + 
                            arr[min_l]+ " and " + arr[min_r]); 
    } 
      
    // driver code 
    public static void Main ()  
    { 
        int []arr = {1, 60, -10, 70, -80, 85}; 
        int n = arr.Length; 
          
        minAbsSumPair(arr, n); 
    } 
      
    /* Functions for QuickSort */
      
    /* This function takes last element as pivot, 
    places the pivot element at its correct 
    position in sorted array, and places all 
    smaller (smaller than pivot) to left of 
    pivot and all greater elements to right 
    of pivot */
    static int partition(int []arr, int low, int high) 
    { 
        int pivot = arr[high];  
        int i = (low-1); // index of smaller element 
          
        for (int j = low; j < high; j++) 
        { 
            // If current element is smaller than or 
            // equal to pivot 
            if (arr[j] <= pivot) 
            { 
                i++; 
  
                // swap arr[i] and arr[j] 
                int temp = arr[i]; 
                arr[i] = arr[j]; 
                arr[j] = temp; 
            } 
        } 
  
        // swap arr[i+1] and arr[high] (or pivot) 
        int temp1 = arr[i+1]; 
        arr[i+1] = arr[high]; 
        arr[high] = temp1; 
  
        return i+1; 
    } 
  
  
    /* The main function that implements QuickSort() 
    arr[] --> Array to be sorted, 
    low --> Starting index, 
    high --> Ending index */
    static void sort(int []arr, int low, int high) 
    { 
        if (low < high) 
        { 
            /* pi is partitioning index, arr[pi] is  
            now at right place */
            int pi = partition(arr, low, high); 
  
            // Recursively sort elements before 
            // partition and after partition 
            sort(arr, low, pi-1); 
            sort(arr, pi+1, high); 
        } 
    } 
} 
  
// This code is contributed by Sam007
```

输出：

```
The two elements whose sum is minimum are -80 and 85
```

时间复杂度：排序的复杂度和找到最佳对的复杂度`= O(nlogn) + O(n) = O(nlogn)`。

方法 2 的 STL 实现：

算法：

1.  使用其绝对值对输入数组的所有元素进行排序。
2.  如果`arr[i-1]`和`arr[i]`的绝对和小于绝对值`min`更新`min`，则检查它们的绝对和。
3.  使用两个变量存储元素的索引。

实现：

## C++

```
// C++ implementation using STL 
#include <bits/stdc++.h> 
using namespace std; 
  
// Modified to sort by abolute values 
bool compare(int x, int y) 
{ 
    return abs(x) < abs(y); 
} 
  
void findMinSum(int arr[], int n) 
{ 
    sort(arr, arr + n, compare); 
    int min = INT_MAX, x, y; 
    for (int i = 1; i < n; i++) { 
  
        // Absolute value shows how close it is to zero 
        if (abs(arr[i - 1] + arr[i]) <= min) { 
  
            // if found an even close value 
            // update min and store the index 
            min = abs(arr[i - 1] + arr[i]); 
            x = i - 1; 
            y = i; 
        } 
    } 
    cout << "The two elements whose sum is minimum are "
         << arr[x] << " and " << arr[y]; 
} 
  
// Driver code 
int main() 
{ 
  
    int arr[] = { 1, 60, -10, 70, -80, 85 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    findMinSum(arr, n); 
    return 0; 
    // This code is contributed by ceeyesharish 
}
```

输出：

```
The two elements whose sum is minimum are -80 and 85
```

时间复杂度：`O(nlogn)`。

空间复杂度：`O(1)`。