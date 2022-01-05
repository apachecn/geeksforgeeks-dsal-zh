# 矩阵减法程序

> 原文:[https://www.geeksforgeeks.org/program-subtraction-matices/](https://www.geeksforgeeks.org/program-subtraction-matices/)

下面的程序减去两个大小为 4*4 的方阵，我们可以为不同的维度改变 N。

## C++

```
// C++ program for subtraction of matrices
#include <bits/stdc++.h>
using namespace std;
#define N 4

// This function subtracts B[][] from A[][], and stores
// the result in C[][]
void subtract(int A[][N], int B[][N], int C[][N])
{
    int i, j;
    for (i = 0; i < N; i++)
        for (j = 0; j < N; j++)
            C[i][j] = A[i][j] - B[i][j];
}

// Driver code
int main()
{
    int A[N][N] = { {1, 1, 1, 1},
                    {2, 2, 2, 2},
                    {3, 3, 3, 3},
                    {4, 4, 4, 4}};

    int B[N][N] = { {1, 1, 1, 1},
                    {2, 2, 2, 2},
                    {3, 3, 3, 3},
                    {4, 4, 4, 4}};

    int C[N][N]; // To store result
    int i, j;
    subtract(A, B, C);

    cout << "Result matrix is " << endl;
    for (i = 0; i < N; i++)
    {
        for (j = 0; j < N; j++)
        cout << C[i][j] << " ";
        cout << endl;
    }

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include <stdio.h>
#define N 4

// This function subtracts B[][] from A[][], and stores
// the result in C[][]
void subtract(int A[][N], int B[][N], int C[][N])
{
    int i, j;
    for (i = 0; i < N; i++)
        for (j = 0; j < N; j++)
            C[i][j] = A[i][j] - B[i][j];
}

int main()
{
    int A[N][N] = { {1, 1, 1, 1},
                    {2, 2, 2, 2},
                    {3, 3, 3, 3},
                    {4, 4, 4, 4}};

    int B[N][N] = { {1, 1, 1, 1},
                    {2, 2, 2, 2},
                    {3, 3, 3, 3},
                    {4, 4, 4, 4}};

    int C[N][N]; // To store result
    int i, j;
    subtract(A, B, C);

    printf("Result matrix is \n");
    for (i = 0; i < N; i++)
    {
        for (j = 0; j < N; j++)
           printf("%d ", C[i][j]);
        printf("\n");
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for subtraction of matrices

class GFG
{
     static final int N=4;

    // This function subtracts B[][]
    // from A[][], and stores
    // the result in C[][]
    static void subtract(int A[][], int B[][], int C[][])
    {
        int i, j;
        for (i = 0; i < N; i++)
            for (j = 0; j < N; j++)
                C[i][j] = A[i][j] - B[i][j];
    }

    // Driver code
    public static void main (String[] args)
    {
        int A[][] = { {1, 1, 1, 1},
                        {2, 2, 2, 2},
                        {3, 3, 3, 3},
                        {4, 4, 4, 4}};

        int B[][] = { {1, 1, 1, 1},
                        {2, 2, 2, 2},
                        {3, 3, 3, 3},
                        {4, 4, 4, 4}};

        // To store result
        int C[][]=new int[N][N];

        int i, j;
        subtract(A, B, C);

        System.out.print("Result matrix is \n");
        for (i = 0; i < N; i++)
        {
            for (j = 0; j < N; j++)
            System.out.print(C[i][j] + " ");
            System.out.print("\n");
        }
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python 3 program for subtraction
# of matrices

N = 4

# This function returns 1
# if A[][] and B[][] are identical
# otherwise returns 0
def subtract(A, B, C):

    for i in range(N):
        for j in range(N):
            C[i][j] = A[i][j] - B[i][j]

# Driver Code
A = [ [1, 1, 1, 1],
      [2, 2, 2, 2],
      [3, 3, 3, 3],
      [4, 4, 4, 4]]

B = [ [1, 1, 1, 1],
      [2, 2, 2, 2],
      [3, 3, 3, 3],
      [4, 4, 4, 4]]

C = A[:][:] # To store result

subtract(A, B, C)

print("Result matrix is")
for i in range(N):
    for j in range(N):
        print(C[i][j], " ", end = '')
    print()

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program for subtraction of matrices
using System;

class GFG
{
static int N = 4;

// This function subtracts B[][]
// from A[][], and stores
// the result in C[][]
public static void subtract(int[][] A,
                            int[][] B,
                            int[, ] C)
{
    int i, j;
    for (i = 0; i < N; i++)
    {
        for (j = 0; j < N; j++)
        {
            C[i, j] = A[i][j] - B[i][j];
        }
    }
}

// Driver code
public static void Main(string[] args)
{
    int[][] A = new int[][]
    {
        new int[] {1, 1, 1, 1},
        new int[] {2, 2, 2, 2},
        new int[] {3, 3, 3, 3},
        new int[] {4, 4, 4, 4}
    };

    int[][] B = new int[][]
    {
        new int[] {1, 1, 1, 1},
        new int[] {2, 2, 2, 2},
        new int[] {3, 3, 3, 3},
        new int[] {4, 4, 4, 4}
    };

    // To store result

    int[, ] C = new int[N, N];

    int i, j;
    subtract(A, B, C);

    Console.Write("Result matrix is \n");
    for (i = 0; i < N; i++)
    {
        for (j = 0; j < N; j++)
        {
            Console.Write(C[i, j] + " ");
        }
        Console.Write("\n");
    }
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// This function subtracts B[][]
// from A[][], and stores the
// result in C[][]
function subtract(&$A, &$B, &$C)
{
    $N = 4;
    for ($i = 0; $i < $N; $i++)
        for ($j = 0; $j < $N; $j++)
            $C[$i][$j] = $A[$i][$j] -
                         $B[$i][$j];
}

// Driver code
$N = 4;
$A = array(array(1, 1, 1, 1),
           array(2, 2, 2, 2),
           array(3, 3, 3, 3),
           array(4, 4, 4, 4));

$B = array(array(1, 1, 1, 1),
           array(2, 2, 2, 2),
           array(3, 3, 3, 3),
           array(4, 4, 4, 4));

subtract($A, $B, $C);

echo "Result matrix is \n";
for ($i = 0; $i < $N; $i++)
{
    for ($j = 0; $j < $N; $j++)
    {
        echo $C[$i][$j];
        echo " ";
    }
        echo "\n";
}

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program for subtraction of matrices
var N = 4;

// This function subtracts B[][] from A[][], and stores
// the result in C[][]
function subtract(A, B, C)
{
    var i, j;
    for (i = 0; i < N; i++)
        for (j = 0; j < N; j++)
            C[i][j] = A[i][j] - B[i][j];
}

// Driver code
var A = [ [1, 1, 1, 1],
                [2, 2, 2, 2],
                [3, 3, 3, 3],
                [4, 4, 4, 4]];
var B = [ [1, 1, 1, 1],
                [2, 2, 2, 2],
                [3, 3, 3, 3],
                [4, 4, 4, 4]];
var C = Array.from(Array(N), () => Array(N)); // To store result
var i, j;
subtract(A, B, C);
document.write( "Result matrix is " + "<br>");
for (i = 0; i < N; i++)
{
    for (j = 0; j < N; j++)
        document.write( C[i][j] + " ");
    document.write("<br>");
}

// This code is contributed by itsok.
</script>
```

**输出:**

```
Result matrix is
0 0 0 0
0 0 0 0
0 0 0 0
0 0 0 0
```

**注–**第一个矩阵第 0 行第 0 列的数字减去第二个矩阵第 0 行第 0 列的数字。并且其减法结果被初始化为结果矩阵的第 0 行和第 0 列的值。对所有元素应用相同的减法过程

该程序可以扩展到矩形矩阵。下面的帖子对扩展这个程序很有用。
[如何在 C 中传递一个 2D 数组作为参数？](https://www.geeksforgeeks.org/pass-2d-array-parameter-c/)
上述程序的时间复杂度为 O(n <sup>2</sup> )。

以上程序的辅助空间为 O(n <sup>2</sup> )。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。