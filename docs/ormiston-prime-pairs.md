# 奥米斯顿素数对

> 原文:[https://www.geeksforgeeks.org/ormiston-prime-pairs/](https://www.geeksforgeeks.org/ormiston-prime-pairs/)

给定两个整数 **N1** 和 **N2** ，任务是检查这两对是否都是素数。

> 奥米斯顿质数是那些质数，并且具有不同顺序的相同数字。
> 前几个奥米斯顿素数对是:
> (1913，1931)，(18379，18397)，(19013，19031)，(25013，25031)……等。

**示例:**

> **输入:** N1 = 1913，N2 = 1931
> T3】输出:是
> 
> **输入:** n1 = 5，N2 = 7
> T3】输出:否

**接近**:检查 N1 和 N2 是否都是[素数](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)和[字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)。如果数是质数和字谜，那么数就是奥米斯顿质数对。

下面是上述方法的实现:

## C++

```
// C++ implementation to
// check Ormiston prime

#include <iostream>
using namespace std;

// Function to check if the
// number is a prime or not
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

const int TEN = 10;

// Function to update the frequency array
// such that freq[i] stores the
// frequency of digit i in n
void updateFreq(int n, int freq[])
{

    // While there are digits
    // left to process
    while (n) {
        int digit = n % TEN;

        // Update the frequency of
        // the current digit
        freq[digit]++;

        // Remove the last digit
        n /= TEN;
    }
}

// Function that returns true if a and b
// are anagrams of each other
bool areAnagrams(int a, int b)
{

    // To store the frequencies of
    // the digits in a and b
    int freqA[TEN] = { 0 };
    int freqB[TEN] = { 0 };

    // Update the frequency of
    // the digits in a
    updateFreq(a, freqA);

    // Update the frequency of
    // the digits in b
    updateFreq(b, freqB);

    // Match the frequencies of
    // the common digits
    for (int i = 0; i < TEN; i++) {

        // If frequency differs for any digit
        // then the numbers are not
        // anagrams of each other
        if (freqA[i] != freqB[i])
            return false;
    }

    return true;
}

// Returns true if n1 and
// n2 are Ormiston primes
bool OrmistonPrime(int n1, int n2)
{
    return (isPrime(n1) && isPrime(n2) &&
                 areAnagrams(n1, n2));
}

// Driver code
int main()
{
    int n1 = 1913, n2 = 1931;
    if (OrmistonPrime(n1, n2))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// check Ormiston prime
import java.util.*;
class GFG{

// Function to check if the
// number is a prime or not
static boolean isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 ||
            n % (i + 2) == 0)
            return false;

    return true;
}

static int TEN = 10;

// Function to update the frequency array
// such that freq[i] stores the
// frequency of digit i in n
static void updateFreq(int n, int freq[])
{

    // While there are digits
    // left to process
    while (n > 0)
    {
        int digit = n % TEN;

        // Update the frequency of
        // the current digit
        freq[digit]++;

        // Remove the last digit
        n /= TEN;
    }
}

// Function that returns true if a and b
// are anagrams of each other
static boolean areAnagrams(int a, int b)
{

    // To store the frequencies of
    // the digits in a and b
    int freqA[] = new int[TEN];
    int freqB[] = new int[TEN];

    // Update the frequency of
    // the digits in a
    updateFreq(a, freqA);

    // Update the frequency of
    // the digits in b
    updateFreq(b, freqB);

    // Match the frequencies of
    // the common digits
    for (int i = 0; i < TEN; i++)
    {

        // If frequency differs for any digit
        // then the numbers are not
        // anagrams of each other
        if (freqA[i] != freqB[i])
            return false;
    }
    return true;
}

// Returns true if n1 and
// n2 are Ormiston primes
static boolean OrmistonPrime(int n1, int n2)
{
    return (isPrime(n1) && isPrime(n2) &&
                   areAnagrams(n1, n2));
}

// Driver code
public static void main(String[] args)
{
    int n1 = 1913, n2 = 1931;
    if (OrmistonPrime(n1, n2))
        System.out.print("YES" +"\n");
    else
        System.out.print("NO" +"\n");
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to
# check Ormiston prime

# Function to check if the
# number is a prime or not
def isPrime(n):

    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False

    i = 5
    while(i * i <= n):
        if (n % i == 0 or n % (i + 2) == 0):
            return False

        i = i + 6

    return True

TEN = 10

# Function to update the frequency array
# such that freq[i] stores the
# frequency of digit i in n
def updateFreq(n, freq):

    # While there are digits
    # left to process
    while (n):
        digit = n % TEN

        # Update the frequency of
        # the current digit
        freq[digit] += 1

        # Remove the last digit
        n = n // TEN

# Function that returns true if a and b
# are anagrams of each other
def areAnagrams(a, b):

    # To store the frequencies of
    # the digits in a and b
    freqA = [0] * TEN
    freqB = [0] * TEN 

    # Update the frequency of
    # the digits in a
    updateFreq(a, freqA)

    # Update the frequency of
    # the digits in b
    updateFreq(b, freqB)

    # Match the frequencies of
    # the common digits
    for i in range(TEN):

        # If frequency differs for any digit
        # then the numbers are not
        # anagrams of each other
        if (freqA[i] != freqB[i]):
            return False

    return True

# Returns true if n1 and
# n2 are Ormiston primes
def OrmistonPrime(n1, n2):

    return (isPrime(n1) and
            isPrime(n2) and
            areAnagrams(n1, n2))

# Driver code
n1, n2 = 1913, 1931

if (OrmistonPrime(n1, n2)):
    print("YES")
else:
    print("NO")

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation to
// check Ormiston prime
using System;

class GFG{

// Function to check if the
// number is a prime or not
static bool isPrime(int n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(int i = 5; i * i <= n; i = i + 6)
       if (n % i == 0 || n % (i + 2) == 0)
           return false;

    return true;
}

static int TEN = 10;

// Function to update the frequency array
// such that freq[i] stores the
// frequency of digit i in n
static void updateFreq(int n, int []freq)
{

    // While there are digits
    // left to process
    while (n > 0)
    {
        int digit = n % TEN;

        // Update the frequency of
        // the current digit
        freq[digit]++;

        // Remove the last digit
        n /= TEN;
    }
}

// Function that returns true if a and b
// are anagrams of each other
static bool areAnagrams(int a, int b)
{

    // To store the frequencies of
    // the digits in a and b
    int []freqA = new int[TEN];
    int []freqB = new int[TEN];

    // Update the frequency of
    // the digits in a
    updateFreq(a, freqA);

    // Update the frequency of
    // the digits in b
    updateFreq(b, freqB);

    // Match the frequencies of
    // the common digits
    for(int i = 0; i < TEN; i++)
    {

       // If frequency differs for any
       // digit then the numbers are not
       // anagrams of each other
       if (freqA[i] != freqB[i])
           return false;
    }
    return true;
}

// Returns true if n1 and
// n2 are Ormiston primes
static bool OrmistonPrime(int n1, int n2)
{
    return (isPrime(n1) && isPrime(n2) &&
                   areAnagrams(n1, n2));
}

// Driver code
public static void Main(String[] args)
{
    int n1 = 1913, n2 = 1931;

    if (OrmistonPrime(n1, n2))
        Console.Write("YES" + "\n");
    else
        Console.Write("NO" + "\n");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation to
// check Ormiston prime

    // Function to check if the
    // number is a prime or not
    function isPrime( n) {
        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (let i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    const TEN = 10;

    // Function to update the frequency array
    // such that freq[i] stores the
    // frequency of digit i in n
    function updateFreq( n, freq)
    {

        // While there are digits
        // left to process
        while (n > 0) {
            let digit = n % TEN;

            // Update the frequency of
            // the current digit
            freq[digit]++;

            // Remove the last digit
            n = parseInt(n/TEN);
        }
    }

    // Function that returns true if a and b
    // are anagrams of each other
    function areAnagrams( a ,b) {

        // To store the frequencies of
        // the digits in a and b
        let freqA = Array(TEN).fill(0);
        let freqB = Array(TEN).fill(0);

        // Update the frequency of
        // the digits in a
        updateFreq(a, freqA);

        // Update the frequency of
        // the digits in b
        updateFreq(b, freqB);

        // Match the frequencies of
        // the common digits
        for ( i = 0; i < TEN; i++) {

            // If frequency differs for any digit
            // then the numbers are not
            // anagrams of each other
            if (freqA[i] != freqB[i])
                return false;
        }
        return true;
    }

    // Returns true if n1 and
    // n2 are Ormiston primes
    function OrmistonPrime( n1, n2)
    {
        return (isPrime(n1) && isPrime(n2) && areAnagrams(n1, n2));
    }

    // Driver code
    let n1 = 1913, n2 = 1931;
    if (OrmistonPrime(n1, n2))
        document.write("YES" + "\n");
    else
        document.write("NO" + "\n");

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(N)

**参考:**T2】OEIST4】