# 数组中所有素数的异或运算

> 原文:[https://www . geesforgeks . org/数组中所有素数的异或/](https://www.geeksforgeeks.org/xor-of-all-prime-numbers-in-an-array/)

给定整数数组 *arr[]* 。任务是找到数组中所有素数的按位异或。
**示例** :

```
Input: arr[] = {2, 5, 8, 4, 3}
Output: 4

Input: arr[] = {7, 12, 2, 6, 11}
Output: 14
```

**进场:**

*   创建一个[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)来检查一个元素在 O(1)中是否是质数。
*   遍历数组，检查数字是否是质数。
*   计算数组中所有素元素的异或。

以下是上述方法的实现:

## C++

```
// C++ program to find Xor of all
// Prime numbers in array

#include <bits/stdc++.h>
using namespace std;

bool prime[100005];

void SieveOfEratosthenes(int n)
{

    memset(prime, true, sizeof(prime));

    // false here indicates
    // that it is not prime
    prime[1] = false;

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to compute xor of all
// prime elements
int xorPrimes(int arr[], int n)
{
    SieveOfEratosthenes(100005);

    int xorVal = 0;

    for (int i = 0; i < n; i++) {

        // if the element is prime
        if (prime[arr[i]])
            xorVal = xorVal ^ arr[i];
    }

    return xorVal;
}

// Driver code
int main()
{

    int arr[] = { 4, 3, 2, 6, 100, 17 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << xorPrimes(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Xor of all
// Prime numbers in array
import java.util.Arrays;

class GFG
{
    static boolean prime[] = new boolean[100005];

    static void SieveOfEratosthenes(int n)
    {
        Arrays.fill(prime, true);

        // false here indicates
        // that it is not prime
        prime[1] = false;

        for (int p = 2; p * p < n; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p])
            {
                // Update all multiples of p,
                // set them to non-prime
                for (int i = p * 2; i < n; i += p)
                {
                    prime[i] = false;
                }
            }
        }
    }

    // Function to compute xor of all
    // prime elements
    static int xorPrimes(int arr[], int n)
    {
        SieveOfEratosthenes(100005);
        int xorVal = 0;
        for (int i = 0; i < n; i++)
        {
            // if the element is prime
            if (prime[arr[i]])
            {
                xorVal = xorVal ^ arr[i];
            }
        }
        return xorVal;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {4, 3, 2, 6, 100, 17};
        int n = arr.length;
        System.out.println(xorPrimes(arr, n));
    }
}

// This code is contributed by
// Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find Xor of
# all Prime numbers in array

prime = [True] * (100005)

def SieveOfEratosthenes(n):

    # False here indicates
    # that it is not prime
    prime[1] = False
    p = 2

    while p*p <= n:

        # If prime[p] is not changed,
        # then it is a prime
        if prime[p]: 

            # Update all multiples of p,
            # set them to non-prime
            for i in range(p * 2, n+1, p):
                prime[i] = False

        p += 1

# Function to compute xor
# of all prime elements
def xorPrimes(arr, n):

    SieveOfEratosthenes(100004)

    xorVal = 0
    for i in range(0, n): 

        # if the element is prime
        if prime[arr[i]]:
            xorVal = xorVal ^ arr[i]

    return xorVal

# Driver code
if __name__ == "__main__":

    arr = [4, 3, 2, 6, 100, 17] 
    n = len(arr)

    print(xorPrimes(arr, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find Xor of all
// Prime numbers in array
using System;

class GFG
{
    static bool []prime = new bool[100005];

    static void SieveOfEratosthenes(int n)
    {
        for(int i = 0; i < 100005; i++)
            prime[i] = true;

        // false here indicates
        // that it is not prime
        prime[1] = false;

        for (int p = 2; p * p < n; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p])
            {
                // Update all multiples of p,
                // set them to non-prime
                for (int i = p * 2; i < n; i += p)
                {
                    prime[i] = false;
                }
            }
        }
    }

    // Function to compute xor of all
    // prime elements
    static int xorPrimes(int []arr, int n)
    {
        SieveOfEratosthenes(100005);
        int xorVal = 0;
        for (int i = 0; i < n; i++)
        {
            // if the element is prime
            if (prime[arr[i]])
            {
                xorVal = xorVal ^ arr[i];
            }
        }
        return xorVal;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {4, 3, 2, 6, 100, 17};
        int n = arr.Length;
        Console.WriteLine(xorPrimes(arr, n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript program to find Xor of all
// Prime numbers in array

var prime = Array(100005).fill(true);

function SieveOfEratosthenes( n)
{

    // false here indicates
    // that it is not prime
    prime[1] = false;

    for (var p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (var i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to compute xor of all
// prime elements
function xorPrimes( arr, n)
{
    SieveOfEratosthenes(100005);

    var xorVal = 0;

    for (var i = 0; i < n; i++) {

        // if the element is prime
        if (prime[arr[i]])
            xorVal = xorVal ^ arr[i];
    }

    return xorVal;
}

// Driver code
var arr = [ 4, 3, 2, 6, 100, 17 ];
var n = arr.length;
document.write( xorPrimes(arr, n));

</script>
```

**Output:** 

```
16
```