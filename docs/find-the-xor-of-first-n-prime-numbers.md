# 求前 N 个素数的异或

> 原文:[https://www . geeksforgeeks . org/find-the-xor-first-n-prime-numbers/](https://www.geeksforgeeks.org/find-the-xor-of-first-n-prime-numbers/)

给定一个正整数 **N** ，任务是求第一个 **N** 素数的**异或**。
**举例:**

> **输入:** N = 3
> **输出:** 4
> 前 3 个质数为 2、3、5。
> 和 2 ^ 3 ^ 5 = 4
> **输入:** N = 5
> **输出:** 8

**进场:**

1.  创建厄拉多塞的[筛，以识别一个数字在 0(1)时间内是否为质数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
2.  从 **1** 开始循环，直到找到 **N** 个质数。
3.  将所有质数异或，忽略那些不是质数的。
4.  最后，打印**1<sup>ST</sup>T3**N**素数的异或。**

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 10000

// Create a boolean array "prime[0..n]" and initialize
// all entries it as true. A value in prime[i] will
// finally be false if i is Not a prime, else true.
bool prime[MAX + 1];
void SieveOfEratosthenes()
{
    memset(prime, true, sizeof(prime));

    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Set all multiples of p to non-prime
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the xor of 1st N prime numbers
int xorFirstNPrime(int n)
{
    // Count of prime numbers
    int count = 0, num = 1;

    // XOR of prime numbers
    int xorVal = 0;

    while (count < n) {

        // If the number is prime xor it
        if (prime[num]) {
            xorVal ^= num;

            // Increment the count
            count++;
        }

        // Get to the next number
        num++;
    }
    return xorVal;
}

// Driver code
int main()
{
    // Create the sieve
    SieveOfEratosthenes();

    int n = 4;

    // Find the xor of 1st n prime numbers
    cout << xorFirstNPrime(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static final int MAX = 10000;

// Create a boolean array "prime[0..n]"
// and initialize all entries it as true.
// A value in prime[i] will finally be false
// if i is Not a prime, else true.
static boolean prime[] = new boolean [MAX + 1];

static void SieveOfEratosthenes()
{
    int i ;
    for (i = 0; i < MAX + 1; i++)
    {
        prime[i] = true;
    }

    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Set all multiples of p to non-prime
            for (i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the xor of
// 1st N prime numbers
static int xorFirstNPrime(int n)
{
    // Count of prime numbers
    int count = 0, num = 1;

    // XOR of prime numbers
    int xorVal = 0;

    while (count < n)
    {

        // If the number is prime xor it
        if (prime[num])
        {
            xorVal ^= num;

            // Increment the count
            count++;
        }

        // Get to the next number
        num++;
    }
    return xorVal;
}

// Driver code
public static void main (String[] args)
{
    // Create the sieve
    SieveOfEratosthenes();

    int n = 4;

    // Find the xor of 1st n prime numbers
    System.out.println(xorFirstNPrime(n));

}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 10000

# Create a boolean array "prime[0..n]" and
# initialize all entries it as true.
# A value in prime[i] will finally be false +
# if i is Not a prime, else true.
prime = [True for i in range(MAX + 1)]

def SieveOfEratosthenes():

    prime[1] = False

    for p in range(2, MAX + 1):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Set all multiples of p to non-prime
            for i in range(2 * p, MAX + 1, p):
                prime[i] = False

# Function to return the xor of
# 1st N prime numbers
def xorFirstNPrime(n):

    # Count of prime numbers
    count = 0
    num = 1

    # XOR of prime numbers
    xorVal = 0

    while (count < n):

        # If the number is prime xor it
        if (prime[num]):
            xorVal ^= num

            # Increment the count
            count += 1

        # Get to the next number
        num += 1

    return xorVal

# Driver code

# Create the sieve
SieveOfEratosthenes()

n = 4

# Find the xor of 1st n prime numbers
print(xorFirstNPrime(n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int MAX = 10000;

// Create a boolean array "prime[0..n]"
// and initialize all entries it as true.
// A value in prime[i] will finally be false
// if i is Not a prime, else true.
static bool []prime = new bool [MAX + 1];

static void SieveOfEratosthenes()
{
    int i ;
    for (i = 0; i < MAX + 1; i++)
    {
        prime[i] = true;
    }

    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Set all multiples of p to non-prime
            for (i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the xor of
// 1st N prime numbers
static int xorFirstNPrime(int n)
{
    // Count of prime numbers
    int count = 0, num = 1;

    // XOR of prime numbers
    int xorVal = 0;

    while (count < n)
    {

        // If the number is prime xor it
        if (prime[num])
        {
            xorVal ^= num;

            // Increment the count
            count++;
        }

        // Get to the next number
        num++;
    }
    return xorVal;
}

// Driver code
static public void Main ()
{

    // Create the sieve
    SieveOfEratosthenes();
    int n = 4;

    // Find the xor of 1st n prime numbers
    Console.Write(xorFirstNPrime(n));
}
}

// This code is contributed by Sachin
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    let MAX = 10000;

    // Create a boolean array "prime[0..n]" 
    // and initialize all entries it as true. 
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true. 
    let prime = new Array(MAX + 1); 

    function SieveOfEratosthenes() 
    { 
        let i;
        for (i = 0; i < MAX + 1; i++)
        {
            prime[i] = true;
        }

        prime[1] = false; 

        for (let p = 2; p * p <= MAX; p++) 
        { 

            // If prime[p] is not changed, 
            // then it is a prime 
            if (prime[p] == true) 
            { 

                // Set all multiples of p to non-prime 
                for (i = p * 2; i <= MAX; i += p) 
                    prime[i] = false; 
            } 
        } 
    } 

    // Function to return the xor of 
    // 1st N prime numbers 
    function xorFirstNPrime(n) 
    { 
        // Count of prime numbers 
        let count = 0, num = 1; 

        // XOR of prime numbers 
        let xorVal = 0; 

        while (count < n)
        { 

            // If the number is prime xor it 
            if (prime[num]) 
            { 
                xorVal ^= num; 

                // Increment the count 
                count++; 
            } 

            // Get to the next number 
            num++; 
        } 
        return xorVal; 
    }

    // Create the sieve 
    SieveOfEratosthenes(); 
    let n = 4; 

    // Find the xor of 1st n prime numbers 
    document.write(xorFirstNPrime(n)); 

</script>
```

**Output:** 

```
3
```