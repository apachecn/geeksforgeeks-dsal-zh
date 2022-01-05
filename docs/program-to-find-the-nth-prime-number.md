# 寻找第 n 个素数的程序

> 原文:[https://www . geesforgeks . org/program-to-find-the-n-prime-number/](https://www.geeksforgeeks.org/program-to-find-the-nth-prime-number/)

给定一个整数 **N** 。任务是找到第 n 个 T2 素数。

**示例:**

> **输入:**5
> T3】输出: 11
> 
> **输入:**16
> T3】输出: 53
> 
> **输入:**1049
> T3】输出: 8377

**进场:**

*   使用厄拉多塞的[筛找出最大大小的质数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   将所有素数存储在一个向量中。
*   对于给定的数字 N，返回向量中第(N-1)个索引处的元素。

下面是上述方法的实现:

## C++

```
// C++ program to the nth prime number

#include <bits/stdc++.h>
using namespace std;

// initializing the max value
#define MAX_SIZE 1000005

// Function to generate N prime numbers using
// Sieve of Eratosthenes
void SieveOfEratosthenes(vector<int>& primes)
{
    // Create a boolean array "IsPrime[0..MAX_SIZE]" and
    // initialize all entries it as true. A value in
    // IsPrime[i] will finally be false if i is
    // Not a IsPrime, else true.
    bool IsPrime[MAX_SIZE];
    memset(IsPrime, true, sizeof(IsPrime));

    for (int p = 2; p * p < MAX_SIZE; p++) {
        // If IsPrime[p] is not changed, then it is a prime
        if (IsPrime[p] == true) {
            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < MAX_SIZE; i += p)
                IsPrime[i] = false;
        }
    }

    // Store all prime numbers
    for (int p = 2; p < MAX_SIZE; p++)
        if (IsPrime[p])
            primes.push_back(p);
}

// Driver Code
int main()
{
    // To store all prime numbers
    vector<int> primes;

    // Function call
    SieveOfEratosthenes(primes);

    cout << "5th prime number is " << primes[4] << endl;
    cout << "16th prime number is " << primes[15] << endl;
    cout << "1049th prime number is " << primes[1048];

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to the nth prime number 
import java.util.ArrayList;
class GFG
{

    // initializing the max value
    static int MAX_SIZE = 1000005;

    // To store all prime numbers
    static ArrayList<Integer> primes =
       new ArrayList<Integer>();

    // Function to generate N prime numbers
    // using Sieve of Eratosthenes
    static void SieveOfEratosthenes()
    {
        // Create a boolean array "IsPrime[0..MAX_SIZE]"
        // and initialize all entries it as true.
        // A value in IsPrime[i] will finally be false
        // if i is Not a IsPrime, else true.
        boolean [] IsPrime = new boolean[MAX_SIZE];

        for(int i = 0; i < MAX_SIZE; i++)
            IsPrime[i] = true;

        for (int p = 2; p * p < MAX_SIZE; p++)
        {
            // If IsPrime[p] is not changed,
            // then it is a prime
            if (IsPrime[p] == true)
            {
                // Update all multiples of p greater than or
                // equal to the square of it
                // numbers which are multiple of p and are
                // less than p^2 are already been marked.
                for (int i = p * p; i < MAX_SIZE; i += p)
                    IsPrime[i] = false;
            }
        }

        // Store all prime numbers
        for (int p = 2; p < MAX_SIZE; p++)
        if (IsPrime[p] == true)
                primes.add(p);
    }

    // Driver Code
    public static void main (String[] args)
    {

        // Function call
        SieveOfEratosthenes();

        System.out.println("5th prime number is " +
                                    primes.get(4));
        System.out.println("16th prime number is " +
                                    primes.get(15));
        System.out.println("1049th prime number is " +
                                    primes.get(1048));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 program to the nth prime number 
primes = []

# Function to generate N prime numbers using 
# Sieve of Eratosthenes
def SieveOfEratosthenes():

    n = 1000005

    # Create a boolean array "prime[0..n]" and
    # initialize all entries it as true. A value
    # in prime[i] will finally be false if i is
    # Not a prime, else true.
    prime = [True for i in range(n + 1)]

    p = 2
    while (p * p <= n):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * p, n + 1, p):
                prime[i] = False

        p += 1

    # Print all prime numbers
    for p in range(2, n + 1):
        if prime[p]:
            primes.append(p)

# Driver code
if __name__=='__main__':

    # Function call
    SieveOfEratosthenes()

    print("5th prime number is", primes[4]);
    print("16th prime number is", primes[15]);
    print("1049th prime number is", primes[1048]);

# This code is contributed by grand_master
```

## C#

```
// C# program to the nth prime number
using System;
using System.Collections;

class GFG
{

// initializing the max value
static int MAX_SIZE = 1000005;

// To store all prime numbers
static ArrayList primes = new ArrayList();

// Function to generate N prime numbers using
// Sieve of Eratosthenes
static void SieveOfEratosthenes()
{
    // Create a boolean array "IsPrime[0..MAX_SIZE]"
    // and initialize all entries it as true.
    // A value in IsPrime[i] will finally be false
    // if i is Not a IsPrime, else true.
    bool [] IsPrime = new bool[MAX_SIZE];

    for(int i = 0; i < MAX_SIZE; i++)
        IsPrime[i] = true;

    for (int p = 2; p * p < MAX_SIZE; p++)
    {
        // If IsPrime[p] is not changed,
        // then it is a prime
        if (IsPrime[p] == true)
        {
            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < MAX_SIZE; i += p)
                IsPrime[i] = false;
        }
    }

    // Store all prime numbers
    for (int p = 2; p < MAX_SIZE; p++)
    if (IsPrime[p] == true)
            primes.Add(p);
}

// Driver Code
public static void Main ()
{

    // Function call
    SieveOfEratosthenes();

    Console.WriteLine("5th prime number is " +
                                   primes[4]);
    Console.WriteLine("16th prime number is " +
                                   primes[15]);
    Console.WriteLine("1049th prime number is " +
                                   primes[1048]);
}
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// Javascript program to the nth prime number

// initializing the max value
var MAX_SIZE = 1000005;

// Function to generate N prime numbers using
// Sieve of Eratosthenes
function SieveOfEratosthenes(primes)
{
    // Create a boolean array
    // "IsPrime[0..MAX_SIZE]" and
    // initialize all entries it as true.
    // A value in
    // IsPrime[i] will finally be false if i is
    // Not a IsPrime, else true.
    var IsPrime = Array(MAX_SIZE).fill(true);

    var p,i;
    for (p = 2; p * p < MAX_SIZE;p++)
    {
        // If IsPrime[p] is not changed,
        // then it is a prime
        if (IsPrime[p] == true)
        {
            // Update all multiples of p
            // greater than or
            // equal to the square of it
            // numbers which are multiple
            // of p and are
            // less than p^2 are already
            // been marked.
            for(i = p * p; i < MAX_SIZE; i += p)
                IsPrime[i] = false;
        }
    }

    // Store all prime numbers
    for (p = 2; p < MAX_SIZE; p++)
        if (IsPrime[p])
            primes.push(p);
}

// Driver Code
    // To store all prime numbers
    var primes = [];

    // Function call
    SieveOfEratosthenes(primes);

    document.write(
    "5th prime number is "+primes[4]+"<br>"
    );
    document.write(
    "16th prime number is "+primes[15]+"<br>"
    );
    document.write(
    "1049th prime number is "+primes[1048]+"<br>"
    );

</script>
```

**Output:** 

```
5th prime number is 11
16th prime number is 53
1049th prime number is 8377
```