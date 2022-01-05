# 一个范围内的 K-素数(具有 K 个素数因子的数)

> 原文:[https://www . geesforgeks . org/k-素数-数字-k-素数-因子-范围/](https://www.geeksforgeeks.org/k-primes-numbers-k-prime-factors-range/)

给定三个整数 A，B 和 K，我们需要在[A，B]范围内找到 K-素数的个数。如果一个数正好有 K 个不同的质因数，它就叫做 K-质数。

**例:**

```
Input : A = 4, B = 10, K = 2.
Output : 6 10
Given range is [4, 5, 6, 7, 8, 9, 10].
From the above range 6 and 10 have 2 distinct 
prime factors, 6 = 3*2; 10 = 5*2.

Input : A = 14, B = 18, K = 2.
Output : 14 15 18
Range = [14, 15].
Both 14, 15 and 18 have 2 distinct prime factors,
14 = 7*2, 15 = 3*5 and 18 = 2*3*3
```

一个简单的解决方案是遍历给定的范围。对于这个系列的每一个元素，[找到它的主要因素](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。最后打印所有质因数为 k 的数字。

一个有效的解决方案是使用厄拉多塞的 T2 筛算法

```
prime[n] = {true};
for (int p=2; p*p<=n; p++)
{
   // If prime[p] is not changed, then 
   // it is a prime
   if (prime[p] == true)
   {
      // Update all multiples of p
      for (int i=p*2; i<=n; i += p)
         prime[i] = false;
    }
}

```

如果我们清楚地观察上面的算法，它具有迭代所有小于 n 的素数的倍数的性质，所以算法标记一个不是素数的数的次数等于该数的素数因子的个数。要实现这一点，请维护一个名为 marked 的数组，并在每次被算法标记为 not prime 时增加一个数字的计数。而在下一步中，如果标记了[number]= = k .

## c++

T9

```
// CPP program to count all those numbers in
// given range whose count of prime factors
// is k
#include <bits/stdc++.h>
using namespace std;

void printKPFNums(int A, int B, int K)
{
    // Count prime factors of all numbers
    // till B.
    bool prime[B+1] = { true };
    int p_factors[B+1] = { 0 };
    for (int p = 2; p <= B; p++)
        if (p_factors[p] == 0)
            for (int i = p; i <= B; i += p)
                p_factors[i]++;

    // Print all numbers with k prime factors
    for (int i = A; i <= B; i++)
        if (p_factors[i] == K)
            cout << i << " ";
}

// Driver code
int main()
{
    int A = 14, B = 18, K = 2;
    printKPFNums(A, B, K);
    return 0;
}
```

## Java

```
// Java program to count
// all those numbers in
// given range whose count
// of prime factors
// is k

import java.io.*;
import java.util.*;

class GFG {

    static void printKPFNums(int A, int B, int K)
    {
        // Count prime factors of all numbers
        // till B.
        int p_factors[] = new int[B+1];
        Arrays.fill(p_factors,0);

        for (int p = 2; p <= B; p++)
            if (p_factors[p] == 0)
                for (int i = p; i <= B; i += p)
                    p_factors[i]++;

        // Print all numbers with k prime factors
        for (int i = A; i <= B; i++)
            if (p_factors[i] == K)
                System.out.print( i + " ");
    }

    // Driver code
    public static void main(String args[])
    {
        int A = 14, B = 18, K = 2;
        printKPFNums(A, B, K);
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## python 3

```
# Python 3 program to count
# all those numbers in
# given range whose count
# of prime factors
# is k

def printKPFNums(A, B, K) :

    # Count prime factors
    # of all numbers
    # till B.
    prime = [ True]*(B+1)
    p_factors= [ 0 ]*(B+1)
    for p in range(2,B+1) :
        if (p_factors[p] == 0)  :
            for i in range(p,B+1,p) :
                p_factors[i] = p_factors[i] + 1

    # Print all numbers with
    # k prime factors
    for i in range(A,B+1) :
        if (p_factors[i] == K) :
            print( i ,end=" ")

# Driver code
A = 14
B = 18
K = 2
printKPFNums(A, B, K)

# This code is contributed
# by Nikita Tiwari.
```

## c#

```
// C# program to count all
// those numbers in given
// range whose count of
// prime factors is k
using System;

class GFG {

    static void printKPFNums(int A, int B,
                                    int K)
    {
        // Count prime factors of
        // all numbers till B.
        bool []prime = new bool[B + 1];

        for(int i = 0; i < B + 1; i++)
            prime[i] = true;

        int []p_factors = new int[B + 1];

        for(int i = 0; i < B + 1; i++)
            p_factors[i] = 0;

        for (int p = 2; p <= B; p++)
            if (p_factors[p] == 0)
                for (int i = p; i <= B; i += p)
                    p_factors[i]++;

        // Print all numbers with
        // k prime factors
        for (int i = A; i <= B; i++)
            if (p_factors[i] == K)
                Console.Write( i + " ");
    }

    // Driver code
    public static void Main()
    {
        int A = 14, B = 18, K = 2;
        printKPFNums(A, B, K);
    }
}

// This code is contributed by nitin mittal.
```

## PHP

```
<?php
// PHP program to count all those numbers
// in given range whose count of prime
// factors is k

function printKPFNums($A, $B, $K)
{
    // Count prime factors of all
    // numbers till B.
    $prime = array_fill(true, $B + 1, NULL);
    $p_factors = array_fill(0, $B + 1, NULL);
    for ($p = 2; $p <= $B; $p++)
        if ($p_factors[$p] == 0)
            for ($i = $p; $i <= $B; $i += $p)
                $p_factors[$i]++;

    // Print all numbers with
    // k prime factors
    for ($i = $A; $i <= $B; $i++)
        if ($p_factors[$i] == $K)
            echo $i . " ";
}

// Driver code
$A = 14;
$B = 18;
$K = 2;
printKPFNums($A, $B, $K);

// This code is contributed
// by ChitraNayal
?>
```

**输出:**

```
14 15 18
```