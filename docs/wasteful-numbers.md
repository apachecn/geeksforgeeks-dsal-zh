# 浪费的数字

> 原文:[https://www.geeksforgeeks.org/wasteful-numbers/](https://www.geeksforgeeks.org/wasteful-numbers/)

如果一个数 **N** 的素数因子分解中的位数(包括幂)大于 **N** 中的位数，则称该数为**浪费数**。所有质数都是浪费的。
例如，52 是一个浪费的数字，因为它的素分解是 **2*2*13** ，它的素分解总共有四个数字(1，2，2，3)，比 52 中的数字总数还多。
前几个浪费的数字是:

> 4, 6, 8, 9, 12, 18, 20, 22, 24,…

### 打印小于或等于给定数字 N 的浪费数字的程序

给定一个数字 **N** ，任务是打印小于或等于 **N** 的**浪费数字**。
**示例:**

> **输入:** N = 10
> **输出:** 4、6、8、9
> **输入:** N = 12
> **输出:** 4、6、8、9、12

**进场:**

1.  使用圣达兰的[筛数所有质数直到**10<sup>6</sup>T3。**](https://www.geeksforgeeks.org/sieve-sundaram-print-primes-smaller-n/)
2.  求 **N** 中的位数。
3.  找出 N 的所有质因数，并对每个质因数 **p** 执行以下操作:
    *   求 **p** 中的位数。
    *   数一下 **p** 除以 **N** 的最高幂。
    *   求上面两个的和。
4.  如果质因数中的数字比原始数字中的数字多，则返回 true。否则返回 false。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
const int MAX = 10000;

// Array to store all prime less
// than and equal to MAX.
vector<int> primes;

// Function for Sieve of Sundaram
void sieveSundaram()
{
    // Boolean Array
    bool marked[MAX / 2 + 1] = { 0 };

    // Mark all numbers which do not
    // generate prime number by 2*i+1
    for (int i = 1;
         i <= (sqrt(MAX) - 1) / 2; i++) {

        for (int j = (i * (i + 1)) << 1;
             j <= MAX / 2;
             j = j + 2 * i + 1) {
            marked[j] = true;
        }
    }

    // Since 2 is a prime number
    primes.push_back(2);

    // Print remaining primes are of the
    // form 2*i + 1 such that marked[i]
    // is false.
    for (int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.push_back(2 * i + 1);
}

// Function that returns true if n
// is a Wasteful number
bool isWasteful(int n)
{
    if (n == 1)
        return false;

    // Count digits in original number
    int original_no = n;
    int sumDigits = 0;

    while (original_no > 0) {
        sumDigits++;
        original_no = original_no / 10;
    }

    int pDigit = 0, count_exp = 0, p;

    // Count all digits in prime factors of N
    // pDigit is going to hold this value.
    for (int i = 0; primes[i] <= n / 2; i++) {

        // Count powers of p in n
        while (n % primes[i] == 0) {

            // If primes[i] is a prime factor,
            p = primes[i];
            n = n / p;

            // Count the power of prime factors
            count_exp++;
        }

        // Add its digits to pDigit
        while (p > 0) {
            pDigit++;
            p = p / 10;
        }

        // Add digits of power of
        // prime factors to pDigit.
        while (count_exp > 1) {
            pDigit++;
            count_exp = count_exp / 10;
        }
    }

    // If n!=1 then one prime factor
    // still to be summed up
    if (n != 1) {

        while (n > 0) {
            pDigit++;
            n = n / 10;
        }
    }

    // If digits in prime factors is more than
    // digits in original number  then
    // return true. Else return false.
    return (pDigit > sumDigits);
}

// Function to print Wasteful Number before N
void Solve(int N)
{
    // Iterate till N and check if i
    // is wastefull or not
    for (int i = 1; i < N; i++) {
        if (isWasteful(i)) {
            cout << i << " ";
        }
    }
}

// Driver code
int main()
{
    // Precompute prime numbers upto 10^6
    sieveSundaram();
    int N = 10;

    // Function Call
    Solve(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{
static int MAX = 10000;

// Array to store all prime less
// than and equal to MAX.
static Vector<Integer> primes = new Vector<Integer>();

// Function for Sieve of Sundaram
static void sieveSundaram()
{
    // Boolean Array
    boolean marked[] = new boolean[MAX / 2 + 1];

    // Mark all numbers which do not
    // generate prime number by 2*i+1
    for (int i = 1;
             i <= (Math.sqrt(MAX) - 1) / 2; i++)
    {

        for (int j = (i * (i + 1)) << 1;
                 j <= MAX / 2;
                 j = j + 2 * i + 1)
        {
            marked[j] = true;
        }
    }

    // Since 2 is a prime number
    primes.add(2);

    // Print remaining primes are of the
    // form 2*i + 1 such that marked[i]
    // is false.
    for (int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.add(2 * i + 1);
}

// Function that returns true if n
// is a Wasteful number
static boolean isWasteful(int n)
{
    if (n == 1)
        return false;

    // Count digits in original number
    int original_no = n;
    int sumDigits = 0;

    while (original_no > 0)
    {
        sumDigits++;
        original_no = original_no / 10;
    }

    int pDigit = 0, count_exp = 0, p = 0;

    // Count all digits in prime factors of N
    // pDigit is going to hold this value.
    for (int i = 0; primes.get(i) <= n / 2; i++)
    {

        // Count powers of p in n
        while (n % primes.get(i) == 0)
        {

            // If primes[i] is a prime factor,
            p = primes.get(i);
            n = n / p;

            // Count the power of prime factors
            count_exp++;
        }

        // Add its digits to pDigit
        while (p > 0)
        {
            pDigit++;
            p = p / 10;
        }

        // Add digits of power of
        // prime factors to pDigit.
        while (count_exp > 1)
        {
            pDigit++;
            count_exp = count_exp / 10;
        }
    }

    // If n!=1 then one prime factor
    // still to be summed up
    if (n != 1)
    {
        while (n > 0)
        {
            pDigit++;
            n = n / 10;
        }
    }

    // If digits in prime factors is more than
    // digits in original number then
    // return true. Else return false.
    return (pDigit > sumDigits);
}

// Function to print Wasteful Number before N
static void Solve(int N)
{
    // Iterate till N and check if i
    // is wastefull or not
    for (int i = 1; i < N; i++)
    {
        if (isWasteful(i))
        {
            System.out.print(i + " ");
        }
    }
}

// Driver code
public static void main(String[] args)
{
    // Precompute prime numbers upto 10^6
    sieveSundaram();
    int N = 10;

    // Function Call
    Solve(N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
import math
MAX = 10000

# Array to store all prime
# less than and equal to MAX.
primes = []

# Function for Sieve of
# Sundaram
def sieveSundaram():

    # Boolean Array
    marked = [False] * ((MAX // 2) + 1)

    # Mark all numbers which do not
    # generate prime number by 2*i+1
    for i in range(1, ((int(math.sqrt(MAX)) -
                        1) // 2) + 1):
        j = (i * (i + 1)) << 1
        while j <= (MAX // 2):
            marked[j] = True
            j = j + 2 * i + 1

    # Since 2 is a prime number
    primes.append(2)

    # Print remaining primes are of the
    # form 2*i + 1 such that marked[i]
    # is false.
    for i in range(1, (MAX // 2) + 1):
        if marked[i] == False:
            primes.append(2 * i + 1)

# Function that returns true if n
# is a Wasteful number
def isWasteful(n):

    if (n == 1):
        return False

    # Count digits in original
    # number
    original_no = n
    sumDigits = 0

    while (original_no > 0):
        sumDigits += 1
        original_no = original_no // 10

    pDigit, count_exp, p = 0, 0, 0

    # Count all digits in prime
    # factors of N pDigit is going
    # to hold this value.
    i = 0

    while(primes[i] <= (n//2)):

        # Count powers of p in n
        while (n % primes[i] == 0):

            # If primes[i] is a prime
            # factor,
            p = primes[i]
            n = n // p

            # Count the power of prime
            # factors
            count_exp += 1

        # Add its digits to pDigit
        while (p > 0):
            pDigit += 1
            p = p // 10

        # Add digits of power of
        # prime factors to pDigit.
        while (count_exp > 1):
            pDigit += 1
            count_exp = count_exp // 10

        i += 1

    # If n!=1 then one prime factor
    # still to be summed up
    if (n != 1):
        while (n > 0):
            pDigit += 1
            n = n // 10

    # If digits in prime factors
    # is more than digits in
    # original number then return
    # true. Else return false.
    return bool(pDigit > sumDigits)

# Function to print Wasteful Number
# before N
def Solve(N):

    # Iterate till N and check
    # if i is wastefull or not
    for i in range(1, N):
        if (isWasteful(i)):
            print(i, end = " ")

# Driver code
# Precompute prime numbers
# upto 10^6
sieveSundaram()
N = 10

# Function Call
Solve(N)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{
static int MAX = 10000;

// Array to store all prime less
// than and equal to MAX.
static List<int> primes = new List<int>();

// Function for Sieve of Sundaram
static void sieveSundaram()
{
    // Boolean Array
    bool []marked = new bool[MAX / 2 + 1];

    // Mark all numbers which do not
    // generate prime number by 2*i+1
    for (int i = 1;
             i <= (Math.Sqrt(MAX) - 1) / 2; i++)
    {
        for (int j = (i * (i + 1)) << 1;
                 j <= MAX / 2;
                 j = j + 2 * i + 1)
        {
            marked[j] = true;
        }
    }

    // Since 2 is a prime number
    primes.Add(2);

    // Print remaining primes are of the
    // form 2*i + 1 such that marked[i]
    // is false.
    for (int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.Add(2 * i + 1);
}

// Function that returns true if n
// is a Wasteful number
static bool isWasteful(int n)
{
    if (n == 1)
        return false;

    // Count digits in original number
    int original_no = n;
    int sumDigits = 0;

    while (original_no > 0)
    {
        sumDigits++;
        original_no = original_no / 10;
    }

    int pDigit = 0, count_exp = 0, p = 0;

    // Count all digits in prime factors of N
    // pDigit is going to hold this value.
    for (int i = 0; primes[i] <= n / 2; i++)
    {

        // Count powers of p in n
        while (n % primes[i] == 0)
        {

            // If primes[i] is a prime factor,
            p = primes[i];
            n = n / p;

            // Count the power of prime factors
            count_exp++;
        }

        // Add its digits to pDigit
        while (p > 0)
        {
            pDigit++;
            p = p / 10;
        }

        // Add digits of power of
        // prime factors to pDigit.
        while (count_exp > 1)
        {
            pDigit++;
            count_exp = count_exp / 10;
        }
    }

    // If n!=1 then one prime factor
    // still to be summed up
    if (n != 1)
    {
        while (n > 0)
        {
            pDigit++;
            n = n / 10;
        }
    }

    // If digits in prime factors is more than
    // digits in original number then
    // return true. Else return false.
    return (pDigit > sumDigits);
}

// Function to print Wasteful Number before N
static void Solve(int N)
{
    // Iterate till N and check if i
    // is wastefull or not
    for (int i = 1; i < N; i++)
    {
        if (isWasteful(i))
        {
            Console.Write(i + " ");
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    // Precompute prime numbers upto 10^6
    sieveSundaram();
    int N = 10;

    // Function Call
    Solve(N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation for the above approach

let MAX = 10000;

// Array to store all prime less
// than and equal to MAX.
let primes = [];

// Function for Sieve of Sundaram
function sieveSundaram()
{
    // Boolean Array
    let marked = Array.from({length:  MAX / 2 + 1},
    (_, i) => 0);

    // Mark all numbers which do not
    // generate prime number by 2*i+1
    for (let i = 1;
             i <= Math.floor((Math.sqrt(MAX) - 1) / 2);
             i++)
    {

        for (let j = (i * (i + 1)) << 1;
                 j <= Math.floor(MAX / 2);
                 j = j + 2 * i + 1)
        {
            marked[j] = true;
        }
    }

    // Since 2 is a prime number
    primes.push(2);

    // Print remaining primes are of the
    // form 2*i + 1 such that marked[i]
    // is false.
    for (let i = 1; i <= Math.floor(MAX / 2); i++)
        if (marked[i] == false)
            primes.push(2 * i + 1);
}

// Function that returns true if n
// is a Wasteful number
function isWasteful(n)
{
    if (n == 1)
        return false;

    // Count digits in original number
    let original_no = n;
    let sumDigits = 0;

    while (original_no > 0)
    {
        sumDigits++;
        original_no = Math.floor(original_no / 10);
    }

    let pDigit = 0, count_exp = 0, p = 0;

    // Count all digits in prime factors of N
    // pDigit is going to hold this value.
    for (let i = 0; primes[i] <= Math.floor(n / 2);
    i++)
    {

        // Count powers of p in n
        while (n % primes[i] == 0)
        {

            // If primes[i] is a prime factor,
            p = primes[i];
            n = Math.floor(n / p);

            // Count the power of prime factors
            count_exp++;
        }

        // Add its digits to pDigit
        while (p > 0)
        {
            pDigit++;
            p = Math.floor(p / 10);
        }

        // Add digits of power of
        // prime factors to pDigit.
        while (count_exp > 1)
        {
            pDigit++;
            count_exp = Math.floor(count_exp / 10);
        }
    }

    // If n!=1 then one prime factor
    // still to be summed up
    if (n != 1)
    {
        while (n > 0)
        {
            pDigit++;
            n = Math.floor(n / 10);
        }
    }

    // If digits in prime factors is more than
    // digits in original number then
    // return true. Else return false.
    return (pDigit > sumDigits);
}

// Function to print Wasteful Number before N
function Solve(N)
{
    // Iterate till N and check if i
    // is wastefull or not
    for (let i = 1; i < N; i++)
    {
        if (isWasteful(i))
        {
            document.write(i + " ");
        }
    }
}

    // Driver Code

    // Precompute prime numbers upto 10^6
    sieveSundaram();
    let N = 10;

    // Function Call
    Solve(N);

</script>
```

**Output:** 

```
4 6 8 9
```

**时间复杂度:***O(N * log(log N))*
**参考:**[https://oeis.org/A046760](https://oeis.org/A046760)