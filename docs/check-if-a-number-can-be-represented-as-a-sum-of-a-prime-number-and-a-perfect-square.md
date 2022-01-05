# 检查一个数是否可以表示为一个素数和一个完美平方的和

> 原文:[https://www . geesforgeks . org/check-如果一个数可以表示为一个素数和一个完美平方的和/](https://www.geeksforgeeks.org/check-if-a-number-can-be-represented-as-a-sum-of-a-prime-number-and-a-perfect-square/)

给定一个正整数 **N** ，任务是检查 **N** 是否可以表示为一个[素数](https://www.geeksforgeeks.org/prime-numbers/)和一个[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)的和。如果可以用要求的形式表示 **N** ，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** N = 27
> **输出:**是
> **说明:** 27 可以表示为 2(素数)和 25(完美平方)的和。
> 
> **输入:**N = 64
> T3】输出:否

**天真方法:**解决给定问题最简单的方法是将所有小于或等于 **N** 的[完美方块](https://www.geeksforgeeks.org/find-number-perfect-squares-two-given-numbers/)存储在[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中。对于数组中的每一个[完美正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)，说 **X** ，检查[**(N–X)**是否为素数](https://www.geeksforgeeks.org/prime-numbers/)。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// number is prime or not
bool isPrime(int n)
{
    // Base Cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return true;

    // Check if n is divisible by 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Iterate over every 6 number
    // from the range [5, sqrt(N)]
    for (int i = 5; i * i <= n;
         i = i + 6) {

        // If n is found to be non-prime
        if (n % i == 0
            || n % (i + 2) == 0) {
            return false;
        }
    }

    // Otherwise, return true
    return true;
}

// Function to check if a number can
// be represented as the sum of a prime
// number and a perfect square or not
void sumOfPrimeSquare(int n)
{
    int i = 0;

    // Stores all perfect
    // squares less than N
    vector<int> squares;
    while (i * i < n) {

        // Store the perfect square
        // in the array
        squares.push_back(i * i);
        i++;
    }

    bool flag = false;

    // Iterate over all perfect squares
    for (i = 0; i < squares.size(); i++) {

        // Store the difference of
        // perfect square from n
        int difference = n - squares[i];

        // If difference is prime
        if (isPrime(difference)) {

            // Update flag
            flag = true;

            // Break out of the loop
            break;
        }
    }

    // If N is the sum of a prime
    // number and a perfect square
    if (flag) {
        cout << "Yes";
    }
    else
        cout << "No";
}

// Driver Code
int main()
{
    int N = 27;
    sumOfPrimeSquare(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if a
// number is prime or not
static boolean isPrime(int n)
{

    // Base Cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return true;

    // Check if n is divisible by 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Iterate over every 6 number
    // from the range [5, sqrt(N)]
    for(int i = 5; i * i <= n;
            i = i + 6)
    {

        // If n is found to be non-prime
        if (n % i == 0 || n % (i + 2) == 0)
        {
            return false;
        }
    }

    // Otherwise, return true
    return true;
}

// Function to check if a number can
// be represented as the sum of a prime
// number and a perfect square or not
static void sumOfPrimeSquare(int n)
{
    int i = 0;

    // Stores all perfect
    // squares less than N
    ArrayList<Integer> squares = new ArrayList<Integer>();

    while (i * i < n)
    {

        // Store the perfect square
        // in the array
        squares.add(i * i);
        i++;
    }

    boolean flag = false;

    // Iterate over all perfect squares
    for(i = 0; i < squares.size(); i++)
    {

        // Store the difference of
        // perfect square from n
        int difference = n - squares.get(i);

        // If difference is prime
        if (isPrime(difference))
        {

            // Update flag
            flag = true;

            // Break out of the loop
            break;
        }
    }

    // If N is the sum of a prime
    // number and a perfect square
    if (flag)
    {
        System.out.print("Yes");
    }
    else
        System.out.print("No");
}

// Driver Code
public static void main(String[] args)
{
    int N = 27;

    sumOfPrimeSquare(N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt

# Function to check if a
# number is prime or not
def isPrime(n):

    # Base Cases
    if (n <= 1):
        return False

    if (n <= 3):
        return True

    # Check if n is divisible by 2 or 3
    if (n % 2 == 0 or n % 3 == 0):
        return False

    # Iterate over every 6 number
    # from the range [5, sqrt(N)]
    for i in range(5, int(sqrt(n)) + 1, 6):

        # If n is found to be non-prime
        if (n % i == 0 or n % (i + 2) == 0):
            return False

    # Otherwise, return true
    return True

# Function to check if a number can
# be represented as the sum of a prime
# number and a perfect square or not
def sumOfPrimeSquare(n):

    i = 0

    # Stores all perfect
    # squares less than N
    squares = []

    while (i * i < n):

        # Store the perfect square
        # in the array
        squares.append(i * i)
        i += 1

    flag = False

    # Iterate over all perfect squares
    for i in range(len(squares)):

        # Store the difference of
        # perfect square from n
        difference = n - squares[i]

        # If difference is prime
        if (isPrime(difference)):

            # Update flag
            flag = True

            # Break out of the loop
            break

    # If N is the sum of a prime
    # number and a perfect square
    if (flag):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    N = 27

    sumOfPrimeSquare(N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;

class GFG{

// Function to check if a
// number is prime or not
static bool isPrime(int n)
{

    // Base Cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return true;

    // Check if n is divisible by 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Iterate over every 6 number
    // from the range [5, sqrt(N)]
    for (int i = 5; i * i <= n;
         i = i + 6) {

        // If n is found to be non-prime
        if (n % i == 0
            || n % (i + 2) == 0) {
            return false;
        }
    }

    // Otherwise, return true
    return true;
}

// Function to check if a number can
// be represented as the sum of a prime
// number and a perfect square or not
static void sumOfPrimeSquare(int n)
{
    int i = 0;

    // Stores all perfect
    // squares less than N
    List<int> squares = new List<int>();
    while (i * i < n) {

        // Store the perfect square
        // in the array
        squares.Add(i * i);
        i++;
    }

    bool flag = false;

    // Iterate over all perfect squares
    for (i = 0; i < squares.Count; i++) {

        // Store the difference of
        // perfect square from n
        int difference = n - squares[i];

        // If difference is prime
        if (isPrime(difference)) {

            // Update flag
            flag = true;

            // Break out of the loop
            break;
        }
    }

    // If N is the sum of a prime
    // number and a perfect square
    if (flag) {
        Console.Write("Yes");
    }
    else
       Console.Write("No");
}

// Driver Code
public static void Main()
{
    int N = 27;
    sumOfPrimeSquare(N);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if a
// number is prime or not
function isPrime(n)
{

    // Base Cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return true;

    // Check if n is divisible by 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Iterate over every 6 number
    // from the range [5, sqrt(N)]
    for(let i = 5; i * i <= n;
            i = i + 6)
    {

        // If n is found to be non-prime
        if (n % i == 0 || n % (i + 2) == 0)
        {
            return false;
        }
    }

    // Otherwise, return true
    return true;
}

// Function to check if a number can
// be represented as the sum of a prime
// number and a perfect square or not
function sumOfPrimeSquare(n)
{
    let i = 0;

    // Stores all perfect
    // squares less than N
    let squares = [];

    while (i * i < n)
    {

        // Store the perfect square
        // in the array
        squares.push(i * i);
        i++;
    }

    let flag = false;

    // Iterate over all perfect squares
    for(i = 0; i < squares.length; i++)
    {

        // Store the difference of
        // perfect square from n
        let difference = n - squares[i];

        // If difference is prime
        if (isPrime(difference))
        {

            // Update flag
            flag = true;

            // Break out of the loop
            break;
        }
    }

    // If N is the sum of a prime
    // number and a perfect square
    if (flag)
    {
        document.write("Yes");
    }
    else
        document.write("No");
}

// Driver Code
let N = 27;

sumOfPrimeSquare(N);

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N)*
***辅助空间:** O(√N)*

**高效方法:**上述方法可以通过使用厄拉多塞的[筛将所有小于**N**T5】的素数存储在](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中来优化。如果有[质数](https://www.geeksforgeeks.org/prime-numbers/)，说 **X** ，[检查**(N–X)**是否为正方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to store all prime
// numbers less than or equal to N
void SieveOfEratosthenes(bool prime[],
                         int n)
{
    // Update prime[0] and
    // prime[1] as false
    prime[0] = false;
    prime[1] = false;

    // Iterate over the range [2, sqrt(N)]
    for (int p = 2; p * p <= n; p++) {

        // If p is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            // which are <= n as non-prime
            for (int i = p * p; i <= n;
                 i += p) {

                prime[i] = false;
            }
        }
    }
}

// Function to check whether a number
// can be represented as the sum of a
// prime number and a perfect square
void sumOfPrimeSquare(int n)
{
    bool flag = false;

    // Stores all the prime numbers
    // less than or equal to n
    bool prime[n + 1];
    memset(prime, true, sizeof(prime));

    // Update the array prime[]
    SieveOfEratosthenes(prime, n);

    // Iterate over the range [0, n]
    for (int i = 0; i <= n; i++) {

        // If current number
        // is non-prime
        if (!prime[i])
            continue;

        // Update difference
        int dif = n - i;

        // If difference is a
        // perfect square
        if (ceil((double)sqrt(dif))
            == floor((double)sqrt(dif))) {

            // If true, update flag
            // and break out of loop
            flag = true;
            break;
        }
    }

    // If N can be expressed as sum
    // of prime number and perfect square
    if (flag) {
        cout << "Yes";
    }
    else
        cout << "No";
}

// Driver Code
int main()
{
    int N = 27;
    sumOfPrimeSquare(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to store all prime
// numbers less than or equal to N
static void SieveOfEratosthenes(boolean prime[],
                                int n)
{

    // Update prime[0] and
    // prime[1] as false
    prime[0] = false;
    prime[1] = false;

    // Iterate over the range [2, Math.sqrt(N)]
    for(int p = 2; p * p <= n; p++)
    {

        // If p is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            // which are <= n as non-prime
            for(int i = p * p; i <= n; i += p)
            {
                prime[i] = false;
            }
        }
    }
}

// Function to check whether a number
// can be represented as the sum of a
// prime number and a perfect square
static void sumOfPrimeSquare(int n)
{
    boolean flag = false;

    // Stores all the prime numbers
    // less than or equal to n
    boolean []prime = new boolean[n + 1];
    for(int i = 0; i < prime.length; i++)
        prime[i] = true;

    // Update the array prime[]
    SieveOfEratosthenes(prime, n);

    // Iterate over the range [0, n]
    for(int i = 0; i <= n; i++)
    {

        // If current number
        // is non-prime
        if (!prime[i])
            continue;

        // Update difference
        int dif = n - i;

        // If difference is a
        // perfect square
        if (Math.ceil((double)Math.sqrt(dif)) ==
           Math.floor((double)Math.sqrt(dif)))
        {

            // If true, update flag
            // and break out of loop
            flag = true;
            break;
        }
    }

    // If N can be expressed as sum
    // of prime number and perfect square
    if (flag)
    {
        System.out.print("Yes");
    }
    else
        System.out.print("No");
}

// Driver Code
public static void main(String[] args)
{
    int N = 27;
    sumOfPrimeSquare(N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to store all prime
# numbers less than or equal to N
def SieveOfEratosthenes(prime, n):

    # Update prime[0] and
    # prime[1] as false
    prime[0] = False
    prime[1] = False

    # Iterate over the range [2, sqrt(N)]
    for p in range(2, int(n ** (1 / 2))):

        # If p is a prime
        if (prime[p] == True):

            # Update all multiples of p
            # which are <= n as non-prime
            for i in range(p ** 2, n + 1, p):
                prime[i] = False

# Function to check whether a number
# can be represented as the sum of a
# prime number and a perfect square
def sumOfPrimeSquare(n):

    flag = False

    # Stores all the prime numbers
    # less than or equal to n
    prime = [True] * (n + 1)

    # Update the array prime[]
    SieveOfEratosthenes(prime, n)

    # Iterate over the range [0, n]
    for i in range(n + 1):

        # If current number
        # is non-prime
        if (not prime[i]):
            continue

        # Update difference
        dif = n - i

        # If difference is a
        # perfect square
        if (math.ceil(dif ** (1 / 2)) ==
           math.floor(dif ** (1 / 2))):

            # If true, update flag
            # and break out of loop
            flag = True
            break

    # If N can be expressed as sum
    # of prime number and perfect square
    if (flag):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == "__main__":

    N = 27

    sumOfPrimeSquare(N)

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to store all prime
// numbers less than or equal to N
static void SieveOfEratosthenes(bool[] prime, int n)
{

    // Update prime[0] and
    // prime[1] as false
    prime[0] = false;
    prime[1] = false;

    // Iterate over the range [2, sqrt(N)]
    for(int p = 2; p * p <= n; p++)
    {

        // If p is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            // which are <= n as non-prime
            for(int i = p * p; i <= n; i += p)
            {
                prime[i] = false;
            }
        }
    }
}

// Function to check whether a number
// can be represented as the sum of a
// prime number and a perfect square
static void sumOfPrimeSquare(int n)
{
    bool flag = false;

    // Stores all the prime numbers
    // less than or equal to n
    bool[] prime = new bool[n + 1];
    Array.Fill(prime, true);

    // Update the array prime[]
    SieveOfEratosthenes(prime, n);

    // Iterate over the range [0, n]
    for(int i = 0; i <= n; i++)
    {

        // If current number
        // is non-prime
        if (!prime[i])
            continue;

        // Update difference
        int dif = n - i;

        // If difference is a
        // perfect square
        if (Math.Ceiling((double)Math.Sqrt(dif)) ==
            Math.Floor((double)Math.Sqrt(dif)))
        {

            // If true, update flag
            // and break out of loop
            flag = true;
            break;
        }
    }

    // If N can be expressed as sum
    // of prime number and perfect square
    if (flag)
    {
        Console.WriteLine("Yes");
    }
    else
        Console.WriteLine("No");
}

// Driver Code
public static void Main()
{
    int N = 27;

    sumOfPrimeSquare(N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to store all prime
// numbers less than or equal to N
function SieveOfEratosthenes(prime, n)
{

    // Update prime[0] and
    // prime[1] as false
    prime[0] = false;
    prime[1] = false;

    // Iterate over the range [2, sqrt(N)]
    for(let p = 2; p * p <= n; p++)
    {

        // If p is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            // which are <= n as non-prime
            for(let i = p * p; i <= n; i += p)
            {
                prime[i] = false;
            }
        }
    }
}

// Function to check whether a number
// can be represented as the sum of a
// prime number and a perfect square
function sumOfPrimeSquare(n)
{
    let flag = false;

    // Stores all the prime numbers
    // less than or equal to n
    let prime = new Array(n + 1).fill(true);

    // Update the array prime[]
    SieveOfEratosthenes(prime, n);

    // Iterate over the range [0, n]
    for(let i = 0; i <= n; i++)
    {

        // If current number
        // is non-prime
        if (!prime[i])
            continue;

        // Update difference
        let dif = n - i;

        // If difference is a
        // perfect square
        if (Math.ceil(Math.sqrt(dif)) ==
           Math.floor(Math.sqrt(dif)))
        {

            // If true, update flag
            // and break out of loop
            flag = true;
            break;
        }
    }

    // If N can be expressed as sum
    // of prime number and perfect square
    if (flag)
    {
        document.write("Yes");
    }
    else
        document.write("No");
}

// Driver Cod
let N = 27;

sumOfPrimeSquare(N);

// This code is contributed by subhammahato348

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N * log(log(N))*
***辅助空间:** O(N)*