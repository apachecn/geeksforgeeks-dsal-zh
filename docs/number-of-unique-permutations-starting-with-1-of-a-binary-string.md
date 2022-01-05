# 二进制字符串中以 1 开始的唯一排列数

> 原文:[https://www . geesforgeks . org/唯一排列数-以二进制字符串的 1 开头/](https://www.geeksforgeeks.org/number-of-unique-permutations-starting-with-1-of-a-binary-string/)

给定一个由 0 和 1 组成的二进制字符串，任务是找出以 1 开头的字符串的唯一置换数。
**注**:由于答案可以很大，所以在模 10 <sup>9</sup> + 7 下打印答案。
**例:**

```
Input : str ="10101001001"
Output : 210

Input : str ="101110011"
Output : 56
```

其思想是首先在给定的字符串中找到 1 的计数和 0 的计数。现在让我们考虑一下字符串的长度![L  ](img/edbf47fa8b4436b19e35189733d4ca7e.png "Rendered by QuickLaTeX.com")，字符串至少由一个 1 组成。设 1 的个数为![n  ](img/31d70d7c99878a33c601d487c9b6eb43.png "Rendered by QuickLaTeX.com")，0 的个数为![m  ](img/f6f741a04f72d354961833095c36b79f.png "Rendered by QuickLaTeX.com")。在 1 的 **n** 数中，我们必须在字符串的开头放置一个 1，这样我们就剩下 **n-1** 1 和 **m** 0 了，我们必须排列字符串的这些 **(n-1)** 1 和 **m** 0 的长度(L-1)。
因此，排列数将为:

```
(L-1)! / ((n-1)!*(m)!)
```

以下是上述思路的实现:

## C++

```
// C++ program to find number of unique permutations
// of a binary string starting with 1

#include <bits/stdc++.h>
using namespace std;

#define MAX 1000003
#define mod 1000000007

// Array to store factorial of i at
// i-th index
long long fact[MAX];

// Precompute factorials under modulo mod
// upto MAX
void factorial()
{
    // factorial of 0 is 1
    fact[0] = 1;

    for (int i = 1; i < MAX; i++) {
        fact[i] = (fact[i - 1] * i) % mod;
    }
}

// Iterative Function to calculate (x^y)%p in O(log y)
long long power(long long x, long long y, long long p)
{
    long long res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0) {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function to find the modular inverse
long long inverse(int n)
{

    return power(n, mod - 2, mod);
}

// Function to find the number of permutation
// starting with 1 of a binary string
int countPermutation(string s)
{
    // Generate factorials upto MAX
    factorial();

    int length = s.length(), num1 = 0, num0;
    long long count = 0;

    // find number of 1's
    for (int i = 0; i < length; i++) {
        if (s[i] == '1')
            num1++;
    }

    // number of 0's
    num0 = length - num1;

    // Find the number of permutation of
    // string starting with 1 using the formulae:
    // (L-1)! / ((n-1)!*(m)!)
    count = (fact[length - 1] *
            inverse((fact[num1 - 1] *
                    fact[num0]) % mod)) % mod;

    return count;
}

// Driver code
int main()
{
    string str = "10101001001";

    cout << countPermutation(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of unique permutations
// of a binary string starting with 1

public class Improve {

    final static int MAX = 1000003 ;
    final static int mod = 1000000007 ;

    // Array to store factorial of i at
    // i-th index
    static long fact[] = new long [MAX];

    // Pre-compute factorials under modulo mod
    // upto MAX
    static void factorial()
    {
        // factorial of 0 is 1
        fact[0] = 1;

        for (int i = 1; i < MAX; i++) {
            fact[i] = (fact[i - 1] * i) % mod;
        }
    }

    // Iterative Function to calculate (x^y)%p in O(log y)
    static long power(long x, long y, long p)
    {
        long res = 1; // Initialize result

        x = x % p; // Update x if it is more than or
        // equal to p

        while (y > 0) {
            // If y is odd, multiply x with result
            if (y % 2 != 0)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

    // Function to find the modular inverse
    static long inverse(int n)
    {

        return power(n, mod - 2, mod);
    }

    // Function to find the number of permutation
    // starting with 1 of a binary string
    static int countPermutation(String s)
    {
        // Generate factorials upto MAX
        factorial();

        int length = s.length(), num1 = 0, num0;
        long count = 0;

        // find number of 1's
        for (int i = 0; i < length; i++) {
            if (s.charAt(i) == '1')
                num1++;
        }

        // number of 0's
        num0 = length - num1;

        // Find the number of permutation of
        // string starting with 1 using the formulae:
        // (L-1)! / ((n-1)!*(m)!)
        count = (fact[length - 1] * 
                inverse((int) ((fact[num1 - 1] * 
                        fact[num0]) % mod))) % mod;

        return (int) count;
    }

    // Driver code
    public static void main(String args[])
    {
           String str = "10101001001";

           System.out.println(countPermutation(str));
    }
    // This Code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python 3 program to find number
# of unique permutations of a
# binary string starting with 1
MAX = 1000003
mod = 1000000007

# Array to store factorial of
# i at i-th index
fact = [0] * MAX

# Precompute factorials under
# modulo mod upto MAX
def factorial():

    # factorial of 0 is 1
    fact[0] = 1

    for i in range(1, MAX):
        fact[i] = (fact[i - 1] * i) % mod

# Iterative Function to calculate
# (x^y)%p in O(log y)
def power(x, y, p):

    res = 1 # Initialize result

    x = x % p # Update x if it is
              # more than or equal to p

    while (y > 0) :

        # If y is odd, multiply
        # x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1 # y = y/2
        x = (x * x) % p

    return res

# Function to find the modular inverse
def inverse( n):
    return power(n, mod - 2, mod)

# Function to find the number of
# permutation starting with 1 of
# a binary string
def countPermutation(s):

    # Generate factorials upto MAX
    factorial()

    length = len(s)
    num1 = 0
    count = 0

    # find number of 1's
    for i in range(length) :
        if (s[i] == '1'):
            num1 += 1

    # number of 0's
    num0 = length - num1

    # Find the number of permutation
    # of string starting with 1 using
    # the formulae: (L-1)! / ((n-1)!*(m)!)
    count = (fact[length - 1] *
            inverse((fact[num1 - 1] *
                     fact[num0]) % mod)) % mod

    return count

# Driver code
if __name__ =="__main__":
    s = "10101001001"

    print(countPermutation(s))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find number of
// unique permutations of a
// binary string starting with 1
using System;

class GFG
{
static int MAX = 1000003 ;
static int mod = 1000000007 ;

// Array to store factorial
// of i at i-th index
static long []fact = new long [MAX];

// Pre-compute factorials under
// modulo mod upto MAX
static void factorial()
{
    // factorial of 0 is 1
    fact[0] = 1;

    for (int i = 1; i < MAX; i++)
    {
        fact[i] = (fact[i - 1] * i) % mod;
    }
}

// Iterative Function to calculate
// (x^y)%p in O(log y)
static long power(long x,
                  long y, long p)
{
    long res = 1; // Initialize result

    x = x % p; // Update x if it is more
               // than or equal to p

    while (y > 0)
    {
        // If y is odd, multiply
        // x with result
        if (y % 2 != 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function to find the modular inverse
static long inverse(int n)
{
    return power(n, mod - 2, mod);
}

// Function to find the number of
// permutation starting with 1 of
// a binary string
static int countPermutation(string s)
{
    // Generate factorials upto MAX
    factorial();

    int length = s.Length, num1 = 0, num0;
    long count = 0;

    // find number of 1's
    for (int i = 0; i < length; i++)
    {
        if (s[i] == '1')
            num1++;
    }

    // number of 0's
    num0 = length - num1;

    // Find the number of permutation
    // of string starting with 1 using
    // the formulae: (L-1)! / ((n-1)!*(m)!)
    count = (fact[length - 1] *
             inverse((int) ((fact[num1 - 1] *
                    fact[num0]) % mod))) % mod;

    return (int) count;
}

// Driver code
public static void Main()
{
    string str = "10101001001";

    Console.WriteLine(countPermutation(str));
}
}

// This code is contributed
// by anuj_67
```

## java 描述语言

```
<script>

// Javascript program to find number of unique permutations
// of a binary string starting with 1

var MAX = 1000003
var mod = 100000007

// Array to store factorial of i at
// i-th index
var fact = Array(MAX);

// Precompute factorials under modulo mod
// upto MAX
function factorial()
{
    // factorial of 0 is 1
    fact[0] = 1;

    for (var i = 1; i < MAX; i++) {
        fact[i] = (fact[i - 1] * i) % mod;
    }
}

// Iterative Function to calculate (x^y)%p in O(log y)
function power(x, y, p)
{
    var res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0) {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function to find the modular inverse
function inverse(n)
{

    return power(n, mod - 2, mod);
}

// Function to find the number of permutation
// starting with 1 of a binary string
function countPermutation(s)
{
    // Generate factorials upto MAX
    factorial();

    var length = s.length, num1 = 0, num0;
    var count = 0;

    // find number of 1's
    for (var i = 0; i < length; i++) {
        if (s[i] == '1')
            num1++;
    }

    // number of 0's
    num0 = length - num1;

    // Find the number of permutation of
    // string starting with 1 using the formulae:
    // (L-1)! / ((n-1)!*(m)!)
    count = (fact[length - 1] *
            inverse((fact[num1 - 1] *
                    fact[num0]) % mod)) % mod;

    return count;
}

// Driver code
var str = "10101001001";
document.write( countPermutation(str));

</script>
```

**Output:** 

```
210
```

**时间复杂度:** O(n)，其中 n 为字符串的长度。