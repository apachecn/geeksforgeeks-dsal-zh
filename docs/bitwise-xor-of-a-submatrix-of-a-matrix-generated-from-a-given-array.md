# 从给定数组生成的矩阵的子矩阵的逐位异或

> 原文:[https://www . geeksforgeeks . org/从给定数组生成矩阵的子矩阵按位异或/](https://www.geeksforgeeks.org/bitwise-xor-of-a-submatrix-of-a-matrix-generated-from-a-given-array/)

给定一个长度为 **N、**的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，在数组 **arr[]** 上定义了一个尺寸矩阵 **N * N** ，其中 **M <sub>i，j</sub>= arr<sub>I</sub>T32】arr<sub>j</sub>T17】。给定四个整数 **X，Y，S** 和 **T** ，任务是从*左上角 **(X，Y)*** 到*右下角 **(S，T)*** 找到子矩阵所有元素的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。**

**示例:**

> **输入:** N = 3，A[] = {2，3，4}，(X，Y)=(0，1)，(S，T)=(2，2)
> **输出:** 5
> **说明:**
> A 上定义的矩阵为
> {(2&2)、(2 & 3)、(2 & 4)}、
> {(3 & 2)、(3 & 3)、(3 &
> 
> 最后，矩阵将为:
> {{2，2，0}，
> {2，3，0}，
> {0，0，4}}
> **XOR 值** = (2^0)^(3^0)^(0^4) = 5
> 
> **输入:** N=3，A[]={1，2，3}，(X，Y)=(0，1)，(S，T)=(1，2)
> **输出:** 1

**朴素方法:**最简单的方法是从给定的数组中生成矩阵 **M** ，并计算 M 的给定子矩阵中存在的所有元素的按位异或

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**有效方法:**想法是使用“异或”和“与”运算的以下分配属性:

> 只有男同性恋。同性恋帕拉自由，同性恋从帕拉-

因此，从左上方(X，Y)到右下方(S，T)的子矩阵的最终异或可以由以下等式计算:

> **最终异或**
> =(x)^(xor 行与 X+1)^.行的异或。。。s 排的^(xor)
> =(a<sub>x</sub>t26】(a<sub>y</sub>^.。。。^ a<sub>t</sub>)^。
> 。。。^(a<sub>s</sub>t27(a<sub>y</sub>^.。。。^a<sub>t</sub>)
> =(a<sub>y</sub>^.。。。^a<sub>t</sub>)&(a<sub>x</sub>^.。。^A <sub>S</sub>

*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)从索引 **Y** 到 **T** 并计算元素的**异或**。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)从索引 **X** 到 **S** 并计算元素的异或。
*   最后，计算计算出的异或的按位“与”，它等于子矩阵从(X，Y)到(S，T)的按位“异或”

下面是上述方法的实现:

## C++

```
// C++ program of the
// above approach

#include <iostream>
using namespace std;

// Function to find the submatrix
// XOR of the given matrix
int submatrix_xor(int* A, int N,
                  int X, int Y,
                  int S, int T)
{
    int left_xor = 0, i, right_xor = 0;

    // Calculating left xor
    // i.e A[Y]^A[Y+1]^. . .^A[T]
    for (i = Y; i <= T; i++) {
        left_xor ^= A[i];
    }

    // Calculating right xor
    // i.e A[X]^A[X+1]^. . .^A[S]
    for (i = X; i <= S; i++) {
        right_xor ^= A[i];
    }

    // Bitwise AND of left_xor and
    // right_xor gives required result
    return left_xor & right_xor;
}

// Driver Code
int main()
{
    int A[3] = { 2, 3, 4 }, X = 0,
        Y = 1, S = 2, T = 2, N = 3;

    // Printing xor of submatrix
    cout << submatrix_xor(A, N, X,
                          Y, S, T);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the
// above approach
import java.io.*;

class GFG{

// Function to find the submatrix
// XOR of the given matrix
static int submatrix_xor(int[] A, int N,
                         int X, int Y,
                         int S, int T)
{
    int left_xor = 0, i, right_xor = 0;

    // Calculating left xor
    // i.e A[Y]^A[Y+1]^. . .^A[T]
    for(i = Y; i <= T; i++)
    {
        left_xor ^= A[i];
    }

    // Calculating right xor
    // i.e A[X]^A[X+1]^. . .^A[S]
    for(i = X; i <= S; i++)
    {
        right_xor ^= A[i];
    }

    // Bitwise AND of left_xor and
    // right_xor gives required result
    return left_xor & right_xor;
}

// Driver Code
public static void main (String[] args)
{
    int[] A = { 2, 3, 4 };
    int X = 0, Y = 1, S = 2,
        T = 2, N = 3;

    // Printing xor of submatrix
    System.out.print(submatrix_xor(A, N, X,
                                   Y, S, T));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program of the
# above approach

# Function to find the submatrix
# XOR of the given matrix
def submatrix_xor(A, N, X, Y, S, T):

    left_xor = 0
    i = 0
    right_xor = 0

    # Calculating left xor
    # i.e A[Y]^A[Y+1]^. . .^A[T]
    for i in range(Y, T + 1):
        left_xor ^= A[i]

    # Calculating right xor
    # i.e A[X]^A[X+1]^. . .^A[S]
    for i in range(X, S + 1):
        right_xor ^= A[i]

    # Bitwise AND of left_xor and
    # right_xor gives required result
    return left_xor & right_xor

# Driver Code
if __name__ == '__main__':

    A = [ 2, 3, 4 ]
    X = 0
    Y = 1
    S = 2
    T = 2
    N = 3

    # Printing xor of submatrix
    print(submatrix_xor(A, N, X, Y, S, T))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach 
using System;

class GFG{

// Function to find the submatrix
// XOR of the given matrix
static int submatrix_xor(int[] A, int N,
                         int X, int Y,
                         int S, int T)
{
    int left_xor = 0, i, right_xor = 0;

    // Calculating left xor
    // i.e A[Y]^A[Y+1]^. . .^A[T]
    for(i = Y; i <= T; i++)
    {
        left_xor ^= A[i];
    }

    // Calculating right xor
    // i.e A[X]^A[X+1]^. . .^A[S]
    for(i = X; i <= S; i++)
    {
        right_xor ^= A[i];
    }

    // Bitwise AND of left_xor and
    // right_xor gives required result
    return left_xor & right_xor;
}

// Driver Code
public static void Main ()
{
    int[] A = { 2, 3, 4 };
    int X = 0, Y = 1, S = 2,
        T = 2, N = 3;

    // Printing xor of submatrix
    Console.Write(submatrix_xor(A, N, X,
                                Y, S, T));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the submatrix
// XOR of the given matrix
function submatrix_xor(A, N, X, Y, S, T)
{
    let left_xor = 0, i, right_xor = 0;

    // Calculating left xor
    // i.e A[Y]^A[Y+1]^. . .^A[T]
    for(i = Y; i <= T; i++)
    {
        left_xor ^= A[i];
    }

    // Calculating right xor
    // i.e A[X]^A[X+1]^. . .^A[S]
    for(i = X; i <= S; i++)
    {
        right_xor ^= A[i];
    }

    // Bitwise AND of left_xor and
    // right_xor gives required result
    return left_xor & right_xor;
}

// Driver code
    let A = [ 2, 3, 4 ];
    let X = 0, Y = 1, S = 2,
        T = 2, N = 3;

    // Printing xor of submatrix
    document.write(submatrix_xor(A, N, X,
                                   Y, S, T));

// This code is contributed by target_2.
</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N)，其中 N 为阵的大小*
T5**辅助空间:** O(1)