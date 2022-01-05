# 求有序对的个数，a * p + b * q = N，其中 p 和 q 为素数

> 原文:[https://www . geesforgeks . org/find-有序对的数量-这样-a-p-b-q-n-其中-p-和-q-是素数/](https://www.geeksforgeeks.org/find-the-number-of-ordered-pairs-such-that-a-p-b-q-n-where-p-and-q-are-primes/)

给定一个数组 **arr[]** ，以及表示查询数的整数 **Q** 和两个数字 **a，b** ，任务是找到有序对(p，Q)的数量，使得 **a * p + b * q = arr[i]** ，其中 p 和 Q 是素数。
**举例:**

> **输入:** Q = 3，arr[] = { 2，7，11 }，a = 1，b = 2
> **输出:** 0 1 2
> **解释:**
> 2 - >不存在 p + 2*q = 2 的有序对(p，Q)。
> 7 - >只有一个有序对(p，q) = (3，2)，这样 p + 2*q = 7。
> 11 - >有两个有序对(p，q) = (7，2)，(5，3)，这样 p + 2*q = 11。
> **输入:** Q = 2，arr[] = { 15，25 }，a = 1，b = 2
> **输出:** 2 3

**方法:**想法是使用厄拉多塞的[筛将每个素数存储在一个数组中。存储素数后，计算有序对(p，q)的数量，使得素数数组中(p，q)的每个组合的 a*p + b*q = N。
以下是上述方法的实施:](http://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ program to find the number of ordered
// pairs such that a * p + b * q = N
// where p and q are primes

#include <bits/stdc++.h>
#define size 10001
using namespace std;
int prime[size];
int freq[size];

// Sieve of erastothenes
// to store the prime numbers
// and their frequency in form a*p+b*q
void sieve(int a, int b)
{
    prime[1] = 1;

    // Performing Sieve of Eratosthenes
    // to find the prime numbers unto 10001
    for (int i = 2; i * i < size; i++) {
        if (prime[i] == 0) {
            for (int j = i * 2; j < size; j += i)
                prime[j] = 1;
        }
    }

    // Loop to find the number of
    // ordered pairs for every combination
    // of the prime numbers
    for (int p = 1; p < size; p++) {
        for (int q = 1; q < size; q++) {
            if (prime[p] == 0 && prime[q] == 0
                && a * p + b * q < size) {
                freq[a * p + b * q]++;
            }
        }
    }
}

// Driver code
int main()
{
    int queries = 2, a = 1, b = 2;
    sieve(a, b);
    int arr[queries] = { 15, 25 };

    // Printing the number of ordered pairs
    // for every query
    for (int i = 0; i < queries; i++) {
        cout << freq[arr[i]] << " ";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of ordered
// pairs such that a * p + b * q = N
// where p and q are primes
public class GFG {

    final static int size = 10001;
    static int prime[] = new int[size];
    static int freq[] = new int [size];

    // Sieve of erastothenes
    // to store the prime numbers
    // and their frequency in form a*p+b*q
    static void sieve(int a, int b)
    {
        prime[1] = 1;

        // Performing Sieve of Eratosthenes
        // to find the prime numbers unto 10001
        for (int i = 2; i * i < size; i++) {
            if (prime[i] == 0) {
                for (int j = i * 2; j < size; j += i)
                    prime[j] = 1;
            }
        }

        // Loop to find the number of
        // ordered pairs for every combination
        // of the prime numbers
        for (int p = 1; p < size; p++) {
            for (int q = 1; q < size; q++) {
                if (prime[p] == 0 && prime[q] == 0
                    && a * p + b * q < size) {
                    freq[a * p + b * q]++;
                }
            }
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int queries = 2, a = 1, b = 2;
        sieve(a, b);
        int arr[] = { 15, 25 };

        // Printing the number of ordered pairs
        // for every query
        for (int i = 0; i < queries; i++) {
            System.out.print(freq[arr[i]] + " ");
        }

    }
}
// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find the number of ordered
# pairs such that a * p + b * q = N
# where p and q are primes
from math import sqrt
size = 1000
prime = [0 for i in range(size)]
freq = [0 for i in range(size)]

# Sieve of erastothenes
# to store the prime numbers
# and their frequency in form a*p+b*q
def sieve(a, b):
    prime[1] = 1

    # Performing Sieve of Eratosthenes
    # to find the prime numbers unto 10001
    for i in range(2, int(sqrt(size)) + 1, 1):
        if (prime[i] == 0):
            for j in range(i*2, size, i):
                prime[j] = 1

    # Loop to find the number of
    # ordered pairs for every combination
    # of the prime numbers
    for p in range(1, size, 1):
        for q in range(1, size, 1):
            if (prime[p] == 0 and prime[q] == 0 and a * p + b * q < size):
                freq[a * p + b * q] += 1

# Driver code
if __name__ == '__main__':
    queries = 2
    a = 1
    b = 2
    sieve(a, b)
    arr = [15, 25]

    # Printing the number of ordered pairs
    # for every query
    for i in range(queries):
        print(freq[arr[i]],end = " ")

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to find the number of ordered
// pairs such that a * p + b * q = N
// where p and q are primes
using System;

class GFG {

    static int size = 10001;
    static int []prime = new int[size];
    static int []freq = new int [size];

    // Sieve of erastothenes
    // to store the prime numbers
    // and their frequency in form a*p+b*q
    static void sieve(int a, int b)
    {
        prime[1] = 1;

        // Performing Sieve of Eratosthenes
        // to find the prime numbers unto 10001
        for (int i = 2; i * i < size; i++) {
            if (prime[i] == 0) {
                for (int j = i * 2; j < size; j += i)
                    prime[j] = 1;
            }
        }

        // Loop to find the number of
        // ordered pairs for every combination
        // of the prime numbers
        for (int p = 1; p < size; p++) {
            for (int q = 1; q < size; q++) {
                if (prime[p] == 0 && prime[q] == 0
                    && a * p + b * q < size) {
                    freq[a * p + b * q]++;
                }
            }
        }
    }

    // Driver code
    public static void Main (string[] args)
    {
        int queries = 2, a = 1, b = 2;
        sieve(a, b);
        int []arr = { 15, 25 };

        // Printing the number of ordered pairs
        // for every query
        for (int i = 0; i < queries; i++) {
            Console.Write(freq[arr[i]] + " ");
        }

    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript program to find the number of ordered
// pairs such that a * p + b * q = N
// where p and q are primes

size=10001
prime = Array(size).fill(0);
freq = Array(size).fill(0);

// Sieve of erastothenes
// to store the prime numbers
// and their frequency in form a*p+b*q
function sieve(a, b)
{
    prime[1] = 1;

    // Performing Sieve of Eratosthenes
    // to find the prime numbers unto 10001
    for (var i = 2; i * i < size; i++) {
        if (prime[i] == 0) {
            for (var j = i * 2; j < size; j += i)
                prime[j] = 1;
        }
    }

    // Loop to find the number of
    // ordered pairs for every combination
    // of the prime numbers
    for (var p = 1; p < size; p++) {
        for (var q = 1; q < size; q++) {
            if (prime[p] == 0 && prime[q] == 0
                && a * p + b * q < size) {
                freq[a * p + b * q]++;
            }
        }
    }
}

// Driver code
var queries = 2, a = 1, b = 2;
sieve(a, b);
var arr = [ 15, 25 ];

// Printing the number of ordered pairs
// for every query
for(var i = 0; i < queries; i++) {
    document.write(freq[arr[i]] + " ");
}

</script>
```

**Output:** 

```
2 3
```

**时间复杂度:** O(N)

**辅助空间:** O(大小)