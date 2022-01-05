# 字符串中字符素数频率的异或

> 原文:[https://www . geeksforgeeks . org/字符串中字符的素数频率异或/](https://www.geeksforgeeks.org/xor-of-prime-frequencies-of-characters-in-a-string/)

给定一个只包含小写英文字母的字符串。任务是找到字符串中字符的所有素数频率的按位异或。如果没有主要频率，则打印-1。
**例** :

```
Input : str = "gggggeeekkkks"
Output : 6

Input : str = "aabbbbw"
Output : -1
```

**进场:**

*   使用[映射 STL](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 遍历字符串并存储所有字符的频率。
*   使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)找出素数的频率。
*   [计算所有这些质数频率的异或](https://www.geeksforgeeks.org/calculate-xor-1-n/)。

以下是上述方法的实现:

## C++

```
// C++ program to find XOR of Prime
// Frequencies of Characters in a String
#include <bits/stdc++.h>
using namespace std;

// Function to create Sieve to check primes
void SieveOfEratosthenes(bool prime[], int p_size)
{
    // false here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= p_size; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to find XOR of prime frequencies
int xorOfPrime(string s)
{
    bool prime[100005];
    memset(prime, true, sizeof(prime));

    SieveOfEratosthenes(prime, 10005);

    int i, j;

    // map is used to store character
    // frequencies
    map<char, int> m;
    for (i = 0; i < s.length(); i++)
        m[s[i]]++;

    int result = 0;
    int flag = 0;

    // Traverse the map
    for (auto it = m.begin(); it != m.end(); it++) {
        // Calculate XOR of all prime
        // frequencies
        if (prime[it->second]) {
            result ^= it->second;
            flag = 1;
        }
    }

    if (!flag)
        return -1;

    return result;
}

// Driver code
int main()
{
    string s = "gggggeeekkkks";

    cout << xorOfPrime(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find XOR of Prime
// Frequencies of Characters in a String
import java.util.*;

class GFG
{

// Function to create Sieve to check primes
static void SieveOfEratosthenes(boolean prime[], int p_size)
{
    // false here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= p_size; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p])
        {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to find XOR of prime frequencies
static int xorOfPrime(char[] s)
{
    boolean []prime = new boolean[100005];
    for(int i = 0; i < 100005; i++)
        prime[i] = true;

    SieveOfEratosthenes(prime, 10005);

    int i, j;

    // map is used to store character
    // frequencies
    Map<Character,Integer> m = new HashMap<>();
    for (i = 0; i < s.length; i++)
    {
        if(m.containsKey(s[i]))
        {
            m.put(s[i], m.get(s[i])+1);
        }
        else
        {
            m.put(s[i], 1);
        }
    }

    int result = 0;
    int flag = 0;

    // Traverse the map
    for (Map.Entry<Character,Integer> entry : m.entrySet())
    {
        // Calculate XOR of all prime
        // frequencies
        if (prime[entry.getValue()])
        {
            result ^= entry.getValue();
            flag = 1;
        }
    }

    if (flag != 1)
        return -1;

    return result;
}

// Driver code
public static void main(String[] args)
{
    char[] s = "gggggeeekkkks".toCharArray();

    System.out.println(xorOfPrime(s));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find XOR of Prime
# Frequencies of Characters in a String
from collections import defaultdict

# Function to create Sieve to check primes
def SieveOfEratosthenes(prime, p_size):

    # False here indicates
    # that it is not prime
    prime[0] = False
    prime[1] = False
    p = 2

    while p * p <= p_size:

        # If prime[p] is not changed,
        # then it is a prime
        if prime[p]:

            # Update all multiples of p,
            # set them to non-prime
            for i in range(p * 2, p_size + 1, p):
                prime[i] = False

        p += 1

# Function to find XOR of prime frequencies
def xorOfPrime(s):

    prime = [True] * 100005

    SieveOfEratosthenes(prime, 10005)

    # map is used to store character frequencies
    m = defaultdict(lambda:0)
    for i in range(0, len(s)):
        m[s[i]] += 1

    result = flag = 0

    # Traverse the map
    for it in m:

        # Calculate XOR of all prime frequencies
        if prime[m[it]]:
            result ^= m[it]
            flag = 1

    if not flag:
        return -1

    return result

# Driver code
if __name__ == "__main__":

    s = "gggggeeekkkks"

    print(xorOfPrime(s))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find XOR of Prime
// Frequencies of Characters in a String
using System;    
using System.Collections.Generic;

class GFG
{

// Function to create Sieve to check primes
static void SieveOfEratosthenes(Boolean []prime, int p_size)
{
    // false here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= p_size; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p])
        {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to find XOR of prime frequencies
static int xorOfPrime(char[] s)
{
    Boolean []prime = new Boolean[100005];
    for(int i = 0; i < 100005; i++)
        prime[i] = true;

    SieveOfEratosthenes(prime, 10005);

    // map is used to store character
    // frequencies
    Dictionary<char, int> mp = new Dictionary<char,int>();
    for (int i = 0; i < s.Length; i++)
        {
            if (mp.ContainsKey(s[i]))
            {
                var v = mp[s[i]] + 1;
                mp.Remove(s[i]);
                mp.Add(s[i], v);
            }
            else
            {
                mp.Add(s[i], 1);
            }
        }

    int result = 0;
    int flag = 0;

    // Traverse the map
    foreach(KeyValuePair<char, int> entry in mp)
    {
        // Calculate XOR of all prime
        // frequencies
        if (prime[entry.Value])
        {
            result ^= entry.Value;
            flag = 1;
        }
    }

    if (flag != 1)
        return -1;

    return result;
}

// Driver code
public static void Main(String[] args)
{
    char[] s = "gggggeeekkkks".ToCharArray();

    Console.WriteLine(xorOfPrime(s));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find XOR of Prime
// Frequencies of Characters in a String

// Function to create Sieve to check primes
function SieveOfEratosthenes(prime, p_size)
{
    // false here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (var p = 2; p * p <= p_size; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (var i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to find XOR of prime frequencies
function xorOfPrime(s)
{
    var prime = Array(100005).fill(true);

    SieveOfEratosthenes(prime, 10005);

    var i, j;

    // map is used to store character
    // frequencies
    var m = new Map();
    for (i = 0; i < s.length; i++)
    {
        if(m.has(s[i]))
        {
            m.set(s[i], m.get(s[i])+1);
        }
        else
        {
            m.set(s[i],1);
        }
    }

    var result = 0;
    var flag = 0;

    // Traverse the map
    m.forEach((value,key) => {
        // Calculate XOR of all prime
        // frequencies
        if (prime[value]) {
            result ^= value;
            flag = 1;
        }
    });

    if (!flag)
        return -1;

    return result;
}

// Driver code
var s = "gggggeeekkkks";
document.write( xorOfPrime(s));

</script>
```

**Output:** 

```
6
```