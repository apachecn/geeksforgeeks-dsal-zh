# 计算 ASCII 值为质数的字符串中的字符数

> 原文:[https://www . geesforgeks . org/count-字符串中的字符-其 ascii 值为-prime/](https://www.geeksforgeeks.org/count-characters-in-a-string-whose-ascii-values-are-prime/)

给定一根绳子 **S** 。任务是计算并打印 ASCII 值为质数的字符串中的字符数。

**示例:**

> **输入:** S = "geeksforgeeks"
> **输出:**3
> “g”、“e”和“k”是 ASCII 值为质数的唯一字符，即分别为 103、101 和 107。
> 
> **输入:**S = " abcdefghijklmnopqrstuvwxyz "
> T3】输出: 6

**方法:**思路是使用厄拉多塞的[筛生成字符串 S 字符最大 ASCII 值以内的所有素数。现在，迭代字符串并获取每个字符的 ASCII 值。如果 ASCII 值是质数，则增加**计数**。最后，打印**计数**。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;
#define max_val 257

// Function to find prime characters in the string
int PrimeCharacters(string s)
{

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a Boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    vector<bool> prime(max_val + 1, true);

    // 0 and 1 are not primes
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    int count = 0;

    // Traverse all the characters
    for (int i = 0; i < s.length(); ++i) {
        if (prime[int(s[i])])
            count++;
    }

    return count;
}

// Driver program
int main()
{
    string S = "geeksforgeeks";

    // print required answer
    cout << PrimeCharacters(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class Solution
{
static final int max_val=257;

// Function to find prime characters in the String
static int PrimeCharacters(String s)
{

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a Boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    boolean prime[]= new boolean[max_val+1];

    //initialize the value
    for(int i=0;i<=max_val;i++)
    prime[i]=true;

    // 0 and 1 are not primes
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    int count = 0;

    // Traverse all the characters
    for (int i = 0; i < s.length(); ++i) {
        if (prime[(int)(s.charAt(i))])
            count++;
    }

    return count;
}

// Driver program
public static void main(String args[])
{
    String S = "geeksforgeeks";

    // print required answer
    System.out.print( PrimeCharacters(S));

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of above approach

from math import sqrt

max_val = 257

# Function to find prime characters in the string
def PrimeCharacters(s) :

    # USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    # THAN OR EQUAL TO max_val
    # Create a Boolean array "prime[0..n]". A
    # value in prime[i] will finally be false
    # if i is Not a prime, else true.
    prime = [True] * (max_val + 1)

    # 0 and 1 are not primes
    prime[0] = False
    prime[1] = False
    for p in range(2, int(sqrt(max_val)) + 1) :

        # If prime[p] is not changed, then
        # it is a prime
        if (prime[p] == True) :

            # Update all multiples of p
            for i in range(2*p ,max_val + 1, p) :
                prime[i] = False

    count = 0

    # Traverse all the characters
    for i in range(len(s)) :
        if (prime[ord(s[i])]) :
            count += 1

    return count

# Driver program
if __name__ == "__main__" :

    S = "geeksforgeeks";

    # print required answer
    print(PrimeCharacters(S))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of above approach
using System;
class GFG{

static readonly int max_val = 257;

// Function to find prime characters in the String
static int PrimeCharacters(String s)
{
    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a Boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    bool []prime = new bool[max_val + 1];

    //initialize the value
    for(int i = 0; i <= max_val; i++)
    prime[i] = true;

    // 0 and 1 are not primes
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p <= max_val; p++)
    {
        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
            prime[i] = false;

        }

    }

    int count = 0;

    // Traverse all the characters
    for (int i = 0; i < s.Length; ++i)
    {
        if (prime[(int)(s[i])])
        count++;

    }
    return count;

}

// Driver Code
public static void Main()
{
    String S = "geeksforgeeks";

    // print required answer
    Console.Write( PrimeCharacters(S));

}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
      // JavaScript implementation of above approach
      const max_val = 257;

      // Function to find prime characters in the String
      function PrimeCharacters(s) {
        // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
        // THAN OR EQUAL TO max_val
        // Create a Boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        var prime = new Array(max_val + 1);

        //initialize the value
        for (var i = 0; i <= max_val; i++) prime[i] = true;

        // 0 and 1 are not primes
        prime[0] = false;
        prime[1] = false;
        for (var p = 2; p * p <= max_val; p++) {
          // If prime[p] is not changed, then
          // it is a prime
          if (prime[p] === true) {
            // Update all multiples of p
            for (var i = p * 2; i <= max_val; i += p) prime[i] = false;
          }
        }

        var count = 0;

        // Traverse all the characters
        for (var i = 0; i < s.length; ++i) {
          if (prime[s[i].charCodeAt(0)]) count++;
        }
        return count;
      }

      // Driver Code
      var S = "geeksforgeeks";

      // print required answer
      document.write(PrimeCharacters(S));

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
8
```