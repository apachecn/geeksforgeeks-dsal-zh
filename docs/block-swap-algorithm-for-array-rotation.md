# 数组旋转的块交换算法

> 原文： [https://www.geeksforgeeks.org/block-swap-algorithm-for-array-rotation/](https://www.geeksforgeeks.org/block-swap-algorithm-for-array-rotation/)

编写一个函数`turn(ar[], d, n)`，该函数将大小为`n`的`arr[]`旋转`d`个元素。

![Array](img/ba17844d7fa31a1b00169a41fc3bc3d3.png "Array")

将上面的数组旋转 2 将产生数组：

![ArrayRotation1](img/a0ca29059e52fd48e525698f91766984.png "ArrayRotation1")



**算法**：

```
Initialize A = arr[0..d-1] and B = arr[d..n-1]
1) Do following until size of A is equal to size of B

  a)  If A is shorter, divide B into Bl and Br such that Br is of same 
       length as A. Swap A and Br to change ABlBr into BrBlA. Now A
       is at its final place, so recur on pieces of B.  

   b)  If A is longer, divide A into Al and Ar such that Al is of same 
       length as B Swap Al and B to change AlArB into BArAl. Now B
       is at its final place, so recur on pieces of A.

2)  Finally when A and B are of equal size, block swap them.

```

**递归实现**：

## C++ 

```cpp

#include <bits/stdc++.h> 
using namespace std; 

/*Prototype for utility functions */
void printArray(int arr[], int size);  
void swap(int arr[], int fi, int si, int d);  

void leftRotate(int arr[], int d, int n)  
{  
    /* Return If number of elements to be rotated   
    is zero or equal to array size */
    if(d == 0 || d == n)  
        return;  

    /*If number of elements to be rotated  
    is exactly half of array size */
    if(n - d == d)  
    {  
        swap(arr, 0, n - d, d);  
        return;  
    }  

    /* If A is shorter*/        
    if(d < n - d)  
    {  
        swap(arr, 0, n - d, d);  
        leftRotate(arr, d, n - d);      
    }  
    else /* If B is shorter*/        
    {  
        swap(arr, 0, d, n - d);  
        leftRotate(arr + n - d, 2 * d - n, d); /*This is tricky*/
    }  
}  

/*UTILITY FUNCTIONS*/
/* function to print an array */
void printArray(int arr[], int size)  
{  
    int i;  
    for(i = 0; i < size; i++)  
        cout << arr[i] << " ";  
    cout << endl;  
}  

/*This function swaps d elements starting at index fi  
with d elements starting at index si */
void swap(int arr[], int fi, int si, int d)  
{  
    int i, temp;  
    for(i = 0; i < d; i++)  
    {  
        temp = arr[fi + i];  
        arr[fi + i] = arr[si + i];  
        arr[si + i] = temp;  
    }  
}  

// Driver Code 
int main()  
{  
    int arr[] = {1, 2, 3, 4, 5, 6, 7};  
    leftRotate(arr, 2, 7);  
    printArray(arr, 7);  
    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c
#include<stdio.h>
 
/*Prototype for utility functions */
void printArray(int arr[], int size);
void swap(int arr[], int fi, int si, int d);
 
void leftRotate(int arr[], int d, int n)
{ 
  /* Return If number of elements to be rotated is 
    zero or equal to array size */ 
  if(d == 0 || d == n)
    return;
     
  /*If number of elements to be rotated is exactly 
    half of array size */ 
  if(n-d == d)
  {
    swap(arr, 0, n-d, d);   
    return;
  }  
     
 /* If A is shorter*/             
  if(d < n-d)
  {  
    swap(arr, 0, n-d, d);
    leftRotate(arr, d, n-d);    
  }    
  else /* If B is shorter*/             
  {
    swap(arr, 0, d, n-d);
    leftRotate(arr+n-d, 2*d-n, d); /*This is tricky*/
  }
}
 
/*UTILITY FUNCTIONS*/
/* function to print an array */
void printArray(int arr[], int size)
{
  int i;
  for(i = 0; i < size; i++)
    printf("%d ", arr[i]);
  printf("\n ");
} 
 
/*This function swaps d elements starting at index fi
  with d elements starting at index si */
void swap(int arr[], int fi, int si, int d)
{
   int i, temp;
   for(i = 0; i<d; i++)   
   {
     temp = arr[fi + i];
     arr[fi + i] = arr[si + i];
     arr[si + i] = temp;
   }     
}     
 
/* Driver program to test above functions */
int main()
{
   int arr[] = {1, 2, 3, 4, 5, 6, 7};
   leftRotate(arr, 2, 7);
   printArray(arr, 7);
   getchar();
   return 0;
}    
```

## Java

```java
import java.util.*;
 
class GFG 
{
    // Wrapper over the recursive function leftRotateRec()
    // It left rotates arr[] by d.
    public static void leftRotate(int arr[], int d, 
                                                int n)
    {
        leftRotateRec(arr, 0, d, n);
    }
 
    public static void leftRotateRec(int arr[], int i, 
                                  int d, int n)
    {
        /* Return If number of elements to be rotated 
        is zero or equal to array size */
        if(d == 0 || d == n) 
            return; 
         
        /*If number of elements to be rotated 
        is exactly half of array size */
        if(n - d == d) 
        { 
            swap(arr, i, n - d + i, d); 
            return; 
        } 
         
        /* If A is shorter*/   
        if(d < n - d) 
        { 
            swap(arr, i, n - d + i, d); 
            leftRotateRec(arr, i, d, n - d);     
        } 
        else /* If B is shorter*/   
        { 
            swap(arr, i, d, n - d); 
            leftRotateRec(arr, n - d + i, 2 * d - n, d); /*This is tricky*/
        } 
    }
 
/*UTILITY FUNCTIONS*/
/* function to print an array */
public static void printArray(int arr[], int size) 
{ 
    int i; 
    for(i = 0; i < size; i++) 
        System.out.print(arr[i] + " "); 
    System.out.println(); 
} 
 
/*This function swaps d elements 
starting at index fi with d elements
starting at index si */
public static void swap(int arr[], int fi,
                        int si, int d) 
{ 
    int i, temp; 
    for(i = 0; i < d; i++) 
    { 
        temp = arr[fi + i]; 
        arr[fi + i] = arr[si + i]; 
        arr[si + i] = temp; 
    } 
} 
 
// Driver Code
public static void main (String[] args) 
{
    int arr[] = {1, 2, 3, 4, 5, 6, 7}; 
    leftRotate(arr, 2, 7); 
    printArray(arr, 7);     
}
}
 
// This code is contributed by codeseeker
```

## Python3

```py
# Wrapper over the recursive function leftRotateRec()
# It left rotates arr by d.
def leftRotate(arr, d, n):
    leftRotateRec(arr, 0, d, n);
 
def leftRotateRec(arr, i, d, n):
    '''
     * Return If number of elements to be 
     rotated is zero or equal to array size
     '''
    if (d == 0 or d == n):
        return;
 
    '''
     * If number of elements to be rotated 
     is exactly half of array size
     '''
    if (n - d == d):
        swap(arr, i, n - d + i, d);
        return;
 
    ''' If A is shorter '''
    if (d < n - d):
        swap(arr, i, n - d + i, d);
        leftRotateRec(arr, i, d, n - d);
        ''' If B is shorter '''
    else:
        swap(arr, i, d, n - d);
         
        ''' This is tricky '''
        leftRotateRec(arr, n - d + i, 2 * d - n, d); 
 
''' UTILITY FUNCTIONS '''
''' function to pran array '''
def printArray(arr, size):
    for i in range(size):
        print(arr[i], end = " ");
    print();
 
'''
 * This function swaps d elements starting at 
 * index fi with d elements starting at index si
 '''
def swap(arr, fi, si, d):
    for i in range(d):
        temp = arr[fi + i];
        arr[fi + i] = arr[si + i];
        arr[si + i] = temp;
 
# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5, 6, 7];
    leftRotate(arr, 2, 7);
    printArray(arr, 7);
 
# This code is contributed by Rohit_ranjan
```

## C#


```cs
using System;
 
class GFG{
     
// Wrapper over the recursive function
// leftRotateRec() 
// It left rotates []arr by d.
public static void leftRotate(int []arr, 
                              int d, int n)
{
    leftRotateRec(arr, 0, d, n);
}
 
public static void leftRotateRec(int []arr, int i, 
                                 int d, int n)
{
     
    // Return If number of elements 
    // to be rotated is zero or equal
    // to array size
    if(d == 0 || d == n) 
        return; 
     
    // If number of elements to be rotated 
    // is exactly half of array size 
    if(n - d == d) 
    { 
        swap(arr, i, n - d + i, d); 
        return; 
    } 
     
    // If A is shorter
    if(d < n - d) 
    { 
        swap(arr, i, n - d + i, d); 
        leftRotateRec(arr, i, d, n - d);     
    } 
     
    // If B is shorter
    else
    { 
        swap(arr, i, d, n - d); 
         
        // This is tricky
        leftRotateRec(arr, n - d + i, 
                       2 * d - n, d); 
    } 
}
 
// UTILITY FUNCTIONS
// Function to print an array 
public static void printArray(int []arr,
                              int size) 
{ 
    int i; 
    for(i = 0; i < size; i++) 
        Console.Write(arr[i] + " "); 
         
    Console.WriteLine(); 
} 
 
// This function swaps d elements 
// starting at index fi with d elements
// starting at index si 
public static void swap(int []arr, int fi,
                        int si, int d) 
{ 
    int i, temp; 
    for(i = 0; i < d; i++) 
    { 
        temp = arr[fi + i]; 
        arr[fi + i] = arr[si + i]; 
        arr[si + i] = temp; 
    } 
} 
 
// Driver Code
public static void Main(String[] args) 
{
    int []arr = { 1, 2, 3, 4, 5, 6, 7 }; 
     
    leftRotate(arr, 2, 7); 
    printArray(arr, 7);     
}
}
 
// This code is contributed by amal kumar choubey
```

迭代实现：

这是相同算法的迭代实现。 此处使用相同的工具函数`swap()`。

## C

```c
void leftRotate(int arr[], int d, int n)
{
  int i, j;
  if(d == 0 || d == n)
    return;
  i = d;
  j = n - d;
  while (i != j)
  {
    if(i < j) /*A is shorter*/
    {
      swap(arr, d-i, d+j-i, i);
      j -= i;
    }
    else /*B is shorter*/
    {
      swap(arr, d-i, d, j);
      i -= j;
    }
    // printArray(arr, 7);
  }
  /*Finally, block swap A and B*/
  swap(arr, d-i, d, i);
}
```

## Java

```java
//Java code for above implementation
static void leftRotate(int arr[], int d, int n) 
{ 
int i, j; 
if(d == 0 || d == n) 
    return; 
i = d; 
j = n - d; 
while (i != j) 
{ 
    if(i < j) /*A is shorter*/
    { 
    swap(arr, d-i, d+j-i, i); 
    j -= i; 
    } 
    else /*B is shorter*/
    { 
    swap(arr, d-i, d, j); 
    i -= j; 
    } 
    // printArray(arr, 7); 
} 
/*Finally, block swap A and B*/
swap(arr, d-i, d, i); 
} 
```

## Python

```py
# Python3 code for above implementation
 
def leftRotate(arr, d, n): 
    if(d == 0 or d == n): 
        return; 
    i = d 
    j = n - d 
    while (i != j): 
         
        if(i < j): # A is shorter
            swap(arr, d - i, d + j - i, i) 
            j -= i 
         
        else: # B is shorter
            swap(arr, d - i, d, j) 
            i -= j 
     
    swap(arr, d - i, d, i)
 
# This code is contributed 
# by Adarsh_Verma
```

## C#

```cs
// C# code for above implementation 
static void leftRotate(int []arr, int d, int n) 
{ 
    int i, j; 
    if(d == 0 || d == n) 
        return; 
    i = d; 
    j = n - d; 
    while (i != j) 
    { 
        if(i < j) /*A is shorter*/
        { 
            swap(arr, d-i, d+j-i, i); 
            j -= i; 
        } 
        else /*B is shorter*/
        { 
            swap(arr, d-i, d, j); 
            i -= j; 
        } 
         
    } 
     
    /*Finally, block swap A and B*/
    swap(arr, d-i, d, i); 
} 
 
// This code is contributed by Rajput-Ji
```

时间复杂度：`O(n)`。