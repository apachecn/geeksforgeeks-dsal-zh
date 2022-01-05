# 使用双指针

将所有零移动到数组的末尾

> 原文:[https://www . geesforgeks . org/使用两个指针将全零移动到数组末尾/](https://www.geeksforgeeks.org/move-all-zeroes-to-end-of-array-using-two-pointers/)

给定一个随机数数组，将给定数组的所有零推到数组的末尾。例如，如果给定的数组是{1，0，2，6，0，4}，则应该将其更改为{1，2，6，4，0，0}。所有其他元素的顺序应该相同。
**例:**

```
Input: arr[]={8, 9, 0, 1, 2, 0, 3}
Output: arr[]={8, 9, 1, 2, 3, 0, 0}
Explanation: 
Swap {0 ,1} -> Resulting array {8, 9, 1, 0, 2, 0, 3}
Swap {0 ,2} -> Resulting array {8, 9, 1, 2, 0, 0, 3}
Swap {0 ,3} -> Final array {8, 9, 1, 2, 3, 0, 0}

Input: arr[]={4, 5, 0, 0, 0, 0, 6, 7}
Output: arr[]={4, 5, 6, 7, 0, 0, 0, 0}
```

**进场:**

1.  从 **0** 到 **N** 迭代数组。

2.  保留两个指针，一个用于零元素，另一个用于非零元素。

3.  用紧随其后的非零元素交换每个零元素。

## C

```
// C implementation to move all zeroes at
// the end of array
#include<stdio.h>

// Function to move all zeroes at
// the end of array
void moveZerosToEnd(int arr[], int n)
{
    int j=0, temp, i;

    // Traverse the array. If arr[i] is
    // non-zero and arr[j] is zero,
    // then swap both the element
    for(i=0;i<n;i++)
    {
        if(arr[i]!=0 && arr[j]==0)
            {
             temp=arr[i];
             arr[i]=arr[j];
             arr[j]=temp;
            }
        if(arr[j]!=0)
            j+=1;
    }
}

// Function to print the array elements
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
         printf("%d ", arr[i]);
}

// Driver Code
int main()
{
    int arr[] = {8, 9, 0, 1, 2, 0, 3};
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Original array: ");
    printArray(arr, n);

    moveZerosToEnd(arr, n);

    printf("\nModified array: ");
    printArray(arr, n);

    return 0;
}
```

## C++

```
// C++ implementation to move all zeroes at
// the end of array
#include <iostream>
using namespace std;

// Function to move all zeroes at
// the end of array
void moveZerosToEnd(int arr[], int n)
{
    int j=0, temp, i;

    // Traverse the array. If arr[i] is
    // non-zero and arr[j] is zero,
    // then swap both the element
    for(i=0;i<n;i++)
    {
        if(arr[i]!=0 && arr[j]==0)
            {
             swap(arr[i],arr[j]);
            }
        if(arr[j]!=0)
            j+=1;
    }
}

// Function to print the array elements
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{
    int arr[] = {8, 9, 0, 1, 2, 0, 3};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Original array: ";
    printArray(arr, n);

    moveZerosToEnd(arr, n);

    cout << "\nModified array: ";
    printArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to move all zeroes at
// the end of array

class GFG {

    // Function to move all zeroes at
    // the end of array
    static void moveZerosToEnd(int arr[], int n) {
        int j = 0, i;

        // Traverse the array. If arr[i] is
        // non-zero and arr[j] is zero,
        // then swap both the element
        for (i = 0; i < n; i++) {
            if (arr[i] != 0 && arr[j] == 0) {
                arr = swap(arr, i, j);
            }
            if (arr[j] != 0)
                j += 1;
        }
    }

    static int[] swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Function to print the array elements
    static void printArray(int arr[], int n) {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 8, 9, 0, 1, 2, 0, 3 };
        int n = arr.length;

        System.out.print("Original array: ");
        printArray(arr, n);

        moveZerosToEnd(arr, n);

        System.out.print("\nModified array: ");
        printArray(arr, n);

    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to move all zeroes at
# the end of array

# Function to move all zeroes at
# the end of array
def moveZerosToEnd(nums):
    j = 0

    for i in range(len(nums)):
        if nums[i]!= 0 and nums[j]== 0:
            nums[i], nums[j]= nums[j], nums[i]
        if nums[j]!= 0:
            j+= 1

# Function to print the array elements
def printArray(arr, n):

    for i in range(0, n):
        print(arr[i],end=" ")

# Driver program to test above
arr = [8, 9, 0, 1, 2, 0, 3]
n = len(arr)

print("Original array:", end=" ")
printArray(arr, n)

moveZerosToEnd(arr)

print("\nModified array: ", end=" ")
printArray(arr, n)
```

## C#

```
// C# implementation to move all zeroes
// at the end of array
using System;

class GFG{

// Function to move all zeroes
// at the end of array
static void moveZerosToEnd(int []arr, int n)
{
    int j = 0, i;

    // Traverse the array. If arr[i]
    // is non-zero and arr[j] is zero,
    // then swap both the element
    for(i = 0; i < n; i++)
    {
       if (arr[i] != 0 && arr[j] == 0)
       {
           arr = swap(arr, i, j);
       }
       if (arr[j] != 0)
           j += 1;
    }
}

static int[] swap(int[] arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Function to print the array elements
static void printArray(int []arr, int n)
{
    for(int i = 0; i < n; i++)
       Console.Write(arr[i] + " ");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 8, 9, 0, 1, 2, 0, 3 };
    int n = arr.Length;

    Console.Write("Original array: ");
    printArray(arr, n);

    moveZerosToEnd(arr, n);

    Console.Write("\nModified array: ");
    printArray(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation to move all zeroes at
// the end of array

// Function to move all zeroes at
// the end of array
function moveZerosToEnd(arr, n)
{
    let j=0, temp, i;

    // Traverse the array. If arr[i] is
    // non-zero and arr[j] is zero,
    // then swap both the element
    for(i=0;i<n;i++)
    {
        if(arr[i]!=0 && arr[j]==0)
            {
                let temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        if(arr[j]!=0)
            j+=1;
    }
}

// Function to print the array elements
function printArray(arr, n)
{
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Driver Code
    let arr = [8, 9, 0, 1, 2, 0, 3];
    let n = arr.length;

    document.write("Original array: ");
    printArray(arr, n);

    moveZerosToEnd(arr, n);

    document.write("<br>Modified array: ");
    printArray(arr, n);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
Original array: 8 9 0 1 2 0 3 
Modified array: 8 9 1 2 3 0 0
```

**时间复杂度:** O(N)。
**辅助空间:** O(1)