# 求给定 N*N 矩阵特征值之和

> 原文:[https://www . geeksforgeeks . org/find-给定 nn 矩阵特征值之和/](https://www.geeksforgeeks.org/find-the-sum-of-eigen-values-of-the-given-nn-matrix/)

给定一个 **N*N** 矩阵 **mat[][]** ，任务是找到给定矩阵的特征值之和。
**例:**

> **输入:** mat[][] = {
> {2，-1，0}，
> {-1，2，-1}，
> {0，-1，2 } }
> T6】输出:6
> T9】输入: mat[][] = {
> {1，2，3，4}，
> {5，6，7，8}，
> {9，10，11，12}，
> { 0

**方法:**矩阵特征值之和等于矩阵的迹。n × n 正方形矩阵 A 的迹定义为 A 的主对角线(从左上角到右下角的对角线)上元素的和。
下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 4

// Function to return the sum of eigen
// values of the given matrix
int sumEigen(int mat[N][N])
{
    int sum = 0;

    // Calculate the sum of
    // the diagonal elements
    for (int i = 0; i < N; i++)
        sum += (mat[i][i]);

    return sum;
}

// Driver code
int main()
{
    int mat[N][N] = { { 1, 2, 3, 4 },
                      { 5, 6, 7, 8 },
                      { 9, 10, 11, 12 },
                      { 13, 14, 15, 16 } };

    cout << sumEigen(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

static int N = 4;

// Function to return the sum of eigen
// values of the given matrix
static int sumEigen(int mat[][])
{
    int sum = 0;

    // Calculate the sum of
    // the diagonal elements
    for (int i = 0; i < N; i++)
        sum += (mat[i][i]);

    return sum;
}

// Driver code
public static void main (String[] args)
{

    int mat[][] = { { 1, 2, 3, 4 },
                    { 5, 6, 7, 8 },
                    { 9, 10, 11, 12 },
                    { 13, 14, 15, 16 } };

    System.out.println (sumEigen(mat));
}
}

// The code is contributed by Tushil..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

N=4

# Function to return the sum of eigen
# values of the given matrix
def sumEigen(mat):

    sum = 0

    # Calculate the sum of
    # the diagonal elements
    for i in range(N):
        sum += (mat[i][i])

    return sum

# Driver code
mat= [ [ 1, 2, 3, 4 ],
    [ 5, 6, 7, 8 ],
    [ 9, 10, 11, 12 ],
    [ 13, 14, 15, 16 ] ]

print(sumEigen(mat))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int N = 4;

// Function to return the sum of eigen
// values of the given matrix
static int sumEigen(int [,]mat)
{
    int sum = 0;

    // Calculate the sum of
    // the diagonal elements
    for (int i = 0; i < N; i++)
        sum += (mat[i,i]);

    return sum;
}

// Driver code
static public void Main ()
{

    int [,]mat = { { 1, 2, 3, 4 },
                    { 5, 6, 7, 8 },
                    { 9, 10, 11, 12 },
                    { 13, 14, 15, 16 } };

    Console.Write(sumEigen(mat));
}
}

// The code is contributed by ajit...
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var N = 4;

// Function to return the sum of eigen
// values of the given matrix
function sumEigen(mat)
{
    var sum = 0;

    // Calculate the sum of
    // the diagonal elements
    for (var i = 0; i < N; i++)
        sum += (mat[i][i]);

    return sum;
}

// Driver code
var mat = [ [ 1, 2, 3, 4 ],
                  [ 5, 6, 7, 8 ],
                  [ 9, 10, 11, 12 ],
                  [ 13, 14, 15, 16 ] ];
document.write( sumEigen(mat));

</script>
```

**Output:** 

```
34
```