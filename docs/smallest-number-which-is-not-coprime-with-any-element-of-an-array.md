# 与数组的任何元素都不是互质的最小数

> 原文:[https://www . geesforgeks . org/最小数与数组中的任何元素都不是互素/](https://www.geeksforgeeks.org/smallest-number-which-is-not-coprime-with-any-element-of-an-array/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**大小 **N** ，任务是找到与给定数组的任何元素都不是同素的最小数。

**示例:**

> **输入:** arr[] = {3，4，6，7，8，9，10}
> **输出:** 42
> **解释:**数组元素的素分解为:
> 3 = 3
> 4 = 2 * 2
> 6 = 2 * 3
> 7 = 7
> 8 = 2 * 2 * 2
> 9 = 3 * 3
> 10 = 2 * 5
> 考虑素
> 
> **输入:** arr[] = {4，3}
> **输出:** 6
> **说明:**数组元素的素因子分解是:
> 4 = 2 * 2
> 3 = 3
> 考虑素因子{2，3}得到的数 X (= 2 * 3 = 6)，与其他任何数组元素都不是共素的。

**方法:**这个想法是基于这样的观察:所需的数字，比如说 **X，**不应该与任何数组元素**arr【I】**同素。必须存在某种共同因素， **d ≥ 2** 对于每个数组元素 **arr[i]** ，它将 **arr[i]** 和 **X 分开。**最小的 **d** 可能是一个[质数](https://www.geeksforgeeks.org/prime-numbers/)。因此，我们的想法是考虑素数集合，使它们的乘积不与所有数组元素同素，并找到可能的最小数。按照以下步骤解决问题:

*   初始化一个变量，比如说**和**，作为 [INT_MAX](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 来存储需要的结果。
*   初始化一个数组，**质数[]** 到[存储质数](https://www.geeksforgeeks.org/print-all-prime-numbers-less-than-or-equal-to-n/)。
*   [生成这个数组的所有子集](https://www.geeksforgeeks.org/find-distinct-subsets-given-set/)，对于每个子集，将其乘积存储在一个变量中，比如**[检查它是否与任何数组元素](https://www.geeksforgeeks.org/gcd-two-array-numbers/)不互质。如果发现为真，则更新**和**的值。**
*   **否则，移动到下一个子集。**
*   **完成上述步骤后，打印**和**的值作为结果。**T3】****

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define MAX 50

// Function check if a
// number is prime or not
bool isPrime(ll n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check if n is divisible by 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Check for every 6th number. The above
    // checking allows to skip middle 5 numbers
    for (ll i = 5; i * i <= n; i = i + 6)

        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to store primes in an array
void findPrime(vector<ll>& primes)
{
    for (ll i = 2; i <= MAX; i++) {
        if (isPrime(i))
            primes.push_back(i);
    }
}

// Function to calculate
// GCD of two numbers
ll gcd(ll a, ll b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to find the smallest
// number which is not coprime with
// any element of the array arr[]
void findMinimumNumber(ll arr[], ll N)
{
    // Store the prime numbers
    vector<ll> primes;

    // Function call to fill
    // the prime numbers
    findPrime(primes);

    // Stores the answer
    ll ans = INT_MAX;

    ll n = primes.size();

    // Generate all non-empty
    // subsets of the primes[] array
    for (ll i = 1; i < (1 << n); i++) {

        // Stores product of the primes
        ll temp = 1;
        for (ll j = 0; j < n; j++) {
            if (i & (1 << j)) {
                temp *= primes[j];
            }
        }

        // Checks if temp is coprime
        // with the array or not
        bool check = true;

        // Check if the product temp is
        // not coprime with the whole array
        for (ll k = 0; k < N; k++) {
            if (gcd(temp, arr[k]) == 1) {
                check = false;
                break;
            }
        }

        // If the product is not
        // co-prime with the array
        if (check)
            ans = min(ans, temp);
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    // Given array
    ll arr[] = { 3, 4, 6, 7, 8, 9, 10 };

    // Stores the size of the array
    ll N = sizeof(arr) / sizeof(arr[0]);

    findMinimumNumber(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

static long MAX = 50;

// Function check if a
// number is prime or not
static boolean isPrime(long n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check if n is divisible by 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Check for every 6th number. The above
    // checking allows to skip middle 5 numbers
    for(long i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to store primes in an array
static void findPrime(ArrayList<Long> primes)
{
    for(long i = 2; i <= MAX; i++)
    {
        if (isPrime(i))
            primes.add(i);
    }
}

// Function to calculate
// GCD of two numbers
static long gcd(long a, long b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to find the smallest
// number which is not coprime with
// any element of the array arr[]
static void findMinimumNumber(long []arr, long N)
{
    ArrayList<Long> primes = new ArrayList<Long>();

    // Function call to fill
    // the prime numbers
    findPrime(primes);

    // Stores the answer
    long ans = 2147483647;

    int n = primes.size();

    // Generate all non-empty
    // subsets of the primes[] array
    for(int i = 1; i < (1 << n); i++)
    {

        // Stores product of the primes
        long temp = 1;
        for(int j = 0; j < n; j++)
        {
            if ((i & (1 << j)) > 0)
            {
                temp *= primes.get(j);
            }
        }

        // Checks if temp is coprime
        // with the array or not
        boolean check = true;

        // Check if the product temp is
        // not coprime with the whole array
        for(long k = 0; k < N; k++)
        {
            if (gcd(temp, arr[(int)k]) == 1l)
            {
                check = false;
                break;
            }
        }

        // If the product is not
        // co-prime with the array
        if (check == true)
            ans = Math.min(ans, temp);
    }

    // Prlong the answer
    System.out.print(ans);
}

// Driver code  
public static void main (String[] args)
{

    // Given array
    long []arr = { 3, 4, 6, 7, 8, 9, 10 };

    // Stores the size of the array
    long N = arr.length;

    findMinimumNumber(arr, N);
}
}

// This code is contributed by offbeat
```

## **蟒蛇 3**

```
# Python 3 program for the above approach
MAX = 50

import sys
from math import sqrt,gcd

# Function check if a
# number is prime or not
def isPrime(n):

    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # Check if n is divisible by 2 or 3
    if (n % 2 == 0 or n % 3 == 0):
        return False

    # Check for every 6th number. The above
    # checking allows to skip middle 5 numbers
    for i in range(5,int(sqrt(n))+1,6):
        if (n % i == 0 or n % (i + 2) == 0):
            return False

    return True

# Function to store primes in an array
def findPrime(primes):
    global MAX
    for i in range(2, MAX + 1, 1):
        if(isPrime(i)):
            primes.append(i)

# Function to find the smallest
# number which is not coprime with
# any element of the array arr[]
def findMinimumNumber(arr, N):

    # Store the prime numbers
    primes = []

    # Function call to fill
    # the prime numbers
    findPrime(primes)

    # Stores the answer
    ans = sys.maxsize
    n = len(primes)

    # Generate all non-empty
    # subsets of the primes[] array
    for i in range(1, (1 << n), 1):

        # Stores product of the primes
        temp = 1
        for j in range(n):
            if (i & (1 << j)):
                temp *= primes[j]

        # Checks if temp is coprime
        # with the array or not
        check = True

        # Check if the product temp is
        # not coprime with the whole array
        for k in range(N):
            if (gcd(temp, arr[k]) == 1):
                check = False
                break

        # If the product is not
        # co-prime with the array
        if (check):
            ans = min(ans, temp)

    # Print the answer
    print(ans)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr =  [3, 4, 6, 7, 8, 9, 10]

    # Stores the size of the array
    N = len(arr)
    findMinimumNumber(arr, N)

    # This code is contributed by ipg2016107.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static long MAX = 50;

// Function check if a
// number is prime or not
static bool isPrime(long n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check if n is divisible by 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Check for every 6th number. The above
    // checking allows to skip middle 5 numbers
    for(long i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to store primes in an array
static void findPrime(List<long> primes)
{
    for(long i = 2; i <= MAX; i++)
    {
        if (isPrime(i))
            primes.Add(i);
    }
}

// Function to calculate
// GCD of two numbers
static long gcd(long a, long b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to find the smallest
// number which is not coprime with
// any element of the array arr[]
static void findMinimumNumber(long []arr, long N)
{

    List<long> primes = new List<long>();

    // Function call to fill
    // the prime numbers
    findPrime(primes);

    // Stores the answer
    long ans = 2147483647;

    int n = primes.Count;

    // Generate all non-empty
    // subsets of the primes[] array
    for(int i = 1; i < (1 << n); i++)
    {

        // Stores product of the primes
        long temp = 1;
        for(int j = 0; j < n; j++)
        {
            if ((i & (1 << j)) > 0)
            {
                temp *= primes[j];
            }
        }

        // Checks if temp is coprime
        // with the array or not
        bool check = true;

        // Check if the product temp is
        // not coprime with the whole array
        for(long k = 0; k < N; k++)
        {
            if (gcd(temp, arr[k]) == 1)
            {
                check = false;
                break;
            }
        }

        // If the product is not
        // co-prime with the array
        if (check == true)
            ans = Math.Min(ans, temp);
    }

    // Prlong the answer
    Console.Write(ans);
}

// Driver Code
public static void Main()
{

    // Given array
    long []arr = { 3, 4, 6, 7, 8, 9, 10 };

    // Stores the size of the array
    long N = arr.Length;

    findMinimumNumber(arr, N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

let MAX = 50

let primes = [];

// Function check if a
// number is prime or not
function isPrime(n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check if n is divisible by 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Check for every 6th number. The above
    // checking allows to skip middle 5 numbers
    for (let i = 5; i * i <= n; i = i + 6)

        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to store primes in an array
function findPrime()
{
    for (let i = 2; i <= MAX; i++) {
        if (isPrime(i))
            primes.push(i);
    }
}

// Function to calculate
// GCD of two numbers
function gcd(a, b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to find the smallest
// number which is not coprime with
// any element of the array arr[]
function findMinimumNumber(arr, N)
{
    // Store the prime numbers

    // Function call to fill
    // the prime numbers
    findPrime();

    // Stores the answer
    let ans = Number.MAX_SAFE_INTEGER;

    let n = primes.length;

    // Generate all non-empty
    // subsets of the primes[] array
    for (let i = 1; i < (1 << n); i++) {

        // Stores product of the primes
        let temp = 1;
        for (let j = 0; j < n; j++) {
            if (i & (1 << j)) {
                temp *= primes[j];
            }
        }

        // Checks if temp is coprime
        // with the array or not
        let check = true;

        // Check if the product temp is
        // not coprime with the whole array
        for (let k = 0; k < N; k++) {
            if (gcd(temp, arr[k]) == 1) {
                check = false;
                break;
            }
        }

        // If the product is not
        // co-prime with the array
        if (check)
            ans = Math.min(ans, temp);
    }

    // Print the answer
    document.write(ans);
}

// Driver Code
// Given array
let arr = [ 3, 4, 6, 7, 8, 9, 10 ];

// Stores the size of the array
let N = arr.length;

findMinimumNumber(arr, N);

</script>
```

****Output:** 

```
42
```** 

*****时间复杂度:** O(2 <sup>M</sup> *N*log(X))，其中 **M** 是数组* [*的大小*](https://www.geeksforgeeks.org/how-to-find-size-of-array-in-cc-without-using-sizeof-operator/) *素数【】和 **X** 是*中 [*最小元素*数组**](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)T22】arr【】
***辅助空间*****