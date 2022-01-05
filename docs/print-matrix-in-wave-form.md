# 以波形打印矩阵

> 原文:[https://www.geeksforgeeks.org/print-matrix-in-wave-form/](https://www.geeksforgeeks.org/print-matrix-in-wave-form/)

给定一个[矩阵](https://www.geeksforgeeks.org/matrix-introduction/)**mat【】【】**，以波形打印。

> **输入:** mat[][] = {{ 1，2，3，4}
> { 5，6，7，8}
> { 9，10，11，12}
> {13，14，15，16}
> {17，18，19，20}}
> **输出:**1 5 9 13 17 18 14 10 6 2 3 11 15 19 20 16 12 8 4【T4
> 
> **输入:** mat[][] = {{1，9，4，10}
> { 3，6，90，11}
> { 2，30，85，72}
> { 6，31，99，15 } }
> T6】输出: 1 3 2 6 31 30 6 9 4 90 85 99 15 72 11 10

**方法:**这个问题是基于实现的，并且有一个类似于[这篇](https://www.geeksforgeeks.org/print-matrix-reverse-wave-form/)文章中讨论的方法。要获得给定[矩阵](https://www.geeksforgeeks.org/matrix-introduction/)的所需波形，首先，向下打印矩阵第一列的元素，然后向上打印 2 <sup>和</sup>列的元素，然后向下打印第三列的元素，以此类推。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

#define R 5
#define C 4

// Function to print wave
// Form for a given matrix
void WavePrint(int m, int n, int arr[R][C])
{
    // Loop to traverse matrix
    for (int j = 0; j < n; j++) {

        // If the current column
        // is even indexed, print
        // it in forward order
        if (j % 2 == 0) {
            for (int i = 0; i < m; i++) {
                cout << arr[i][j] << " ";
            }
        }

        // If the current column
        // is odd indexed, print
        // it in reverse order
        else {
            for (int i = m - 1; i >= 0; i--) {
                cout << arr[i][j] << " ";
            }
        }
    }
}

// Driver Code
int main()
{
    int arr[R][C] = { { 1, 2, 3, 4 },
                      { 5, 6, 7, 8 },
                      { 9, 10, 11, 12 },
                      { 13, 14, 15, 16 },
                      { 17, 18, 19, 20 } };

    WavePrint(R, C, arr);

    return 0;
}
```

## C

```
// C Program for above approach
#include <stdio.h>

#define R 5
#define C 4

// Function to print wave
// Form for a given matrix
void WavePrint(int m, int n, int arr[R][C])
{
    // Loop to traverse matrix
    for (int j = 0; j < n; j++) {

        // If the current column
        // is even indexed, print
        // it in forward order
        if (j % 2 == 0) {
            for (int i = 0; i < m; i++) {
                printf("%d ", arr[i][j]);
            }
        }

        // If the current column
        // is odd indexed, print
        // it in reverse order
        else {
            for (int i = m - 1; i >= 0; i--) {
                printf("%d ", arr[i][j]);
            }
        }
    }
}

// Driver Code
int main()
{
    int arr[R][C] = { { 1, 2, 3, 4 },
                      { 5, 6, 7, 8 },
                      { 9, 10, 11, 12 },
                      { 13, 14, 15, 16 },
                      { 13, 14, 15, 16 } };
    WavePrint(R, C, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;
class GFG {

  public static int R = 5;
  public static int C = 4;

  // Function to print wave
  // Form for a given matrix
  public static void WavePrint(int m, int n, int[][] arr)
  {

    // Loop to traverse matrix
    for (int j = 0; j < n; j++) {

      // If the current column
      // is even indexed, print
      // it in forward order
      if (j % 2 == 0) {
        for (int i = 0; i < m; i++) {
          System.out.print(arr[i][j] + " ");
        }
      }

      // If the current column
      // is odd indexed, print
      // it in reverse order
      else {
        for (int i = m - 1; i >= 0; i--) {
          System.out.print(arr[i][j] + " ");
        }
      }
    }
  }

  // Driver Code
  public static void main (String[] args)
  {
    int[][] arr = { { 1, 2, 3, 4 },
                   { 5, 6, 7, 8 },
                   { 9, 10, 11, 12 },
                   { 13, 14, 15, 16 },
                   { 17, 18, 19, 20 } };

    WavePrint(R, C, arr);
  }
}

// This code is contributed by Shubham Singh
```

## 蟒蛇 3

```
# Python code for the above approach
R = 5
C = 4

# Function to print wave
# Form for a given matrix
def WavePrint(m, n, arr):

    # Loop to traverse matrix
    for j in range(n):

        # If the current column
        # is even indexed, print
        # it in forward order
        if (j % 2 == 0):
            for i in range(m):
                print(arr[i][j], end= " ")

        # If the current column
        # is odd indexed, print
        # it in reverse order
        else:
            for i in range(m - 1, -1, -1):
                print(arr[i][j], end= " ")

# Driver Code
arr = [[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12], [13, 14, 15, 16], [17, 18, 19, 20]]

WavePrint(R, C, arr)

# This code is contributed by gfgking
```

## C#

```
// C# program for above approach
using System;

class GFG{

public static int R = 5;
public static int C = 4;

// Function to print wave
// Form for a given matrix
public static void WavePrint(int m, int n, int[,] arr)
{

    // Loop to traverse matrix
    for(int j = 0; j < n; j++)
    {

        // If the current column
        // is even indexed, print
        // it in forward order
        if (j % 2 == 0)
        {
            for(int i = 0; i < m; i++)
            {
                Console.Write(arr[i, j] + " ");
            }
        }

        // If the current column
        // is odd indexed, print
        // it in reverse order
        else
        {
            for(int i = m - 1; i >= 0; i--)
            {
                Console.Write(arr[i, j] + " ");
            }
        }
    }
}

// Driver Code
public static void Main ()
{
    int[,] arr = { { 1, 2, 3, 4 },
                   { 5, 6, 7, 8 },
                   { 9, 10, 11, 12 },
                   { 13, 14, 15, 16 },
                   { 17, 18, 19, 20 } };

    WavePrint(R, C, arr);
}
}

// This code is contributed by gfgking
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       let R = 5
       let C = 4

       // Function to print wave
       // Form for a given matrix
       function WavePrint(m, n, arr)
       {

           // Loop to traverse matrix
           for (let j = 0; j < n; j++) {

               // If the current column
               // is even indexed, print
               // it in forward order
               if (j % 2 == 0) {
                   for (let i = 0; i < m; i++) {
                       document.write(arr[i][j] + " ")
                   }
               }

               // If the current column
               // is odd indexed, print
               // it in reverse order
               else {
                   for (let i = m - 1; i >= 0; i--) {
                       document.write(arr[i][j] + " ")
                   }
               }
           }
       }

       // Driver Code
       let arr = [[1, 2, 3, 4],
       [5, 6, 7, 8],
       [9, 10, 11, 12],
       [13, 14, 15, 16],
       [17, 18, 19, 20]];

       WavePrint(R, C, arr);

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
1 5 9 13 17 18 14 10 6 2 3 7 11 15 19 20 16 12 8 4 
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*