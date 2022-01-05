# 求有向图中长度为 K 的路径数

> 原文:[https://www . geeksforgeeks . org/find-有向图中长度为 k 的路径数/](https://www.geeksforgeeks.org/find-the-number-of-paths-of-length-k-in-a-directed-graph/)

给定一个有向的、未加权的图，图中有 **N** 个顶点和一个整数 **K** 。任务是为每对顶点 **(u，v)** 找到长度为 **K** 的路径数。路径不必很简单，也就是说，在一条路径中，顶点和边可以被访问任意多次。
图表示为[邻接矩阵](https://www.geeksforgeeks.org/graph-and-its-representations/)，其中值 **G[i][j] = 1** 表示从顶点 **i** 到顶点 **j** ， **G[i][j] = 0** 表示从 **i** 到 **j** 没有边。
**举例:**

> **输入:** K = 2，
> 
> ![](img/78e899912130bd39bf65cdd52626e851.png)
> 
> **输出:**
> 1 2 2
> 0 1 0
> 0 0 1
> 长度为 k 的从 0 到 0 的路径数为 1({ 0->0->0)
> 长度为 k 的从 0 到 1 的路径数为 2({0- > 0- > 1}、{ 0->2->1)
> 长度为 k 的从 0 到 2 的路径数为 2({ 0-> {0- > 1- > 2})
> 长度为 K 的从 1 到 1 的路径数为 1({1- > 2- > 1})
> 长度为 K 的从 2 到 2 的路径数为 1({2- > 1- > 2})
> **输入:** K = 3，
> 
> ![](img/c75d36558b147a6b373a56621645a7af.png)
> 
> **输出:**
> 1 0 0
> 0 1 0
> 0 0 1
> 长度为 k 的从 0 到 0 的路径数为 1({ 0->1->2->0)
> 长度为 k 的从 1 到 1 的路径数为 1({ 1->2->0->1)
> 长度为 k 的从 2 到 2 的路径数为 1({2- > 1-

**先决条件:** [矩阵求幂](https://www.geeksforgeeks.org/matrix-exponentiation/)、[矩阵乘法](https://www.geeksforgeeks.org/c-program-multiply-two-matrices/)
**方法:**显而易见，对于 **k = 1** 的情况，给定邻接矩阵就是问题的答案。它包含每对顶点之间长度为 **1** 的路径数量。
我们假设有些 **k** 的答案是**Mat<sub>k</sub>T19**k+1**的答案是**Mat<sub>k+1</sub>T25】。
**Mat<sub>k+1</sub>【I】【j】=∑<sub>p = 1</sub><sup>N</sup>Mat<sub>k</sub>【I】【p】* G【p】【j】**
很容易看出，除了矩阵**Mat<sub>k</sub>T41】和 **G** 的乘积之外，公式什么也不会计算，即** 问题的解决方法可以表示为**Mat<sub>k</sub>= G * G *……* G(k 次)= G <sup>k</sup>**
以下是上述方法的实现:**** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define N 3

// Function to multiply two matrices
void multiply(int a[][N], int b[][N], int res[][N])
{
    int mul[N][N];
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            mul[i][j] = 0;
            for (int k = 0; k < N; k++)
                mul[i][j] += a[i][k] * b[k][j];
        }
    }

    // Storing the multiplication result in res[][]
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            res[i][j] = mul[i][j];
}

// Function to compute G raised to the power n
void power(int G[N][N], int res[N][N], int n)
{

    // Base condition
    if (n == 1) {
        for (int i = 0; i < N; i++)
            for (int j = 0; j < N; j++)
                res[i][j] = G[i][j];
        return;
    }

    // Recursion call for first half
    power(G, res, n / 2);

    // Multiply two halves
    multiply(res, res, res);

    // If n is odd
    if (n % 2 != 0)
        multiply(res, G, res);
}

// Driver code
int main()
{
    int G[N][N] = { { 1, 1, 1 },
                    { 0, 0, 1 },
                    { 0, 1, 0 } };

    int k = 2, res[N][N];

    power(G, res, k);

    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++)
            cout << res[i][j] << " ";
        cout << "\n";
    }

    return 0;
}
// This Code is improved by cidacoder
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int N = 3;

// Function to multiply two matrices
static void multiply(int a[][], int b[][], int res[][])
{
    int [][]mul = new int[N][N];
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
        {
            mul[i][j] = 0;
            for (int k = 0; k < N; k++)
                mul[i][j] += a[i][k] * b[k][j];
        }
    }

    // Storing the multiplication result in res[][]
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            res[i][j] = mul[i][j];
}

// Function to compute G raised to the power n
static void power(int G[][], int res[][], int n)
{

    // Base condition
    if (n == 1) {
        for (int i = 0; i < N; i++)
            for (int j = 0; j < N; j++)
                res[i][j] = G[i][j];
        return;
    }

    // Recursion call for first half
    power(G, res, n / 2);

    multiply(res, res, res);

    // If n is odd
    if (n % 2 != 0)
        multiply(res, G, res);
}

// Driver code
public static void main(String[] args)
{
    int G[][] = { { 1, 1, 1 },
                    { 0, 0, 1 },
                    { 0, 1, 0 } };

    int k = 2;
    int [][]res = new int[N][N];

    power(G, res, k);

    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
            System.out.print(res[i][j] + " ");
        System.out.println("");
    }
}
}

// This code is contributed by 29AjayKumar
// This Code is improved by cidacoder
```

## 蟒蛇 3

```
# Python3 implementation of the approach

import numpy as np

N = 3

# Function to multiply two matrices
def multiply(a, b, res) :

    mul = np.zeros((N,N));

    for i in range(N) :
        for j in range(N) :
            mul[i][j] = 0;
            for k in range(N) :
                mul[i][j] += a[i][k] * b[k][j];

    # Storing the multiplication result in res[][]
    for i in range(N) :
        for j in range(N) :
            res[i][j] = mul[i][j];

# Function to compute G raised to the power n
def power(G, res, n) :

    # Base condition
    if (n == 1) :
        for i in range(N) :
            for j in range(N) :
                res[i][j] = G[i][j];
        return;

    # Recursion call for first half
    power(G, res, n // 2);

    # Multiply two halves
    multiply(res, res, res);

    # If n is odd
    if (n % 2 != 0) :
        multiply(res, G, res);

# Driver code
if __name__ == "__main__" :

    G = [
        [ 1, 1, 1 ],
        [ 0, 0, 1 ],
        [ 0, 1, 0 ]
        ];

    k = 2;
    res = np.zeros((N,N));

    power(G, res, k);

    for i in range(N) :
        for j in range(N) :
            print(res[i][j],end = " ");

        print()

# This code is contributed by AnkitRai01
# This Code is improved by cidacoder
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int N = 3;

// Function to multiply two matrices
static void multiply(int [,]a, int [,]b, int [,]res)
{
    int [,]mul = new int[N,N];
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
        {
            mul[i,j] = 0;
            for (int k = 0; k < N; k++)
                mul[i,j] += a[i,k] * b[k,j];
        }
    }

    // Storing the multiplication result in res[][]
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            res[i,j] = mul[i,j];
}

// Function to compute G raised to the power n
static void power(int [,]G, int [,]res, int n)
{

    // Base condition
    if (n == 1) {
        for (int i = 0; i < N; i++)
            for (int j = 0; j < N; j++)
                res[i,j] = G[i,j];
        return;
    }

    // Recursion call for first half
    power(G, res, n / 2);

    // Multiply two halves
    multiply(res, res, res);

    // If n is odd
    if (n % 2 != 0)
        multiply(res, G, res);
}

// Driver code
public static void Main()
{
    int [,]G = { { 1, 1, 1 },
                    { 0, 0, 1 },
                    { 0, 1, 0 } };

    int k = 2;
    int [,]res = new int[N,N];

    power(G, res, k);

    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
            Console.Write(res[i,j] + " ");
        Console.WriteLine("");
    }
}
}

// This code is contributed by anuj_67..
// This code is improved by cidacoder
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let N = 3;

    // Function to multiply two matrices
    function multiply(a, b, res)
    {
        let mul = new Array(N);
        for (let i = 0; i < N; i++)
        {
            mul[i] = new Array(N);
            for (let j = 0; j < N; j++)
            {
                mul[i][j] = 0;
                for (let k = 0; k < N; k++)
                    mul[i][j] += a[i][k] * b[k][j];
            }
        }

        // Storing the multiplication result in res[][]
        for (let i = 0; i < N; i++)
            for (let j = 0; j < N; j++)
                res[i][j] = mul[i][j];
    }

    // Function to compute G raised to the power n
    function power(G, res, n)
    {

        // Base condition
        if (n == 1) {
            for (let i = 0; i < N; i++)
                for (let j = 0; j < N; j++)
                    res[i][j] = G[i][j];
            return;
        }

        // Recursion call for first half
        power(G, res, parseInt(n / 2, 10));

        // Multiply two halves
        multiply(res, res, res);

        // If n is odd
        if (n % 2 != 0)
            multiply(res, G, res);
    }

    let G = [ [ 1, 1, 1 ],
             [ 0, 0, 1 ],
             [ 0, 1, 0 ] ];

    let k = 2;
    let res = new Array(N);
    for (let i = 0; i < N; i++)
    {
        res[i] = new Array(N);
        for (let j = 0; j < N; j++)
        {
            res[i][j] = 0;
        }
    }

    power(G, res, k);

    for (let i = 0; i < N; i++)
    {
        for (let j = 0; j < N; j++)
            document.write(res[i][j] + " ");
        document.write("</br>");
    }

</script>
```

**Output:** 

```
1 2 2 
0 1 0 
0 0 1
```

**时间复杂度–**
由于我们必须将邻接矩阵 log(k)乘以(使用矩阵求幂)，算法的时间复杂度为**o((|v|^3)*log(k)】**，其中 v 为顶点数，k 为路径长度。