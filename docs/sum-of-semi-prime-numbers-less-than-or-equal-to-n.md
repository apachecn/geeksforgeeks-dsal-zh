# 小于或等于 N 的半素数之和

> 原文:[https://www . geesforgeks . org/半素数之和-小于或等于 n/](https://www.geeksforgeeks.org/sum-of-semi-prime-numbers-less-than-or-equal-to-n/)

给定一个整数 **N** ，任务是求小于或等于 **N** 的半素数之和。半素数是两个素数的倍数。

**示例:**

> **输入:** N = 6
> **输出:** 10
> 4 和 6 为半素数≤ 6
> 4 + 6 = 10
> **输入:** N = 10000000
> **输出:** 9322298311255

**进场:**

1.  首先用筛子计算小于或等于 N 的素数，并按排序顺序将它们存储在向量中。
2.  迭代素数向量。修复其中一个素数，并开始用这个固定素数检查所有素数乘积的值。
3.  由于素数是按排序顺序排列的，一旦我们找到一个素数的乘积超过 N，那么它将超过所有剩余的素数。因此，在这里打破嵌套循环。
4.  将所有有效对的乘积值添加到答案变量中。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Vector to store the primes
vector<ll> pr;

// Create a boolean array "prime[0..n]"
bool prime[10000000 + 1];
void sieve(ll n)
{

    // Initialize all prime values to be true
    for (int i = 2; i <= n; i += 1) {
        prime[i] = 1;
    }

    for (ll p = 2; (ll)p * (ll)p <= n; p++) {

        // If prime[p] is not changed then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked
            for (ll i = (ll)p * (ll)p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Print all prime numbers
    for (ll p = 2; p <= n; p++)
        if (prime[p])
            pr.push_back(p);
}

// Function to return the semi-prime sum
ll SemiPrimeSum(ll N)
{

    // Variable to store the sum of semi-primes
    ll ans = 0;

    // Iterate over the prime values
    for (int i = 0; i < pr.size(); i += 1) {

        for (int j = i; j < pr.size(); j += 1) {

            // Break the loop once the product exceeds N
            if ((ll)pr[i] * (ll)pr[j] > N)
                break;

            // Add valid products which are less than
            // or equal to N
            // each product is a semi-prime number
            ans += (ll)pr[i] * (ll)pr[j];
        }
    }
    return ans;
}

// Driver code
int main()
{

    ll N = 6;

    sieve(N);

    cout << SemiPrimeSum(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Vector to store the primes
static Vector<Long> pr = new Vector<>();

// Create a boolean array "prime[0..n]"
static boolean prime[] = new boolean[10000000 + 1];
static void sieve(long n)
{

    // Initialize along prime values to be true
    for (int i = 2; i <= n; i += 1)
    {
        prime[i] = true;
    }

    for (int p = 2; (int)p * (int)p <= n; p++)
    {

        // If prime[p] is not changed then it is a prime
        if (prime[p] == true)
        {

            // Update along multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked
            for (int i = (int)p * (int)p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Print all prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            pr.add((long)p);
}

// Function to return the semi-prime sum
static long SemiPrimeSum(long N)
{

    // Variable to store the sum of semi-primes
    long ans = 0;

    // Iterate over the prime values
    for (int i = 0; i < pr.size(); i += 1)
    {

        for (int j = i; j < pr.size(); j += 1)
        {

            // Break the loop once the product exceeds N
            if ((long)pr.get(i) * (long)pr.get(j) > N)
                break;

            // Add valid products which are less than
            // or equal to N
            // each product is a semi-prime number
            ans += (long)pr.get(i) * (long)pr.get(j);
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    long N = 6;

    sieve(N);

    System.out.println(SemiPrimeSum(N));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Vector to store the primes
pr=[]

# Create a boolean array "prime[0..n]"
prime = [1 for i in range(10000000 + 1)]
def sieve(n):

    for p in range(2, n):

        if p * p > n:
            break

        # If prime[p] is not changed then it is a prime
        if (prime[p] == True):

            # Update amultiples of p greater than or
            # equal to the square of it
            # numbers which are multiple of p and are
            # less than p^2 are already been marked
            for i in range(2 * p, n + 1, p):
                prime[i] = False

    # Praprime numbers
    for p in range(2, n + 1):
        if (prime[p]):
            pr.append(p)

# Function to return the semi-prime sum
def SemiPrimeSum(N):

    # Variable to store the sum of semi-primes
    ans = 0

    # Iterate over the prime values
    for i in range(len(pr)):

        for j in range(i,len(pr)):

            # Break the loop once the product exceeds N
            if (pr[i] * pr[j] > N):
                break

            # Add valid products which are less than
            # or equal to N
            # each product is a semi-prime number
            ans += pr[i] * pr[j]

    return ans

# Driver code
N = 6

sieve(N)

print(SemiPrimeSum(N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Vector to store the primes
static List<long> pr = new List<long>();

// Create a boolean array "prime[0..n]"
static bool []prime = new bool[10000000 + 1];
static void sieve(long n)
{

    // Initialize along prime values to be true
    for (int i = 2; i <= n; i += 1)
    {
        prime[i] = true;
    }

    for (int p = 2; (int)p * (int)p <= n; p++)
    {

        // If prime[p] is not changed then it is a prime
        if (prime[p] == true)
        {

            // Update along multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked
            for (int i = (int)p * (int)p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Print all prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            pr.Add((long)p);
}

// Function to return the semi-prime sum
static long SemiPrimeSum(long N)
{

    // Variable to store the sum of semi-primes
    long ans = 0;

    // Iterate over the prime values
    for (int i = 0; i < pr.Count; i += 1)
    {

        for (int j = i; j < pr.Count; j += 1)
        {

            // Break the loop once the product exceeds N
            if ((long)pr[i] * (long)pr[j] > N)
                break;

            // Add valid products which are less than
            // or equal to N
            // each product is a semi-prime number
            ans += (long)pr[i] * (long)pr[j];
        }
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    long N = 6;

    sieve(N);

    Console.WriteLine(SemiPrimeSum(N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Vector to store the primes
let pr = [];

// Create a boolean array "prime[0..n]"
let prime = new Array(10000000 + 1);
function sieve(n)
{

    // Initialize all prime values to be true
    for (let i = 2; i <= n; i += 1) {
        prime[i] = 1;
    }

    for (let p = 2; p * p <= n; p++) {

        // If prime[p] is not changed then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked
            for (let i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Print all prime numbers
    for (let p = 2; p <= n; p++)
        if (prime[p])
            pr.push(p);
}

// Function to return the semi-prime sum
function SemiPrimeSum(N)
{

    // Variable to store the sum of semi-primes
    let ans = 0;

    // Iterate over the prime values
    for (let i = 0; i < pr.length; i += 1) {

        for (let j = i; j < pr.length; j += 1) {

            // Break the loop once the product exceeds N
            if (pr[i] * pr[j] > N)
                break;

            // Add valid products which are less than
            // or equal to N
            // each product is a semi-prime number
            ans += pr[i] * pr[j];
        }
    }
    return ans;
}

// Driver code

    let N = 6;

    sieve(N);

    document.write(SemiPrimeSum(N));

</script>
```

**Output:** 

```
10
```