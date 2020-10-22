# 在无限排序数组中查找元素的位置

> 原文： [https://www.geeksforgeeks.org/find-position-element-sorted-array-infinite-numbers/](https://www.geeksforgeeks.org/find-position-element-sorted-array-infinite-numbers/)

假设您有一个无穷个排序数组，那么如何搜索数组中的元素？

资料来源：Amazon 面试经历。

由于数组已排序，因此首先想到的是二分搜索，但是这里的问题是我们不知道数组的大小。

如果数组是无限的，则意味着我们没有适当的界限来应用二分搜索。 因此，为了找到键的位置，我们首先找到边界，然后应用二分搜索算法。

让`low`指向数组的第一个元素，`high`指向数组的第二个元素，现在将键与高索引元素进行比较，如果大于高索引元素，则将高索引复制到低索引中并将高索引加倍。如果较小，则对找到的高低索引进行二分搜索。



以下是上述算法的实现：

## C++ 

```cpp

// C++ program to demonstrate working of an algorithm that finds 
// an element in an array of infinite size 
#include<bits/stdc++.h> 
using namespace std; 

// Simple binary search algorithm 
int binarySearch(int arr[], int l, int r, int x) 
{ 
    if (r>=l) 
    { 
        int mid = l + (r - l)/2; 
        if (arr[mid] == x) 
            return mid; 
        if (arr[mid] > x) 
            return binarySearch(arr, l, mid-1, x); 
        return binarySearch(arr, mid+1, r, x); 
    } 
    return -1; 
} 

// function takes an infinite size array and a key to be 
//  searched and returns its position if found else -1\. 
// We don't know size of arr[] and we can assume size to be 
// infinite in this function. 
// NOTE THAT THIS FUNCTION ASSUMES arr[] TO BE OF INFINITE SIZE 
// THEREFORE, THERE IS NO INDEX OUT OF BOUND CHECKING 
int findPos(int arr[], int key) 
{ 
    int l = 0, h = 1; 
    int val = arr[0]; 

    // Find h to do binary search 
    while (val < key) 
    { 
        l = h;        // store previous high 
        h = 2*h;      // double high index 
        val = arr[h]; // update new val 
    } 

    // at this point we have updated low and 
    // high indices, Thus use binary search  
    // between them 
    return binarySearch(arr, l, h, key); 
} 

// Driver program 
int main() 
{ 
    int arr[] = {3, 5, 7, 9, 10, 90, 100, 130,  
                               140, 160, 170}; 
    int ans = findPos(arr, 10); 
    if (ans==-1) 
        cout << "Element not found"; 
    else
        cout << "Element found at index " << ans; 
    return 0; 
} 

```

## Java

```java

// Java program to demonstrate working of  
// an algorithm that finds an element in an  
// array of infinite size 

class Test 
{ 
    // Simple binary search algorithm 
    static int binarySearch(int arr[], int l, int r, int x) 
    { 
        if (r>=l) 
        { 
            int mid = l + (r - l)/2; 
            if (arr[mid] == x) 
                return mid; 
            if (arr[mid] > x) 
                return binarySearch(arr, l, mid-1, x); 
            return binarySearch(arr, mid+1, r, x); 
        } 
        return -1; 
    } 

    // Method takes an infinite size array and a key to be 
    // searched and returns its position if found else -1\. 
    // We don't know size of arr[] and we can assume size to be 
    // infinite in this function. 
    // NOTE THAT THIS FUNCTION ASSUMES arr[] TO BE OF INFINITE SIZE 
    // THEREFORE, THERE IS NO INDEX OUT OF BOUND CHECKING 
    static int findPos(int arr[],int key)  
    { 
        int l = 0, h = 1; 
        int val = arr[0]; 

        // Find h to do binary search 
        while (val < key) 
        { 
            l = h;     // store previous high 
            //check that 2*h doesn't exceeds array  
            //length to prevent ArrayOutOfBoundException 
            if(2*h < arr.length-1) 
               h = 2*h;              
            else
               h = arr.length-1; 

            val = arr[h]; // update new val 
        } 

        // at this point we have updated low 
        // and high indices, thus use binary  
        // search between them 
        return binarySearch(arr, l, h, key); 
    } 

    // Driver method to test the above function 
    public static void main(String[] args)  
    { 
        int arr[] = new int[]{3, 5, 7, 9, 10, 90,  
                            100, 130, 140, 160, 170}; 
        int ans = findPos(arr,10); 

        if (ans==-1) 
            System.out.println("Element not found"); 
        else
            System.out.println("Element found at index " + ans); 
    } 
} 

```

## Python

```py

# Python Program to demonstrate working of an algorithm that finds 
# an element in an array of infinite size 

# Binary search algorithm implementation 
def binary_search(arr,l,r,x): 

    if r >= l: 
        mid = l+(r-l)/2

        if arr[mid] == x: 
            return mid 

        if arr[mid] > x: 
            return binary_search(arr,l,mid-1,x) 

        return binary_search(arr,mid+1,r,x) 

    return -1

# function takes an infinite size array and a key to be 
# searched and returns its position if found else -1\. 
# We don't know size of a[] and we can assume size to be 
# infinite in this function. 
# NOTE THAT THIS FUNCTION ASSUMES a[] TO BE OF INFINITE SIZE 
# THEREFORE, THERE IS NO INDEX OUT OF BOUND CHECKING 
def findPos(a, key): 

    l, h, val = 0, 1, arr[0] 

    # Find h to do binary search 
    while val < key: 
        l = h            #store previous high 
        h = 2*h          #double high index 
        val = arr[h]       #update new val 

    # at this point we have updated low and high indices, 
    # thus use binary search between them 
    return binary_search(a, l, h, key) 

# Driver function 
arr = [3, 5, 7, 9, 10, 90, 100, 130, 140, 160, 170] 
ans = findPos(arr,10) 
if ans == -1: 
    print "Element not found"
else: 
    print"Element found at index",ans 

# This code is contributed by __Devesh Agrawal__ 

```

## C# 

```cs

// C# program to demonstrate working of an  
// algorithm that finds an element in an 
// array of infinite size 
using System; 

class GFG { 

    // Simple binary search algorithm 
    static int binarySearch(int []arr, int l, 
                                int r, int x) 
    { 
        if (r >= l) 
        { 
            int mid = l + (r - l)/2; 

            if (arr[mid] == x) 
                return mid; 
            if (arr[mid] > x) 
                return binarySearch(arr, l,  
                                   mid-1, x); 

            return binarySearch(arr, mid+1, 
                                       r, x); 
        } 

        return -1; 
    } 

    // Method takes an infinite size array 
    // and a key to be searched and returns 
    // its position if found else -1\. We 
    // don't know size of arr[] and we can 
    // assume size to be infinite in this  
    // function. 
    // NOTE THAT THIS FUNCTION ASSUMES  
    // arr[] TO BE OF INFINITE SIZE 
    // THEREFORE, THERE IS NO INDEX OUT  
    // OF BOUND CHECKING 
    static int findPos(int []arr,int key)  
    { 
        int l = 0, h = 1; 
        int val = arr[0]; 

        // Find h to do binary search 
        while (val < key) 
        { 
            l = h;     // store previous high 
            h = 2 * h;// double high index 
            val = arr[h]; // update new val 
        } 

        // at this point we have updated low 
        // and high indices, thus use binary  
        // search between them 
        return binarySearch(arr, l, h, key); 
    } 

    // Driver method to test the above 
    // function 
    public static void Main()  
    { 
        int []arr = new int[]{3, 5, 7, 9, 
            10, 90, 100, 130, 140, 160, 170}; 
        int ans = findPos(arr, 10); 

        if (ans == -1) 
            Console.Write("Element not found"); 
        else
            Console.Write("Element found at "
                            + "index " + ans); 
    } 
} 

// This code is contributed by nitin mittal. 

```

## PHP

```php

<?php 
// PHP program to demonstrate working 
// of an algorithm that finds an  
// element in an array of infinite size 

// Simple binary search algorithm 
function binarySearch($arr, $l,  
                      $r, $x) 
{ 
    if ($r >= $l) 
    { 
        $mid = $l + ($r - $l)/2; 
        if ($arr[$mid] == $x) 
            return $mid; 
        if ($arr[$mid] > $x) 
            return binarySearch($arr, $l,  
                           $mid - 1, $x); 
        return binarySearch($arr, $mid + 1, 
                                   $r, $x); 
    } 
    return -1; 
} 

// function takes an infinite 
// size array and a key to be 
// searched and returns its  
// position if found else -1\. 
// We don't know size of arr[]  
// and we can assume size to be 
// infinite in this function. 
// NOTE THAT THIS FUNCTION ASSUMES 
// arr[] TO BE OF INFINITE SIZE 
// THEREFORE, THERE IS NO INDEX  
// OUT OF BOUND CHECKING 
function findPos( $arr, $key) 
{ 
    $l = 0; $h = 1; 
    $val = $arr[0]; 

    // Find h to do binary search 
    while ($val < $key) 
    { 

        // store previous high 
        $l = $h;      

         // double high index 
        $h = 2 * $h; 

        // update new val 
        $val = $arr[$h];  
    } 

    // at this point we have 
    // updated low and high  
    // indices, Thus use binary 
    // search between them 
    return binarySearch($arr, $l,  
                        $h, $key); 
} 

    // Driver Code 
    $arr = array(3, 5, 7, 9, 10, 90, 100, 
                 130, 140, 160, 170); 
    $ans = findPos($arr, 10); 
    if ($ans==-1) 
        echo "Element not found"; 
    else
        echo "Element found at index " , $ans; 

// This code is contributed by anuj_67\. 
?> 

```

输出：

```
Element found at index 4
```

令`p`为要搜索元素的位置。 查找高索引`h`的步骤数为`O(Log p)`。 `h`的值必须小于`2 * p`。` h / 2`和`h`之间的元素数必须为`O(p)`。 因此，二分搜索步骤的时间复杂度也为`O(Log p)`，总时间复杂度为`2 * O(Log p)`，即`O(Log p)`。

