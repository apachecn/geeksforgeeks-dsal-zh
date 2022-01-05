# 最慢的排序算法

> 原文:[https://www . geesforgeks . org/最慢排序算法/](https://www.geeksforgeeks.org/the-slowest-sorting-algorithms/)

一种[排序算法](https://www.geeksforgeeks.org/sorting-algorithms/)用于根据元素上的比较运算符重新排列给定的数组或列表元素。比较运算符用于确定元素在相应的[数据结构](https://www.geeksforgeeks.org/data-structures/)中的新顺序。但是下面是一些最慢的排序算法:

[**走狗排序:**](https://www.geeksforgeeks.org/stooge-sort/) 走狗排序是一种[递归](https://www.geeksforgeeks.org/recursion/)排序算法。它递归地对数组进行部分划分和[排序。以下是排序的步骤:](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)

[*   If the value of index **0** is greater than that of the last index, exchange them.*   If the number of elements in the array is greater than 2:
    *   Recursively call the [T0】 stoogsort 【T1] function to get the initial **2/3 element** of the array.
    *   Recursively call the **function of the last **2/3 element** of the array.**
    *   Recursively call the [T2】 stoogsort 【T3] function of the initial **2/3 element** again to confirm whether the result array is sorted.*   Print the sorted array.](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)

下面是上述方法的实现:

## c++

```
// C++ program for the stooge sort
#include <iostream>
using namespace std;

// Function to implement stooge sort
void stoogesort(int arr[], int l, int h)
{
    // Base Case
    if (l >= h)
        return;

    // If first element is smaller than
    // last element, swap them
    if (arr[l] > arr[h])
        swap(arr[l], arr[h]);

    // If there are more than 2 elements
    // in the array
    if (h - l + 1 > 2) {
        int t = (h - l + 1) / 3;

        // Recursively sort the first
        // 2/3 elements
        stoogesort(arr, l, h - t);

        // Recursively sort the last
        // 2/3 elements
        stoogesort(arr, l + t, h);

        // Recursively sort the first
        // 2/3 elements again
        stoogesort(arr, l, h - t);
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 5, 3, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    stoogesort(arr, 0, N - 1);

    // Display the sorted array
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }

    return 0;
}
```

## Java

```
// Java program for the
// stooge sort
class GFG{

// Function to implement
// stooge sort
static void stoogesort(int arr[],
                       int l, int h)
{
  // Base Case
  if (l >= h)
    return;

  // If first element is smaller
  // than last element, swap them
  if (arr[l] > arr[h])
  {
    int temp = arr[l];
    arr[l] = arr[h];
    arr[h] = temp;
  }

  // If there are more than
  // 2 elements in the array
  if (h - l + 1 > 2)
  {
    int t = (h - l + 1) / 3;

    // Recursively sort the
    // first 2/3 elements
    stoogesort(arr, l, h - t);

    // Recursively sort the
    // last 2/3 elements
    stoogesort(arr, l + t, h);

    // Recursively sort the
    // first 2/3 elements again
    stoogesort(arr, l, h - t);
  }
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {2, 4, 5, 3, 1};
  int N = arr.length;

  // Function Call
  stoogesort(arr, 0, N - 1);

  // Display the sorted array
  for (int i = 0; i < N; i++)
  {
    System.out.print(arr[i] + " ");
  }
}
}

// This code is contributed by Chitranayal
```

## python 3

```
# Python3 program for the stooge sort

# Function to implement stooge sort
def stoogesort(arr, l, h):

    # Base Case
    if (l >= h):
        return

    # If first element is smaller than
    # last element, swap them
    if (arr[l] > arr[h]):
        temp = arr[l]
        arr[l] = arr[h]
        arr[h] = temp

    # If there are more than 2 elements
    # in the array
    if (h - l + 1 > 2):
        t = (h - l + 1) // 3

        # Recursively sort the first
        # 2/3 elements
        stoogesort(arr, l, h - t)

        # Recursively sort the last
        # 2/3 elements
        stoogesort(arr, l + t, h)

        # Recursively sort the first
        # 2/3 elements again
        stoogesort(arr, l, h - t)

# Driver Code
arr = [ 2, 4, 5, 3, 1 ]
N = len(arr)

# Function Call
stoogesort(arr, 0, N - 1)

# Display the sorted array
for i in range(N):
    print(arr[i], end = " ")

# This code is contributed by code_hunt
```

## c#

T3

## Javascript

```
<script>

// Javascript program for the
// stooge sort

// Function to implement
// stooge sort
function stoogesort(arr, l, h)
{

    // Base Case
    if (l >= h)
        return;

    // If first element is smaller
    // than last element, swap them
    if (arr[l] > arr[h])
    {
        let temp = arr[l];
        arr[l] = arr[h];
        arr[h] = temp;
    }

    // If there are more than
    // 2 elements in the array
    if (h - l + 1 > 2)
    {
        let t = Math.floor((h - l + 1) / 3);

        // Recursively sort the
        // first 2/3 elements
        stoogesort(arr, l, h - t);

        // Recursively sort the
        // last 2/3 elements
        stoogesort(arr, l + t, h);

        // Recursively sort the
        // first 2/3 elements again
        stoogesort(arr, l, h - t);
    }
}

// Driver Code
let arr = [ 2, 4, 5, 3, 1 ];
let N = arr.length;

// Function Call
stoogesort(arr, 0, N - 1);

// Display the sorted array
for (let i = 0; i < N; i++)
{
    document.write(arr[i] + " ");
}

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
1 2 3 4 5
```