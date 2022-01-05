# 求 Z 的质因数，使得 Z 是所有偶数的乘积，直到 N 是两个不同质数的乘积

> 原文:[https://www . geesforgeks . org/find-prime-factors-of-z-so-z-is-product-of-all-偶数-to-n-is-product-of-two-distinct-prime-numbers/](https://www.geeksforgeeks.org/find-prime-factors-of-z-such-that-z-is-product-of-all-even-numbers-till-n-that-are-product-of-two-distinct-prime-numbers/)

给定一个数 **N (N > 6)** ，任务是打印[一个数 **Z** 的素因子分解](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)，其中 **Z** 是所有偶数的乘积≤ **N** ，而可以表示为两个不同的[素数的乘积。](https://www.geeksforgeeks.org/prime-numbers/)

**示例:**

> **输入:** N = 6
> **输出:** 2→1
> 3→1
> **说明:** 6 是唯一一个≤ N 的数，它是偶数，是两个截然不同的素数(2 和 3)的乘积。因此， **Z** =6。
> 现在， **Z** 的素分解=2×3
> 
> **输入:** N = 5
> **输出:** 2→2
> 3→1
> 5→1
> **说明:**唯一可以表示为两个不同素数乘积的偶数≤ **N** 是 6 (2×3)和 10 (2×5)。因此，**Z**= 6 * 10 = 60 = 2x2x2x3x 5

**观察:**以下观察有助于解决问题:

1.  由于所需的数字必须是偶数，并且是两个不同的[素数](https://www.geeksforgeeks.org/tag/prime-number/)的乘积，因此它们的形式为 **2×P** ，其中 **P 是一个** [**素数**](https://www.geeksforgeeks.org/python-program-to-check-whether-a-number-is-prime-or-not/) **≤ N / 2。**
2.  因此， **Z** 的素数因式分解将是 2<sup>X</sup>3<sup>1</sup>5<sup>1</sup>…P<sup>1</sup>的形式，其中 **P** 是最后一个素数 **≤ N/2** ， **X** 是**素数**在**【3，N/2】范围内的个数。**

**方法:**按照步骤解决问题:

1.  将所有**质数≤ N / 2** 存储，使用厄拉多塞的[筛在一个向量中，说**质数**。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
2.  将**【3，N/2】**范围内的素数存储在一个变量中，比如 **x** 。
3.  打印素数因式分解，其中 2 的系数为 **x** ，范围内所有其他素数的系数为**【3，N/2】**为 1。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the prime factorization of the product
// of all numbers <=N that are even and can be expressed as a
// product of two distinct prime numbers
void primeFactorization(int N)
{
    // sieve of Eratosthenese
    int sieve[N / 2 + 1] = { 0 };
    for (int i = 2; i <= N / 2; i++) {
        if (sieve[i] == 0) {
            for (int j = i * i; j <= N / 2; j += i) {
                sieve[j] = 1;
            }
        }
    }

    // Store prime numbers in the range [3, N/2]
    vector<int> prime;
    for (int i = 3; i <= N / 2; i++)
        if (sieve[i] == 0)
            prime.push_back(i);

    // print the coefficient of 2 in the prime
    // factorization
    int x = prime.size();
    cout << "2->" << x << endl;

    // print the coefficients of other primes
    for (int i : prime)
        cout << i << "->1" << endl;
}
// Driver code
int main()
{
    // Input
    int N = 18;

    // Function calling
    primeFactorization(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;
import java.util.HashMap;

class GFG{

// Function to print the prime factorization
// of the product of all numbers <=N that are
// even and can be expressed as a product of
// two distinct prime numbers
static void primeFactorization(int N)
{

    // Sieve of Eratosthenese
    int[] sieve = new int[N / 2 + 1];
    for(int i = 0; i <= N / 2; i++)
    {
        sieve[i] = 0;
    }
    for(int i = 2; i <= N / 2; i++)
    {
        if (sieve[i] == 0)
        {
            for(int j = i * i; j <= N / 2; j += i)
            {
                sieve[j] = 1;
            }
        }
    }

    // Store prime numbers in the range [3, N/2]
    ArrayList<Integer> prime = new ArrayList<Integer>();
    for(int i = 3; i <= N / 2; i++)
        if (sieve[i] == 0)
            prime.add(i);

    // Print the coefficient of 2 in the prime
    // factorization
    int x = prime.size();
    System.out.println("2->" + x);

    // Print the coefficients of other primes
    for(int i : prime)
        System.out.println(i + "->1");
}

// Driver Code
public static void main(String args[])
{

    // Input
    int N = 18;

    // Function calling
    primeFactorization(N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 implementation for the above approach

# Function to print the prime factorization
# of the product of all numbers <=N that are
# even and can be expressed as a product of
# two distinct prime numbers
def primeFactorization(N):

    # Sieve of Eratosthenese
    sieve = [0 for i in range(N // 2 + 1)]
    for i in range(2, N // 2 + 1, 1):
        if (sieve[i] == 0):
            for j in range(i * i, N // 2 + 1, i):
                sieve[j] = 1

    # Store prime numbers in the range [3, N/2]
    prime = []
    for i in range(3, N // 2 + 1, 1):
        if (sieve[i] == 0):
            prime.append(i)

    # Print the coefficient of 2 in the
    # prime factorization
    x = len(prime)
    print("2->", x)

    # Print the coefficients of other primes
    for i in prime:
        print(i, "->1")

# Driver code
if __name__ == '__main__':

    # Input
    N = 18

    # Function calling
    primeFactorization(N)

# This code is contributed by ipg2016107
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the prime factorization
// of the product of all numbers <=N that are
// even and can be expressed as a product of
// two distinct prime numbers
static void primeFactorization(int N)
{

    // sieve of Eratosthenese
    int[] sieve = new int[N / 2 + 1];
    for(int i = 0; i <= N / 2; i++)
    {
        sieve[i] = 0;
    }
    for(int i = 2; i <= N / 2; i++)
    {
        if (sieve[i] == 0)
        {
            for (int j = i * i; j <= N / 2; j += i)
            {
                sieve[j] = 1;
            }
        }
    }

    // Store prime numbers in the range [3, N/2]
    List<int> prime = new List<int>();
    for(int i = 3; i <= N / 2; i++)
        if (sieve[i] == 0)
            prime.Add(i);

    // Print the coefficient of 2 in the prime
    // factorization
    int x = prime.Count;
    Console.WriteLine("2->" + x);

    // Print the coefficients of other primes
    foreach(int i in prime)
        Console.WriteLine(i + "->1");
}

// Driver Code
public static void Main(String[] args)
{

    // Input
    int N = 18;

    // Function calling
    primeFactorization(N);
}
}

// This code is contributed by avijitmondal1998
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print the prime factorization
// of the product of all numbers <=N that are
// even and can be expressed as a product of
// two distinct prime numbers
function primeFactorization(N)
{

    // Sieve of Eratosthenese
    let sieve = new Array(parseInt(N / 2) + 1).fill(0);
    for(let i = 2; i <= N / 2; i++)
    {
        if (sieve[i] == 0)
        {
            for(let j = i * i; j <= N / 2; j += i)
            {
                sieve[j] = 1;
            }
        }
    }

    // Store prime numbers in the range [3, N/2]
    let prime = [];
    for(let i = 3; i <= N / 2; i++)
        if (sieve[i] == 0)
            prime.push(i);

    // Print the coefficient of 2 in the prime
    // factorization
    let x = prime.length;
    document.write("2->" + x);
    document.write("<br>")

    // Print the coefficients of other primes
    for(let i of prime)
    {
        document.write(i + "->1");
        document.write("<br>");
    }
}

// Driver code

// Input
let N = 18;

// Function calling
primeFactorization(N);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
2->3
3->1
5->1
7->1
```

***时间复杂度:**O(N * log(log(N))*
***辅助空间:** O(N)*