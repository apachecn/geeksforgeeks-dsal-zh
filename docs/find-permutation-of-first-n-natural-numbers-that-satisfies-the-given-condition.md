# 求满足给定条件的前 N 个自然数的排列

> 原文:[https://www . geeksforgeeks . org/find-满足给定条件的第 n 个自然数的排列/](https://www.geeksforgeeks.org/find-permutation-of-first-n-natural-numbers-that-satisfies-the-given-condition/)

给定两个整数 **N** 和 **K** ，任务是找到第一个 **N** 自然数的排列 **P** ，使得对于所有 **1 ≤ i ≤ N** 恰好有 K 个元素满足条件 **GCD(P[i]，i) > 1** 。
**示例:**

> **输入:** N = 3，K = 1
> **输出:** 2 1 3
> GCD(P[1]，1) = GCD(2，1) = 1
> GCD(P[2]，2) = GCD(1，2) = 1
> GCD(P[3]，3) = GCD(3，3) = 3
> 恰好有一个元素使得 GCD(P[i]，i) > 1

****进场:**保持最后 **K** 元素就位。移动其余的元件，使得**I<sup>th</sup>T7】元件放置在 **(i + 1) <sup>th</sup>** 位置，并且**(N–K)<sup>th</sup>**元件保持在位置 **1** ，因为 **gcd(x，x + 1) = 1** 。
以下是上述办法的实施:**** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find permutation(p) of first N
// natural numbers such that there are exactly K
// elements of permutation such that GCD(p[i], i)>1
void Permutation(int n, int k)
{
    int p[n + 1];

    // First place all the numbers
    // in their respective places
    for (int i = 1; i <= n; i++)
        p[i] = i;

    // Modify for first n-k integers
    for (int i = 1; i < n - k; i++)
        p[i + 1] = i;

    // In first index place n-k
    p[1] = n - k;

    // Print the permutation
    for (int i = 1; i <= n; i++)
        cout << p[i] << " ";
}

// Driver code
int main()
{
    int n = 5, k = 2;
    Permutation(n, k);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach

class GFG
{

    // Function to find permutation(p) of first N
    // natural numbers such that there are exactly K
    // elements of permutation such that GCD(p[i], i)>1
    static void Permutation(int n, int k)
    {
        int[] p = new int[n + 1];

        // First place all the numbers
        // in their respective places
        for (int i = 1; i <= n; i++)
            p[i] = i;

        // Modify for first n-k integers
        for (int i = 1; i < n - k; i++)
            p[i + 1] = i;

        // In first index place n-k
        p[1] = n - k;

        // Print the permutation
        for (int i = 1; i <= n; i++)
            System.out.print(p[i] + " ");
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5, k = 2;
        Permutation(n, k);
    }
}

// This code is contributed by Naman_Garg
```

## **蟒蛇 3**

```
# Python 3 implementation of the approach

# Function to find permutation(p)
# of first N natural numbers such that
# there are exactly K elements of
# permutation such that GCD(p[i], i)>1
def Permutation(n, k):
    p = [0 for i in range(n + 1)]

    # First place all the numbers
    # in their respective places
    for i in range(1, n + 1):
        p[i] = i

    # Modify for first n-k integers
    for i in range(1, n - k):
        p[i + 1] = i

    # In first index place n-k
    p[1] = n - k

    # Print the permutation
    for i in range(1, n + 1):
        print(p[i], end = " ")

# Driver code
if __name__ == '__main__':
    n = 5
    k = 2
    Permutation(n, k)

# This code is contributed by
# Surendra_Gangwar
```

## **C#**

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to find permutation(p) of first N
    // natural numbers such that there are exactly K
    // elements of permutation such that GCD(p[i], i)>1
    static void Permutation(int n, int k)
    {
        int[] p = new int[n + 1];

        // First place all the numbers
        // in their respective places
        for (int i = 1; i <= n; i++)
            p[i] = i;

        // Modify for first n-k integers
        for (int i = 1; i < n - k; i++)
            p[i + 1] = i;

        // In first index place n-k
        p[1] = n - k;

        // Print the permutation
        for (int i = 1; i <= n; i++)
            Console.Write(p[i] + " ");
    }

    // Driver code
    static public void Main ()
    {
        int n = 5, k = 2;
        Permutation(n, k);
    }
}

// This code is contributed by ajit.
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP implementation of the approach

// Function to find permutation(p) of first N
// natural numbers such that there are exactly K
// elements of permutation such that GCD(p[i], i)>1
function Permutation($n, $k)
{
    $p = array();

    // First place all the numbers
    // in their respective places
    for ($i = 1; $i <= $n; $i++)
        $p[$i] = $i;

    // Modify for first n-k integers
    for ($i = 1; $i < $n - $k; $i++)
        $p[$i + 1] = $i;

    // In first index place n-k
    $p[1] = $n - $k;

    // Print the permutation
    for ($i = 1; $i <= $n; $i++)
        echo $p[$i], " ";
}

// Driver code
$n = 5; $k = 2;
Permutation($n, $k);

// This code is contributed by AnkitRai01
?>
```

## **java 描述语言**

```
<script>
//Javascript implementation of the approach

// Function to find permutation(p) of first N
// natural numbers such that there are exactly K
// elements of permutation such that GCD(p[i], i)>1
function Permutation(n, k)
{
    let p  = new Array(n + 1);

    // First place all the numbers
    // in their respective places
    for (let i = 1; i <= n; i++)
        p[i] = i;

    // Modify for first n-k integers
    for (let i = 1; i < n - k; i++)
        p[i + 1] = i;

    // In first index place n-k
    p[1] = n - k;

    // Print the permutation
    for (let i = 1; i <= n; i++)
        document.write(p[i] + " ");
}

// Driver code
    let n = 5, k = 2;
    Permutation(n, k);

// This code is contributed by Mayank Tyagi
</script>
```

****Output:** 

```
3 1 2 4 5
```**