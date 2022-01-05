# 重新排列排序后的数组，使所有奇数索引元素位于所有偶数索引元素之前

> 原文:[https://www . geeksforgeeks . org/rearray-sorted-array-so-all-奇数索引-elements-before-all-偶数索引-element/](https://www.geeksforgeeks.org/rearrange-sorted-array-such-that-all-odd-indices-elements-comes-before-all-even-indices-element/)

给定一个由正整数 **N** 组成的排序后的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是重新排列数组，使得所有奇数索引元素位于所有偶数索引元素之前。

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6，7，8，9}
> **输出:** 2 4 6 8 1 3 5 7 9
> 
> **输入:** arr[] = {0，3，7，7，10}
> **输出:** 3 7 0 7 10

**方法:**通过将值 **(** [**)最大数组元素**](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) **+ 1)** 作为**轴**(说)修改给定数组，然后对于数组的前半部分，在奇数索引处添加值**(arr【odd index】% pivot)* pivot****odd index**，对于数组的后半部分，添加值**完成上述步骤后，将每个数组元素除以**轴**的值。下图也是同样的情况:**

> 考虑数组 arr[] = {3，7}，那么 pivot 的值是 7 + 1 = 8。
> 
> 前半部分:
> 修改数组元素 arr[0] = 3 + (7%8)*8 = 3+ 56 = 59。
> 
> 对于后半部分:
> 
> 修改数组元素 arr[1] = 7 + (59%8)*8 = 7 + 24 = 31。
> 
> 将每个数组元素除以透视会将数组修改为{7，3}，这是所需的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the array
void printTheArray(int arr[], int N)
{
  for (int i = 0; i < N; i++)
    cout << arr[i] << " ";
}

// Function to rearrange the array such
// that odd indexed elements come before
// even indexed elements
void rearrange(int arr[], int N)
{
  //Reduces the size of array by one
  //because last element does not need
  //to be changed in case N = odd
  if (N & 1)
    N--;

  // Initialize the variables
  int odd_idx = 1, even_idx = 0;

  int i, max_elem = arr[N - 1] + 1;

  // Iterate over the range
  for (i = 0; i < N / 2; i++) {

    // Add the modified element at
    // the odd position
    arr[i] += (arr[odd_idx] % max_elem) * max_elem;

    odd_idx += 2;
  }

  // Iterate over the range
  for (; i < N; i++) {

    // Add the modified element at
    // the even position
    arr[i] += (arr[even_idx] % max_elem) * max_elem;

    even_idx += 2;
  }

  // Iterate over the range
  for (int i = 0; i < N; i++) {

    // Divide by the maximum element
    arr[i] = arr[i] / max_elem;
  }
}

// Driver Code
int main()
{
  int arr[] = { 1, 2, 3, 4, 5, 16, 18, 19 };
  int N = sizeof(arr) / sizeof(arr[0]);

  rearrange(arr, N);
  printTheArray(arr, N);

  return 0;
}

//This code is contributed by Akash Jha
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

// Function to print the array
static void printTheArray(int arr[], int N)
{
  for (int i = 0; i < N; i++)
   System.out.print(arr[i] + " ");
}

// Function to rearrange the array such
// that odd indexed elements come before
// even indexed elements
static void rearrange(int arr[], int N)
{

  // Reduces the size of array by one
  // because last element does not need
  // to be changed in case N = odd
  if ((N & 1) != 0)
    N--;

  // Initialize the variables
  int odd_idx = 1, even_idx = 0;

  int i, max_elem = arr[N - 1] + 1;

  // Iterate over the range
  for (i = 0; i < N / 2; i++) {

    // Add the modified element at
    // the odd position
    arr[i] += (arr[odd_idx] % max_elem) * max_elem;

    odd_idx += 2;
  }

  // Iterate over the range
  for (; i < N; i++) {

    // Add the modified element at
    // the even position
    arr[i] += (arr[even_idx] % max_elem) * max_elem;

    even_idx += 2;
  }

  // Iterate over the range
  for (i = 0; i < N; i++) {

    // Divide by the maximum element
    arr[i] = arr[i] / max_elem;
  }
}

// Driver Code
public static void main (String[] args)
{
     int arr[] = { 1, 2, 3, 4, 5, 16, 18, 19 };
    int N = arr.length;

    rearrange(arr, N);
    printTheArray(arr, N);

}
}

// This code is contributed by avijitmondal1998.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to print the array
def printArray(arr, n):
  for i in range(N):
    print(arr[i],end=" ")
  print("\n")

# Function to rearrange the array such
# that odd indexed elements come before
# even indexed elements
def rearrange(arr, N):

  #Reduces the size of array by one
  #because last element does not need
  #to be changed in case N = odd
  if (N & 1):
    N-=1

  # Initialize the variables
  odd_idx = 1
  even_idx = 0
  max_elem = arr[N - 1] + 1

  # Iterate over the range
  for i in range(N//2):

    # Add the modified element at
    # the odd position
    arr[i] += (arr[odd_idx] % max_elem) * max_elem
    odd_idx += 2

  # Iterate over the range
  for i in range(N//2,N):

    # Add the modified element at
    # the even position
    arr[i] += (arr[even_idx] % max_elem) * max_elem
    even_idx += 2

  # Iterate over the range
  for i in range(N):

    # Divide by the maximum element
    arr[i] = arr[i] // max_elem

# Driver Code
if __name__=="__main__":

  arr = [ 1, 2, 3, 4, 5, 16, 18, 19 ]
  N = len(arr)

  rearrange(arr, N)
  printArray(arr, N);

#This code is contributed by Akash Jha
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the array
static void printTheArray(int []arr, int N)
{
  for (int i = 0; i < N; i++)
    Console.Write(arr[i]+" ");
}

// Function to rearrange the array such
// that odd indexed elements come before
// even indexed elements
static void rearrange(int []arr, int N)
{
  // Reduces the size of array by one
  // because last element does not need
  // to be changed in case N = odd
  if ((N & 1) != 0)
    N--;

  // Initialize the variables
  int odd_idx = 1, even_idx = 0;

  int i, max_elem = arr[N - 1] + 1;

  // Iterate over the range
  for (i = 0; i < N / 2; i++) {

    // Add the modified element at
    // the odd position
    arr[i] += (arr[odd_idx] % max_elem) * max_elem;

    odd_idx += 2;
  }

  // Iterate over the range
  for (; i < N; i++) {

    // Add the modified element at
    // the even position
    arr[i] += (arr[even_idx] % max_elem) * max_elem;

    even_idx += 2;
  }

  // Iterate over the range
  for(i = 0; i < N; i++) {

    // Divide by the maximum element
    arr[i] = arr[i] / max_elem;
  }
}

// Driver Code
public static void Main()
{
  int []arr = { 1, 2, 3, 4, 5, 16, 18, 19};
  int N = arr.Length;

  rearrange(arr, N);
  printTheArray(arr, N);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to print the array
function printTheArray(arr, N)
{
  for (let i = 0; i < N; i++)
    document.write(Math.floor(arr[i]) + " ");
}

// Function to rearrange the array such
// that odd indexed elements come before
// even indexed elements
function rearrange(arr, N)
{
  // Reduces the size of array by one
  // because last element does not need
  // to be changed in case N = odd
  if (N & 1)
    N--;

  // Initialize the variables
  let odd_idx = 1, even_idx = 0;

  let i, max_elem = arr[N - 1] + 1;

  // Iterate over the range
  for (i = 0; i < N / 2; i++) {

    // Add the modified element at
    // the odd position
    arr[i] += (arr[odd_idx] % max_elem) * max_elem;

    odd_idx += 2;
  }

  // Iterate over the range
  for (; i < N; i++) {

    // Add the modified element at
    // the even position
    arr[i] += (arr[even_idx] % max_elem) * max_elem;

    even_idx += 2;
  }

  // Iterate over the range
  for (let i = 0; i < N; i++) {

    // Divide by the maximum element
    arr[i] = arr[i] / max_elem;
  }
}

// Driver Code
  let arr =[ 1, 2, 3, 4, 5, 16, 18, 19 ];
  let N = arr.length;

  rearrange(arr, N);
  printTheArray(arr, N);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
2 4 16 19 1 3 5 18
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)