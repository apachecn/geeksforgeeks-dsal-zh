# 在排序的数组中搜索，插入和删除

> 原文： [https://www.geeksforgeeks.org/search-insert-and-delete-in-a-sorted-array/](https://www.geeksforgeeks.org/search-insert-and-delete-in-a-sorted-array/)

在此后搜索中，讨论了排序数组中的插入和删除操作。



**搜索操作**：

在排序数组中，可以使用[二分搜索](http://quiz.geeksforgeeks.org/binary-search/)来执行搜索操作。

![](img/c0f4731d3e0cb3c5d181088760286a87.png)

## C++ 

```cpp

// C++ program to implement binary search in sorted array 
#include <bits/stdc++.h> 
using namespace std; 

int binarySearch(int arr[], int low, int high, int key) 
{ 
    if (high < low) 
        return -1; 
    int mid = (low + high) / 2; /*low + (high - low)/2;*/
    if (key == arr[mid]) 
        return mid; 
    if (key > arr[mid]) 
        return binarySearch(arr, (mid + 1), high, key); 
    return binarySearch(arr, low, (mid - 1), key); 
} 

/* Driver code */
int main() 
{ 
    // Let us search 3 in below array 
    int arr[] = { 5, 6, 7, 8, 9, 10 }; 
    int n, key; 

    n = sizeof(arr) / sizeof(arr[0]); 
    key = 10; 

    cout << "Index: " << binarySearch(arr, 0, n, key) << endl; 
    return 0; 
} 

// This code is contributed by NamrataSrivastava1 

```

## C

```c

// C program to implement binary search in sorted array 
#include <stdio.h> 

int binarySearch(int arr[], int low, int high, int key) 
{ 
    if (high < low) 
        return -1; 
    int mid = (low + high) / 2; /*low + (high - low)/2;*/
    if (key == arr[mid]) 
        return mid; 
    if (key > arr[mid]) 
        return binarySearch(arr, (mid + 1), high, key); 
    return binarySearch(arr, low, (mid - 1), key); 
} 

/* Driver program to check above functions */
int main() 
{ 
    // Let us search 3 in below array 
    int arr[] = { 5, 6, 7, 8, 9, 10 }; 
    int n, key; 

    n = sizeof(arr) / sizeof(arr[0]); 
    key = 10; 

    printf("Index: %d\n", binarySearch(arr, 0, n, key)); 
    return 0; 
} 

```

## Java

```java

// Java program to implement binary 
// search in a sorted array 

class Main { 
    // function to implement 
    // binary search 
    static int binarySearch(int arr[], int low, int high, int key) 
    { 
        if (high < low) 
            return -1; 

        /*low + (high - low)/2;*/
        int mid = (low + high) / 2; 
        if (key == arr[mid]) 
            return mid; 
        if (key > arr[mid]) 
            return binarySearch(arr, (mid + 1), high, key); 
        return binarySearch(arr, low, (mid - 1), key); 
    } 

    /* Driver program to test above function */
    public static void main(String[] args) 
    { 
        int arr[] = { 5, 6, 7, 8, 9, 10 }; 
        int n, key; 
        n = arr.length; 
        key = 10; 

        System.out.println("Index: " + binarySearch(arr, 0, n, key)); 
    } 
} 

```

## Python3

```py

# python 3  program to implement 
# binary search in sorted array 

def binarySearch(arr, low, high, key): 

    if (high < low): 
        return -1
    # low + (high - low)/2 
    mid = (low + high)/2

    if (key == arr[int(mid)]): 
        return mid 

    if (key > arr[int(mid)]): 
        return binarySearch(arr, 
           (mid + 1), high, key) 

    return (binarySearch(arr, low, 
           (mid -1), key)) 

# Driver program to check above functions  
# Let us search 3 in below array 
arr = [5, 6, 7, 8, 9, 10] 
n = len(arr) 
key = 10
print("Index:", int(binarySearch(arr, 0, n, key) )) 

# This code is contributed by 
# Smitha Dinesh Semwal 

```

## C# 

```cs

using System; 

// C# program to implement binary 
// search in a sorted array 

public class GFG { 
    // function to implement 
    // binary search 
    public static int binarySearch(int[] arr, int low, int high, int key) 
    { 
        if (high < low) { 
            return -1; 
        } 

        /*low + (high - low)/2;*/
        int mid = (low + high) / 2; 
        if (key == arr[mid]) { 
            return mid; 
        } 
        if (key > arr[mid]) { 
            return binarySearch(arr, (mid + 1), high, key); 
        } 
        return binarySearch(arr, low, (mid - 1), key); 
    } 

    /* Driver program to test above function */
    public static void Main(string[] args) 
    { 
        int[] arr = new int[] { 5, 6, 7, 8, 9, 10 }; 
        int n, key; 
        n = arr.Length; 
        key = 10; 

        Console.WriteLine("Index: " + binarySearch(arr, 0, n, key)); 
    } 
} 

// This code is contributed by Shrikant13 

```

## PHP

```php

<?php 
// PHP program to implement 
// binary search in sorted array 

function binarySearch($arr, $low,  
                      $high, $key)  
{ 
    if ($high < $low)  
    return -1; 

    // low + (high - low)/2 
    $mid = ($low + $high) / 2; 

    if ($key == $arr[(int)$mid]) 
        return $mid; 

    if ($key > $arr[(int)$mid])  
        return binarySearch($arr, ($mid + 1),  
                            $high, $key); 

    return (binarySearch($arr, $low,  
                        ($mid -1), $key)); 
} 

// Driver Code 

// Let us search 3 in below array 
$arr = array(5, 6, 7, 8, 9, 10); 
$n = count($arr); 
$key = 10; 
echo "Index: ", (int)binarySearch($arr, 0,  
                                  $n, $key); 

// This code is contributed by 
// Srathore 
?> 

```

**输出**：

```
Index: 5

```

**插入操作**：

在未排序的数组中，插入操作比已排序的数组要快，这是因为我们不必关心元素放置的位置。

![](img/c1979fba349cca66801c1475cf220ce7.png)

## C++

```

// C++ program to implement insert operation in 
// an sorted array. 
#include <iostream> 
using namespace std; 

// Inserts a key in arr[] of given capacity. n is current 
// size of arr[]. This function returns n+1 if insertion 
// is successful, else n. 
int insertSorted(int arr[], int n, int key, int capacity) 
{ 
    // Cannot insert more elements if n is already 
    // more than or equal to capcity 
    if (n >= capacity) 
        return n; 

    int i; 
    for (i = n - 1; (i >= 0 && arr[i] > key); i--) 
        arr[i + 1] = arr[i]; 

    arr[i + 1] = key; 

    return (n + 1); 
} 

/* Driver code */
int main() 
{ 
    int arr[20] = { 12, 16, 20, 40, 50, 70 }; 
    int capacity = sizeof(arr) / sizeof(arr[0]); 
    int n = 6; 
    int i, key = 26; 

    cout<< "\nBefore Insertion: "; 
    for (i = 0; i < n; i++) 
        cout << arr[i] << " "; 

    // Inserting key 
    n = insertSorted(arr, n, key, capacity); 

    cout << "\nAfter Insertion: "; 
    for (i = 0; i < n; i++) 
        cout << arr[i]<< " "; 

    return 0; 
} 

// This code is contributed by SHUBHAMSINGH10 

```

## Java

```
// Java program to insert an
// element in a sorted array
 
class Main {
    // Inserts a key in arr[] of given
    // capacity.  n is current size of arr[].
    // This function returns n+1 if insertion
    // is successful, else n.
    static int insertSorted(int arr[], int n, int key, int capacity)
    {
        // Cannot insert more elements if n is already
        // more than or equal to capcity
        if (n >= capacity)
            return n;
 
        int i;
        for (i = n - 1; (i >= 0 && arr[i] > key); i--)
            arr[i + 1] = arr[i];
 
        arr[i + 1] = key;
 
        return (n + 1);
    }
 
    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = new int[20];
        arr[0] = 12;
        arr[1] = 16;
        arr[2] = 20;
        arr[3] = 40;
        arr[4] = 50;
        arr[5] = 70;
        int capacity = arr.length;
        int n = 6;
        int key = 26;
 
        System.out.print("\nBefore Insertion: ");
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
 
        // Inserting key
        n = insertSorted(arr, n, key, capacity);
 
        System.out.print("\nAfter Insertion: ");
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }
}
```

## Python3

```
# Python3 program to implement insert 
# operation in an sorted array.
 
# Inserts a key in arr[] of given capacity. 
# n is current size of arr[]. This function 
# returns n+1 if insertion is successful, else n.
def insertSorted(arr, n, key, capacity):
     
    # Cannot insert more elements if n is 
    # already more than or equal to capcity
    if (n >= capacity):
        return n
 
    i = n - 1
    while i >= 0 and arr[i] > key:
        arr[i + 1] = arr[i]
        i -= 1
 
    arr[i + 1] = key
 
    return (n + 1)
 
# Driver Code
arr = [12, 16, 20, 40, 50, 70]
 
for i in range(20):
    arr.append(0)
 
capacity = len(arr)
n = 6
key = 26
 
print("Before Insertion: ", end = " ");
for i in range(n):
    print(arr[i], end = " ")
     
# Inserting key
n = insertSorted(arr, n, key, capacity)
 
print("\nAfter Insertion: ", end = "")
for i in range(n):
    print(arr[i], end = " ")
 
# This code is contributed by Mohit Kumar
```

## C#

```
using System;
 
// C# program to insert an
// element in a sorted array
 
public class GFG {
    // Inserts a key in arr[] of given
    // capacity.  n is current size of arr[].
    // This function returns n+1 if insertion
    // is successful, else n.
    public static int insertSorted(int[] arr, int n, int key, int capacity)
    {
        // Cannot insert more elements if n is already
        // more than or equal to capcity
        if (n >= capacity) {
            return n;
        }
 
        int i;
        for (i = n - 1; (i >= 0 && arr[i] > key); i--) {
            arr[i + 1] = arr[i];
        }
 
        arr[i + 1] = key;
 
        return (n + 1);
    }
 
    /* Driver program to test above function */
    public static void Main(string[] args)
    {
        int[] arr = new int[20];
        arr[0] = 12;
        arr[1] = 16;
        arr[2] = 20;
        arr[3] = 40;
        arr[4] = 50;
        arr[5] = 70;
        int capacity = arr.Length;
        int n = 6;
        int key = 26;
 
        Console.Write("\nBefore Insertion: ");
        for (int i = 0; i < n; i++) {
            Console.Write(arr[i] + " ");
        }
 
        // Inserting key
        n = insertSorted(arr, n, key, capacity);
 
        Console.Write("\nAfter Insertion: ");
        for (int i = 0; i < n; i++) {
            Console.Write(arr[i] + " ");
        }
    }
}
 
// This code is contributed by Shrikant13
```

输出：

```
Array before deletion
10 20 30 40 50 

Array after deletion
10 20 40 50 
```

删除操作的时间复杂度：`O(n)`【在最坏的情况下，所有元素都可能必须移动】。

<https://www.youtube.com/watch?v=SX1rtrsJ4R4>