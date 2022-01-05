# 字符串中字符素频率的和与积

> 原文:[https://www . geeksforgeeks . org/字符串中字符频率的和与积/](https://www.geeksforgeeks.org/sum-and-product-of-prime-frequencies-of-characters-in-a-string/)

给定一个只包含小写英文字母的字符串 **str** ，任务是找出 **str** 中所有字符的素数频率的和与积。
**例:**

> **输入:** str = "geeksforgeeks"
> **输出:** 6，8
> 只有字符' g '，' k '和' s '具有质数频率，即 2 + 2 + 2 = 6 和 2 * 2* 2 = 8
> 
> <figure class="table">
> 
> | 性格；角色；字母 | 频率 |
> | g | Two |
> | e | four |
> | k | Two |
> | s | Two |
> | f | one |
> | o | one |
> | r | one |
> 
> **输入:** str = "算法"
> **输出:** 0，0
> 
> </figure>

**进场:**

*   遍历字符串并将所有字符的频率存储在哈希表中。
*   使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)找出主要频率。
*   计算所有这些主频率的和与积，最后打印和与积。

以下是上述方法的实现:

## C++

```
// C++ program to find Sum and product of Prime
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

// Function to find the sum of prime frequencies
// of the characters of the given string
void sumProdOfPrimeFreq(string s)
{
    bool prime[s.length() + 1];
    memset(prime, true, sizeof(prime));

    SieveOfEratosthenes(prime, s.length() + 1);

    int i, j;

    // map is used to store
    // character frequencies
    unordered_map<char, int> m;
    for (i = 0; i < s.length(); i++)
        m[s[i]]++;

    int sum = 0, product = 1;

    // Traverse the map
    for (auto it = m.begin(); it != m.end(); it++) {

        // If the frequency is prime
        if (prime[it->second]) {
            sum += it->second;
            product *= it->second;
        }
    }

    cout << "Sum = " << sum;
    cout << "\nProduct = " << product;
}

// Driver code
int main()
{
    string s = "geeksforgeeks";

    sumProdOfPrimeFreq(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Sum and product of Prime
// Frequencies of Characters in a String
import java.util.*;

class GFG
{

    // Function to create Sieve to check primes
    static void SieveOfEratosthenes(boolean prime[],
                                        int p_size)
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
                for (int i = p * 2; i < p_size; i += p)
                {
                    prime[i] = false;
                }
            }
        }
    }

    // Function to find the sum of prime frequencies
    // of the characters of the given string
    static void sumProdOfPrimeFreq(char[] s)
    {
        boolean[] prime = new boolean[s.length + 1];
        Arrays.fill(prime, true);

        SieveOfEratosthenes(prime, s.length + 1);

        int i, j;

        // map is used to store
        // character frequencies
        Map<Character, Integer> mp = new HashMap<>();
        for (i = 0; i < s.length; i++)
        {
            mp.put(s[i], mp.get(s[i]) == null ? 1 : mp.get(s[i]) + 1);
        }

        int sum = 0, product = 1;

        // Traverse the map
        for (Map.Entry<Character, Integer> it : mp.entrySet())
        {

            // If the frequency is prime
            if (prime[it.getValue()])
            {
                sum += it.getValue();
                product *= it.getValue();
            }
        }

        System.out.print("Sum = " + sum);
        System.out.println("\nProduct = " + product);
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "geeksforgeeks";

        sumProdOfPrimeFreq(s.toCharArray());
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find Sum and product of Prime
# Frequencies of Characters in a String

# Function to create Sieve to check primes
def SieveofEratosthenes(prime, p_size):

    # false here indicates
    # that it is not prime
    prime[0] = False
    prime[1] = False

    for p in range(2, p_size + 1):

        # If prime[p] is not changed,
        # then it is a prime
        if prime[p]:

            # Update all multiples of p,
            # set them to non-prime
            for i in range(p * 2, p_size + 1, p):
                prime[i] = False

# Function to find the sum of prime frequencies
# of the characters of the given string
def sumProdOfPrimeFreq(s):
    prime = [True] * (len(s) + 2)

    SieveofEratosthenes(prime, len(s) + 1)

    i = 0
    j = 0

    # map is used to store
    # character frequencies
    m = dict()

    for i in range(len(s)):
        m[s[i]] = (m[s[i]] + 1) if s[i] in m else 1

    s = 0
    product = 1

    # Traverse the map
    for it in m:

        # If the frequency is prime
        if prime[m[it]]:
            s += m[it]
            product *= m[it]

    print("Sum =", s)
    print("Product =", product)

# Driver code
if __name__ == "__main__":
    s = "geeksforgeeks"
    sumProdOfPrimeFreq(s)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find Sum and product of Prime
// Frequencies of Characters in a String
using System;
using System.Collections.Generic;

class GFG
{

    // Function to create Sieve to check primes
    static void SieveOfEratosthenes(bool []prime,
                                        int p_size)
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
                for (int i = p * 2; i < p_size; i += p)
                {
                    prime[i] = false;
                }
            }
        }
    }

    // Function to find the sum of prime frequencies
    // of the characters of the given string
    static void sumProdOfPrimeFreq(char[] s)
    {
        int i;
        bool[] prime = new bool[s.Length + 1];
        for(i=0;i<s.Length + 1;i++){
            prime[i]=true;
        }

        SieveOfEratosthenes(prime, s.Length + 1);

        // map is used to store
        // character frequencies
        Dictionary<char, int> mp = new Dictionary<char, int>();
        for (i = 0 ; i < s.Length; i++)
        {
            if(mp.ContainsKey(s[i]))
            {
                var val = mp[s[i]];
                mp.Remove(s[i]);
                mp.Add(s[i], val + 1);
            }
            else
            {
                mp.Add(s[i], 1);
            }
        }

        int sum = 0, product = 1;

        // Traverse the map
        foreach(KeyValuePair<char, int> it in mp)
        {

            // If the frequency is prime
            if (prime[it.Value])
            {
                sum += it.Value;
                product *= it.Value;
            }
        }

        Console.Write("Sum = " + sum);
        Console.WriteLine("\nProduct = " + product);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "geeksforgeeks";

        sumProdOfPrimeFreq(s.ToCharArray());
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program to find Sum and product of Prime
// Frequencies of Characters in a String

// Function to create Sieve to check primes
function SieveOfEratosthenes(prime, p_size) {
    // false here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (let p = 2; p * p <= p_size; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (let i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the sum of prime frequencies
// of the characters of the given string
function sumProdOfPrimeFreq(s) {
    let prime = new Array(s.length + 1);
    prime.fill(true);

    SieveOfEratosthenes(prime, s.length + 1);

    let i, j;

    // map is used to store
    // character frequencies
    let m = new Map();
    for (i = 0; i < s.length; i++)
        m.set(s[i], m.get(s[i]) == null ? 1 : m.get(s[i]) + 1);

    let sum = 0, product = 1;

    // Traverse the map
    for (let it of m) {
        console.log(m)
        // If the frequency is prime
        if (prime[it[1]]) {
            sum += it[1];
            product *= it[1];
        }
    }

    document.write("Sum = " + sum);
    document.write("<br>Product = " + product);
}

// Driver code

let s = "geeksforgeeks";

sumProdOfPrimeFreq(s);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
Sum = 6
Product = 8
```