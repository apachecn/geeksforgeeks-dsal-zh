# 编写程序来反转数组或字符串

> 原文： [https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)

给定一个数组（或字符串），任务是反转数组/字符串。

**示例**：

```
Input  : arr[] = {1, 2, 3}
Output : arr[] = {3, 2, 1}

Input :  arr[] = {4, 5, 1, 2}
Output : arr[] = {2, 1, 5, 4}

```



**迭代方式**：

1.  将开始和结束索引初始化为`start = 0`，`end = n-1`。

2.  在循环中，将`arr[start]`与`arr[end]`交换，并如下更改开始和结束：

    

    `start = start + 1`，`end = end – 1`。

![reverse-a-number](img/ac100da44b19cb37e2ef992cd9b3259c.png)

另一个反转字符串的示例：

![reverse-a-string](img/9b328e311de45bcc72d74cd7342ad4a0.png)

下面是上述方法的实现：

## C++ 

```cpp

// Iterative C++ program to reverse an array 
#include <bits/stdc++.h> 
using namespace std; 

/* Function to reverse arr[] from start to end*/
void rvereseArray(int arr[], int start, int end) 
{ 
    while (start < end) 
    { 
        int temp = arr[start];  
        arr[start] = arr[end]; 
        arr[end] = temp; 
        start++; 
        end--; 
    }  
}      

/* Utility function to print an array */
void printArray(int arr[], int size) 
{ 
   for (int i = 0; i < size; i++) 
   cout << arr[i] << " "; 

   cout << endl; 
}  

/* Driver function to test above functions */
int main()  
{ 
    int arr[] = {1, 2, 3, 4, 5, 6}; 

    int n = sizeof(arr) / sizeof(arr[0]);  

    // To print original array  
    printArray(arr, n); 

    // Function calling 
    rvereseArray(arr, 0, n-1); 

    cout << "Reversed array is" << endl; 

    // To print the Reversed array 
    printArray(arr, n); 

    return 0; 
} 

```

## C

```c
// Iterative C program to reverse an array
#include<stdio.h>
 
/* Function to reverse arr[] from start to end*/
void rvereseArray(int arr[], int start, int end)
{
    int temp;
    while (start < end)
    {
        temp = arr[start];   
        arr[start] = arr[end];
        arr[end] = temp;
        start++;
        end--;
    }   
}     
 
/* Utility that prints out an array on a line */
void printArray(int arr[], int size)
{
  int i;
  for (i=0; i < size; i++)
    printf("%d ", arr[i]);
 
  printf("\n");
} 
 
/* Driver function to test above functions */
int main() 
{
    int arr[] = {1, 2, 3, 4, 5, 6};
    int n = sizeof(arr) / sizeof(arr[0]); 
    printArray(arr, n);
    rvereseArray(arr, 0, n-1);
    printf("Reversed array is \n");
    printArray(arr, n);    
    return 0;
}
```

## Java

```java
// Iterative java program to reverse an
// array
public class GFG {
     
   /* Function to reverse arr[] from 
    start to end*/
    static void rvereseArray(int arr[],
                    int start, int end)
    {
        int temp;
          
        while (start < end)
        {
            temp = arr[start]; 
            arr[start] = arr[end];
            arr[end] = temp;
            start++;
            end--;
        } 
    }     
      
    /* Utility that prints out an
    array on a line */
    static void printArray(int arr[], 
                            int size)
    {
        for (int i = 0; i < size; i++)
             System.out.print(arr[i] + " ");
          
         System.out.println();
    } 
 
    // Driver code
    public static void main(String args[]) {
         
        int arr[] = {1, 2, 3, 4, 5, 6};
        printArray(arr, 6);
        rvereseArray(arr, 0, 5);
        System.out.print("Reversed array is \n");
        printArray(arr, 6); 
        
    }
}
 
// This code is contributed by Sam007
```

## Python

```py
# Iterative python program to reverse an array
 
# Function to reverse A[] from start to end
def reverseList(A, start, end):
    while start < end:
        A[start], A[end] = A[end], A[start]
        start += 1
        end -= 1
 
# Driver function to test above function
A = [1, 2, 3, 4, 5, 6]
print(A)
reverseList(A, 0, 5)
print("Reversed list is")
print(A)
# This program is contributed by Pratik Chhajer
```

## C#

```cs
// Iterative C# program to reverse an
// array
using System;
 
class GFG {
 
    /* Function to reverse arr[] from 
    start to end*/
    static void rvereseArray(int []arr,
                    int start, int end)
    {
        int temp;
         
        while (start < end)
        {
            temp = arr[start]; 
            arr[start] = arr[end];
            arr[end] = temp;
            start++;
            end--;
        } 
    }     
     
    /* Utility that prints out an
    array on a line */
    static void printArray(int []arr, 
                            int size)
    {
        for (int i = 0; i < size; i++)
            Console.Write(arr[i] + " ");
         
        Console.WriteLine();
    } 
     
    // Driver function
    public static void Main()
    {
        int []arr = {1, 2, 3, 4, 5, 6};
        printArray(arr, 6);
        rvereseArray(arr, 0, 5);
        Console.Write("Reversed array is \n");
        printArray(arr, 6); 
    }
}
 
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// Iterative PHP program 
// to reverse an array
 
/* Function to reverse 
$arr from start to end*/
function rvereseArray(&$arr, $start, 
                       $end)
{
    while ($start < $end)
    {
        $temp = $arr[$start]; 
        $arr[$start] = $arr[$end];
        $arr[$end] = $temp;
        $start++;
        $end--;
    } 
}     
 
/* Utility function to 
   print an array */
function printArray(&$arr, $size)
{
for ($i = 0; $i < $size; $i++)
echo $arr[$i] . " ";
 
echo "\n";
} 
 
// Driver code
$arr = array(1, 2, 3, 4, 5, 6);
 
// To print original array
printArray($arr, 6);
 
// Function calling
rvereseArray($arr, 0, 5);
 
echo "Reversed array is" ."\n";
 
// To print the Reversed array
printArray($arr, 6);
 
// This code is contributed
// by ChitraNayal
?>
```

输出：

```
1 2 3 4 5 6 
Reversed array is 
6 5 4 3 2 1 
```

时间复杂度：`O(n)`

递归方式：
 

+   初始化开始和结束索引为`start = 0`，`end = n-1`。
+   用`arr[end]`交换`arr[start]`。
+   递归调用反向数组的其余部分。

下面是上述方法的实现：

## C++

```cpp
// Recursive C++ program to reverse an array
#include <bits/stdc++.h>
using namespace std;
 
/* Function to reverse arr[] from start to end*/
void rvereseArray(int arr[], int start, int end)
{
    if (start >= end)
    return;
     
    int temp = arr[start]; 
    arr[start] = arr[end];
    arr[end] = temp;
     
    // Recursive Function calling
    rvereseArray(arr, start + 1, end - 1); 
}     
 
 
/* Utility function to print an array */
void printArray(int arr[], int size)
{
   for (int i = 0; i < size; i++)
   cout << arr[i] << " ";
 
   cout << endl;
} 
 
/* Driver function to test above functions */
int main() 
{
    int arr[] = {1, 2, 3, 4, 5, 6};
     
    // To print original array
    printArray(arr, 6);
     
    // Function calling
    rvereseArray(arr, 0, 5);
     
    cout << "Reversed array is" << endl;
     
    // To print the Reversed array
    printArray(arr, 6);
     
    return 0;
}
```

## C

```c
// Recursive C program to reverse an array
#include <stdio.h>
 
/* Function to reverse arr[] from start to end*/
void rvereseArray(int arr[], int start, int end)
{
   int temp;
   if (start >= end)
     return;
   temp = arr[start];   
   arr[start] = arr[end];
   arr[end] = temp;
   rvereseArray(arr, start+1, end-1);   
}     
 
/* Utility that prints out an array on a line */
void printArray(int arr[], int size)
{
  int i;
  for (i=0; i < size; i++)
    printf("%d ", arr[i]);
 
  printf("\n");
} 
 
/* Driver function to test above functions */
int main() 
{
    int arr[] = {1, 2, 3, 4, 5, 6};
    printArray(arr, 6);
    rvereseArray(arr, 0, 5);
    printf("Reversed array is \n");
    printArray(arr, 6);    
    return 0;
}
```

## Java

```java
// Recursive Java Program to reverse an array
import java.io.*;
 
class ReverseArray {
 
    /* Function to reverse arr[] from start to end*/
    static void rvereseArray(int arr[], int start, int end)
    {
        int temp;
        if (start >= end)
            return;
        temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
        rvereseArray(arr, start+1, end-1);
    }
 
    /* Utility that prints out an array on a line */
    static void printArray(int arr[], int size)
    {
        for (int i=0; i < size; i++)
            System.out.print(arr[i] + " ");
        System.out.println("");
    }
 
    /*Driver function to check for above functions*/
    public static void main (String[] args) {
        int arr[] = {1, 2, 3, 4, 5, 6};
        printArray(arr, 6);
        rvereseArray(arr, 0, 5);
        System.out.println("Reversed array is ");
        printArray(arr, 6);
    }
}
/*This article is contributed by Devesh Agrawal*/
```

## Python

```py
# Recursive python program to reverse an array
 
# Function to reverse A[] from start to end
def reverseList(A, start, end):
    if start >= end:
        return
    A[start], A[end] = A[end], A[start]
    reverseList(A, start+1, end-1)
 
# Driver function to test above function
A = [1, 2, 3, 4, 5, 6]
print(A)
reverseList(A, 0, 5)
print("Reversed list is")
print(A)
# This program is contributed by Pratik Chhajer
```

## C#

```cs
// C# program to reverse an array
using System;
 
class GFG
{
    /* Function to reverse arr[] 
    from start to end*/
    static void rvereseArray(int []arr, int start,
                                        int end)
    {
        int temp;
        if (start >= end)
            return;
             
        temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
         
        rvereseArray(arr, start+1, end-1);
    }
 
    /* Utility that prints out an 
    array on a line */
    static void printArray(int []arr, int size)
    {
        for (int i =  0; i < size; i++)
            Console.Write(arr[i] + " ");
     
        Console.WriteLine("");
    }
 
    // Driver Code
    public static void Main () 
    {
        int []arr = {1, 2, 3, 4, 5, 6};
         
        printArray(arr, 6);
        rvereseArray(arr, 0, 5);
         
        Console.WriteLine("Reversed array is ");
        printArray(arr, 6);
    }
}
 
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// Iterative PHP program 
// to reverse an array
 
/* Function to reverse
$arr from start to end*/
function rvereseArray(&$arr, 
                       $start, $end)
{
    if ($start >= $end)
    return;
     
    $temp = $arr[$start]; 
    $arr[$start] = $arr[$end];
    $arr[$end] = $temp;
 
    //Recursive Function calling
    rvereseArray($arr, $start + 1,
                       $end - 1); 
}     
 
/* Utility function 
to print an array */
function printArray(&$arr, $size)
{
for ($i = 0; $i < $size; $i++)
echo $arr[$i] . " ";
 
echo "\n";
} 
 
// Driver code
$arr = array(1, 2, 3, 4, 5, 6);
 
// To print original array
printArray($arr, 6);
 
// Function calling
rvereseArray($arr, 0, 5);
 
echo "Reversed array is" ."\n";
 
// To print the Reversed array
printArray($arr, 6);
 
// This code is contributed
// by ChitraNayal
?>
```

输出：

```
1 2 3 4 5 6 
Reversed array is 
6 5 4 3 2 1 
```

时间复杂度：`O(n)`。

另一种方法 - 使用Python列表切片：

## Python3

```py
def reverseList(A):
  print( A[::-1])
     
# Driver function to test above function 
A = [1, 2, 3, 4, 5, 6] 
print(A) 
print("Reversed list is") 
reverseList(A)  
```

输出：

```
[1, 2, 3, 4, 5, 6]
Reversed list is
[6, 5, 4, 3, 2, 1]
```

