# 交替反转矩阵的行和列

> 原文:[https://www . geeksforgeeks . org/反转矩阵的行和列-或者/](https://www.geeksforgeeks.org/reverse-the-rows-and-columns-of-a-matrix-alternatively/)

给定一个大小为 **M*N** 的矩阵 **arr[][]** ，其中 **M** 是**行**的数量， **N** 是**列**的数量。任务是将矩阵**的**行**和**列**交替**反转**，即先反转第一行，再反转第二列，依此类推。**

**示例**:

> **输入** : arr[][] = {
> {3，4，1，8}，
> {11，23，43，21}，
> {12，17，65，91}，
> {71，56，34，24}
> }
> **输出** : {
> {8，56，4，24}，
> {11，17，43，12}
> 
> *   反转第一行
> *   反转第二列
> *   反转第三行
> *   反转第四行
> 
> **输入** : { {11，23，43，21}、{12，17，65，91}、{71，56，34，24} }
> **输出** : { {21，56，23，71}、{12，17，65，91}、{24，34，43，11} }

**方法:**可以通过简单地运行两个 while 循环来交替遍历行和列来解决该任务。最后，打印结果矩阵。

下面是上述方法的实现:

## C++

```
// C++ program to find Reverse the
// rows and columns of a matrix alternatively.
#include <bits/stdc++.h>
using namespace std;
const int N = 4;
const int M = 4;

// Print matrix elements
void showArray(int arr[][N])
{
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++)
            cout << arr[i][j] << " ";
        cout << endl;
    }
}

// Function to Reverse the rows and columns
// of a matrix alternatively.
void reverseAlternate(int arr[][N])
{
    int turn = 0;

    while (turn < M && turn < N) {
        if (turn % 2 == 0) {
            int start = 0, end = N - 1, temp;
            while (start < end) {
                temp = arr[turn][start];
                arr[turn][start] = arr[turn][end];
                arr[turn][end] = temp;
                start += 1;
                end -= 1;
            }
            turn += 1;
        }

        if (turn % 2 == 1) {
            int start = 0, end = M - 1, temp;
            while (start < end) {
                temp = arr[start][turn];
                arr[start][turn] = arr[end][turn];
                arr[end][turn] = temp;
                start += 1;
                end -= 1;
            }
            turn += 1;
        }
    }
}

// Driver code
int main()
{

    int matrix[][N] = { { 3, 4, 1, 8 },
                        { 11, 23, 43, 21 },
                        { 12, 17, 65, 91 },
                        { 71, 56, 34, 24 } };
    reverseAlternate(matrix);
    showArray(matrix);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{
  static int N = 4;
  static int M = 4;

  // Print matrix elements
  static void showArray(int arr[][])
  {
    for (int i = 0; i < M; i++) {
      for (int j = 0; j < N; j++)
        System.out.print(arr[i][j] + " ");
      System.out.println();
    }
  }

  // Function to Reverse the rows and columns
  // of a matrix alternatively.
  static void reverseAlternate(int arr[][])
  {
    int turn = 0;

    while (turn < M && turn < N) {
      if (turn % 2 == 0) {
        int start = 0, end = N - 1, temp;
        while (start < end) {
          temp = arr[turn][start];
          arr[turn][start] = arr[turn][end];
          arr[turn][end] = temp;
          start += 1;
          end -= 1;
        }
        turn += 1;
      }

      if (turn % 2 == 1) {
        int start = 0, end = M - 1, temp;
        while (start < end) {
          temp = arr[start][turn];
          arr[start][turn] = arr[end][turn];
          arr[end][turn] = temp;
          start += 1;
          end -= 1;
        }
        turn += 1;
      }
    }
  }

  // Driver Code
  public static void main(String args[])
  {

    int matrix[][] = { { 3, 4, 1, 8 },
                      { 11, 23, 43, 21 },
                      { 12, 17, 65, 91 },
                      { 71, 56, 34, 24 } };
    reverseAlternate(matrix);
    showArray(matrix);
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python3 program to find Reverse the
# rows and columns of a matrix alternatively.
N = 4
M = 4

# Print matrix elements
def showArray(arr):

    for i in range(M):
        for j in range(N):
            print(arr[i][j], end = " ")

        print()

# Function to Reverse the rows and columns
# of a matrix alternatively.
def reverseAlternate(arr):

    turn = 0

    while turn < M and turn < N:
        if (turn % 2 == 0):
            start = 0
            end = N - 1

            while (start < end):
                temp = arr[turn][start]
                arr[turn][start] = arr[turn][end]
                arr[turn][end] = temp
                start += 1
                end -= 1

            turn += 1

        if (turn % 2 == 1):
            start = 0
            end = M - 1

            while (start < end):
                temp = arr[start][turn]
                arr[start][turn] = arr[end][turn]
                arr[end][turn] = temp
                start += 1
                end -= 1

            turn += 1

# Driver code
matrix = [ [ 3, 4, 1, 8 ],
           [ 11, 23, 43, 21 ],
           [ 12, 17, 65, 91 ],
           [ 71, 56, 34, 24 ] ]

reverseAlternate(matrix)
showArray(matrix)

# This code is contributed by Potta Lokesh
```

## C#

```
// C# program to find Reverse the
// rows and columns of a matrix alternatively.
using System;
class GFG {
  const int N = 4;
  const int M = 4;

  // Print matrix elements
  static void showArray(int[, ] arr)
  {
    for (int i = 0; i < M; i++) {
      for (int j = 0; j < N; j++)
        Console.Write(arr[i, j] + " ");
      Console.WriteLine();
    }
  }

  // Function to Reverse the rows and columns
  // of a matrix alternatively.
  static void reverseAlternate(int[, ] arr)
  {
    int turn = 0;

    while (turn < M && turn < N) {
      if (turn % 2 == 0) {
        int start = 0, end = N - 1, temp;
        while (start < end) {
          temp = arr[turn, start];
          arr[turn, start] = arr[turn, end];
          arr[turn, end] = temp;
          start += 1;
          end -= 1;
        }
        turn += 1;
      }

      if (turn % 2 == 1) {
        int start = 0, end = M - 1, temp;
        while (start < end) {
          temp = arr[start, turn];
          arr[start, turn] = arr[end, turn];
          arr[end, turn] = temp;
          start += 1;
          end -= 1;
        }
        turn += 1;
      }
    }
  }

  // Driver code
  public static void Main()
  {

    int[, ] matrix = { { 3, 4, 1, 8 },
                      { 11, 23, 43, 21 },
                      { 12, 17, 65, 91 },
                      { 71, 56, 34, 24 } };
    reverseAlternate(matrix);
    showArray(matrix);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
    // JavaScript program to find Reverse the
    // rows and columns of a matrix alternatively.
    const N = 4;
    const M = 4;

    // Print matrix elements
    const showArray = (arr) => {
        for (let i = 0; i < M; i++) {
            for (let j = 0; j < N; j++)
                document.write(`${arr[i][j]} `);
            document.write("<br/>");
        }
    }

    // Function to Reverse the rows and columns
    // of a matrix alternatively.
    const reverseAlternate = (arr) => {
        let turn = 0;

        while (turn < M && turn < N) {
            if (turn % 2 == 0) {
                let start = 0, end = N - 1, temp;
                while (start < end) {
                    temp = arr[turn][start];
                    arr[turn][start] = arr[turn][end];
                    arr[turn][end] = temp;
                    start += 1;
                    end -= 1;
                }
                turn += 1;
            }

            if (turn % 2 == 1) {
                let start = 0, end = M - 1, temp;
                while (start < end) {
                    temp = arr[start][turn];
                    arr[start][turn] = arr[end][turn];
                    arr[end][turn] = temp;
                    start += 1;
                    end -= 1;
                }
                turn += 1;
            }
        }
    }

    // Driver code
    let matrix = [[3, 4, 1, 8],
    [11, 23, 43, 21],
    [12, 17, 65, 91],
    [71, 56, 34, 24]];
    reverseAlternate(matrix);
    showArray(matrix);

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
8 56 4 24 
11 17 43 12 
91 65 23 21 
71 1 34 3 
```

***时间复杂度*** : O(M*N)
***空间复杂度*** : O(1)，不使用额外空间。