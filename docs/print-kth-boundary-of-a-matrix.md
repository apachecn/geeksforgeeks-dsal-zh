# 打印矩阵的第 k 个边界

> 原文:[https://www . geeksforgeeks . org/print-kth-矩阵边界/](https://www.geeksforgeeks.org/print-kth-boundary-of-a-matrix/)

给定一个方阵 **mat[][]** 和一个正整数 **K** 。任务是打印**mat【】【】**的 **K** 边界。

**示例:**

> **输入:** mat[][] = {{1，2，3，4，5}，K = 1
> {6，7，8，9，10}
> {11，12，13，14，15}
> {16，17，18，19，20}
> {21，22，23，24，25}}
> **输出:**1 2 3 4 5
> 6 10【t100
> 
> **输入:** mat[][] = {{1，2，3}，K = 2
> {4，5，6}
> {7，8，9}}
> **输出:** 5

**方法:**这个问题是基于实现的。遍历矩阵，检查每个元素是否位于 Kth 边界上。如果是，则打印元素否则打印空格字符。按照以下步骤解决给定的问题。

*   对于**我**从 **0** 到 **N**
    *   用于从 **0** 到 **N** 的 j
        *   if((I = = K–1 或 I = = N–K)和(j > = K–1 和 j < = N–K))
            *   打印垫[i][j]
        *   否则，如果(j = = K–1 或 j = = N–K)和(I > = K–1 和 I < = N–K):
            *   打印垫[i][j]
*   这将给出 mat[][]所需的 Kth 边框

下面是上述方法的实现。

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print Kth border of a matrix
void printKthBorder(vector<vector<int>> mat, int N, int K)
{
    for (int i = 0; i < N; i++)
    {
        cout << endl;
        for (int j = 0; j < N; j++)
        {
            // To keep track of which element to skip
            int flag = 0;

            if ((i == K - 1 || i == N - K) &&
                (j >= K - 1 && j <= N - K)) {

                // Print the element
                cout << mat[i][j] << " ";

                flag = 1;
            }
            else if ((j == K - 1 || j == N - K) &&
                    (i >= K - 1 && i <= N - K)) {

                // Print the element
                cout << mat[i][j] << " ";

                flag = 1;
            }
            if (flag == 0)
                cout << "  ";
        }
    }
}

// Driver code
int main() {
    int N = 5;
    int K = 1;

    vector<vector<int>> mat = {{1, 2, 3, 4, 5},
                            {6, 7, 8, 9, 10},
                            {11, 12, 13, 14, 15},
                            {16, 17, 18, 19, 20},
                            {21, 22, 23, 24, 25}};

    printKthBorder(mat, N, K);
}

// This code is contributed by Samim Hossain Mondal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;

public class GFG
{
// Function to print Kth border of a matrix
static void printKthBorder(int [][]mat, int N, int K)
{
    for (int i = 0; i < N; i++)
    {
        System.out.println();
        for (int j = 0; j < N; j++)
        {
            // To keep track of which element to skip
            int flag = 0;

            if ((i == K - 1 || i == N - K) &&
                (j >= K - 1 && j <= N - K)) {

                // Print the element
                System.out.print(mat[i][j] + " ");

                flag = 1;
            }
            else if ((j == K - 1 || j == N - K) &&
                    (i >= K - 1 && i <= N - K)) {

                // Print the element
                System.out.print(mat[i][j] + " ");

                flag = 1;
            }
            if (flag == 0)
                System.out.print("  ");
        }
    }
}

// Driver code
public static void main(String args[]) {
    int N = 5;
    int K = 1;

    int [][]mat = {{1, 2, 3, 4, 5},
                    {6, 7, 8, 9, 10},
                    {11, 12, 13, 14, 15},
                    {16, 17, 18, 19, 20},
                    {21, 22, 23, 24, 25}};

    printKthBorder(mat, N, K);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python program for above approach

# Function to print Kth border of a matrix
def printKthBorder(mat, N, K):
    for i in range(N):
        print()
        for j in range(N):

            # To keep track of which element to skip
            flag = 0

            if((i == K-1 or i == N-K) \
                  and (j >= K-1 and j <= N-K)):

                # Print the element
                print(mat[i][j], end =" ")

                flag = 1

            elif (j == K-1 or j == N-K) \
                  and (i >= K-1 and i <= N-K):

                # Print the element
                print(mat[i][j], end =" ")

                flag = 1

            if flag == 0:
                print(end ="  ")

# Driver code
N = 5
K = 1

mat = [[1, 2, 3, 4, 5], \
       [6, 7, 8, 9, 10], \
       [11, 12, 13, 14, 15],
       [16, 17, 18, 19, 20], \
       [21, 22, 23, 24, 25]]

printKthBorder(mat, N, K)
```

## C#

```
// C# Program to implement
// the above approach
using System;

class GFG
{

// Function to print Kth border of a matrix
static void printKthBorder(int [,]mat, int N, int K)
{
    for (int i = 0; i < N; i++)
    {
        Console.WriteLine();
        for (int j = 0; j < N; j++)
        {
            // To keep track of which element to skip
            int flag = 0;

            if ((i == K - 1 || i == N - K) &&
                (j >= K - 1 && j <= N - K)) {

                // Print the element
                Console.Write(mat[i, j] + " ");

                flag = 1;
            }
            else if ((j == K - 1 || j == N - K) &&
                    (i >= K - 1 && i <= N - K)) {

                // Print the element
                Console.Write(mat[i, j] + " ");

                flag = 1;
            }
            if (flag == 0)
                Console.Write("  ");
        }
    }
}

// Driver code
public static void Main() {
    int N = 5;
    int K = 1;

    int [,]mat = {{1, 2, 3, 4, 5},
                    {6, 7, 8, 9, 10},
                    {11, 12, 13, 14, 15},
                    {16, 17, 18, 19, 20},
                    {21, 22, 23, 24, 25}};

    printKthBorder(mat, N, K);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Function to print Kth border of a matrix
       function printKthBorder(mat, N, K)
       {
           for (let i = 0; i < N; i++)
           {
               document.write('<br>')
               for (let j = 0; j < N; j++)
               {

                   // To keep track of which element to skip
                   flag = 0

                   if ((i == K - 1 || i == N - K) &&
                       (j >= K - 1 && j <= N - K)) {

                       // Print the element
                       document.write(mat[i][j] + " ")

                       flag = 1
                   }
                   else if ((j == K - 1 || j == N - K) &&
                       (i >= K - 1 && i <= N - K)) {

                       // Print the element
                       document.write(mat[i][j] + " ")

                       flag = 1
                   }
                   if (flag == 0)
                       document.write("  ");
               }
           }
       }

       // Driver code
       N = 5
       K = 1

       mat = [[1, 2, 3, 4, 5],
       [6, 7, 8, 9, 10],
       [11, 12, 13, 14, 15],
       [16, 17, 18, 19, 20],
       [21, 22, 23, 24, 25]]

       printKthBorder(mat, N, K)

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
1   2  3  4  5 
6           10 
11          15 
16          20 
21 22 23 24 25 
```

**时间复杂度:**o(n^2)
T3】空间复杂度: O(1)