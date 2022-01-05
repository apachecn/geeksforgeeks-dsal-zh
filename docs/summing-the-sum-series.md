# 求和系列

> 原文:[https://www.geeksforgeeks.org/summing-the-sum-series/](https://www.geeksforgeeks.org/summing-the-sum-series/)

定义了一个函数，该函数将第一个 **N 个**自然数之和的**乘以**和(N)** 。你的任务是将函数修改为 **sumX(N，M，K)** 计算**和(K +和(K +和(K+…和(K+N)……)))】**，继续 M 项。对于给定的 **N、M 和 K** 计算 **sumX(N、M、K)** 的值。
**注意:**由于答案可能会很大，所以在**中打印答案取模 10^9 + 7** 。
**例:**** 

> **输入:** N = 1，M = 2，K = 3
> **输出:** 552
> 对于 M = 2
> 和(3 +和(3 + 1)) =和(3 + 20) = 552。
> **输入:** N = 3，M =3，K = 2
> **输出:** 1120422
> 对于 M = 3
> 和(2 +和(2 +和(2 + 3))) =和(2 +和(2 + 30)) =和(2 + 1056) = 1120422。

**进场:**

*   使用公式 **N*(N + 1)** 计算**和(N)** 的值。
*   运行循环 **M** 次，每次将 **K** 加到前面的答案上，并应用 **sum(prev_ans + K)** ，每次取 10^9 + 7 的模。
*   最后打印 **sumX(N，M，K)** 的值。

以下是上述方法的实现:

## C++

```
// C++ program to calculate the 
// terms of summing of sum series

#include <iostream>

using namespace std;
# define MOD 1000000007

// Function to calculate
// twice of sum of first N natural numbers
long sum(long N){

    long val = N * (N+1);
    val = val % MOD;

    return val;
}

// Function to calculate the
// terms of summing of sum series
int sumX(int N, int M, int K){

    for (int i = 0; i < M; i++) {
        N = (int)sum(K + N);
    }

    N = N % MOD;
    return N;
}

// Driver Code
int main()
{
    int N = 1, M = 2, K = 3;
    cout << sumX(N, M, K) << endl;

    return 0;
}

// This code is contributed by Rituraj Jain
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the
// terms of summing of sum series

import java.io.*;
import java.util.*;
import java.lang.*;

class GFG {

    static int MOD = 1000000007;

    // Function to calculate
    // twice of sum of first N natural numbers
    static long sum(long N)
    {
        long val = N * (N + 1);

        // taking modulo 10 ^ 9 + 7
        val = val % MOD;

        return val;
    }

    // Function to calculate the
    // terms of summing of sum series
    static int sumX(int N, int M, int K)
    {
        for (int i = 0; i < M; i++) {
            N = (int)sum(K + N);
        }
        N = N % MOD;
        return N;
    }

    // Driver code
    public static void main(String args[])
    {
        int N = 1, M = 2, K = 3;
        System.out.println(sumX(N, M, K));
    }
}
```

## 蟒蛇 3

```
# Python3 program to calculate the 
# terms of summing of sum series

MOD = 1000000007

# Function to calculate
# twice of sum of first N natural numbers
def Sum(N):

    val = N * (N + 1)

    # taking modulo 10 ^ 9 + 7
    val = val % MOD

    return val

# Function to calculate the
# terms of summing of sum series
def sumX(N, M, K):

    for i in range(M):
        N = int(Sum(K + N))

    N = N % MOD
    return N

if __name__ == "__main__":

    N, M, K = 1, 2, 3
    print(sumX(N, M, K))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to calculate the
// terms of summing of sum series

using System;
class GFG {

    static int MOD = 1000000007;

    // Function to calculate
    // twice of sum of first N natural numbers
    static long sum(long N)
    {
        long val = N * (N + 1);

        // taking modulo 10 ^ 9 + 7
        val = val % MOD;

        return val;
    }

    // Function to calculate the
    // terms of summing of sum series
    static int sumX(int N, int M, int K)
    {
        for (int i = 0; i < M; i++) {
            N = (int)sum(K + N);
        }
        N = N % MOD;
        return N;
    }

    // Driver code
    public static void Main()
    {
        int N = 1, M = 2, K = 3;
        Console.WriteLine(sumX(N, M, K));
    }
}

// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate the
// terms of summing of sum series

// Function to calculate twice of
// sum of first N natural numbers
function sum($N)
{
    $MOD = 1000000007;
    $val = $N * ($N + 1);
    $val = $val % $MOD;

    return $val;
}

// Function to calculate the terms
// of summing of sum series
function sumX($N, $M, $K)
{
    $MOD = 1000000007;
    for ($i = 0; $i < $M; $i++)
    {
        $N = sum($K + $N);
    }

    $N = $N % $MOD;
    return $N;
}

// Driver Code
$N = 1;
$M = 2;
$K = 3;
echo (sumX($N, $M, $K));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to calculate the
// terms of summing of sum series

// Function to calculate twice of
// sum of first N natural numbers
function sum(N)
{
    let MOD = 1000000007;
    let val = N * (N + 1);
    val = val % MOD;

    return val;
}

// Function to calculate the terms
// of summing of sum series
function sumX(N, M, K)
{
    let MOD = 1000000007;
    for (let i = 0; i < M; i++)
    {
        N = sum(K + N);
    }

    N = N % MOD;
    return N;
}

// Driver Code
let N = 1;
let M = 2;
let K = 3;
document.write (sumX(N, M, K));

// This code is contributed
// by Sravan

</script>
```

**Output:** 

```
552
```