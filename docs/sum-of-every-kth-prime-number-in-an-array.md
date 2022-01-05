# 数组中每第 K 个素数的和

> 原文:[https://www . geesforgeks . org/每 kth 素数之和数组/](https://www.geeksforgeeks.org/sum-of-every-kth-prime-number-in-an-array/)

给定一个整数数组(小于 10^6)，任务是找出出现在每个(k-1)素数
之后的所有素数的和，即数组中的每个第 k 个素数。
**例:**

```
Input : Array : 2, 3, 5, 7, 11 ; n=5; k=2
Output : Sum = 10
Explanation: All the elements of the array are prime. So,
the prime numbers after every K intervals are 3, 7 and their sum is 10\.   

Input : Array : 41, 23, 12, 17, 18, 19 ; n=6; k=2
Output : Sum = 42
```

**一个简单的方法**
我们必须遍历数组，找到每(k-1)个素数之后的素数。这样，我们将不得不检查数组的每个元素是否是质数，随着数组大小的增加，这将花费更多的时间。
**高效方法**
我们将创建一个存储一个数是否是质数的筛子。然后，它可以用来在 O(1)时间内检查一个数字是否符合质数。这样，我们只需要跟踪每一个第 K 个素数，并保持运行和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000000
bool prime[MAX + 1];
void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and initialize
    // all the entries as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    memset(prime, true, sizeof(prime));

    // 0 and 1 are not prime numbers
    prime[1] = false;
    prime[0] = false;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// compute the answer
void solve(int arr[], int n, int k)
{
    // count of primes
    int c = 0;

    // sum of the primes
    long long int sum = 0;

    // traverse the array
    for (int i = 0; i < n; i++) {

        // if the number is a prime
        if (prime[arr[i]]) {

            // increase the count
            c++;

            // if it is the K'th prime
            if (c % k == 0) {
                sum += arr[i];
                c = 0;
            }
        }
    }
    cout << sum << endl;
}

// Driver code
int main()
{

    // create the sieve
    SieveOfEratosthenes();

    int n = 5, k = 2;

    int arr[n] = { 2, 3, 5, 7, 11 };

    solve(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    static final int MAX=1000000;
    static boolean []prime=new boolean[MAX + 1];
    static void SieveOfEratosthenes()
    {
        // Create a boolean array "prime[0..n]" and initialize
        // all the entries as true. A value in prime[i] will
        // finally be false if i is Not a prime, else true.
        for(int i=0;i<=MAX;i++)
            prime[i]=true;

        // 0 and 1 are not prime numbers
        prime[1] = false;
        prime[0] = false;

        for (int p = 2; p * p <= MAX; p++) {

            // If prime[p] is not changed, then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= MAX; i += p)
                    prime[i] = false;
            }
        }
    }

    // compute the answer
    static void solve(int []arr, int n, int k)
    {
        // count of primes
        int c = 0;

        // sum of the primes
        long  sum = 0;

        // traverse the array
        for (int i = 0; i < n; i++) {

            // if the number is a prime
            if (prime[arr[i]]) {

                // increase the count
                c++;

                // if it is the K'th prime
                if (c % k == 0) {
                    sum += arr[i];
                    c = 0;
                }
            }
        }
        System.out.println(sum);
    }

    // Driver code
    public static void main(String []args)
    {

        // create the sieve
        SieveOfEratosthenes();

        int n = 5, k = 2;

        int []arr = { 2, 3, 5, 7, 11 };

        solve(arr, n, k);

    }

}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
def SieveOfEratosthenes():

    # 0 and 1 are not prime numbers
    prime[1] = False
    prime[0] = False
    p = 2

    while p * p <= MAX:

        # If prime[p] is not changed,
        # then it is a prime
        if prime[p] == True:

            # Update all multiples of p
            for i in range(p * 2, MAX + 1, p):
                prime[i] = False

        p += 1

# Compute the answer
def solve(arr, n, k):

    # count of primes
    c = 0

    # sum of the primes
    Sum = 0

    # Traverse the array
    for i in range(0, n):

        # if the number is a prime
        if prime[arr[i]]:

            # increase the count
            c += 1
            # if it is the K'th prime
            if c % k == 0:
                Sum += arr[i]
                c = 0

    print(Sum)

# Driver code
if __name__ == "__main__":

    MAX = 1000000
    prime = [True] * (MAX + 1)

    # Create the sieve
    SieveOfEratosthenes()

    n, k = 5, 2
    arr = [2, 3, 5, 7, 11]

    solve(arr, n, k)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach

using System;
class GFG
{

    static int MAX=1000000;
    static bool []prime=new bool[MAX + 1];
    static void SieveOfEratosthenes()
    {
        // Create a boolean array "prime[0..n]" and initialize
        // all the entries as true. A value in prime[i] will
        // finally be false if i is Not a prime, else true.
        for(int i=0;i<=MAX;i++)
            prime[i]=true;

        // 0 and 1 are not prime numbers
        prime[1] = false;
        prime[0] = false;

        for (int p = 2; p * p <= MAX; p++) {

            // If prime[p] is not changed, then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= MAX; i += p)
                    prime[i] = false;
            }
        }
    }

    // compute the answer
    static void solve(int []arr, int n, int k)
    {
        // count of primes
        int c = 0;

        // sum of the primes
        long  sum = 0;

        // traverse the array
        for (int i = 0; i < n; i++) {

            // if the number is a prime
            if (prime[arr[i]]) {

                // increase the count
                c++;

                // if it is the K'th prime
                if (c % k == 0) {
                    sum += arr[i];
                    c = 0;
                }
            }
        }
        Console.WriteLine(sum);
    }

    // Driver code
    public static void Main()
    {

        // create the sieve
        SieveOfEratosthenes();

        int n = 5, k = 2;

        int []arr = { 2, 3, 5, 7, 11 };

        solve(arr, n, k);

    }

}
```

## java 描述语言

```
<script>

// Javascript program to find next
// greater number than N

MAX = 1000000;
prime = new Array(MAX + 1);
function SieveOfEratosthenes()
{
    // Create a boolean array
    // "prime[0..n]" and initialize
    // all the entries as true.
    // A value in prime[i] will
    // finally be false if i is Not a prime,
    // else true.
    prime.fill(true);

    // 0 and 1 are not prime numbers
    prime[1] = false;
    prime[0] = false;

    for (var p = 2; p * p <= MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (var i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// compute the answer
function solve(arr, n, k)
{
    // count of primes
    var c = 0;

    // sum of the primes
    var sum = 0;

    // traverse the array
    for (var i = 0; i < n; i++) {

        // if the number is a prime
        if (prime[arr[i]]) {

            // increase the count
            c++;

            // if it is the K'th prime
            if (c % k == 0) {
                sum += arr[i];
                c = 0;
            }
        }
    }
    document.write( sum + "<br>")
}

SieveOfEratosthenes();
var n = 5, k = 2;
var arr = [ 2, 3, 5, 7, 11 ];
solve(arr, n, k);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
10
```