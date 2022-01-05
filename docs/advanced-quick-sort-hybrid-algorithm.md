# 高级快速排序(混合算法)

> 原文:[https://www . geesforgeks . org/advanced-quick-sort-hybrid-algorithm/](https://www.geeksforgeeks.org/advanced-quick-sort-hybrid-algorithm/)

**先决条件:** [插入排序](https://www.geeksforgeeks.org/insertion-sort/)、[快速排序](https://www.geeksforgeeks.org/quick-sort/)、[选择排序](https://www.geeksforgeeks.org/selection-sort/)
本文实现了[快速排序](https://www.geeksforgeeks.org/quick-sort/)和[插入排序](https://www.geeksforgeeks.org/insertion-sort/)相结合的混合算法。顾名思义，混合算法结合了多个算法。
**为什么混合算法:**
[快速排序](https://www.geeksforgeeks.org/quick-sort/)如果输入的大小很大，算法是高效的。但是，在小数组的情况下，[插入排序](https://www.geeksforgeeks.org/insertion-sort/)比快速排序更有效，因为与快速排序相比，比较和交换的数量更少。因此，我们将这两种算法结合起来，使用这两种方法进行高效排序。
**注:** [选择](https://www.geeksforgeeks.org/selection-sort/)算法也可以与[快速排序](https://www.geeksforgeeks.org/quick-sort/)结合使用。虽然时间复杂度为 O(N)<sup>2</sup>，但是这些算法在这种情况下被证明是有效的，因为这些算法仅在数组的大小小于阈值时使用(本文中的 **10** )。

**算法的试运行:**

> 让 arr[] = {24，97，40，67，88，85，15，66，53，44，26，48，16，52，45，23，90，18，49，80}
> 
> [![Example pictorial explanation](https://media.geeksforgeeks.org/wp-content/uploads/20200214193554/hybridgfg.png)](https://media.geeksforgeeks.org/wp-content/uploads/20200214193554/hybridgfg.png)
> 
> 示例说明

**方法:**思路是利用递归，不断寻找数组的大小。如果大小大于阈值(10)，则为该部分数组调用 quicksort 函数。否则，将调用插入排序。
下面是混合算法的实现:

## C++

```
// C++ implementation of the above approach

#include<bits/stdc++.h>
using namespace std;

// Function to perform the insertion sort

void insertion_sort(int arr[], int low, int n)
  {

    for(int i=low+1;i<n+1;i++)
    {
      int val = arr[i] ;
      int j = i ;
    while (j>low && arr[j-1]>val)
      {
        arr[j]= arr[j-1] ;
      j-= 1;
    }
    arr[j]= val ;
    }

  }

//The following two functions are used
// to perform quicksort on the array.

// Partition function for quicksort

int partition(int arr[], int low, int high)
{
  int pivot = arr[high] ;
  int i ,j;
  i = low;
  j = low;

  for (int i = low; i < high; i++)
     {
      if(arr[i]<pivot)
      {
        int temp = arr[i];
      arr[i] = arr[j];
      arr[j] = temp;
      j += 1;
      }
    }

    int temp = arr[j];
    arr[j] = arr[high];
    arr[high] = temp;

  return j;
  }

// Function to call the partition function
// and perform quick sort on the array

void quick_sort(int arr[], int low,int high)
{
  if (low < high)
  {
    int pivot = partition(arr, low, high);
    quick_sort(arr, low, pivot-1) ;
    quick_sort(arr, pivot + 1, high) ;

  }
}

// Hybrid function -> Quick + Insertion sort

void hybrid_quick_sort(int arr[], int low, int high)
{
  while (low < high)
    {

    // If the size of the array is less
    // than threshold apply insertion sort
    // and stop recursion

    if (high-low + 1 < 10)
      {
        insertion_sort(arr, low, high);
      break;
    }

    else

        {
          int pivot = partition(arr, low, high) ;

      // Optimised quicksort which works on
      // the smaller arrays first

      // If the left side of the pivot
      // is less than right, sort left part
      // and move to the right part of the array

      if (pivot-low<high-pivot)
        {
          hybrid_quick_sort(arr, low, pivot - 1);
        low = pivot + 1;
      }
      else
        {

        // If the right side of pivot is less
        // than left, sort right side and
        // move to the left side

        hybrid_quick_sort(arr, pivot + 1, high);
        high = pivot-1;
        }

     }

   }
}
// Driver Code
int main()
{
 int  arr[21] = { 24, 97, 40, 67, 88, 85, 15,
  66, 53, 44, 26, 48, 16, 52,
  45, 23, 90, 18, 49, 80, 23 };

hybrid_quick_sort(arr, 0, 20);

  for(int i = 0; i < 21; i++)
    cout << arr[i] << ", ";
}

// This code is contributed by ishayadav2918
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;
class GFG {

    private static void insertionSort(int a[], int low,
                                     int high)
    {
        for (int i = low + 1; i <= high; i++) {
            for (int j = i - 1; j >= low; j--) {
                if (a[j] > a[j + 1]) {
                    // Swap
                    int temp = a[j];
                    a[j] = a[j + 1];
                    a[j + 1] = temp;
                }
                else
                    break;
            }
        }
    }

    private static int partition(int arr[], int low,
                                int high)
    {
        int pivot = arr[high];
        int i = low;
        int j = low;

        while (i <= high) {
            if (arr[i] > pivot)
                i++;
            else {
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
                i++;
                j++;
            }
        }
        return j - 1;
    }

    public static void hybridQuickSort(int arr[], int low,
                                       int high)
    {
        while (low < high) {
            // Check if array size on which we will be working is less than 10
            if (high - low < 10) {
                insertionSort(arr, low, high);
                break;
            }
            else {
                int pivot = partition(arr, low, high);

                // We will do recursion on small size
                // subarray So we can check pivot - low  and
                // pivot - high

                if (pivot - low < pivot - high) {
                    hybridQuickSort(arr, low, pivot - 1);
                    low = pivot + 1;
                }
                else {
                    hybridQuickSort(arr, pivot + 1, high);
                    high = pivot - 1;
                }
            }
        }
    }

  // Driver code
    public static void main(String[] args)
    {

        int arr[]
            = { 24, 97, 40, 67, 88, 85, 15, 66, 53, 44, 26,
                48, 16, 52, 45, 23, 90, 18, 49, 80, 23 };

        hybridQuickSort(arr, 0, arr.length - 1);
        for (int i : arr)
            System.out.print(i + "  ");
    }
}

// This code is contribute  by @mahi_07
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to perform the insertion sort
def insertion_sort(arr, low, n):
    for i in range(low + 1, n + 1):
        val = arr[i]
        j = i
        while j>low and arr[j-1]>val:
            arr[j]= arr[j-1]
            j-= 1
        arr[j]= val

# The following two functions are used
# to perform quicksort on the array.

# Partition function for quicksort
def partition(arr, low, high):
    pivot = arr[high]
    i = j = low
    for i in range(low, high):
        if arr[i]<pivot:
            a[i], a[j]= a[j], a[i]
            j+= 1
    a[j], a[high]= a[high], a[j]
    return j

# Function to call the partition function
# and perform quick sort on the array
def quick_sort(arr, low, high):
    if low<high:
        pivot = partition(arr, low, high)
        quick_sort(arr, low, pivot-1)
        quick_sort(arr, pivot + 1, high)
        return arr

# Hybrid function -> Quick + Insertion sort
def hybrid_quick_sort(arr, low, high):
    while low<high:

        # If the size of the array is less
        # than threshold apply insertion sort
        # and stop recursion
        if high-low + 1<10:
            insertion_sort(arr, low, high)
            break

        else:
            pivot = partition(arr, low, high)

            # Optimised quicksort which works on
            # the smaller arrays first

            # If the left side of the pivot
            # is less than right, sort left part
            # and move to the right part of the array
            if pivot-low<high-pivot:
                hybrid_quick_sort(arr, low, pivot-1)
                low = pivot + 1
            else:
                # If the right side of pivot is less
                # than left, sort right side and
                # move to the left side
                hybrid_quick_sort(arr, pivot + 1, high)
                high = pivot-1

# Driver code

a = [ 24, 97, 40, 67, 88, 85, 15,
      66, 53, 44, 26, 48, 16, 52,
      45, 23, 90, 18, 49, 80, 23 ]
hybrid_quick_sort(a, 0, 20)
print(a)
```

**Output**

```
15, 16, 18, 23, 23, 24, 26, 40, 44, 45, 48, 49, 52, 53, 66, 67, 80, 85, 88, 90, 97, 
```

**时间复杂度:**o(n^2)
T3】辅助空间: O(N)