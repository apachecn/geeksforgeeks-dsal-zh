# 给定 2D 阵列(矩阵)中反转列的程序

> 原文:[https://www . geesforgeks . org/program-to-reverse-columns-in-给定-2d-array-matrix/](https://www.geeksforgeeks.org/program-to-reverse-columns-in-given-2d-array-matrix/)

给定一个大小为 **M x N** 的整数的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **arr[][]** ，其中 **N** 是列数， **M** 是数组中的行数。任务是反转给定 2D 数组的每一列。

> **输入:** arr[][] =
> 
> {{3, 2, 1}
> 
>   {4, 5, 6},
> 
>   {9, 8, 7}}
> 
> **输出:**
> 
> 9 8 7
> 
> 4 5 6
> 
> 3 2 1
> 
> **输入:** arr[][] =
> 
> {{7, 9}, 
> 
>   {1, 5}, 
> 
>   {4, 6}, 
> 
>   {19, 3}}
> 
> **输出:**
> 
> 19 3
> 
> 4 6
> 
> 1 5
> 
> 7 9

**方法:**对于给定二维数组或矩阵中的每一列，执行以下步骤:

*   将起始索引初始化为 0，结束索引初始化为 M–1。
*   迭代 for 循环，直到开始索引小于结束索引，交换这些索引处的值，并将索引更新为:

```
swap(arr[start][i], arr[end][i]);
start++;
end--;
```

下面是上述算法的实现:

## C++

```
// C++ implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

const int M = 3;
const int N = 3;

// A utility function
// for swapping two elements.
void swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Print the arr[][]
void printMatrix(int arr[M][N])
{

    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            cout << arr[i][j] << ' ';
        }
        cout << endl;
    }
}

// Function to reverse
// the given 2D arr[][]
void reverseColumnArray(int arr[M][N])
{

    // Print the arr[][] before
    // reversing every column
    printMatrix(arr);
    cout << endl;

    // Traverse each column of arr[][]
    for (int i = 0; i < N; i++) {
        // Initialise start and end index
        int start = 0;
        int end = M - 1;

        // Till start < end, swap the
        // element at start and end index
        while (start < end) {
            // Swap the element
            swap(&arr[start][i], &arr[end][i]);

            // Increment start and decrement
            // end for next pair of swapping
            start++;
            end--;
        }
    }

    // Print the arr[][] after
    // reversing every column
    printMatrix(arr);
}

// Driver Code
int main()
{
    int arr[][3]
        = { { 3, 2, 1 }, { 4, 5, 6 }, { 9, 8, 7 } };

    // Function call
    reverseColumnArray(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;
class GFG{

  static int M = 3;
  static int N = 3;

  // A utility function
  // for swapping two elements.
  private static int[][] swap(int[][] arr, int start,
                              int i, int end, int j)
  {

    int temp = arr[start][i];
    arr[start][i] = arr[end][j];
    arr[end][j] = temp;
    return arr;
  }

  // Print the arr[][]
  static void printMatrix(int arr[][])
  {

    for (int i = 0; i < M; i++) {
      for (int j = 0; j < N; j++) {
        System.out.print(arr[i][j] +" ");
      }
      System.out.println();
    }
  }

  // Function to reverse
  // the given 2D arr[][]
  static void reverseColumnArray(int arr[][])
  {

    // Print the arr[][] before
    // reversing every column
    printMatrix(arr);
    System.out.println();

    // Traverse each column of arr[][]
    for (int i = 0; i < N; i++) {
      // Initialise start and end index
      int start = 0;
      int end = M - 1;

      // Till start < end, swap the
      // element at start and end index
      while (start < end)
      {

        // Swap the element
        arr = swap(arr,start,i,end,i);

        // Increment start and decrement
        // end for next pair of swapping
        start++;
        end--;
      }
    }

    // Print the arr[][] after
    // reversing every column
    printMatrix(arr);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[][]
      = { { 3, 2, 1 }, { 4, 5, 6 }, { 9, 8, 7 } };

    // Function call
    reverseColumnArray(arr);
  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python implementation of the
# above approach
M = 3
N = 3

# Print the arr[][]
def printMatrix(arr):

    for i in range(0, M):
        for j in range(0, N):
            print(arr[i][j], end=' ')

        print()

# Function to reverse
# the given 2D arr[][]
def reverseColumnArray(arr):

    # Print the arr[][] before
    # reversing every column
    printMatrix(arr)
    print()

    # Traverse each column of arr[][]
    for i in range(0, N):
        # Initialise start and end index
        start = 0
        end = M - 1

        # Till start < end, swap the
        # element at start and end index
        while (start < end):
            # Swap the element
            temp = arr[start][i]
            arr[start][i] = arr[end][i]
            arr[end][i] = temp

            # Increment start and decrement
            # end for next pair of swapping
            start += 1
            end -= 1

        # Print the arr[][] after
        # reversing every column
    printMatrix(arr)

# Driver Code
if __name__ == "__main__":

    arr = [[3, 2, 1], [4, 5, 6], [9, 8, 7]]

    # Function call
    reverseColumnArray(arr)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# implementation of the
// above approach
using System;
class GFG
{

    static int M = 3;
    static int N = 3;

    // A utility function
    // for swapping two elements.
    private static int[,] swap(int[,] arr, int start,
                                int i, int end, int j)
    {

        int temp = arr[start, i];
        arr[start, i] = arr[end, j];
        arr[end, j] = temp;
        return arr;
    }

    // Print the arr[][]
    static void printMatrix(int[,] arr)
    {

        for (int i = 0; i < M; i++)
        {
            for (int j = 0; j < N; j++)
            {
                Console.Write(arr[i, j] + " ");
            }
            Console.WriteLine("");
        }
    }

    // Function to reverse
    // the given 2D arr[][]
    static void reverseColumnArray(int[,] arr)
    {

        // Print the arr[][] before
        // reversing every column
        printMatrix(arr);
        Console.WriteLine();

        // Traverse each column of arr[][]
        for (int i = 0; i < N; i++)
        {
            // Initialise start and end index
            int start = 0;
            int end = M - 1;

            // Till start < end, swap the
            // element at start and end index
            while (start < end)
            {

                // Swap the element
                arr = swap(arr, start, i, end, i);

                // Increment start and decrement
                // end for next pair of swapping
                start++;
                end--;
            }
        }

        // Print the arr[][] after
        // reversing every column
        printMatrix(arr);
    }

    // Driver Code
    public static void Main()
    {
        int[,] arr = { { 3, 2, 1 }, { 4, 5, 6 }, { 9, 8, 7 } };

        // Function call
        reverseColumnArray(arr);
    }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
   // JavaScript code for the above approach
   let M = 3;
   let N = 3;

   // Print the arr[][]
   function printMatrix(arr) {

     for (let i = 0; i < M; i++) {
       for (let j = 0; j < N; j++) {
         document.write(arr[i][j] + ' ');
       }
       document.write('<br>')
     }
   }

   // Function to reverse
   // the given 2D arr[][]
   function reverseColumnArray(arr) {

     // Print the arr[][] before
     // reversing every column
     printMatrix(arr);
     document.write('<br>')

     // Traverse each column of arr[][]
     for (let i = 0; i < N; i++)
     {

       // Initialise start and end index
       let start = 0;
       let end = M - 1;

       // Till start < end, swap the
       // element at start and end index
       while (start < end)
       {

         // Swap the element
         let temp = arr[start][i]
         arr[start][i] = arr[end][i]
         arr[end][i] = temp

         // Increment start and decrement
         // end for next pair of swapping
         start++;
         end--;
       }
     }

     // Print the arr[][] after
     // reversing every column
     printMatrix(arr);
   }

   // Driver Code
   let arr
     = [[3, 2, 1], [4, 5, 6], [9, 8, 7]];

   // Function call
   reverseColumnArray(arr);

 // This code is contributed by Potta Lokesh
 </script>
```

**Output**

```
3 2 1 
4 5 6 
9 8 7 

9 8 7 
4 5 6 
3 2 1 
```

**时间复杂度:** O(N <sup>2</sup> )，使用两个 for 循环，一个循环遍历所有列，内部循环交换每列的开始和结束索引。
**辅助复杂度:** 0(1)作为无额外空间，甚至不用于交换两个元素。