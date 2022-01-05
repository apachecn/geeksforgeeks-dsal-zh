# 检查两个给定矩阵是否相同的程序

> 原文:[https://www . geesforgeks . org/program-to-check-如果两个给定矩阵相同/](https://www.geeksforgeeks.org/program-to-check-if-two-given-matrices-are-identical/)

下面的程序检查大小为 4*4 的两个方阵是否相同。对于任何两个相等的矩阵，矩阵中的行数和列数都应该相等，相应的元素也应该相等。

## C++

```
// C++ Program to check if two
// given matrices are identical
#include <bits/stdc++.h>
#define N 4
using namespace std;

// This function returns 1 if A[][] and B[][] are identical
// otherwise returns 0
int areSame(int A[][N], int B[][N])
{
    int i, j;
    for (i = 0; i < N; i++)
        for (j = 0; j < N; j++)
            if (A[i][j] != B[i][j])
                return 0;
    return 1;
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

    if (areSame(A, B))
        cout << "Matrices are identical";
    else
        cout << "Matrices are not identical";
    return 0;
}
//This code is contributed by Shivi_Aggarwal
```

## C

```
// C Program to check if two
// given matrices are identical
#include <stdio.h>
#define N 4

// This function returns 1 if A[][] and B[][] are identical
// otherwise returns 0
int areSame(int A[][N], int B[][N])
{
    int i, j;
    for (i = 0; i < N; i++)
        for (j = 0; j < N; j++)
            if (A[i][j] != B[i][j])
                return 0;
    return 1;
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

    if (areSame(A, B))
        printf("Matrices are identical");
    else
        printf("Matrices are not identical");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if two
// given matrices are identical

class GFG
{
    static final int N = 4;

    // This function returns 1 if A[][]
    // and B[][] are identical
    // otherwise returns 0
    static int areSame(int A[][], int B[][])
    {
        int i, j;
        for (i = 0; i < N; i++)
            for (j = 0; j < N; j++)
                if (A[i][j] != B[i][j])
                    return 0;
            return 1;
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

        if (areSame(A, B) == 1)
            System.out.print("Matrices are identical");
        else
            System.out.print("Matrices are not identical");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 Program to check if two
# given matrices are identical

N = 4

# This function returns 1
# if A[][] and B[][] are identical
# otherwise returns 0
def areSame(A,B):

    for i in range(N):
        for j in range(N):
            if (A[i][j] != B[i][j]):
                return 0
    return 1

# driver code
A= [ [1, 1, 1, 1],
    [2, 2, 2, 2],
    [3, 3, 3, 3],
    [4, 4, 4, 4]]

B= [ [1, 1, 1, 1],
    [2, 2, 2, 2],
    [3, 3, 3, 3],
    [4, 4, 4, 4]]

if (areSame(A, B)==1):
    print("Matrices are identical")
else:
    print("Matrices are not identical")

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# Program to check if two
// given matrices are identical
using System;

class GFG {

    static int N = 4;

    // This function returns 1 if A[][]
    // and B[][] are identical
    // otherwise returns 0
    static int areSame(int [,]A, int [,]B)
    {
        int i, j;
        for (i = 0; i < N; i++)
            for (j = 0; j < N; j++)
                if (A[i,j] != B[i,j])
                    return 0;
            return 1;
    }

    // Driver code
    public static void Main ()
    {
        int [,]A = { {1, 1, 1, 1},
                    {2, 2, 2, 2},
                    {3, 3, 3, 3},
                    {4, 4, 4, 4}};

        int [,]B = { {1, 1, 1, 1},
                    {2, 2, 2, 2},
                    {3, 3, 3, 3},
                    {4, 4, 4, 4}};

        if (areSame(A, B) == 1)
            Console.WriteLine("Matrices "
                      + "are identical"); 
        else
            Console.WriteLine("Matrices "
                  + "are not identical");
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check if two
// given matrices are identical

// function returns 1 if A[][]
// and B[][] are identical
// otherwise returns 0
function areSame($A, $B)
{

    for($i = 0; $i < 4; $i++)
        for ($j = 0; $j < 4; $j++)
            if ($A[$i][$j] != $B[$i][$j])
                return 0;
    return 1;
}

// Driver Code
$A = array(array(1, 1, 1, 1),
           array(2, 2, 2, 2),
           array(3, 3, 3, 3),
           array(4, 4, 4, 4));

$B = array(array(1, 1, 1, 1),
           array(2, 2, 2, 2),
           array(3, 3, 3, 3),
           array(4, 4, 4, 4));

    if (areSame($A, $B) == 1)
        echo "Matrices are identical";
    else
        echo "Matrices are not identical";

// This code is contributed by Anuj_67
?>
```

## java 描述语言

```
<script>

// Javascript Program to check if two
// given matrices are identical

const N = 4;

// This function returns 1 if A[][]
// and B[][] are identical
// otherwise returns 0
function areSame(A, B)
{
    let i, j;
    for (i = 0; i < N; i++)
        for (j = 0; j < N; j++)
            if (A[i][j] != B[i][j])
                return 0;
    return 1;
}

    let A = [ [1, 1, 1, 1],
              [2, 2, 2, 2],
              [3, 3, 3, 3],
              [4, 4, 4, 4]];

    let B = [ [1, 1, 1, 1],
              [2, 2, 2, 2],
              [3, 3, 3, 3],
              [4, 4, 4, 4]];

    if (areSame(A, B))
        document.write("Matrices are identical");
    else
        document.write("Matrices are not identical");

</script>
```

**输出:**

```
Matrices are identical
```

该程序可以扩展到矩形矩阵。下面的帖子对扩展这个程序很有用。
[如何在 C 中传递一个 2D 数组作为参数？](https://www.geeksforgeeks.org/pass-2d-array-parameter-c/)
上述程序的时间复杂度为 O(n <sup>2</sup> )。

上述程序的辅助空间为 O(1)。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。