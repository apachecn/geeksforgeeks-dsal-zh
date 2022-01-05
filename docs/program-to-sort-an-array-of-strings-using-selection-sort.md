# 使用选择排序对字符串数组进行排序的程序

> 原文:[https://www . geesforgeks . org/program-to-sort-a-array-of-string-use-selection-sort/](https://www.geeksforgeeks.org/program-to-sort-an-array-of-strings-using-selection-sort/)

给定一个字符串数组，使用[选择排序](https://www.geeksforgeeks.org/selection-sort/)对数组进行排序。

**例:**

```
Input  : paper true soap floppy flower
Output : floppy, flower, paper, soap, true
```

前提条件:[选拔出来](https://www.geeksforgeeks.org/selection-sort/)。

## 

## 

## 

```
// Java program to implement selection sort
// on array of strings
import java.util.*;
import java.io.*;

class Main
{

// Sorts an array of strings
static void selectionSort(String arr[],int n)
{
    // One by one move boundary of unsorted subarray
    for(int i = 0; i < n - 1; i++)
    {

        // Find the minimum element in unsorted array
        int min_index = i;
        String minStr = arr[i];
        for(int j = i + 1; j < n; j++)
        {

            /*compareTo() will return a -ve value,
            if string1 (arr[j]) is smaller than string2 (minStr)*/
            // If arr[j] is smaller than minStr

            if(arr[j].compareTo(minStr) < 0)
            {
                // Make arr[j] as minStr and update min_idx
                minStr = arr[j];
                min_index = j;
            }
        }

    // Swapping the minimum element
    // found with the first element.
    if(min_index != i)
    {
        String temp = arr[min_index];
        arr[min_index] = arr[i];
        arr[i] = temp;
    }
    }
}

// Driver code
public static void main(String args[])
{
    String arr[] = {"GeeksforGeeks",
                    "Practice.GeeksforGeeks",
                    "GeeksQuiz"};
    int n = arr.length;
        System.out.println("Given array is");

    // Printing the array before sorting
    for(int i = 0; i < n; i++)
    {
        System.out.println(i+": "+arr[i]);
    }
    System.out.println();

    selectionSort(arr, n);

    System.out.println("Sorted array is");

    // Printing the array after sorting
    for(int i = 0; i < n; i++)
    {
        System.out.println(i+": "+arr[i]);
    }
}
}

/*This code is contributed by rajesh999*/
```

```
Given array is
0: GeeksforGeeks
1: Practice.GeeksforGeeks
2: GeeksQuiz

Sorted array is
0: GeeksQuiz
1: GeeksforGeeks
2: Practice.GeeksforGeeks

```