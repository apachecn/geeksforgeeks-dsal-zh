# 用右侧的最大元素替换每个元素

> 原文： [https://www.geeksforgeeks.org/replace-every-element-with-the-greatest-on-right-side/](https://www.geeksforgeeks.org/replace-every-element-with-the-greatest-on-right-side/)

给定一个整数数组，将每个元素替换为数组中的下一个最大元素（右侧的最大元素）。 由于最后一个元素旁边没有元素，因此将其替换为 -1。 例如，如果数组为`{16, 17, 4, 4, 3, 5, 2}`，则应将其修改为`{17, 5, 5, 5, 2, -1}`。

## 强烈建议您在继续解决方案之前，单击这里进行练习。

这个问题与本帖的非常相似，[解决方案也相似](https://www.geeksforgeeks.org/leaders-in-an-array/)。

**朴素的方法**是要运行两个循环。 外循环将从左到右一个接一个的拾取数组元素。 内循环将在选取的元素之后找到最大的元素。 最后，外循环将用内循环找到的最大元素替换选取的元素。 此方法的时间复杂度将为`O(n * n)`。

一种棘手的**方法**是使用数组的一次遍历来替换所有元素。 这个想法是从最右边的元素开始，一个一个地移到左侧，并跟踪最大的元素。 将每个元素替换为最大元素。

## C++ 

```cpp

// C++ Program to replace every element with the greatest  
// element on right side  
#include <bits/stdc++.h> 
using namespace std; 

/* Function to replace every element with the  
next greatest element */
void nextGreatest(int arr[], int size)  
{  

    // Initialize the next greatest element  
    int max_from_right = arr[size-1];  

    // The next greatest element for the rightmost element  
    // is always -1  
    arr[size-1] = -1;  

    // Replace all other elements with the next greatest  
    for(int i = size-2; i >= 0; i--)  
    {  
        // Store the current element (needed later for updating  
        // the next greatest element)  
        int temp = arr[i];  

        // Replace current element with the next greatest  
        arr[i] = max_from_right;  

        // Update the greatest element, if needed  
        if(max_from_right < temp)  
        max_from_right = temp;  
    }  
}  

/* A utility Function that prints an array */
void printArray(int arr[], int size)  
{  
    int i;  
    for (i = 0; i < size; i++)  
        cout << arr[i] << " ";  
    cout << endl;  
}  

/* Driver program to test above function */
int main()  
{  
    int arr[] = {16, 17, 4, 3, 5, 2};  
    int size = sizeof(arr)/sizeof(arr[0]);  
    nextGreatest (arr, size);  
    cout << "The modified array is: \n";  
    printArray (arr, size);  
    return (0);  
}  

// This is code is contributed by rathbhupendra 

```

## C

```c
// C Program to replace every element with the greatest 
// element on right side 
#include <stdio.h> 
  
/* Function to replace every element with the 
   next greatest element */
void nextGreatest(int arr[], int size) 
{ 
  // Initialize the next greatest element  
  int max_from_right =  arr[size-1]; 
  
  // The next greatest element for the rightmost element 
  // is always -1 
  arr[size-1] = -1; 
  
  // Replace all other elements with the next greatest 
  for(int i = size-2; i >= 0; i--) 
  { 
    // Store the current element (needed later for updating 
    // the next greatest element) 
    int temp = arr[i]; 
  
    // Replace current element with the next greatest 
    arr[i] = max_from_right; 
  
    // Update the greatest element, if needed 
    if(max_from_right < temp) 
       max_from_right = temp; 
  } 
} 
  
/* A utility Function that prints an array */
void printArray(int arr[], int size) 
{ 
  int i; 
  for (i=0; i < size; i++) 
    printf("%d ", arr[i]); 
  printf("\n"); 
} 
  
/* Driver program to test above function */
int main() 
{ 
  int arr[] = {16, 17, 4, 3, 5, 2}; 
  int size = sizeof(arr)/sizeof(arr[0]); 
  nextGreatest (arr, size); 
  printf ("The modified array is: \n"); 
  printArray (arr, size); 
  return (0); 
} 
```

## Java

```java
// Java Program to replace every element with the  
// greatest element on right side 
import java.io.*; 
  
class NextGreatest  
{ 
    /* Function to replace every element with the 
       next greatest element */
    static void nextGreatest(int arr[]) 
    { 
        int size = arr.length; 
  
        // Initialize the next greatest element 
        int max_from_right =  arr[size-1]; 
  
        // The next greatest element for the rightmost 
        // element is always -1 
        arr[size-1] = -1; 
  
        // Replace all other elements with the next greatest 
        for (int i = size-2; i >= 0; i--) 
        { 
            // Store the current element (needed later for 
            // updating the next greatest element) 
            int temp = arr[i]; 
  
            // Replace current element with the next greatest 
            arr[i] = max_from_right; 
  
            // Update the greatest element, if needed 
            if(max_from_right < temp) 
            max_from_right = temp; 
        } 
    } 
  
    /* A utility Function that prints an array */
    static void printArray(int arr[]) 
    { 
        for (int i=0; i < arr.length; i++) 
        System.out.print(arr[i]+" "); 
    } 
  
    public static void main (String[] args) 
    { 
        int arr[] = {16, 17, 4, 3, 5, 2}; 
        nextGreatest (arr); 
        System.out.println("The modified array:"); 
        printArray (arr); 
    } 
} 
/*This code is contributed by Devesh Agrawal*/
```

## Python

```py
# Python Program to replace every element with the  
# greatest element on right side 
  
# Function to replace every element with the next greatest 
# element 
def nextGreatest(arr): 
  
    size = len(arr) 
  
    # Initialize the next greatest element 
    max_from_right = arr[size-1] 
  
    # The next greatest element for the rightmost element 
    # is always -1 
    arr[size-1] = -1
  
    # Replace all other elements with the next greatest 
    for i in range(size-2,-1,-1): 
  
        # Store the current element (needed later for updating 
        # the next greatest element) 
        temp = arr[i] 
  
        # Replace current element with the next greatest 
        arr[i]=max_from_right 
  
        # Update the greatest element, if needed 
        if max_from_right< temp: 
            max_from_right=temp 
  
# Utility function to print an array 
def printArray(arr): 
    for i in range(0,len(arr)): 
        print arr[i], 
  
# Driver function to test above function 
arr = [16, 17, 4, 3, 5, 2] 
nextGreatest(arr) 
print "Modified array is"
printArray(arr) 
# This code is contributed by Devesh Agrawal 
```

## C#

```cs
// C# Program to replace every element with the  
// greatest element on right side 
using System; 
  
class GFG { 
      
    /* Function to replace every element with  
    the    next greatest element */
    static void nextGreatest(int []arr) 
    { 
        int size = arr.Length; 
  
        // Initialize the next greatest element 
        int max_from_right = arr[size-1]; 
  
        // The next greatest element for the  
        // rightmost element is always -1 
        arr[size-1] = -1; 
  
        // Replace all other elements with the 
        // next greatest 
        for (int i = size-2; i >= 0; i--) 
        { 
            // Store the current element (needed 
            // later for updating the next  
            // greatest element) 
            int temp = arr[i]; 
  
            // Replace current element with  
            // the next greatest 
            arr[i] = max_from_right; 
  
            // Update the greatest element, if  
            // needed 
            if(max_from_right < temp) 
            max_from_right = temp; 
        } 
    } 
  
    /* A utility Function that prints an array */
    static void printArray(int []arr) 
    { 
        for (int i=0; i < arr.Length; i++) 
        Console.Write(arr[i]+" "); 
    } 
  
    public static void Main () 
    { 
        int []arr = {16, 17, 4, 3, 5, 2}; 
        nextGreatest (arr); 
        Console.WriteLine("The modified array:"); 
        printArray (arr); 
    } 
} 
  
/* This code is contributed by vt_m.*/
```

## PHP

```php
<?php 
// PHP Program to replace every element with  
// the greatest element on right side  
  
/* Function to replace every element  
with the next greatest element */
function nextGreatest(&$arr, $size)  
{  
    // Initialize the next greatest element  
    $max_from_right = $arr[$size - 1];  
      
    // The next greatest element for the  
    // rightmost element is always -1  
    $arr[$size - 1] = -1;  
      
    // Replace all other elements with 
    // the next greatest  
    for($i = $size - 2; $i >= 0; $i--)  
    {  
        // Store the current element (needed  
        // later for updating the next  
        // greatest element)  
        $temp = $arr[$i];  
      
        // Replace current element with the 
        // next greatest  
        $arr[$i] = $max_from_right;  
      
        // Update the greatest element,  
        // if needed  
        if($max_from_right < $temp)  
        $max_from_right = $temp;  
    }  
}  
  
// A utility Function that prints an array 
function printArray($arr, $size)  
{  
    for ($i = 0; $i < $size; $i++)  
        echo $arr[$i] . " ";  
    echo "\n";  
}  
  
// Driver Code 
$arr = array(16, 17, 4, 3, 5, 2);  
$size = count($arr);  
nextGreatest ($arr, $size);  
echo "The modified array is: \n";  
printArray ($arr, $size);  
  
// This code is contributed by  
// rathbhupendra 
?> 
```

输出：

```
The modified array is:
17 5 5 5 2 -1
```

时间复杂度：`O(n)`，其中`n`是数组中元素的数量。
