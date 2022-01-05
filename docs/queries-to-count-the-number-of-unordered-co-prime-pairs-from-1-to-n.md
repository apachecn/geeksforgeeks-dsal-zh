# 对从 1 到 N 的无序共质数对进行计数的查询

> 原文:[https://www . geesforgeks . org/query-to-count-number-of-unordered-co-prime-pairs-from-1-n/](https://www.geeksforgeeks.org/queries-to-count-the-number-of-unordered-co-prime-pairs-from-1-to-n/)

给定一个数字 n。任务是找到从 1 到 n 的无序互质整数对的数量。可以有多个查询。
**例:**

```
Input: 3
Output: 4
(1, 1), (1, 2), (1, 3), (2, 3)

Input: 4
Output: 6
(1, 1), (1, 2), (1, 3), (1, 4), (2, 3), (3, 4)
```

**方法:**这里[欧拉全能性函数](https://www.geeksforgeeks.org/eulers-totient-function-for-all-numbers-smaller-than-or-equal-to-n/)会有帮助。表示为φ(N)的欧拉全能函数是一个算术函数，它计算小于或等于 N 的正整数，这些正整数相对于 N 是素数。
其思想是利用欧拉全能函数的以下性质，即

1.  公式基本上说，对于 n 的所有质因数 p，**φ(n)的值等于 n 乘以(1–1/p)的乘积，例如**φ(6)= 6 *(1-1/2)*(1–1/3)= 2 的值。
2.  对于素数 p，φ(p)是 p-1。**例如**φ(5)是 4，φ(7)是 6，φ(13)是 12。这是显而易见的，从 1 到 p-1 的所有数字的 gcd 都是 1，因为 p 是质数。

现在，使用[前缀求和法求出 1 到 N 之间所有 I 的所有φ(x)的和。](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)利用这个，可以在 o(1)时间内回答。
以下是上述办法的实施情况。

## C++

```
// C++ program to find number of unordered
// coprime pairs of integers from 1 to N
#include <bits/stdc++.h>
using namespace std;
#define N 100005

// to store euler's totient function
int phi[N];

// to store required answer
int S[N];

// Computes and prints totient of all numbers
// smaller than or equal to N.
void computeTotient()
{
    // Initialise the phi[] with 1
    for (int i = 1; i < N; i++)
        phi[i] = i;

    // Compute other Phi values
    for (int p = 2; p < N; p++) {

        // If phi[p] is not computed already,
        // then number p is prime
        if (phi[p] == p) {

            // Phi of a prime number p is
            // always equal to p-1.
            phi[p] = p - 1;

            // Update phi values of all
            // multiples of p
            for (int i = 2 * p; i < N; i += p) {

                // Add contribution of p to its
                // multiple i by multiplying with
                // (1 - 1/p)
                phi[i] = (phi[i] / p) * (p - 1);
            }
        }
    }
}

// function to compute number coprime pairs
void CoPrimes()
{
    // function call to compute
    // euler totient function
    computeTotient();

    // prefix sum of all euler totient function values
    for (int i = 1; i < N; i++)
        S[i] = S[i - 1] + phi[i];
}

// Driver code
int main()
{
    // function call
    CoPrimes();

    int q[] = { 3, 4 };
    int n = sizeof(q) / sizeof(q[0]);

    for (int i = 0; i < n; i++)
        cout << "Number of unordered coprime\n"
             << "pairs of integers from 1 to "
             << q[i] << " are " << S[q[i]] << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of unordered
// coprime pairs of integers from 1 to N
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
static final int N = 100005;

// to store euler's
// totient function
static int[] phi;

// to store required answer
static int[] S ;

// Computes and prints totient
// of all numbers smaller than
// or equal to N.
static void computeTotient()
{
    // Initialise the phi[] with 1
    for (int i = 1; i < N; i++)
        phi[i] = i;

    // Compute other Phi values
    for (int p = 2; p < N; p++)
    {

        // If phi[p] is not computed
        // already, then number p is prime
        if (phi[p] == p)
        {

            // Phi of a prime number p
            // is always equal to p-1.
            phi[p] = p - 1;

            // Update phi values of
            // all multiples of p
            for (int i = 2 * p; i < N; i += p)
            {

                // Add contribution of p to
                // its multiple i by multiplying
                // with (1 - 1/p)
                phi[i] = (phi[i] / p) * (p - 1);
            }
        }
    }
}

// function to compute
// number coprime pairs
static void CoPrimes()
{
    // function call to compute
    // euler totient function
    computeTotient();

    // prefix sum of all euler
    // totient function values
    for (int i = 1; i < N; i++)
        S[i] = S[i - 1] + phi[i];
}

// Driver code
public static void main(String args[])
{
    phi = new int[N];
    S = new int[N];

    // function call
    CoPrimes();

    int q[] = { 3, 4 };
    int n = q.length;

    for (int i = 0; i < n; i++)
        System.out.println("Number of unordered coprime\n" +
                           "pairs of integers from 1 to " +
                                q[i] + " are " + S[q[i]] );
}
}

// This code is contributed
// by Subhadeep
```

## 蟒蛇 3

```
# Python3 program to find number
# of unordered coprime pairs of
# integers from 1 to N
N = 100005

# to store euler's totient function
phi = [0] * N

# to store required answer
S = [0] * N

# Computes and prints totient of all
# numbers smaller than or equal to N.
def computeTotient():

    # Initialise the phi[] with 1
    for i in range(1, N):
        phi[i] = i

    # Compute other Phi values
    for p in range(2, N) :

        # If phi[p] is not computed already,
        # then number p is prime
        if (phi[p] == p) :

            # Phi of a prime number p
            # is always equal to p-1.
            phi[p] = p - 1

            # Update phi values of all
            # multiples of p
            for i in range(2 * p, N, p) :

                # Add contribution of p to its
                # multiple i by multiplying with
                # (1 - 1/p)
                phi[i] = (phi[i] // p) * (p - 1)

# function to compute number
# coprime pairs
def CoPrimes():

    # function call to compute
    # euler totient function
    computeTotient()

    # prefix sum of all euler
    # totient function values
    for i in range(1, N):
        S[i] = S[i - 1] + phi[i]

# Driver code
if __name__ == "__main__":

    # function call
    CoPrimes()

    q = [ 3, 4 ]
    n = len(q)

    for i in range(n):
        print("Number of unordered coprime\n" +
              "pairs of integers from 1 to ",
               q[i], " are " , S[q[i]])

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find number
// of unordered coprime pairs
// of integers from 1 to N
using System;

class GFG
{
static int N = 100005;

// to store euler's
// totient function
static int[] phi;

// to store required answer
static int[] S ;

// Computes and prints totient
// of all numbers smaller than
// or equal to N.
static void computeTotient()
{
    // Initialise the phi[] with 1
    for (int i = 1; i < N; i++)
        phi[i] = i;

    // Compute other Phi values
    for (int p = 2; p < N; p++)
    {

        // If phi[p] is not computed
        // already, then number p is prime
        if (phi[p] == p)
        {

            // Phi of a prime number p
            // is always equal to p-1.
            phi[p] = p - 1;

            // Update phi values of
            // all multiples of p
            for (int i = 2 * p;
                     i < N; i += p)
            {

                // Add contribution of
                // p to its multiple i
                // by multiplying
                // with (1 - 1/p)
                phi[i] = (phi[i] / p) * (p - 1);
            }
        }
    }
}

// function to compute
// number coprime pairs
static void CoPrimes()
{
    // function call to compute
    // euler totient function
    computeTotient();

    // prefix sum of all euler
    // totient function values
    for (int i = 1; i < N; i++)
        S[i] = S[i - 1] + phi[i];
}

// Driver code
public static void Main()
{
    phi = new int[N];
    S = new int[N];

    // function call
    CoPrimes();

    int[] q = { 3, 4 };
    int n = q.Length;

    for (int i = 0; i < n; i++)
        Console.WriteLine("Number of unordered coprime\n" +
                           "pairs of integers from 1 to " +
                                q[i] + " are " + S[q[i]] );
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number
// of unordered coprime pairs
// of integers from 1 to N
$N = 100005;

// to store euler's totient function
$phi = array_fill(0, $N, 0);

// to store required answer
$S = array_fill(0, $N, 0);

// Computes and prints totient
// of all numbers smaller than
// or equal to N.
function computeTotient()
{
    global $N, $phi, $S;

    // Initialise the phi[] with 1
    for ($i = 1; $i < $N; $i++)
        $phi[$i] = $i;

    // Compute other Phi values
    for ($p = 2; $p < $N; $p++)
    {

        // If phi[p] is not computed
        // already, then number p
        // is prime
        if ($phi[$p] == $p)
        {

            // Phi of a prime number p
            // is always equal to p-1.
            $phi[$p] = $p - 1;

            // Update phi values of
            // all multiples of p
            for ($i = 2 * $p;
                 $i < $N; $i += $p)
            {

                // Add contribution of p
                // to its multiple i by
                // multiplying with (1 - 1/p)
                $phi[$i] = (int)(($phi[$i] /
                            $p) * ($p - 1));
            }
        }
    }
}

// function to compute
// number coprime pairs
function CoPrimes()
{
    global $N, $phi, $S;

    // function call to compute
    // euler totient function
    computeTotient();

    // prefix sum of all euler
    // totient function values
    for ($i = 1; $i < $N; $i++)
        $S[$i] = $S[$i - 1] + $phi[$i];
}

// Driver code

// function call
CoPrimes();

$q = array( 3, 4 );
$n = sizeof($q);

for ($i = 0; $i < $n; $i++)
    echo "Number of unordered coprime\n" .
         "pairs of integers from 1 to " .
         $q[$i] . " are ".$S[$q[$i]]."\n";

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find number of unordered
// coprime pairs of integers from 1 to N

    let N = 100005;

    // to store euler's
    // totient function
    let phi = new Array(N);

    // to store required answer
    let S = new Array(N);
    for(let i = 0; i < N; i++)
    {
        phi[i] = 0;
        S[i] = 0;
    }

    // Computes and prints totient
    // of all numbers smaller than
    // or equal to N.
    function computeTotient()
    {
        // Initialise the phi[] with 1
        for (let i = 1; i < N; i++)
        phi[i] = i;

    // Compute other Phi values
    for (let p = 2; p < N; p++)
    {

        // If phi[p] is not computed
        // already, then number p is prime
        if (phi[p] == p)
        {

            // Phi of a prime number p
            // is always equal to p-1.
            phi[p] = p - 1;

            // Update phi values of
            // all multiples of p
            for (let i = 2 * p; i < N; i += p)
            {

                // Add contribution of p to
                // its multiple i by multiplying
                // with (1 - 1/p)
                phi[i] = (phi[i] / p) * (p - 1);
            }
        }
    }
    }

    // function to compute
    // number coprime pairs
    function CoPrimes()
    {
        // function call to compute
    // euler totient function
    computeTotient();

    // prefix sum of all euler
    // totient function values
    for (let i = 1; i < N; i++)
        S[i] = S[i - 1] + phi[i];
    }

    // Driver code

    // function call
    CoPrimes();

    let q = [ 3, 4 ];
    let n = q.length;

    for (let i = 0; i < n; i++)
        document.write("Number of unordered coprime<br>" +
                           "pairs of integers from 1 to " +
                                q[i] + " are " + S[q[i]] +"<br>" );

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Number of unordered coprime
pairs of integers from 1 to 3 are 4
Number of unordered coprime
pairs of integers from 1 to 4 are 6
```