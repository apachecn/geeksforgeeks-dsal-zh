# 求解范围[0，N-1]

内 x 值的线性同余 Ax = B (mod N)

> 原文:[https://www . geeksforgeeks . org/solve-linear-同余-ax-b-mod-n-for-values-of-x-in-range-0-n-1/](https://www.geeksforgeeks.org/solve-linear-congruences-ax-b-mod-n-for-values-of-x-in-range-0-n-1/)

给定三个正整数 **A** 、 **B** 和 **N** ，它们表示形式 **AX=B (mod N)的一个[线性同余](https://www.geeksforgeeks.org/linear-congruence-method-for-generating-pseudo-random-numbers/)，**的任务是打印 **X (mod N)** 的所有可能值，即在满足此等式的范围**【0，N-1】**内。如果没有解决方案，请打印-1。

**示例:**

> **输入:** A=15，B=9，N=18
> **输出:** 15，3，9
> **说明:**满足 AX=B (mod N)条件的 X 的值为{3，9，15}。
> (15 * 15)% 18 = 225% 18 = 9
> (3 * 15)% 18 = 45% 18 = 9
> (9 * 15)% 18 = 135% 18 = 9
> 
> **输入:** A=9，B=21，N=30
> **输出:** 9，19，20

**方法:**该想法基于以下观察:

*   当且仅当 **B** 可被 [**GCD**](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) **(A，N)** 整除，即 **B%GCD(A，N)=0** 时，解存在。
*   **X (mod N)** 的解数为 **GCD(A，N)** 。

**证明:**

> 1.  Given that **ax = b (mod n)**
>     exists a number **y** so that **ax = b+ny**
>     T10] ax-ny = b-(1)
>     This is a [[](https://www.geeksforgeeks.org/linear-diophantine-equations/)
> 2.  Now, using [**to extend Euclidean algorithm,**](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/) **U** and **V** can be found as follows: **Au+NV = GCD (a, n) = D** (say)
>     
> 3.  Suppose
>     Therefore, **u * b/d** is the solution of equation 1.
> 4.  Let **x0** become **u * b/d** .
>     Therefore, the solution of **d** of equation 1 will be **x0, X0+(N/d), X0+2*(N/d), ..., x0+(d-1) * (n/d)**

按照以下步骤解决问题:

*   使用[扩展欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)将变量 **d** 初始化为 **GCD(A，N)** 以及 **u** 。
*   如果 **B** 不能被 **d** 整除，则打印-1 作为结果。
*   否则[使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，d-1】**中迭代，并在每次迭代中打印 **u*(B/d)+i*(N/d)** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to stores the values of x and y
// and find the value of gcd(a, b)
long long ExtendedEuclidAlgo(
    long long a, long long b,
    long long& x, long long& y)
{
    // Base Case
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    else {

        // Store the result of recursive call
        long long x1, y1;
        long long gcd
            = ExtendedEuclidAlgo(b, a % b, x1, y1);

        // Update x and y using results of
        // recursive call
        x = y1;
        y = x1 - floor(a / b) * y1;

        return gcd;
    }
}

// Function to give the distinct
// solutions of ax = b (mod n)
void linearCongruence(long long A,
                      long long B,
                      long long N)
{
    A = A % N;
    B = B % N;

    long long u = 0, v = 0;

    // Function Call to find
    // the value of d and u
    long long d = ExtendedEuclidAlgo(A, N, u, v);

    // No solution exists
    if (B % d != 0) {
        cout << -1 << endl;
        return;
    }

    // Else, initialize the value of x0
    long long x0 = (u * (B / d)) % N;
    if (x0 < 0)
        x0 += N;

    // Print all the answers
    for (long long i = 0; i <= d - 1; i++)
        cout << (x0 + i * (N / d)) % N << " ";
}

// Driver Code
int main()
{
    // Input
    long long A = 15;
    long long B = 9;
    long long N = 18;

    // Function Call
    linearCongruence(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to stores the values of x and y
// and find the value of gcd(a, b)
public static long[] ExtendedEuclidAlgo(long a,
                                        long b)
{

    // Base Case
    if (a == 0)
    {
        return new long[]{b, 0, 1};
    }
    else
    {

        // Store the result of recursive call
        long x1 = 1, y1 = 1;
        long gcdy[] = ExtendedEuclidAlgo(b % a, a);
        long gcd = gcdy[0];
        x1 = gcdy[1];
        y1 = gcdy[2];

        // Update x and y using results of
        // recursive call
        long y = x1;
        long x = y1 - (long)Math.floor(b / a) * x1;

        return new long[] {gcd, x, y};
    }
}

// Function to give the distinct
// solutions of ax = b (mod n)
public static void linearCongruence(long A,
                                    long B,
                                    long N)
{
    A = A % N;
    B = B % N;

    long u = 0, v = 0;

    // Function Call to find
    // the value of d and u
    long person[] = ExtendedEuclidAlgo(A, N);
    long d = person[0];
    u = person[1];
    v = person[2];

    // No solution exists
    if (B % d != 0)
    {
        System.out.println(-1);
        return;
    }

    // Else, initialize the value of x0
    long x0 = (u * (B / d)) % N;
    if (x0 < 0)
        x0 += N;

    // Print all the answers
    for(long i = 0; i <= d - 1; i++)
    {
        long an = (x0 + i * (N / d)) % N;
        System.out.print(an + " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Input
    long A = 15;
    long B = 9;
    long N = 18;

    // Function Call
    linearCongruence(A, B, N);
}
}

// This code is contributed by Shubhamsingh10
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to stores the values of x and y
# and find the value of gcd(a, b)
def ExtendedEuclidAlgo(a, b):

    # Base Case
    if a == 0 :
        return b, 0, 1

    gcd, x1, y1 = ExtendedEuclidAlgo(b % a, a)

    # Update x and y using results of recursive
    # call
    x = y1 - (b // a) * x1
    y = x1

    return gcd, x, y

# Function to give the distinct
# solutions of ax = b (mod n)
def linearCongruence(A, B, N):

    A = A % N
    B = B % N
    u = 0
    v = 0

    # Function Call to find
    # the value of d and u
    d, u, v = ExtendedEuclidAlgo(A, N)

    # No solution exists
    if (B % d != 0):
        print(-1)
        return

    # Else, initialize the value of x0
    x0 = (u * (B // d)) % N
    if (x0 < 0):
        x0 += N

    # Pr all the answers
    for i in range(d):
        print((x0 + i * (N // d)) % N, end = " ")

# Driver Code

# Input
A = 15
B = 9
N = 18

# Function Call
linearCongruence(A, B, N)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program for the above approach
using System;

class GFG{

    // Function to stores the values of x and y
    // and find the value of gcd(a, b)
    public static long[] ExtendedEuclidAlgo(long a,
                                            long b)
    {

        // Base Case
        if (a == 0)
        {
            return new long[]{b, 0, 1};
        }
        else
        {

            // Store the result of recursive call
            long x1 = 1, y1 = 1;
            long[] gcdy = ExtendedEuclidAlgo(b % a, a);
            long gcd = gcdy[0];
            x1 = gcdy[1];
            y1 = gcdy[2];

            // Update x and y using results of
            // recursive call
            long y = x1;
            long x = y1 - (long)(b / a) * x1;

            return new long[] {gcd, x, y};
        }
    }

    // Function to give the distinct
    // solutions of ax = b (mod n)
    public static void linearCongruence(long A,
                                        long B,
                                        long N)
    {
        A = A % N;
        B = B % N;

        long u = 0, v = 0;

        // Function Call to find
        // the value of d and u
        long []person = ExtendedEuclidAlgo(A, N);
        long d = person[0];
        u = person[1];
        v = person[2];

        // No solution exists
        if (B % d != 0)
        {
            Console.WriteLine(-1);
            return;
        }

        // Else, initialize the value of x0
        long x0 = (u * (B / d)) % N;
        if (x0 < 0)
            x0 += N;

        // Print all the answers
        for(long i = 0; i <= d - 1; i++)
        {
            long an = (x0 + i * (N / d)) % N;
            Console.Write(an + " ");
        }
    }

// Driver Code
    static public void Main (){

        // Input
        long A = 15;
        long B = 9;
        long N = 18;

        // Function Call
        linearCongruence(A, B, N);
    }
}

// This code is contributed by Shubhamsingh10
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to stores the values of x and y
// and find the value of gcd(a, b)
function ExtendedEuclidAlgo(a, b)
{

    // Base Case
    if (a == 0)
    {
        return [b, 0, 1];
    }
    else
    {

        // Store the result of recursive call
        let x1 = 1, y1 = 1;
        let gcdy = ExtendedEuclidAlgo(b % a, a);
        let gcd = gcdy[0];
        x1 = gcdy[1];
        y1 = gcdy[2];

        // Update x and y using results of
        // recursive call
        let y = x1;
        let x = y1 - Math.floor(b / a) * x1;

        return [gcd, x, y];
    }
}

// Function to give the distinct
// solutions of ax = b (mod n)
function linearCongruence(A, B, N)
{
    A = A % N;
    B = B % N;

    let u = 0, v = 0;

    // Function Call to find
    // the value of d and u
    let person = ExtendedEuclidAlgo(A, N);
    let d = person[0];
    u = person[1];
    v = person[2];

    // No solution exists
    if (B % d != 0)
    {
        document.write(-1);
        return;
    }

    // Else, initialize the value of x0
    let x0 = (u * (B / d)) % N;
    if (x0 < 0)
        x0 += N;

    // Print all the answers
    for(let i = 0; i <= d - 1; i++)
    {
        let an = (x0 + i * (N / d)) % N;
        document.write(an + " ");
    }
}

// Driver Code

    // Input
    let A = 15;
    let B = 9;
    let N = 18;

    // Function Call
    linearCongruence(A, B, N);

    // This code is contributed by sanjoy_62.
</script>
```

**Output**

```
15 3 9 
```

***时间复杂度:** O(log(min(A，N))*
***辅助空间:** O(1)*