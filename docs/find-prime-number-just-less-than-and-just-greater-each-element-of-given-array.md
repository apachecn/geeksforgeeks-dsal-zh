# 求给定数组中每个元素的小于和大于的素数

> 原文:[https://www . geesforgeks . org/find-质数-给定数组的每个元素小于和大于/](https://www.geeksforgeeks.org/find-prime-number-just-less-than-and-just-greater-each-element-of-given-array/)

给定一个整数[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**的大小 **N** ，任务是找到[质数](https://www.geeksforgeeks.org/tag/prime-number/)刚好小于且刚好大于**A【I】**(对于所有 **0 < =i < N** )。

**示例:**

> **输入:** A={17，28}，N=2
> **输出:**
> 13 19
> 23 29
> **说明:**
> 13 是刚好小于 17 的素数。
> 19 是刚好大于 17 的素数。
> 23 是刚好小于 28 的素数。
> 29 是刚好大于 28 的素数。
> 
> **输入:** A={126，64，2896，156}，N=4
> **输出:**
> 113 127
> 61 67
> 2887 2897
> 151 157

**天真接近:**
**观察:**小于 10 的 <sup>9</sup> 的[最大原始间隙](https://en.wikipedia.org/wiki/Prime_gap#:~:text=As%20of%20September%202017%2C%20the, gap%20has%20merit%20M%20%3D%2013.1829.)为 292。

天真的方法是通过检查一个数除了 1 和它本身之外是否还有其他因子来检查素性。按照以下步骤解决问题:

遍历数组 **A** ，对于每个当前索引 **i** ，执行以下操作:

1.  按照降序从 **A[i]-1** 开始迭代，对于每个当前索引 **j** ，执行以下操作:
    1.  通过检查 **j** 是否有除 1 和自身以外的因子来检查它是否是质数。
    2.  如果 **j** 是质数，打印 j 并终止内环。这给出的质数只比 **A【我】**少一点。
2.  按照升序从 **A[i]+1** 开始迭代，对于每个当前索引 **j** ，执行以下操作:
    1.  通过检查 **j** 是否有除 1 和自身以外的因子来检查它是否是质数。
    2.  如果 **j** 是质数，打印 **j** 并终止内环。这给出的质数刚好小于 **A[i]，**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
// Utility function to check
// for primality of a number X by
// checking whether X haACCs any
// factors other than 1 and itself.
bool isPrime(int X)
{
    for (int i = 2; i * i <= X; i++)
        if (X % i == 0) // Factor found
            return false;
    return true;
}
// Function to print primes
// just less than and just greater
// than of each element in an array
void printPrimes(int A[], int N)
{
    // Traverse the array
    for (int i = 0; i < N; i++) {
        // Traverse for finding prime
        // just less than A[i]
        for (int j = A[i] - 1;; j--) {
            // Prime just less than A[i] found
            if (isPrime(j)) {
                cout << j << " ";
                break;
            }
        }
        // Traverse for finding prime
        // just greater than A[i]
        for (int j = A[i] + 1;; j++) {
            // Prime just greater than A[i] found
            if (isPrime(j)) {
                cout << j << " ";
                break;
            }
        }
        cout << endl;
    }
}
// Driver code
int main()
{
    // Input
    int A[] = { 17, 28 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    printPrimes(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Utility function to check
// for primality of a number X by
// checking whether X has any
// factors other than 1 and itself.
static boolean isPrime(int X)
{
    for(int i = 2; i * i <= X; i++)

        // Factor found
        if (X % i == 0)
            return false;

    return true;
}

// Function to print primes
// just less than and just greater
// than of each element in an array
static void printPrimes(int A[], int N)
{

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Traverse for finding prime
        // just less than A[i]
        for(int j = A[i] - 1;; j--)
        {

            // Prime just less than A[i] found
            if (isPrime(j))
            {
                System.out.print(j + " ");
                break;
            }
        }

        // Traverse for finding prime
        // just greater than A[i]
        for(int j = A[i] + 1;; j++)
        {

            // Prime just greater than A[i] found
            if (isPrime(j))
            {
                System.out.print( j + " ");
                break;
            }
        }
        System.out.println();
    }
}

// Driver code
public static void main(String[] args)
{

    // Input
    int A[] = { 17, 28 };
    int N = A.length;

    // Function call
    printPrimes(A, N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt

# Utility function to check
# for primality of a number X by
# checking whether X haACCs any
# factors other than 1 and itself.
def isPrime(X):

    for i in range(2, int(sqrt(X)) + 1, 1):
        if (X % i == 0):

            # Factor found
            return False

    return True

# Function to print primes
# just less than and just greater
# than of each element in an array
def printPrimes(A, N):

    # Traverse the array
    for i in range(N):

        # Traverse for finding prime
        # just less than A[i]
        j = A[i] - 1

        while(1):

            # Prime just less than A[i] found
            if (isPrime(j)):
                print(j, end = " ")
                break

            j -= 1

        # Traverse for finding prime
        # just greater than A[i]
        j = A[i] + 1

        while (1):

            # Prime just greater than A[i] found
            if (isPrime(j)):
                print(j, end = " ")
                break

            j += 1

        print("\n", end = "")

# Driver code
if __name__ == '__main__':

    # Input
    A = [ 17, 28 ]
    N = len(A)

    # Function call
    printPrimes(A, N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Utility function to check
// for primality of a number X by
// checking whether X has any
// factors other than 1 and itself.
static bool isPrime(int X)
{
    for(int i = 2; i * i <= X; i++)

        // Factor found
        if (X % i == 0)
            return false;

    return true;
}

// Function to print primes
// just less than and just greater
// than of each element in an array
static void printPrimes(int[] A, int N)
{

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Traverse for finding prime
        // just less than A[i]
        for(int j = A[i] - 1;; j--)
        {

            // Prime just less than A[i] found
            if (isPrime(j))
            {
                Console.Write(j + " ");
                break;
            }
        }

        // Traverse for finding prime
        // just greater than A[i]
        for(int j = A[i] + 1;; j++)
        {

            // Prime just greater than A[i] found
            if (isPrime(j))
            {
                Console.Write(j + " ");
                break;
            }
        }
        Console.WriteLine();
    }
}

// Driver code
public static void Main()
{

    // Input
    int []A = { 17, 28 };
    int N = A.Length;

    // Function call
    printPrimes(A, N);
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Utility function to check
// for primality of a number X by
// checking whether X haACCs any
// factors other than 1 and itself.
function isPrime(X) {
    for (let i = 2; i * i <= X; i++)
        if (X % i == 0) // Factor found
            return false;
    return true;
}

// Function to print primes
// just less than and just greater
// than of each element in an array
function printPrimes(A, N)
{

    // Traverse the array
    for (let i = 0; i < N; i++)
    {

        // Traverse for finding prime
        // just less than A[i]
        for (let j = A[i] - 1; ; j--)
        {

            // Prime just less than A[i] found
            if (isPrime(j)) {
                document.write(j + " ");
                break;
            }
        }

        // Traverse for finding prime
        // just greater than A[i]
        for (let j = A[i] + 1; ; j++)
        {

            // Prime just greater than A[i] found
            if (isPrime(j)) {
                document.write(j + " ");
                break;
            }
        }
        document.write("<br>");
    }
}

// Driver code

// Input
let A = [17, 28];
let N = A.length;

// Function call
printPrimes(A, N);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
13 19 
23 29 
```

***时间复杂度:** O(N*G*√M)，其中 G 为最大原始间隙，M 为 A.*
***辅助空间:** O(1)*

**有效方法 1:** 不用检查单个数字，所有素数都可以用厄拉多塞的[筛重新计算。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;
const int M = 1e6;
// Boolean array to store
// if a number is prime or not
bool isPrime[M];
void SieveOfEratosthenes()
{
    // assigh value false
    // to the boolean array isprime
    memset(isPrime, true, sizeof(isPrime));
    for (int i = 2; i * i <= M; i++) {
        // If isPrime[i] is not changed,
        // then it is a prime
        if (isPrime[i]) {
            // Update all multiples of i greater than or
            // equal to the square of it numbers which are
            // multiple of i and are less than i^2 are
            // already been marked.
            for (int j = i * i; j < M; j += i)
                isPrime[j] = false;
        }
    }
}
// Function to print primes
// just less than and just greater
// than of each element in an array
void printPrimes(int A[], int N)
{
    // Precalculating
    SieveOfEratosthenes();
    // Traverse the array
    for (int i = 0; i < N; i++) {
        // Traverse for finding
        // prime just less than A[i]
        for (int j = A[i] - 1;; j--) {
            // Prime just less than A[i] found
            if (isPrime[j]) {
                cout << j << " ";
                break;
            }
        }
        // Traverse for finding
        // prime just greater than A[i]
        for (int j = A[i] + 1;; j++) {
            // Prime just greater than A[i] found
            if (isPrime[j]) {
                cout << j << " ";
                break;
            }
        }
        cout << endl;
    }
}
// Driver code
int main()
{
    // Input
    int A[] = { 17, 28 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    printPrimes(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

static int M = 1000000;

// Boolean array to store
// if a number is prime or not
static boolean isPrime[] = new boolean[M];

static void SieveOfEratosthenes()
{

    // Assigh value false
    // to the boolean array isprime
    Arrays.fill(isPrime, true);
    for(int i = 2; i * i <= M; i++)
    {

        // If isPrime[i] is not changed,
        // then it is a prime
        if (isPrime[i])
        {

            // Update all multiples of i greater than or
            // equal to the square of it numbers which are
            // multiple of i and are less than i^2 are
            // already been marked.
            for(int j = i * i; j < M; j += i)
                isPrime[j] = false;
        }
    }
}

// Function to print primes
// just less than and just greater
// than of each element in an array
static void printPrimes(int A[], int N)
{

    // Precalculating
    SieveOfEratosthenes();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Traverse for finding
        // prime just less than A[i]
        for(int j = A[i] - 1;; j--)
        {

            // Prime just less than A[i] found
            if (isPrime[j])
            {
                System.out.print( j + " ");
                break;
            }
        }

        // Traverse for finding
        // prime just greater than A[i]
        for(int j = A[i] + 1;; j++)
        {

            // Prime just greater than A[i] found
            if (isPrime[j])
            {
                System.out.print(j + " ");
                break;
            }
        }
        System.out.println();
    }
}

// Driver code
public static void main(String[] args)
{

    // Input
    int A[] = { 17, 28 };
    int N = A.length;

    // Function call
    printPrimes(A, N);
}
}

// This code is contributed by sanjoy_62
```

## C#

```
using System;

class GFG {

    static int M = 1000000;

    // Boolean array to store
    // if a number is prime or not
    static bool[] isPrime = new bool[M];

    static void SieveOfEratosthenes()
    {

        // Assigh value false
        // to the boolean array isprime
        Array.Fill(isPrime, true);
        for (int i = 2; i * i <= M; i++) {

            // If isPrime[i] is not changed,
            // then it is a prime
            if (isPrime[i]) {

                // Update all multiples of i greater than or
                // equal to the square of it numbers which
                // are multiple of i and are less than i^2
                // are already been marked.
                for (int j = i * i; j < M; j += i)
                    isPrime[j] = false;
            }
        }
    }

    // Function to print primes
    // just less than and just greater
    // than of each element in an array
    static void printPrimes(int[] A, int N)
    {

        // Precalculating
        SieveOfEratosthenes();

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Traverse for finding
            // prime just less than A[i]
            for (int j = A[i] - 1;; j--) {

                // Prime just less than A[i] found
                if (isPrime[j]) {
                    Console.Write(j + " ");
                    break;
                }
            }

            // Traverse for finding
            // prime just greater than A[i]
            for (int j = A[i] + 1;; j++) {

                // Prime just greater than A[i] found
                if (isPrime[j]) {
                    Console.Write(j + " ");
                    break;
                }
            }
            Console.WriteLine();
        }
    }

    // Driver code
    public static void Main()
    {

        // Input
        int[] A = { 17, 28 };
        int N = A.Length;

        // Function call
        printPrimes(A, N);
    }
}

// This code is contributed by subham348.
```

## java 描述语言

```
<script>

const M = 1000000;
// Boolean array to store
// if a number is prime or not
let isPrime = new Array(M).fill(true);
function SieveOfEratosthenes()
{
    for (let i = 2; i * i <= M; i++) {
        // If isPrime[i] is not changed,
        // then it is a prime
        if (isPrime[i]) {
            // Update all multiples of i greater than or
            // equal to the square of it numbers which are
            // multiple of i and are less than i^2 are
            // already been marked.
            for (let j = i * i; j < M; j += i)
                isPrime[j] = false;
        }
    }
}
// Function to print primes
// just less than and just greater
// than of each element in an array
function printPrimes(A, N)
{
    // Precalculating
    SieveOfEratosthenes();
    // Traverse the array
    for (let i = 0; i < N; i++) {
        // Traverse for finding
        // prime just less than A[i]
        for (let j = A[i] - 1;; j--) {
            // Prime just less than A[i] found
            if (isPrime[j]) {
                document.write(j + " ");
                break;
            }
        }
        // Traverse for finding
        // prime just greater than A[i]
        for (let j = A[i] + 1;; j++) {
            // Prime just greater than A[i] found
            if (isPrime[j]) {
                document.write(j + " ");
                break;
            }
        }
        document.write("<br>");
    }
}
// Driver code
    // Input
    let A = [ 17, 28 ];
    let N = A.length;

    // Function call
    printPrimes(A, N);

</script>
```

**Output**

```
13 19 
23 29 
```

***时间复杂度:** O(N*G+MLog(Log(M))，其中 G 为最大原始间隙，M 为 a 中最大元素.*
***辅助空间:** O(M)*

**有效方法 2:** 可以使用[米勒-拉宾素性检验](https://www.geeksforgeeks.org/primality-test-set-3-miller-rabin/)。

## C++

```
#include <bits/stdc++.h>
using namespace std;
// Utility function to do modular exponentiation.
// It returns (x^y) % p
int power(int x, unsigned int y, int p)
{
    int res = 1; // Initialize result
    x = x % p; // Update x if it is more than or
    // equal to p
    while (y > 0) {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// This function is called for all k trials.
// It returns false if n is composite
// and returns true if n is probably prime.
// d is an odd number such that
// d*2<sup>r</sup> = n-1 for some r >= 1
bool miillerTest(int d, int n)
{
    // Pick a random number in [2..n-2]
    // Corner cases make sure that n > 4
    int a = 2 + rand() % (n - 4);

    // Compute a^d % n
    int x = power(a, d, n);

    if (x == 1 || x == n - 1)
        return true;

    // Keep squaring x while one
    // of the following doesn't happen
    // (i)   d does not reach n-1
    // (ii)  (x^2) % n is not 1
    // (iii) (x^2) % n is not n-1
    while (d != n - 1) {
        x = (x * x) % n;
        d *= 2;

        if (x == 1)
            return false;
        if (x == n - 1)
            return true;
    }

    // Return composite
    return false;
}

// It returns false if n is
// composite and returns true if n
// is probably prime.
// k determines accuracy level. Higher
// value of k indicates more accuracy.
bool isPrime(int n)
{
    // number of iterations
    int k = 4;
    // Corner cases
    if (n <= 1 || n == 4)
        return false;
    if (n <= 3)
        return true;

    // Find r such that
    // n = 2^d * r + 1 for some r >= 1
    int d = n - 1;
    while (d % 2 == 0)
        d /= 2;

    // Iterate given number of 'k' times
    for (int i = 0; i < k; i++)
        if (!miillerTest(d, n))
            return false;

    return true;
}

// Function to print primes
// just less than and just greater
// than of each element in an array
void printPrimes(int A[], int N)
{
    // Precalculating
    // Traverse the array
    for (int i = 0; i < N; i++) {
        // Traverse for finding
        // prime just less than A[i]
        for (int j = A[i] - 1;; j--) {
            // Prime just less than A[i] found
            if (isPrime(j)) {
                cout << j << " ";
                break;
            }
        }
        // Traverse for finding
        // prime just greater than A[i]
        for (int j = A[i] + 1;; j++) {
            // Prime just greater than A[i] found
            if (isPrime(j)) {
                cout << j << " ";
                break;
            }
        }
        cout << endl;
    }
}
// Driver code
int main()
{
    // Input
    int A[] = { 17, 28 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    printPrimes(A, N);

    return 0;
}
```

**Output**

```
13 19 
23 29 
```

***时间复杂度:** O(N*G*KLog <sup>3</sup> M，其中 G 是最大的原始间隙，M 是 A.* *中最大的元素这里，K=4*
***辅助空间:** O(1)*