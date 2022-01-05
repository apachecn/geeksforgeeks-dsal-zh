# 求两个矩阵的交集

> 原文:[https://www . geeksforgeeks . org/find-两个矩阵的交集/](https://www.geeksforgeeks.org/find-the-intersection-of-two-matrices/)

给定两个相同顺序的矩阵 **A[][]** 和**B[][]****m * n**。任务是找到两个矩阵的交集为 C，其中:

*   **C<sub>ij</sub>= A<sub>ij</sub>T5 如果 A <sub>ij</sub> = B <sub>ij</sub>**
*   **C**=“*”，否则。

**示例:**

```
Input : 
A[N][N] = {{2, 4, 6, 8},
           {1, 3, 5, 7},
           {8, 6, 4, 2},
           {7, 5, 3, 1}};

B[N][N] = {{0, 4, 3, 8},
           {1, 3, 5, 7},
           {8, 3, 6, 2},
           {4, 5, 3, 4}};
Output :
* 4 * 8 
1 3 5 7 
8 * * 2 
* 5 3 * 
```

由于两个集合的交集是包含两个集合的公共元素的集合，因此类似地，两个矩阵的交集将只包含对应的公共元素，并将“*”放置在其余不匹配元素的位置。
要找到两个矩阵的交集，只需迭代它们的大小并打印*如果两个矩阵中特定位置的元素不相等，则打印该元素。
以下是上述方法的实现:

## C++

```
// CPP program to find intersection
// of two matrices

#include <bits/stdc++.h>
#define N 4
#define M 4

using namespace std;

// Function to print the resultant matrix
void printIntersection(int A[][N], int B[][N])
{
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {

            // print element value for equal
            // elements else *
            if (A[i][j] == B[i][j])
                cout << A[i][j] << " ";
            else
                cout << "* ";
        }

        cout << "\n";
    }
}

// Driver Code
int main()
{
    int A[M][N] = { { 2, 4, 6, 8 },
                    { 1, 3, 5, 7 },
                    { 8, 6, 4, 2 },
                    { 7, 5, 3, 1 } };
    int B[M][N] = { { 2, 3, 6, 8 },
                    { 1, 3, 5, 2 },
                    { 8, 1, 4, 2 },
                    { 3, 5, 4, 1 } };

    printIntersection(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//  Java program to find intersection
// of two matrices

import java.io.*;

class GFG {
  static int N = 4;
static int M = 4;

// Function to print the resultant matrix
static void printIntersection(int A[][], int B[][])
{
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {

            // print element value for equal
            // elements else *
            if (A[i][j] == B[i][j])
                System.out.print(A[i][j] +" ");
            else
                System.out.print( "* ");
        }

        System.out.println( " ");
    }
}

// Driver Code

    public static void main (String[] args) {
           int A[][] = { { 2, 4, 6, 8 },
                    { 1, 3, 5, 7 },
                    { 8, 6, 4, 2 },
                    { 7, 5, 3, 1 } };
    int B[][] = { { 2, 3, 6, 8 },
                    { 1, 3, 5, 2 },
                    { 8, 1, 4, 2 },
                    { 3, 5, 4, 1 } };

    printIntersection(A, B);

    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to find intersection
# of two matrices
N, M = 4, 4

# Function to print the resultant matrix
def printIntersection(A, B) :

    for i in range(M) :
        for j in range(N) :

            # print element value for equal
            # elements else *
            if (A[i][j] == B[i][j]) :
                print(A[i][j], end = " ")
            else :
                print("* ", end = " ")

        print()

# Driver Code
if __name__ == "__main__" :

    A = [ [2, 4, 6, 8 ],
        [ 1, 3, 5, 7 ],
        [ 8, 6, 4, 2 ],
        [ 7, 5, 3, 1 ] ]

    B = [ [ 2, 3, 6, 8 ],
        [ 1, 3, 5, 2 ],
        [ 8, 1, 4, 2 ],
        [ 3, 5, 4, 1 ] ]

    printIntersection(A, B)

# This code is contributed by Ryuga
```

## C#

```
// C# program to find intersection
// of two matrices

using System;

class GFG {
static int N = 4;
static int M = 4;

// Function to print the resultant matrix
static void printIntersection(int [,]A, int [,]B)
{
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {

            // print element value for equal
            // elements else *
            if (A[i,j] == B[i,j])
                Console.Write(A[i,j] +" ");
            else
                Console.Write( "* ");
        }

        Console.WriteLine( " ");
    }
}

// Driver Code

    public static void Main () {
        int [,]A = { { 2, 4, 6, 8 },
                    { 1, 3, 5, 7 },
                    { 8, 6, 4, 2 },
                    { 7, 5, 3, 1 } };
    int [,]B = { { 2, 3, 6, 8 },
                    { 1, 3, 5, 2 },
                    { 8, 1, 4, 2 },
                    { 3, 5, 4, 1 } };

    printIntersection(A, B);

    }
}
// This code is contributed by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find intersection
// of two matrices

// Function to print the resultant matrix
function printIntersection($A, $B)
{
    $N = 4; $M = 4;
    for ($i = 0; $i < $M; $i++)
    {
        for ($j = 0; $j < $N; $j++)
        {

            // print element value for equal
            // elements else *
            if ($A[$i][$j] == $B[$i][$j])
                echo $A[$i][$j] . " ";
            else
                echo "* ";
        }

        echo "\n";
    }
}

// Driver Code
$A = array(array(2, 4, 6, 8 ),
        array(1, 3, 5, 7 ),
        array(8, 6, 4, 2 ),
        array(7, 5, 3, 1 ) );

$B = array(array(2, 3, 6, 8 ),
        array(1, 3, 5, 2 ),
        array(8, 1, 4, 2 ),
        array(3, 5, 4, 1 ) );

printIntersection($A, $B);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to find intersection
// of two matrices

var N = 4
var M = 4

// Function to print the resultant matrix
function printIntersection( A, B)
{
    for (var i = 0; i < M; i++) {
        for (var j = 0; j < N; j++) {

            // print element value for equal
            // elements else *
            if (A[i][j] == B[i][j])
                document.write( A[i][j] + " ");
            else
                document.write( "* ");
        }

        document.write( "<br>");
    }
}

// Driver Code
var A = [ [ 2, 4, 6, 8 ],
                [ 1, 3, 5, 7 ],
                [ 8, 6, 4, 2 ],
                [ 7, 5, 3, 1 ] ];
var B = [ [ 2, 3, 6, 8 ],
                [ 1, 3, 5, 2 ],
                [ 8, 1, 4, 2 ],
                [ 3, 5, 4, 1 ] ];
printIntersection(A, B);

</script>
```

**Output:** 

```
2 * 6 8 
1 3 5 * 
8 * 4 2 
* 5 * 1
```

***时间复杂度:** O(M * N)*

***辅助空间:** O(1)*