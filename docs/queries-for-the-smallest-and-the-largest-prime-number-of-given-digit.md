# 查询给定数字的最小和最大素数

> 原文:[https://www . geesforgeks . org/查询给定数字的最小和最大素数/](https://www.geeksforgeeks.org/queries-for-the-smallest-and-the-largest-prime-number-of-given-digit/)

给定 **Q** 查询，其中每个查询由一个整数 **D** 组成，任务是找到具有 **D** 位数的最小和最大素数。如果不存在这样的质数，则打印 **-1** 。
**举例:**

> **输入:** Q[] = {2，5}
> **输出:**
> 11 97
> 10007 99991
> **输入:** Q[] = {4，3，1}
> **输出:**
> 1009 9973
> 101 997
> 1 7

**进场:**

1.  **D** 位数从**10<sup>(D–1)</sup>**开始，到**10<sup>D</sup>–1**结束。
2.  现在，任务是从这个范围中找到最小和最大的素数。
3.  要回答多个质数查询，可以使用厄拉多塞的[筛来回答一个数是否是质数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 100000

bool prime[MAX + 1];

void SieveOfEratosthenes()
{

    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the smallest prime
// number with d digits
int smallestPrime(int d)
{
    int l = pow(10, d - 1);
    int r = pow(10, d) - 1;
    for (int i = l; i <= r; i++) {

        // check if prime
        if (prime[i]) {
            return i;
        }
    }
    return -1;
}

// Function to return the largest prime
// number with d digits
int largestPrime(int d)
{
    int l = pow(10, d - 1);
    int r = pow(10, d) - 1;
    for (int i = r; i >= l; i--) {

        // check if prime
        if (prime[i]) {
            return i;
        }
    }
    return -1;
}

// Driver code
int main()
{
    SieveOfEratosthenes();

    int queries[] = { 2, 5 };
    int q = sizeof(queries) / sizeof(queries[0]);

    // Perform queries
    for (int i = 0; i < q; i++) {
        cout << smallestPrime(queries[i]) << " "
             << largestPrime(queries[i]) << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int MAX = 100000;

static boolean []prime = new boolean[MAX + 1];

static void SieveOfEratosthenes()
{

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true.
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    for (int i = 0; i < MAX + 1; i++)
    {
        prime[i] = true;
    }
    for (int p = 2; p * p <= MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the smallest prime
// number with d digits
static int smallestPrime(int d)
{
    int l = (int) Math.pow(10, d - 1);
    int r = (int) Math.pow(10, d) - 1;
    for (int i = l; i <= r; i++)
    {

        // check if prime
        if (prime[i])
        {
            return i;
        }
    }
    return -1;
}

// Function to return the largest prime
// number with d digits
static int largestPrime(int d)
{
    int l = (int) Math.pow(10, d - 1);
    int r = (int) Math.pow(10, d) - 1;
    for (int i = r; i >= l; i--)
    {

        // check if prime
        if (prime[i])
        {
            return i;
        }
    }
    return -1;
}

// Driver code
public static void main(String[] args)
{
    SieveOfEratosthenes();

    int queries[] = { 2, 5 };
    int q = queries.length;

    // Perform queries
    for (int i = 0; i < q; i++)
    {
        System.out.println(smallestPrime(queries[i]) + " " +
                           largestPrime(queries[i]));
    }
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

MAX = 100000

# Create a boolean array "prime[0..n]" and
# initialize all entries it as true.
# A value in prime[i] will finally be false
# if i is Not a prime, else true.
prime = [True] * (MAX + 1)

def SieveOfEratosthenes() :

    for p in range(2, int(sqrt(MAX)) + 1) :

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True) :

            # Update all multiples of p greater than or
            # equal to the square of it
            # numbers which are multiple of p and are
            # less than p^2 are already been marked.
            for i in range(p * p, MAX + 1, p) :
                prime[i] = False;

# Function to return the smallest prime
# number with d digits
def smallestPrime(d) :

    l = 10 ** (d - 1);
    r = (10 ** d) - 1;
    for i in range(l, r + 1) :

        # check if prime
        if (prime[i]) :
            return i;

    return -1;

# Function to return the largest prime
# number with d digits
def largestPrime(d) :

    l = 10 ** (d - 1);
    r = (10 ** d) - 1;
    for i in range(r, l , -1) :

        # check if prime
        if (prime[i]) :
            return i;

    return -1;

# Driver code
if __name__ == "__main__" :

    SieveOfEratosthenes();

    queries = [ 2, 5 ];
    q = len(queries);

    # Perform queries
    for i in range(q) :
        print(smallestPrime(queries[i]), " ",
              largestPrime(queries[i]));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MAX = 100000;

static bool []prime = new bool[MAX + 1];

static void SieveOfEratosthenes()
{

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true.
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    for (int i = 0; i < MAX + 1; i++)
    {
        prime[i] = true;
    }
    for (int p = 2; p * p <= MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p greater than
            // or equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the smallest prime
// number with d digits
static int smallestPrime(int d)
{
    int l = (int) Math.Pow(10, d - 1);
    int r = (int) Math.Pow(10, d) - 1;
    for (int i = l; i <= r; i++)
    {

        // check if prime
        if (prime[i])
        {
            return i;
        }
    }
    return -1;
}

// Function to return the largest prime
// number with d digits
static int largestPrime(int d)
{
    int l = (int) Math.Pow(10, d - 1);
    int r = (int) Math.Pow(10, d) - 1;
    for (int i = r; i >= l; i--)
    {

        // check if prime
        if (prime[i])
        {
            return i;
        }
    }
    return -1;
}

// Driver code
public static void Main(String[] args)
{
    SieveOfEratosthenes();

    int []queries = { 2, 5 };
    int q = queries.Length;

    // Perform queries
    for (int i = 0; i < q; i++)
    {
        Console.WriteLine(smallestPrime(queries[i]) + " " +
                           largestPrime(queries[i]));
    }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

const MAX = 100000;

// Create a boolean array
// "prime[0..n]" and initialize
// all entries it as true.
// A value in prime[i] will
// finally be false if i is Not a prime,
// else true.
let prime = new Array(MAX + 1).fill(true);

function SieveOfEratosthenes()
{

    for (let p = 2; p * p <= MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            // greater than or
            // equal to the square of it
            // numbers which are multiple
            // of p and are
            // less than p^2 are already
            // been marked.
            for (let i = p * p; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the smallest prime
// number with d digits
function smallestPrime(d)
{
    let l = Math.pow(10, d - 1);
    let r = Math.pow(10, d) - 1;
    for (let i = l; i <= r; i++) {

        // check if prime
        if (prime[i]) {
            return i;
        }
    }
    return -1;
}

// Function to return the largest prime
// number with d digits
function largestPrime(d)
{
    let l = Math.pow(10, d - 1);
    let r = Math.pow(10, d) - 1;
    for (let i = r; i >= l; i--) {

        // check if prime
        if (prime[i]) {
            return i;
        }
    }
    return -1;
}

// Driver code
    SieveOfEratosthenes();

    let queries = [ 2, 5 ];
    let q = queries.length;

    // Perform queries
    for (let i = 0; i < q; i++) {
        document.write(smallestPrime(queries[i]) + " "
             + largestPrime(queries[i]) + "<br>");
    }

</script>
```

**Output:** 

```
11 97
10007 99991
```