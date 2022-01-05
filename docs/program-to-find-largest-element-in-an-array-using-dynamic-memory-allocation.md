# 使用动态内存分配来寻找数组中最大元素的程序

> 原文:[https://www . geesforgeks . org/program-to-find-最大数组元素-使用-动态内存分配/](https://www.geeksforgeeks.org/program-to-find-largest-element-in-an-array-using-dynamic-memory-allocation/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是使用[动态内存分配](https://www.geeksforgeeks.org/dynamic-memory-allocation-in-c-using-malloc-calloc-free-and-realloc/)找到给定数组中最大的[元素。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

**示例:**

> **输入:** arr[] = {4，5，6，7}
> **输出:** 7
> **解释:**
> 给定数组中存在的最大元素是 7。
> 
> **输入:** arr[] = {8，9，10，12}
> **输出:** 12
> **解释:**
> 给定数组中存在的最大元素是 12。

**方法:**这里的想法是使用[动态内存](https://www.geeksforgeeks.org/dynamic-memory-allocation-in-c-using-malloc-calloc-free-and-realloc/)来[搜索给定数组](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)中最大的元素。按照以下步骤解决问题:

1.  取 **N** 个元素和一个指针存储 **N** 个元素的地址
2.  为 **N** 元素动态分配内存。
3.  将元素存储在分配的内存中。
4.  遍历数组 **arr[]** ，通过使用指针比较值，找到所有数字中最大的元素。

下面是上述方法的实现:

## C

```
// C program for the above approach
#include <stdio.h>
#include <stdlib.h>

// Function to find the largest element
// using dynamic memory allocation
void findLargest(int* arr, int N)
{
    int i;

    // Traverse the array arr[]
    for (i = 1; i < N; i++) {

        // Update the largest element
        if (*arr < *(arr + i)) {
            *arr = *(arr + i);
        }
    }

    // Print the largest number
    printf("%d ", *arr);
}

// Driver Code
int main()
{
    int i, N = 4;

    int* arr;

    // Memory allocation to arr
    arr = (int*)calloc(N, sizeof(int));

    // Condition for no memory
    // allocation
    if (arr == NULL) {
        printf("No memory allocated");
        exit(0);
    }

    // Store the elements
    *(arr + 0) = 14;
    *(arr + 1) = 12;
    *(arr + 2) = 19;
    *(arr + 3) = 20;

    // Function Call
    findLargest(arr, N);
    return 0;
}
```

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find the largest element
// using dynamic memory allocation
void findLargest(int* arr, int N)
{

    // Traverse the array arr[]
    for (int i = 1; i < N; i++) {

        // Update the largest element
        if (*arr < *(arr + i)) {
            *arr = *(arr + i);
        }
    }

    // Print the largest number
    cout << *arr;
}

// Driver Code
int main()
{
    int N = 4;
    int* arr;

    // Memory allocation to arr
    arr = new int[N];

    // Condition for no memory
    // allocation
    if (arr == NULL) {
        cout << "No memory allocated";
    }

    // Store the elements
    *(arr + 0) = 14;
    *(arr + 1) = 12;
    *(arr + 2) = 19;
    *(arr + 3) = 20;

    // Function Call
    findLargest(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find the largest element
// using dynamic memory allocation
static void findLargest(int []arr, int N)
{
    // Traverse the array arr[]
    for (int i = 1; i < N; i++)
    {
        // Update the largest element
        if (arr[0] < (arr[i]))
        {
            arr[0] = (arr[i]);
        }
    }

    // Print the largest number
    System.out.print(arr[0]);
}

// Driver Code
public static void main(String[] args)
{
    int N = 4;
    int []arr;

    // Memory allocation to arr
    arr = new int[N];

    // Condition for no memory
    // allocation
    if (arr.length < N)
    {
        System.out.print("No memory allocated");
    }

    // Store the elements
    arr[0] = 14;
    arr[1] = 12;
    arr[2] = 19;
    arr[3] = 20;

    // Function Call
    findLargest(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to find the largest element
# using dynamic memory allocation
def findLargest(arr, N):

    # Traverse the array arr
    for i in range(1, N):

        # Update the largest element
        if (arr[0] < (arr[i])):
            arr[0] = (arr[i]);

    # Print largest number
    print(arr[0]);

# Driver Code
if __name__ == '__main__':
    N = 4;

    # Memory allocation to arr
    arr = [0] * N;

    # Condition for no memory
    # allocation
    if (len(arr) < N):
        print("No memory allocated");

    # Store the elements
    arr[0] = 14;
    arr[1] = 12;
    arr[2] = 19;
    arr[3] = 20;

    # Function Call
    findLargest(arr, N);

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the largest
// element using dynamic memory allocation
static void findLargest(int []arr,
                        int N)
{
  // Traverse the array []arr
  for (int i = 1; i < N; i++)
  {
    // Update the largest element
    if (arr[0] < (arr[i]))
    {
      arr[0] = (arr[i]);
    }
  }

  // Print the largest number
  Console.Write(arr[0]);
}

// Driver Code
public static void Main(String[] args)
{
  int N = 4;
  int []arr;

  // Memory allocation to arr
  arr = new int[N];

  // Condition for no memory
  // allocation
  if (arr.Length < N)
  {
    Console.Write("No memory allocated");
  }

  // Store the elements
  arr[0] = 14;
  arr[1] = 12;
  arr[2] = 19;
  arr[3] = 20;

  // Function Call
  findLargest(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
20

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)