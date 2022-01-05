# 计算元素乘积与给定数组相同的长度为 K 的数组

> 原文:[https://www . geeksforgeeks . org/count-长度为 k 的数组-其元素乘积与给定数组的元素乘积相同/](https://www.geeksforgeeks.org/count-arrays-of-length-k-whose-product-of-elements-is-same-as-that-of-given-array/)

给定一个长度为 **N** 的整数数组**arr【】**和一个长度为 **K** 的整数数组，任务是计算长度为 **K** 的可能数组的数量，使得该数组的所有元素的乘积等于给定数组**arr【】**的所有元素的乘积。因为答案可能很大，所以以 10 <sup>9</sup> + 7 为模返回答案。

**示例:**

> **输入:** arr[] = {2，3}，K = 3
> **输出:** 9
> 数组元素的乘积为 2 * 3 = 6。
> 有 9 个这样的长度为 3 的可能数组，其
> 元素的乘积为 6，
> {1，2，3}，{1，3，2}，{2，1，3}，{2，3，1，2}，{3，2，1}，
> {1，1，6}，{1，6，1}和{6，1，1}。
> 
> **输入:** arr[] = {1，3，5，2}，K = 3
> T3】输出: 27

**先决条件:** [素分解](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)[计算 nCr % p](https://www.geeksforgeeks.org/compute-ncr-p-set-3-using-fermat-little-theorem/)
**方法:**让 arr[]所有元素的乘积为 *X* 。 *X* 可以用它的素分解来表示，即*X*= p<sub>1</sub>T17】c<sub>1</sub>T20】* p<sub>2</sub>T23】c<sub>2</sub>T26】*……* p<sub>r</sub>T29】c<sub>r</sub>T32】其中 p <sub>i 【T34 让 **K** 大小的数组为 *B[]* 。不求 *B[]* 的实际整数，求每个 *B <sub>i</sub>* 的素因子分解。来自 *B[]* 的任意数的素因子分解，除了是 *X* 因子的素外，不能有任何素，因为*X*%*B<sub>I</sub>T56】应该等于零。*</sub>

> 由此可见，b<sub>I</sub>= p<sub>【1】</sub><sup>【C1】</sup><sub>【I】</sub>* p<sub>【2】<sup>【C2】</sup>T12 <sub>等等， b<sub>【1】</sub>* b<sub>【2】</sub>*【b】<sub>【k】</sub>= p</sub></sub><sub>1】 * * p<sub>【r】</sub><sup>(c<sub>【r】</sub><sub>【1】</sub>+c<sub>【r】</sub><sub>【2】</sub>+【c】</sup></sub>
> 
> 方程 b<sub>1</sub>* b<sub><sub>*<sub>【k】= x = p <sub><sub><sub>【1】</sub><sub>【1】</sub>+c<sub>【1】</sub><sub>【2】</sub>+【c】<sub><sub>k</sub>
> 。
> 。
> 【r】<sub><sub>【1】</sub>+c<sub>【r】</sub><sub>【2】</sub>+【c】<sub>【r】<sub>【k】</sub></sub></sub></sub></sub></sub></sub></sub></sub>
> 
> 其中 c<sub>I</sub>T2j>= 0

对 i <sup>第</sup>个等式的回答等于在 **K** 个可区分的盒子中分配*C<sub>I</sub>T5】个相同的球的方式数，因此是*T9】C<sub>I</sub>+K–1C<sub>K–1</sub>T15】。所有的方程都是独立的，所以最终答案=每个方程答案的乘积。**

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define MAXN (ll)(1e5 + 1)
#define mod (ll)(1e9 + 7)

// To store the smallest prime factor
// for every number
ll spf[MAXN];

// Initialize map to store
// count of prime factors
map<ll, ll> cnt;

// Function to calculate SPF(Smallest Prime Factor)
// for every number till MAXN
void sieve()
{
    spf[1] = 1;
    for (int i = 2; i < MAXN; i++)

        // Marking smallest prime factor for every
        // number to be itself
        spf[i] = i;

    // Separately marking spf for every even
    // number as 2
    for (int i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    for (int i = 3; i * i < MAXN; i++) {

        // Checking if i is prime
        if (spf[i] == i) {

            // Marking SPF for all numbers divisible by i
            for (int j = i * i; j < MAXN; j += i)

                // Marking spf[j] if it is not
                // previously marked
                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function to factorize using spf
// and store in cnt
void factorize(ll f)
{
    while (f > 1) {
        ll x = spf[f];
        while (f % x == 0) {
            cnt[x]++;
            f /= x;
        }
    }
}

// Function to return n! % p
ll factorial(ll n, ll p)
{

    // Initialize result
    ll res = 1;
    for (int i = 2; i <= n; i++)
        res = (res * i) % p;
    return res;
}

// Iterative Function to calculate (x^y)%p
// in O(log y)
ll power(ll x, ll y, ll p)
{

    // Initialize result
    ll res = 1;

    // Update x if it is >= p
    x = x % p;

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        // y = y/2
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Function that returns n^(-1) mod p
ll modInverse(ll n, ll p)
{
    return power(n, p - 2, p);
}

// Function that returns nCr % p
// using Fermat's little theorem
ll nCrModP(ll n, ll r, ll p)
{
    // Base case
    if (r == 0)
        return 1;

    // Fill factorial array so that we
    // can find all factorial of r, n
    // and n - r
    ll fac[n + 1];
    fac[0] = 1;
    for (int i = 1; i <= n; i++)
        fac[i] = fac[i - 1] * i % p;

    return (fac[n] * modInverse(fac[r], p) % p
            * modInverse(fac[n - r], p) % p)
           % p;
}

// Function to return the count the number of possible
// arrays mod P of length K such that the product of all
// elements of that array is equal to the product of
// all elements of the given array of length N
ll countArrays(ll arr[], ll N, ll K, ll P)
{
    // Initialize result
    ll res = 1;

    // Call sieve to get spf
    sieve();

    for (int i = 0; i < N; i++) {

        // Factorize arr[i], count and
        // store its factors in cnt
        factorize(arr[i]);
    }

    for (auto i : cnt) {
        int ci = i.second;
        res = (res * nCrModP(ci + K - 1, K - 1, P)) % P;
    }

    return res;
}

// Driver code
int main()
{
    ll arr[] = { 1, 3, 5, 2 }, K = 3;
    ll N = sizeof(arr) / sizeof(arr[0]);

    cout << countArrays(arr, N, K, mod);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach 
import java.util.HashMap;

class GFG 
{

    static long MAXN = 100001L, mod = 1000000007L;

    // To store the smallest prime factor
    // for every number
    static long[] spf = new long[(int) MAXN];

    // Initialize map to store
    // count of prime factors
    static HashMap<Long, Long> cnt = new HashMap<>();

    // Function to calculate SPF(Smallest Prime Factor)
    // for every number till MAXN
    public static void sieve() 
    {
        spf[1] = 1;
        for (int i = 2; i < MAXN; i++)

            // Marking smallest prime factor for every
            // number to be itself
            spf[i] = i;

        // Separately marking spf for every even
        // number as 2
        for (int i = 4; i < MAXN; i += 2)
            spf[i] = 2;

        for (int i = 3; i * i < MAXN; i++) 
        {

            // Checking if i is prime
            if (spf[i] == i) {

                // Marking SPF for all numbers divisible by i
                for (int j = i * i; j < MAXN; j += i)

                    // Marking spf[j] if it is not
                    // previously marked
                    if (spf[j] == j)
                        spf[j] = i;
            }
        }
    }

    // Function to factorize using spf
    // and store in cnt
    public static void factorize(long f)
    {
        while (f > 1) 
        {
            long x = spf[(int) f];
            while (f % x == 0) 
            {
                if (cnt.containsKey(x)) 
                {
                    long z = cnt.get(x);
                    cnt.put(x, ++z);
                } 
                else
                    cnt.put(x, (long) 1);
                f /= x;
            }
        }
    }

    // Function to return n! % p
    public static long factorial(long n, long p)
    {

        // Initialize result
        long res = 1;
        for (long i = 2; i <= n; i++)
            res = (res * i) % p;
        return res;
    }

    // Iterative Function to calculate (x^y)%p
    // in O(log y)
    public static long power(long x, long y, long p) 
    {

        // Initialize result
        long res = 1;

        // Update x if it is >= p
        x = x % p;

        while (y > 0) {

            // If y is odd, multiply x with result
            if (y % 2 == 1)
                res = (res * x) % p;

            // y must be even now
            // y = y/2
            y = y >> 1;
            x = (x * x) % p;
        }
        return res;
    }

    // Function that returns n^(-1) mod p
    public static long modInverse(long n, long p) 
    {
        return power(n, p - 2, p);
    }

    // Function that returns nCr % p
    // using Fermat's little theorem
    public static long nCrModP(long n, long r, long p)
    {
        // Base case
        if (r == 0)
            return 1;

        // Fill factorial array so that we
        // can find all factorial of r, n
        // and n - r
        long[] fac = new long[(int) n + 1];
        fac[0] = 1;
        for (int i = 1; i <= n; i++)
            fac[i] = fac[i - 1] * i % p;

        return (fac[(int) n] * modInverse(fac[(int) r], p) % p * 
                modInverse(fac[(int) (n - r)], p) % p) % p;
    }

    // Function to return the count the number of possible
    // arrays mod P of length K such that the product of all
    // elements of that array is equal to the product of
    // all elements of the given array of length N
    public static long countArrays(long[] arr, 
                                   long N, long K, long P)
    {
        // Initialize result
        long res = 1;

        // Call sieve to get spf
        sieve();

        for (int i = 0; i < N; i++) 
        {

            // Factorize arr[i], count and
            // store its factors in cnt
            factorize(arr[i]);
        }

        for (HashMap.Entry<Long, Long> entry : cnt.entrySet())
        {
            long ci = entry.getValue();
            res = (res * nCrModP(ci + K - 1, K - 1, P)) % P;
        }

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        long[] arr = { 1, 3, 5, 2 };
        long K = 3;
        long N = arr.length;
        System.out.println(countArrays(arr, N, K, mod));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

from math import sqrt
MAXN = 100001
mod = 1000000007

# To store the smallest prime factor
# for every number
spf = [0 for i in range(MAXN)]

# Initialize map to store
# count of prime factors
cnt = {i:0 for i in range(10)}

# Function to calculate SPF(Smallest Prime Factor)
# for every number till MAXN
def sieve():
    spf[1] = 1
    for i in range(2,MAXN):

        # Marking smallest prime factor for every
        # number to be itself
        spf[i] = i

    # Separately marking spf for every even
    # number as 2
    for i in range(4,MAXN,2):
        spf[i] = 2

    for i in range(3,int(sqrt(MAXN))+1,1):

        # Checking if i is prime
        if (spf[i] == i):

            # Marking SPF for all numbers divisible by i
            for j in range(i * i,MAXN,i):

                # Marking spf[j] if it is not
                # previously marked
                if (spf[j] == j):
                    spf[j] = i

# Function to factorize using spf
# and store in cnt
def factorize(f):
    while (f > 1):
        x = spf[f]
        while (f % x == 0):
            cnt[x] += 1
            f = int(f/x)

# Function to return n! % p
def factorial(n,p):

    #Initialize result
    res = 1
    for i in range(2,n+1,1):
        res = (res * i) % p
    return res

# Iterative Function to calculate (x^y)%p
# in O(log y)
def power(x, y, p):

    # Initialize result
    res = 1

    # Update x if it is >= p
    x = x % p

    while (y > 0):

        # If y is odd, multiply x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        # y = y/2
        y = y >> 1
        x = (x * x) % p
    return res

# Function that returns n^(-1) mod p
def modInverse(n,p):
    return power(n, p - 2, p)

# Function that returns nCr % p
# using Fermat's little theorem
def nCrModP(n,r,p):

    # Base case
    if (r == 0):
        return 1

    # Fill factorial array so that we
    # can find all factorial of r, n
    # and n - r
    fac = [0 for i in range(n+1)]
    fac[0] = 1
    for i in range(1,n+1,1):
        fac[i] = fac[i - 1] * i % p

    return (fac[n] * modInverse(fac[r], p) % p *
                modInverse(fac[n - r], p) % p)% p

# Function to return the count the number of possible
# arrays mod P of length K such that the product of all
# elements of that array is equal to the product of
# all elements of the given array of length N
def countArrays(arr,N,K,P):
    # Initialize result
    res = 1

    # Call sieve to get spf
    sieve()

    for i in range(N):
        # Factorize arr[i], count and
        # store its factors in cnt
        factorize(arr[i])

    for key,value in cnt.items():
        ci = value
        res = (res * nCrModP(ci + K - 1, K - 1, P)) % P

    return res

# Driver code
if __name__ == '__main__':
    arr = [1, 3, 5, 2]
    K = 3
    N = len(arr)

    print(countArrays(arr, N, K, mod))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach 
using System;
using System.Collections.Generic;                 

class GFG 
{
    static long MAXN = 100001L, mod = 1000000007L;

    // To store the smallest prime factor
    // for every number
    static long[] spf = new long[(int) MAXN];

    // Initialize map to store
    // count of prime factors
    static Dictionary<long, 
                      long> cnt = new Dictionary<long, 
                                                 long>();

    // Function to calculate SPF(Smallest Prime Factor)
    // for every number till MAXN
    public static void sieve() 
    {
        spf[1] = 1;
        for (int i = 2; i < MAXN; i++)

            // Marking smallest prime factor for every
            // number to be itself
            spf[i] = i;

        // Separately marking spf for every even
        // number as 2
        for (int i = 4; i < MAXN; i += 2)
            spf[i] = 2;

        for (int i = 3; i * i < MAXN; i++) 
        {

            // Checking if i is prime
            if (spf[i] == i)
            {

                // Marking SPF for all numbers divisible by i
                for (int j = i * i; j < MAXN; j += i)

                    // Marking spf[j] if it is not
                    // previously marked
                    if (spf[j] == j)
                        spf[j] = i;
            }
        }
    }

    // Function to factorize using spf
    // and store in cnt
    public static void factorize(long f)
    {
        while (f > 1) 
        {
            long x = spf[(int) f];
            while (f % x == 0) 
            {
                if (cnt.ContainsKey(x)) 
                {
                    long z = cnt[x];
                    cnt[x] = ++z;
                } 
                else
                    cnt.Add(x, (long) 1);
                f /= x;
            }
        }
    }

    // Function to return n! % p
    public static long factorial(long n, long p)
    {

        // Initialize result
        long res = 1;
        for (long i = 2; i <= n; i++)
            res = (res * i) % p;
        return res;
    }

    // Iterative Function to calculate (x^y)%p
    // in O(log y)
    public static long power(long x, long y, long p) 
    {

        // Initialize result
        long res = 1;

        // Update x if it is >= p
        x = x % p;

        while (y > 0) 
        {

            // If y is odd, multiply x with result
            if (y % 2 == 1)
                res = (res * x) % p;

            // y must be even now
            // y = y/2
            y = y >> 1;
            x = (x * x) % p;
        }
        return res;
    }

    // Function that returns n^(-1) mod p
    public static long modInverse(long n, long p) 
    {
        return power(n, p - 2, p);
    }

    // Function that returns nCr % p
    // using Fermat's little theorem
    public static long nCrModP(long n, long r, long p)
    {
        // Base case
        if (r == 0)
            return 1;

        // Fill factorial array so that we
        // can find all factorial of r, n
        // and n - r
        long[] fac = new long[(int) n + 1];
        fac[0] = 1;
        for (int i = 1; i <= n; i++)
            fac[i] = fac[i - 1] * i % p;

        return (fac[(int) n] * modInverse(fac[(int) r], p) % p * 
                               modInverse(fac[(int) (n - r)], p) % p) % p;
    }

    // Function to return the count the number of possible
    // arrays mod P of length K such that the product of all
    // elements of that array is equal to the product of
    // all elements of the given array of length N
    public static long countArrays(long[] arr, 
                                   long N, long K, long P)
    {
        // Initialize result
        long res = 1;

        // Call sieve to get spf
        sieve();

        for (int i = 0; i < N; i++) 
        {

            // Factorize arr[i], count and
            // store its factors in cnt
            factorize(arr[i]);
        }

        foreach(KeyValuePair<long, long> entry in cnt)
        {
            long ci = entry.Value;
            res = (res * nCrModP(ci + K - 1, K - 1, P)) % P;
        }

        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        long[] arr = { 1, 3, 5, 2 };
        long K = 3;
        long N = arr.Length;
        Console.WriteLine(countArrays(arr, N, K, mod));
    }
}

// This code is contributed by PrinciRaj1992
```

**Output:**

```
27

```