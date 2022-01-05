# 数组中每个数的最大和最小质因数之和

> 原文:[https://www . geesforgeks . org/数组中每个数字的最大和最小质因数之和/](https://www.geeksforgeeks.org/sum-of-maximum-and-minimum-prime-factor-of-every-number-in-the-array/)

给定一个数组 **arr[]** ，任务是找到给定数组中每个数字的**最大值**和**最小质因数**的**和**。
**举例:**

> **输入:** arr[] = {15}
> **输出:**8
> 15 的最大和最小质因数
> 分别为 5 和 3。
> **输入:** arr[] = {5，10，15，20，25，30}
> **输出:** 10 7 8 7 10 7

**方法:**思路是利用厄拉多塞的[筛，预计算出每个数的所有最小和最大素因子，存储在两个数组中。在这种预计算之后，最小和最大质因数的和可以在恒定时间内找到。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

const int MAX = 100000;

// max_prime[i] represent maximum prime
// number that divides the number i
int max_prime[MAX];

// min_prime[i] represent minimum prime
// number that divides the number i
int min_prime[MAX];

// Function to store the minimum prime factor
// and the maximum prime factor in two arrays
void sieve(int n)
{
    for (int i = 2; i <= n; ++i) {

        // Check for prime number
        // if min_prime[i]>0,
        // then it is not a prime number
        if (min_prime[i] > 0) {
            continue;
        }

        // if i is a prime number
        // min_prime number that divide prime number
        // and max_prime number that divide prime number
        // is the number itself.
        min_prime[i] = i;
        max_prime[i] = i;

        int j = i + i;

        while (j <= n) {
            if (min_prime[j] == 0) {

                // If this number is being visited
                // for first time then this divisor
                // must be the smallest prime number
                // that divides this number
                min_prime[j] = i;
            }

            // Update prime number till
            // last prime number that divides this number

            // The last prime number that
            // divides this number will be maximum.
            max_prime[j] = i;
            j += i;
        }
    }
}

// Function to find the sum of the minimum
// and the maximum prime factors of every
// number from the given array
void findSum(int arr[], int n)
{

    // Pre-calculation
    sieve(MAX);

    // For every element of the given array
    for (int i = 0; i < n; i++) {

        // The sum of its smallest
        // and largest prime factor
        int sum = min_prime[arr[i]]
                  + max_prime[arr[i]];

        cout << sum << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 5, 10, 15, 20, 25, 30 };
    int n = sizeof(arr) / sizeof(int);

    findSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    static int MAX = 100000;

    // max_prime[i] represent maximum prime
    // number that divides the number i
    static int max_prime[] = new int[MAX + 1];

    // min_prime[i] represent minimum prime
    // number that divides the number i
    static int min_prime[] = new int[MAX + 1];

    // Function to store the minimum prime factor
    // and the maximum prime factor in two arrays
    static void sieve(int n)
    {
        for (int i = 2; i <= n; ++i)
        {

            // Check for prime number
            // if min_prime[i] > 0,
            // then it is not a prime number
            if (min_prime[i] > 0)
            {
                continue;
            }

            // if i is a prime number
            // min_prime number that divide prime number
            // and max_prime number that divide prime number
            // is the number itself.
            min_prime[i] = i;
            max_prime[i] = i;

            int j = i + i;

            while (j <= n)
            {
                if (min_prime[j] == 0)
                {

                    // If this number is being visited
                    // for first time then this divisor
                    // must be the smallest prime number
                    // that divides this number
                    min_prime[j] = i;
                }

                // Update prime number till
                // last prime number that divides this number

                // The last prime number that
                // divides this number will be maximum.
                max_prime[j] = i;
                j += i;
            }
        }
    }

    // Function to find the sum of the minimum
    // and the maximum prime factors of every
    // number from the given array
    static void findSum(int arr[], int n)
    {

        // Pre-calculation
        sieve(MAX);

        // For every element of the given array
        for (int i = 0; i < n; i++)
        {

            // The sum of its smallest
            // and largest prime factor
            int sum = min_prime[arr[i]]
                    + max_prime[arr[i]];

            System.out.print(sum + " ");
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 5, 10, 15, 20, 25, 30 };
        int n = arr.length ;

        findSum(arr, n);

    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python3 implementation of the approach
MAX = 100000

# max_prime[i] represent maximum prime
# number that divides the number i
max_prime = [0]*(MAX + 1)

# min_prime[i] represent minimum prime
# number that divides the number i
min_prime = [0]*(MAX + 1)

# Function to store the minimum prime factor
# and the maximum prime factor in two arrays
def sieve(n):
    for i in range(2, n + 1):

        # Check for prime number
        # if min_prime[i]>0,
        # then it is not a prime number
        if (min_prime[i] > 0):
            continue

        # if i is a prime number
        # min_prime number that divide prime number
        # and max_prime number that divide prime number
        # is the number itself.
        min_prime[i] = i
        max_prime[i] = i

        j = i + i

        while (j <= n):
            if (min_prime[j] == 0):

                # If this number is being visited
                # for first time then this divisor
                # must be the smallest prime number
                # that divides this number
                min_prime[j] = i

            # Update prime number till
            # last prime number that divides this number

            # The last prime number that
            # divides this number will be maximum.
            max_prime[j] = i
            j += i

# Function to find the sum of the minimum
# and the maximum prime factors of every
# number from the given array
def findSum(arr, n):

    # Pre-calculation
    sieve(MAX)

    # For every element of the given array
    for i in range(n):

        # The sum of its smallest
        # and largest prime factor
        sum = min_prime[arr[i]] + max_prime[arr[i]]

        print(sum, end = " ")

# Driver code
arr = [5, 10, 15, 20, 25, 30]
n = len(arr)

findSum(arr, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int MAX = 100000;

    // max_prime[i] represent maximum prime
    // number that divides the number i
    static int []max_prime = new int[MAX + 1];

    // min_prime[i] represent minimum prime
    // number that divides the number i
    static int []min_prime = new int[MAX + 1];

    // Function to store the minimum prime factor
    // and the maximum prime factor in two arrays
    static void sieve(int n)
    {
        for (int i = 2; i <= n; ++i)
        {

            // Check for prime number
            // if min_prime[i] > 0,
            // then it is not a prime number
            if (min_prime[i] > 0)
            {
                continue;
            }

            // if i is a prime number
            // min_prime number that divide prime number
            // and max_prime number that divide prime number
            // is the number itself.
            min_prime[i] = i;
            max_prime[i] = i;

            int j = i + i;

            while (j <= n)
            {
                if (min_prime[j] == 0)
                {

                    // If this number is being visited
                    // for first time then this divisor
                    // must be the smallest prime number
                    // that divides this number
                    min_prime[j] = i;
                }

                // Update prime number till
                // last prime number that divides this number

                // The last prime number that
                // divides this number will be maximum.
                max_prime[j] = i;
                j += i;
            }
        }
    }

    // Function to find the sum of the minimum
    // and the maximum prime factors of every
    // number from the given array
    static void findSum(int []arr, int n)
    {

        // Pre-calculation
        sieve(MAX);

        // For every element of the given array
        for (int i = 0; i < n; i++)
        {

            // The sum of its smallest
            // and largest prime factor
            int sum = min_prime[arr[i]]
                    + max_prime[arr[i]];

            Console.Write(sum + " ");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 5, 10, 15, 20, 25, 30 };
        int n = arr.Length ;

        findSum(arr, n);

    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var MAX = 100000;

// max_prime[i] represent maximum prime
// number that divides the number i
var max_prime = Array.from({length: MAX + 1}, (_, i) => 0);

// min_prime[i] represent minimum prime
// number that divides the number i
var min_prime = Array.from({length: MAX + 1}, (_, i) => 0);

// Function to store the minimum prime factor
// and the maximum prime factor in two arrays
function sieve(n)
{
    for (var i = 2; i <= n; ++i)
    {

        // Check for prime number
        // if min_prime[i] > 0,
        // then it is not a prime number
        if (min_prime[i] > 0)
        {
            continue;
        }

        // if i is a prime number
        // min_prime number that divide prime number
        // and max_prime number that divide prime number
        // is the number itself.
        min_prime[i] = i;
        max_prime[i] = i;

        var j = i + i;

        while (j <= n)
        {
            if (min_prime[j] == 0)
            {

                // If this number is being visited
                // for first time then this divisor
                // must be the smallest prime number
                // that divides this number
                min_prime[j] = i;
            }

            // Update prime number till
            // last prime number that divides this number

            // The last prime number that
            // divides this number will be maximum.
            max_prime[j] = i;
            j += i;
        }
    }
}

// Function to find the sum of the minimum
// and the maximum prime factors of every
// number from the given array
function findSum(arr , n)
{

    // Pre-calculation
    sieve(MAX);

    // For every element of the given array
    for (i = 0; i < n; i++)
    {

        // The sum of its smallest
        // and largest prime factor
        var sum = min_prime[arr[i]]
                + max_prime[arr[i]];

        document.write(sum + " ");
    }
}

// Driver code
var arr = [ 5, 10, 15, 20, 25, 30 ];
var n = arr.length ;

findSum(arr, n);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
10 7 8 7 10 7
```