# 对 0、1 和 2s 的数组进行排序(简单计数)

> 原文:[https://www . geesforgeks . org/sort-array-0s-1s-2s-simple-counting/](https://www.geeksforgeeks.org/sort-array-0s-1s-2s-simple-counting/)

给定一个由 0、1 和 2s 组成的数组 A[]，编写一个对 A[]进行排序的函数。这些函数应该将全 0 放在第一位，然后全 1 和全 2 放在最后。

示例:

```
Input :  {0, 1, 2, 0, 1, 2}
Output : {0, 0, 1, 1, 2, 2}

Input :  {0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1}
Output : {0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2}
```

计算 0、1 和 2 的数量。计数后，将所有 0 放在第一位，然后是 1，最后是 2。我们遍历数组两次。时间复杂度将为 0(n)。

## c++

```
// Simple C++ program to sort an array of 0s
// 1s and 2s.
#include <iostream>
using namespace std;

void sort012(int* arr, int n)
{
    // Variables to maintain the count of 0's,
    // 1's and 2's in the array
    int count0 = 0, count1 = 0, count2 = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] == 0)
            count0++;
        if (arr[i] == 1)
            count1++;
        if (arr[i] == 2)
            count2++;
    }

    // Putting the 0's in the array in starting.
    for (int i = 0; i < count0; i++)
        arr[i] = 0;

    // Putting the 1's in the array after the 0's.
    for (int i = count0; i < (count0 + count1); i++)
        arr[i] = 1;

    // Putting the 2's in the array after the 1's
    for (int i = (count0 + count1); i < n; i++)
        arr[i] = 2;

    return;
}

// Prints the array
void printArray(int* arr, int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

// Driver code
int main()
{
    int arr[] = { 0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    sort012(arr, n);
    printArray(arr, n);
    return 0;
}
```

## Java

```
// Simple Java program
// to sort an array of 0s
// 1s and 2s.
import java.util.*;
import java.lang.*;

public class GfG{

    public static void sort012(int arr[], int n)
    {
        // Variables to maintain
        // the count of 0's,
        // 1's and 2's in the array
        int count0 = 0, count1 = 0;
        int count2 = 0;
        for (int i = 0; i < n; i++) {
            if (arr[i] == 0)
                count0++;
            if (arr[i] == 1)
                count1++;
            if (arr[i] == 2)
                count2++;
        }

        // Putting the 0's in the
        // array in starting.
        for (int i = 0; i < count0; i++)
            arr[i] = 0;

        // Putting the 1's in the
        // array after the 0's.
        for (int i = count0; i <
            (count0 + count1); i++)
            arr[i] = 1;

        // Putting the 2's in the
        // array after the 1's
        for (int i = (count0 + count1);
            i < n; i++)
            arr[i] = 2;

        printArray(arr, n);
    }

    // Prints the array
    public static void printArray(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    // Driver function
    public static void main(String args[])
    {

        int arr[] = { 0, 1, 1, 0, 1, 2, 1,
                    2, 0, 0, 0, 1 };
        int n = 12;
        sort012(arr, n);
    }
}

// This code is contributed by Sagar Shukla
```

## python 3

```
# Python C++ program to sort an array of 0s
# 1s and 2s.
import math

def sort012(arr, n):

    # Variables to maintain the count of 0's,
    # 1's and 2's in the array
    count0 = 0
    count1 = 0
    count2 = 0
    for i in range(0,n):
        if (arr[i] == 0):
            count0=count0+1
        if (arr[i] == 1):
            count1=count1+1
        if (arr[i] == 2):
            count2=count2+1

    # Putting the 0's in the array in starting.
    for i in range(0,count0):
        arr[i] = 0

    # Putting the 1's in the array after the 0's.
    for i in range( count0, (count0 + count1)) :
        arr[i] = 1

    # Putting the 2's in the array after the 1's
    for i in range((count0 + count1),n) :
        arr[i] = 2

    return

# Prints the array
def printArray( arr,  n):

    for i in range(0,n):
        print( arr[i] , end=" ")
    print()

# Driver code
arr = [ 0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1 ]
n = len(arr)
sort012(arr, n)
printArray(arr, n)

# This code is contributed by Gitanjali.
```

## c#

```
// Simple C# program
// to sort an array of 0s
// 1s and 2s.
using System;

public class GfG{

    public static void sort012(int []arr, int n)
    {
        // Variables to maintain
        // the count of 0's,
        // 1's and 2's in the array
        int count0 = 0, count1 = 0;
        int count2 = 0;
        for (int i = 0; i < n; i++) {
            if (arr[i] == 0)
                count0++;
            if (arr[i] == 1)
                count1++;
            if (arr[i] == 2)
                count2++;
        }

        // Putting the 0's in the
        // array in starting.
        for (int i = 0; i < count0; i++)
            arr[i] = 0;

        // Putting the 1's in the
        // array after the 0's.
        for (int i = count0; i <
            (count0 + count1); i++)
            arr[i] = 1;

        // Putting the 2's in the
        // array after the 1's
        for (int i = (count0 + count1);
            i < n; i++)
            arr[i] = 2;

        printArray(arr, n);
    }

    // Prints the array
    public static void printArray(int []arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
        Console.WriteLine();
    }

    // Driver function
    public static void Main()
    {

        int []arr = { 0, 1, 1, 0, 1, 2, 1,
                    2, 0, 0, 0, 1 };
        int n = 12;
        sort012(arr, n);
    }
}

// This code is contributed by vt_m
```

## Javascript

```
<script>

// JavaScript program
// to sort an array of 0s
// 1s and 2s.

    function sort012(arr, n)
    {
        // Variables to maintain
        // the count of 0's,
        // 1's and 2's in the array
        let count0 = 0, count1 = 0;
        let count2 = 0;
        for (let i = 0; i < n; i++) {
            if (arr[i] == 0)
                count0++;
            if (arr[i] == 1)
                count1++;
            if (arr[i] == 2)
                count2++;
        }

        // Putting the 0's in the
        // array in starting.
        for (let i = 0; i < count0; i++)
            arr[i] = 0;

        // Putting the 1's in the
        // array after the 0's.
        for (let i = count0; i <
            (count0 + count1); i++)
            arr[i] = 1;

        // Putting the 2's in the
        // array after the 1's
        for (let i = (count0 + count1);
            i < n; i++)
            arr[i] = 2;

        printArray(arr, n);
    }

    // Prints the array
    function printArray(arr, n)
    {
        for (let i = 0; i < n; i++)
            document.write(arr[i] + " ");
        document.write();
    }

// Driver code

        let arr = [ 0, 1, 1, 0, 1, 2, 1,
                    2, 0, 0, 0, 1 ];
        let n = 12;
        sort012(arr, n);

</script>
```

**输出**

```
0 0 0 0 0 1 1 1 1 1 2 2 
```