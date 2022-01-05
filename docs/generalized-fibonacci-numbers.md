# 广义斐波那契数

> 原文:[https://www . geesforgeks . org/generalized-Fibonacci-numbers/](https://www.geeksforgeeks.org/generalized-fibonacci-numbers/)

我们都知道[斐波那契数(Fn)](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/) 是由递推关系定义的

> 斐波那契数(Fn) = F(n-1) + F(n-2)
> 带有种子值
> F0 = 0 和 F1 = 1

同样，我们可以推广这些数字。这样的数列称为**广义斐波那契数(G)** 。
**广义斐波那契数(G)** 由递推关系定义

> 广义斐波那契数(Gn) = (c * G(n-1)) + (d * G(n-2))
> 带种子值
> G0 = a 和 G1 = b

### <u>寻找第 n 项</u>

给定广义斐波那契数的四个常数值为 **a、b、c** 、**和 d** 以及一个整数 **N** ，任务是找到广义斐波那契数的第 N 项，即 **Gn** 。

**示例:**

> **输入:** N = 2，a = 0，b = 1，c = 2，d = 3
> **输出:** 2
> **解释:**
> As a = 0->G(0)= 0
> b = 1->G(1)= 1
> 所以，G(2) = 2 * G(1) + 3 * G(0) = 2
> 
> **输入:** N = 3，a = 0，b = 1，c = 2，d = 3
> T3】输出: 7

**天真方法:**使用给定的值，找到数列的每个项直到第 n 项，然后打印第 n 项。
***时间复杂度:** O(2 <sup>N</sup> )*

**另一种方法:**想法是使用 [DP 制表](https://www.geeksforgeeks.org/tabulation-vs-memoization/)找到所有的术语，直到第 n 个术语，然后打印第 n 个术语。
***时间复杂度:** O(N)*

**高效方法:**利用[矩阵乘法](https://www.geeksforgeeks.org/matrix-multiplication-recursive/)我们可以在 log(N)时间内解决给定的问题。

> ![\small {Given\, G(0)=a\, and\, G(1)=b, \, therefore \, G(2)=c*a+d*b } \\ \small {} \\ \begin{bmatrix} G(2) & G(1)\\ G(1) & G(0) \end{bmatrix} = \begin{bmatrix} d*b+c*a & b\\ b & a \end{bmatrix} \newline \text {Multiplying matrices on RHS will eventually give us our LHS }\\ \begin{bmatrix} G(3) & G(2)\\ G(2) & G(1) \end{bmatrix} = \begin{bmatrix} G(2) & G(1)\\ G(1) & G(0) \end{bmatrix} * \begin{bmatrix} d & 1\\ c & 0 \end{bmatrix} \newline \text {One more step } \\ \begin{bmatrix} G(4) & G(3)\\ G(3) & G(2) \end{bmatrix} = \begin{bmatrix} G(3) & G(2)\\ G(2) & G(1) \end{bmatrix} * \begin{bmatrix} d & 1\\ c & 0 \end{bmatrix} \newline \text {So by looking at the sequence above we can generalize the Nth term as... }\\ \begin{bmatrix} G(N) & G(N-1)\\ G(N-1) & G(N-2) \end{bmatrix} = \begin{bmatrix} G(2) & G(1)\\ G(1) & G(0) \end{bmatrix} * \begin{bmatrix} d & 1\\ c & 0 \end{bmatrix} ^{\!N-2}\newline \text{Now }\begin{bmatrix} d & 1\\ c & 0 \end{bmatrix} ^{\!N-2}} \text{ can be solved in log(N) time complexity }   ](img/4a427ee0890cb1b2a11283aab3ec60d8.png "Rendered by QuickLaTeX.com")

下面是上述方法的实现:

## C++

```
// C++ program to implement the
// Generalised Fibonacci numbers
#include <bits/stdc++.h>
using namespace std;

// Helper function that multiplies
// 2 matrices F and M of size 2*2,
// and puts the multiplication
// result back to F[][]
void multiply(int F[2][2], int M[2][2]);

// Helper function that calculates F[][]
// raised to the power N
// and puts the result in F[][]
void power(int F[2][2], int N, int m, int n);

// Function to find the Nth term
int F(int N, int a, int b, int m, int n)
{
    // m 1
    // n 0
    int F[2][2] = { { m, 1 }, { n, 0 } };

    if (N == 0)
        return a;

    if (N == 1)
        return b;

    if (N == 2)
        return m * b + n * a;

    int initial[2][2]
        = { { m * b + n * a, b },
            { b, a } };

    power(F, N - 2, m, n);

    // Discussed above
    multiply(initial, F);

    return F[0][0];
}

// Function that multiplies
// 2 matrices F and M of size 2*2,
// and puts the multiplication
// result back to F[][]
void multiply(int F[2][2], int M[2][2])
{
    int x = F[0][0] * M[0][0] + F[0][1] * M[1][0];
    int y = F[0][0] * M[0][1] + F[0][1] * M[1][1];
    int z = F[1][0] * M[0][0] + F[1][1] * M[1][0];
    int w = F[1][0] * M[0][1] + F[1][1] * M[1][1];

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}

// Function that calculates F[][]
// raised to the power N
// and puts the result in F[][]
void power(int F[2][2], int N, int m, int n)
{
    int i;
    int M[2][2] = { { m, 1 }, { n, 0 } };

    for (i = 1; i <= N; i++)
        multiply(F, M);
}

// Driver code
int main()
{
    int N = 2, a = 0, b = 1, m = 2, n = 3;
    printf("%d\n", F(N, a, b, m, n));

    N = 3;
    printf("%d\n", F(N, a, b, m, n));

    N = 4;
    printf("%d\n", F(N, a, b, m, n));

    N = 5;
    printf("%d\n", F(N, a, b, m, n));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// Generalised Fibonacci numbers
import java.util.*;

class GFG{

// Function to find the Nth term
static int F(int N, int a, int b,
             int m, int n)
{
    // m 1
    // n 0
    int[][] F = { { m, 1 }, { n, 0 } };

    if (N == 0)
        return a;
    if (N == 1)
        return b;
    if (N == 2)
        return m * b + n * a;

    int[][] initial = { { m * b + n * a, b },
                        { b, a } };

    power(F, N - 2, m, n);

    // Discussed below
    multiply(initial, F);

    return F[0][0];
}

// Function that multiplies
// 2 matrices F and M of size 2*2,
// and puts the multiplication
// result back to F[][]
static void multiply(int[][] F, int[][] M)
{
    int x = F[0][0] * M[0][0] +
            F[0][1] * M[1][0];
    int y = F[0][0] * M[0][1] +
            F[0][1] * M[1][1];
    int z = F[1][0] * M[0][0] +
            F[1][1] * M[1][0];
    int w = F[1][0] * M[0][1] +
            F[1][1] * M[1][1];

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}

// Function that calculates F[][]
// raised to the power N
// and puts the result in F[][]
static void power(int[][] F, int N,
                  int m, int n)
{
    int i;
    int[][] M = { { m, 1 }, { n, 0 } };

    for(i = 1; i <= N; i++)
        multiply(F, M);
}

// Driver code
public static void main(String[] args)
{
    int N = 2, a = 0, b = 1, m = 2, n = 3;
    System.out.println(F(N, a, b, m, n));

    N = 3;
    System.out.println(F(N, a, b, m, n));

    N = 4;
    System.out.println(F(N, a, b, m, n));

    N = 5;
    System.out.println(F(N, a, b, m, n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement the
# Generalised Fibonacci numbers

# Function to find the Nth term
def F(N, a, b, m, n):

    # m 1
    # n 0
    F = [[ m, 1 ], [ n, 0 ]]

    if(N == 0):
        return a
    if(N == 1):
        return b
    if(N == 2):
        return m * b + n * a

    initial = [[ m * b + n * b, b ],
                           [ b, a ]]

    power(F, N - 2, m, n)

    multiply(initial, F)

    return F[0][0]

# Function that multiplies
# 2 matrices F and M of size 2*2,
# and puts the multiplication
# result back to F[][]
def multiply(F, M):

    x = (F[0][0] * M[0][0] +
         F[0][1] * M[1][0])

    y = (F[0][0] * M[0][1] +
         F[0][1] * M[1][1])

    z = (F[1][0] * M[0][0] +
         F[1][1] * M[1][0])

    w = (F[1][0] * M[0][1] +
         F[1][1] * M[1][1])

    F[0][0] = x
    F[0][1] = y
    F[1][0] = z
    F[1][1] = w

# Function that calculates F[][]
# raised to the power N
# and puts the result in F[][]
def power(F, N, m, n):

    M = [[ m, 1 ], [ n, 0 ]]
    for i in range(1, N + 1):
        multiply(F, M)

# Driver code
if __name__ == '__main__':

    N, a, b, m, n = 2, 0, 1, 2, 3
    print(F(N, a, b, m, n))

    N = 3
    print(F(N, a, b, m, n))

    N = 4
    print(F(N, a, b, m, n))

    N = 5
    print(F(N, a, b, m, n))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement the
// Generalised Fibonacci numbers
using System;
class GFG{

// Function to find the Nth term
static int F(int N, int a, int b,
             int m, int n)
{
    // m 1
    // n 0
    int[,] F = { { m, 1 }, { n, 0 } };
    if (N == 0)
        return a;
    if (N == 1)
        return b;
    if (N == 2)
        return m * b + n * a;
    int[,] initial = { { m * b + n * a, b },
                        { b, a } };
    power(F, N - 2, m, n);

    // Discussed below
    multiply(initial, F);
    return F[0, 0];
}

// Function that multiplies
// 2 matrices F and M of size 2*2,
// and puts the multiplication
// result back to F[,]
static void multiply(int[,] F, int[,] M)
{
    int x = F[0, 0] * M[0, 0] +
            F[0, 1] * M[1, 0];
    int y = F[0, 0] * M[0, 1] +
            F[0, 1] * M[1, 1];
    int z = F[1, 0] * M[0, 0] +
            F[1, 1] * M[1, 0];
    int w = F[1, 0] * M[0, 1] +
            F[1, 1] * M[1, 1];

    F[0, 0] = x;
    F[0, 1] = y;
    F[1, 0] = z;
    F[1, 1] = w;
}

// Function that calculates F[,]
// raised to the power N
// and puts the result in F[,]
static void power(int[,] F, int N,
                  int m, int n)
{
    int i;
    int[,] M = { { m, 1 }, { n, 0 } };
    for(i = 1; i <= N; i++)
        multiply(F, M);
}

// Driver code
public static void Main(String[] args)
{
    int N = 2, a = 0, b = 1, m = 2, n = 3;
    Console.WriteLine(F(N, a, b, m, n));
    N = 3;
    Console.WriteLine(F(N, a, b, m, n));
    N = 4;
    Console.WriteLine(F(N, a, b, m, n));
    N = 5;
    Console.WriteLine(F(N, a, b, m, n));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement the
// Generalised Fibonacci numbers

// Function to find the Nth term
function F(N, a, b, m, n)
{
    var F = [ [ m, 1 ], [ n, 0 ] ]

    if (N == 0)
        return a;
    if (N == 1)
        return b;
    if (N == 2)
        return m * b + n * a;

    var initial = [ [ m * b + n * a, b ], [ b, a ] ]

    power(F, N - 2, m, n);

    // Discussed below
    multiply(initial, F);

    return F[0][0];
}

// Function that multiplies
// 2 matrices F and M of size 2*2,
// and puts the multiplication
// result back to F[][]
function multiply(F, M)
{
    var x = F[0][0] * M[0][0] +
            F[0][1] * M[1][0];
    var y = F[0][0] * M[0][1] +
            F[0][1] * M[1][1];
    var z = F[1][0] * M[0][0] +
            F[1][1] * M[1][0];
    var w = F[1][0] * M[0][1] +
            F[1][1] * M[1][1];

    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}

// Function that calculates F[][]
// raised to the power N
// and puts the result in F[][]
function power(F, N, m, n)
{
    var i;
    var M = [ [ m, 1 ], [ n, 0 ] ];

    for(i = 1; i <= N; i++)
        multiply(F, M);
}

// Driver code
var N = 2, a = 0, b = 1, m = 2, n = 3;
document.write(F(N, a, b, m, n) + "</br>");

N = 3;
document.write(F(N, a, b, m, n) + "</br>");

N = 4;
document.write(F(N, a, b, m, n) + "</br>");

N = 5;
document.write(F(N, a, b, m, n));

// This code is contributed by Ankita saini

</script>
```

**Output:**

```
2
7
20
61
```