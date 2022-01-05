# 求同一矩阵的行列主序相加形成的矩阵的迹

> 原文:[https://www . geesforgeks . org/find-trace-matrix-formed-add-row-main-column-main-order-matrix/](https://www.geeksforgeeks.org/find-trace-matrix-formed-adding-row-major-column-major-order-matrix/)

给定两个整数 **N** 和 **M** 。考虑两个矩阵 **A <sub>NXM</sub> ，B<sub>NXM</sub>T9】。*矩阵 A 和矩阵 B 都包含 1 到 N*M 的元素*。矩阵 A 包含行主顺序的元素，矩阵 B 包含列主顺序的元素。任务是寻找 A 和 b 相加形成的矩阵的迹，矩阵 P 的迹 <sub>NXM</sub> 定义为 P[0][0] + P[1][1] + P[2][2] +…..+P[最小值(n-1，m-1)][最小值(n-1，m-1)]，即增加主对角线。
**注意–**矩阵 A 和矩阵 B 都包含 1 到 N*M 的元素**

**示例:**

```
Input : N = 3, M = 3
Output : 30
Therefore,
    1 2 3
A = 4 5 6
    7 8 9

    1 4 7
B = 2 5 8
    3 6 9

        2 6 10
A + B = 6 10 14
       10 14 18

Trace = 2 + 10 + 18 = 30
```

**方法 1(天真法):**
生成矩阵 A 和 B，求和。然后遍历主对角线，求和。

下面是该方法的实现:

## C++

```
// C++ program to find
// trace of matrix formed by
// adding Row-major and
// Column-major order of same matrix
#include <bits/stdc++.h>
using namespace std;

// Return the trace of
// sum of row-major matrix
// and column-major matrix
int trace(int n, int m)
{

    int A[n][m], B[n][m], C[n][m];   

    // Generating the matrix A
    int cnt = 1;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++) {
            A[i][j] = cnt;
            cnt++;
        }   

    // Generating the matrix A
    cnt = 1;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++) {
            B[j][i] = cnt;
            cnt++;
        }

    // Finding sum of matrix A and matrix B
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            C[i][j] = A[i][j] + B[i][j];   

    // Finding the trace of matrix C.
    int sum = 0;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            if (i == j)
                sum += C[i][j];

    return sum;
}

// Driven Program
int main()
{
    int N = 3, M = 3;
    cout << trace(N, M) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// trace of matrix formed by
// adding Row-major and
// Column-major order of same matrix
class GFG
{
    // Return the trace of
    // sum of row-major matrix
    // and column-major matrix
    static int trace(int n, int m)
    {

        int A[][] = new int[n][m];
        int B[][] = new int[n][m];
        int C[][] = new int[n][m];

        // Generating the matrix A
        int cnt = 1;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++) {
                A[i][j] = cnt;
                cnt++;
            }

        // Generating the matrix A
        cnt = 1;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++) {
                B[j][i] = cnt;
                cnt++;
            }

        // Finding sum of matrix A and matrix B
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
                C[i][j] = A[i][j] + B[i][j];

        // Finding the trace of matrix C.
        int sum = 0;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
                if (i == j)
                    sum += C[i][j];

        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 3, M = 3;

        System.out.println(trace(N, M));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find trace of matrix
# formed by adding Row-major and
# Column-major order of same matrix

# Return the trace of sum of row-major
# matrix and column-major matrix
def trace(n, m):

    A = [[0 for x in range(m)]
            for y in range(n)];
    B = [[0 for x in range(m)]
            for y in range(n)];
    C = [[0 for x in range(m)]
            for y in range(n)];

    # Generating the matrix A
    cnt = 1;
    for i in range(n):
        for j in range(m):
            A[i][j] = cnt;
            cnt += 1;

    # Generating the matrix A
    cnt = 1;
    for i in range(n):
        for j in range(m):
            B[j][i] = cnt;
            cnt += 1;

    # Finding sum of matrix A and matrix B
    for i in range(n):
        for j in range(m):
            C[i][j] = A[i][j] + B[i][j];

    # Finding the trace of matrix C.
    sum = 0;
    for i in range(n):
        for j in range(m):
            if (i == j):
                sum += C[i][j];

    return sum;

# Driver Code
N = 3;
M = 3;
print(trace(N, M));

# This code is contributed by mits
```

## C#

```
// C# program to find
// trace of matrix formed by
// adding Row-major and
// Column-major order of same matrix
using System;

class GFG {

    // Return the trace of
    // sum of row-major matrix
    // and column-major matrix
    static int trace(int n, int m)
    {
        int[, ] A = new int[n, m];
        int[, ] B = new int[n, m];
        int[, ] C = new int[n, m];

        // Generating the matrix A
        int cnt = 1;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++) {
                A[i, j] = cnt;
                cnt++;
            }

        // Generating the matrix A
        cnt = 1;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++) {
                B[j, i] = cnt;
                cnt++;
            }

        // Finding sum of matrix A and matrix B
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
                C[i, j] = A[i, j] + B[i, j];

        // Finding the trace of matrix C.
        int sum = 0;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
                if (i == j)
                    sum += C[i, j];

        return sum;
    }

    // Driver code
    public static void Main()
    {
        int N = 3, M = 3;
        Console.WriteLine(trace(N, M));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find trace of matrix
// formed by adding Row-major and
// Column-major order of same matrix

// Return the trace of sum of row-major
// matrix and column-major matrix
function trace($n, $m)
{

    $A = array_fill(0, $n, array_fill(0, $m, 0));
    $B = array_fill(0, $n, array_fill(0, $m, 0));
    $C = array_fill(0, $n, array_fill(0, $m, 0));

    // Generating the matrix A
    $cnt = 1;
    for ($i = 0; $i < $n; $i++)
        for ($j = 0; $j < $m; $j++)
        {
            $A[$i][$j] = $cnt;
            $cnt++;
        }

    // Generating the matrix A
    $cnt = 1;
    for ($i = 0; $i < $n; $i++)
        for ($j = 0; $j < $m; $j++)
        {
            $B[$j][$i] = $cnt;
            $cnt++;
        }

    // Finding sum of matrix A and matrix B
    for ($i = 0; $i < $n; $i++)
        for ($j = 0; $j < $m; $j++)
            $C[$i][$j] = $A[$i][$j] + $B[$i][$j];

    // Finding the trace of matrix C.
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        for ($j = 0; $j < $m; $j++)
            if ($i == $j)
                $sum += $C[$i][$j];

    return $sum;
}

// Driver Code
$N = 3;
$M = 3;
print(trace($N, $M));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// trace of matrix formed by
// adding Row-major and
// Column-major order of same matrix

// Return the trace of
// sum of row-major matrix
// and column-major matrix
function trace(n, m)
{

    let A = new Array(n);

    // Loop to create 2D array using 1D array
    for(var i = 0; i < A.length; i++)
    {
        A[i] = new Array(2);
    }

    let B = new Array(n);

    // Loop to create 2D array using 1D array
    for(var i = 0; i < B.length; i++)
    {
        B[i] = new Array(2);
    }

    let C = new Array(n);

    // Loop to create 2D array using 1D array
    for(var i = 0; i < C.length; i++)
    {
        C[i] = new Array(2);
    }

    // Generating the matrix A
    let cnt = 1;
    for(let i = 0; i < n; i++)
        for(let j = 0; j < m; j++)
        {
            A[i][j] = cnt;
            cnt++;
        }

    // Generating the matrix A
    cnt = 1;
    for(let i = 0; i < n; i++)
        for(let j = 0; j < m; j++)
        {
            B[j][i] = cnt;
            cnt++;
        }

    // Finding sum of matrix A and matrix B
    for(let i = 0; i < n; i++)
        for(let j = 0; j < m; j++)
            C[i][j] = A[i][j] + B[i][j];

    // Finding the trace of matrix C.
    let sum = 0;
    for(let i = 0; i < n; i++)
        for(let j = 0; j < m; j++)
            if (i == j)
                sum += C[i][j];

    return sum;
}

// Driver code
let N = 3, M = 3;

document.write(trace(N, M));

// This code is contributed by susmitakundugoaldanga

</script>
```

**输出:**

```
30
```

**时间复杂度:** O(N*M)。

**方法二(有效途径):**
基本上我们需要求第一个矩阵 A 的主对角线和第二个矩阵 b 的主对角线之和，
我们举个例子，N = 3，M = 4。
因此，行主矩阵将是，

```
     1  2  3  4
A =  5  6  7  8
     9 10 11 12
```

所以，我们需要 1，6，11 的和。
观察，它形成了一个等差数列，有若干列的常数差，m。
同样，第一个元素总是 1。所以，在行主矩阵的情况下形成的 AP 是 1，1+(M+1)，1+2*(M+1)，…..由 N(行数)个元素组成。而我们知道，
S<sub>n</sub>=(n *(a<sub>1</sub>+a<sub>n</sub>)/2
所以，n = R，a <sub>1</sub> = 1，a<sub>n</sub>= 1+(R–1)*(M+1)。
同样，在列-专业的情况下，形成的 AP 将是 1，1+(N+1)，1+2*(N+1)，…..
所以，n = R，a <sub>1</sub> = 1，a<sub>N</sub>= 1+(R–1)*(N+1)。

下面是该方法的实现:

## C++

```
// C++ program to find trace of matrix formed
// by adding Row-major and Column-major order
// of same matrix
#include <bits/stdc++.h>
using namespace std;

// Return sum of first n integers of an AP
int sn(int n, int an)
{
    return (n * (1 + an)) / 2;
}

// Return the trace of sum of row-major matrix
// and column-major matrix
int trace(int n, int m)
{
    // Finding nth element in
    // AP in case of Row major matrix.
    int an = 1 + (n - 1) * (m + 1);

    // Finding sum of first n integers
    // of AP in case of Row major matrix
    int rowmajorSum = sn(n, an);

    // Finding nth element in AP
    // in case of Row major matrix
    an = 1 + (n - 1) * (n + 1);

    // Finding sum of first n integers
    // of AP in case of Column major matrix
    int colmajorSum = sn(n, an);

    return rowmajorSum + colmajorSum;
}

// Driven Program
int main()
{
    int N = 3, M = 3;
    cout << trace(N, M) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find trace of matrix formed
// by adding Row-major and Column-major order
// of same matrix
import java.io.*;

public class GFG {

    // Return sum of first n integers of an AP
    static int sn(int n, int an)
    {
        return (n * (1 + an)) / 2;
    }

    // Return the trace of sum of row-major matrix
    // and column-major matrix
    static int trace(int n, int m)
    {
        // Finding nth element in
        // AP in case of Row major matrix.
        int an = 1 + (n - 1) * (m + 1);

        // Finding sum of first n integers
        // of AP in case of Row major matrix
        int rowmajorSum = sn(n, an);

        // Finding nth element in AP
        // in case of Row major matrix
        an = 1 + (n - 1) * (n + 1);

        // Finding sum of first n integers
        // of AP in case of Column major matrix
        int colmajorSum = sn(n, an);

        return rowmajorSum + colmajorSum;
    }

    // Driven Program
    static public void main(String[] args)
    {
        int N = 3, M = 3;
        System.out.println(trace(N, M));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find trace
# of matrix formed by adding
# Row-major and Column-major
# order of same matrix

# Return sum of first n
# integers of an AP
def sn(n, an):
    return (n * (1 + an)) / 2;

# Return the trace of sum
# of row-major matrix
# and column-major matrix
def trace(n, m):

    # Finding nth element
    # in AP in case of
    # Row major matrix.
    an = 1 + (n - 1) * (m + 1);

    # Finding sum of first
    # n integers of AP in
    # case of Row major matrix
    rowmajorSum = sn(n, an);

    # Finding nth element in AP
    # in case of Row major matrix
    an = 1 + (n - 1) * (n + 1);

    # Finding sum of first n
    # integers of AP in case
    # of Column major matrix
    colmajorSum = sn(n, an);

    return int(rowmajorSum +
               colmajorSum);

# Driver Code
N = 3;
M = 3;
print(trace(N, M));

# This code is contributed mits
```

## C#

```
// C# program to find trace of matrix formed
// by adding Row-major and Column-major order
// of same matrix
using System;

public class GFG {

    // Return sum of first n integers of an AP
    static int sn(int n, int an)
    {
        return (n * (1 + an)) / 2;
    }

    // Return the trace of sum of row-major matrix
    // and column-major matrix
    static int trace(int n, int m)
    {
        // Finding nth element in
        // AP in case of Row major matrix.
        int an = 1 + (n - 1) * (m + 1);

        // Finding sum of first n integers
        // of AP in case of Row major matrix
        int rowmajorSum = sn(n, an);

        // Finding nth element in AP
        // in case of Row major matrix
        an = 1 + (n - 1) * (n + 1);

        // Finding sum of first n integers
        // of AP in case of Column major matrix
        int colmajorSum = sn(n, an);

        return rowmajorSum + colmajorSum;
    }

    // Driven Program
    static public void Main()
    {
        int N = 3, M = 3;
        Console.WriteLine(trace(N, M));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find trace of matrix formed
// by adding Row-major and Column-major order
// of same matrix

// Return sum of first n integers of an AP
function sn($n, $an)
{
    return ($n * (1 + $an)) / 2;
}

// Return the trace of sum
// of row-major matrix
// and column-major matrix
function trace($n, $m)
{

    // Finding nth element in
    // AP in case of Row major matrix.
    $an = 1 + ($n - 1) * ($m + 1);

    // Finding sum of first n integers
    // of AP in case of Row major matrix
    $rowmajorSum = sn($n, $an);

    // Finding nth element in AP
    // in case of Row major matrix
    $an = 1 + ($n - 1) * ($n + 1);

    // Finding sum of first n integers
    // of AP in case of Column major matrix
    $colmajorSum = sn($n, $an);

    return $rowmajorSum + $colmajorSum;
}

    // Driver Code
    $N = 3;
    $M = 3;
    echo trace($N, $M),"\n";

// This code is contributed ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find trace of matrix formed
// by adding Row-major and Column-major order
// of same matrix

    // Return sum of first n integers of an AP
    function sn(n,an)
    {
        return (n * (1 + an)) / 2;
    }

    // Return the trace of sum of row-major matrix
    // and column-major matrix
    function trace(n,m)
    {
        // Finding nth element in
        // AP in case of Row major matrix.
        let an = 1 + (n - 1) * (m + 1);

        // Finding sum of first n integers
        // of AP in case of Row major matrix
        let rowmajorSum = sn(n, an);

        // Finding nth element in AP
        // in case of Row major matrix
        an = 1 + (n - 1) * (n + 1);

        // Finding sum of first n integers
        // of AP in case of Column major matrix
        let colmajorSum = sn(n, an);

        return rowmajorSum + colmajorSum;
    }

    // Driven Program

        let N = 3, M = 3;
        document.write(trace(N, M));

// This code is contributed
// by sravan kumar Gottumukkala

</script>
```

**输出:**

```
30
```