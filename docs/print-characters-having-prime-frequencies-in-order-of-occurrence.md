# 按出现顺序打印具有质数频率的字符

> 原文:[https://www . geesforgeks . org/print-characters-having-prime-frequency-in-order-of-occurrence/](https://www.geeksforgeeks.org/print-characters-having-prime-frequencies-in-order-of-occurrence/)

给定一个只包含小写字符的字符串**字符串**。任务是按照出现的顺序打印具有主要频率的字符。

**注意**具有主频的重复元素按照其出现的顺序被打印的次数与它们出现的次数一样多。

**示例:**

> **输入:**输出: gksgks
> 
> <figure class="table">
> 
> | 性格；角色；字母 | 频率 |
> | --- | --- |
> | g′ | Two |
> | e′ | four |
> | k′ | Two |
> | s | Two |
> | f′ | one |
> | 的 | one |
> | r′ | one |
> 
> </figure>
> 
> g '，' k '和' s '是仅有的具有质数频率的字符。
> **输入:**飞机
> T4【输出: aeae

**方法:**创建一个频率数组来存储给定字符串**字符串**中每个字符的频率。再次遍历字符串，使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)检查该字符的频率是否为质数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define SIZE 26

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

// Function to print the prime frequency characters
// in the order of their occurrence
void printChar(string str, int n)
{

    bool prime[n + 1];
    memset(prime, true, sizeof(prime));

    // Function to create Sieve to check primes
    SieveOfEratosthenes(prime, str.length() + 1);

    // To store the frequency of each of
    // the character of the string
    int freq[SIZE];

    // Initialize all elements of freq[] to 0
    memset(freq, 0, sizeof(freq));

    // Update the frequency of each character
    for (int i = 0; i < n; i++)
        freq[str[i] - 'a']++;

    // Traverse str character by character
    for (int i = 0; i < n; i++) {

        // If frequency of current character is prime
        if (prime[freq[str[i] - 'a']]) {
            cout << str[i];
        }
    }
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int n = str.length();

    printChar(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int SIZE = 26;

// Function to create Sieve to check primes
static void SieveOfEratosthenes(boolean []prime,
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
                prime[i] = false;
        }
    }
}

// Function to print the prime frequency characters
// in the order of their occurrence
static void printChar(String str, int n)
{
    boolean []prime = new boolean[n + 1];
    for(int i = 0; i < n + 1; i++)
        prime[i] = true;

    // Function to create Sieve to check primes
    SieveOfEratosthenes(prime, str.length() + 1);

    // To store the frequency of each of
    // the character of the string
    int []freq = new int[SIZE];

    // Initialize all elements of freq[] to 0
    for(int i =0; i< SIZE; i++)
        freq[i]=0;

    // Update the frequency of each character
    for (int i = 0; i < n; i++)
        freq[str.charAt(i) - 'a']++;

    // Traverse str character by character
    for (int i = 0; i < n; i++)
    {

        // If frequency of current character is prime
        if (prime[freq[str.charAt(i) - 'a']])
        {
            System.out.print(str.charAt(i));
        }
    }
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    int n = str.length();

    printChar(str, n);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
SIZE = 26

from math import sqrt

# Function to create Sieve to check primes
def SieveOfEratosthenes(prime, p_size):

    # false here indicates
    # that it is not prime
    prime[0] = False
    prime[1] = False

    for p in range(2, int(sqrt(p_size)), 1):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]):

            # Update all multiples of p,
            # set them to non-prime
            for i in range(p * 2, p_size, p):
                prime[i] = False

# Function to print the prime frequency characters
# in the order of their occurrence
def printChar(str, n):
    prime = [True for i in range(n + 1)]

    # Function to create Sieve to check primes
    SieveOfEratosthenes(prime, len(str) + 1)

    # To store the frequency of each of
    # the character of the string
    freq = [0 for i in range(SIZE)]

    # Update the frequency of each character
    for i in range(n):
        freq[ord(str[i]) - ord('a')] += 1

    # Traverse str character by character
    for i in range(n):
        # If frequency of current character is prime
        if (prime[freq[ord(str[i]) - ord('a')]]):
            print(str[i], end = "")

# Driver code
if __name__ == '__main__':
    str = "geeksforgeeks"
    n = len(str)

    printChar(str, n)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int SIZE = 26;

    // Function to create Sieve to check primes
    static void SieveOfEratosthenes(bool[] prime,
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
                for (int i = p * 2;
                         i < p_size; i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to print the prime frequency characters
    // in the order of their occurrence
    static void printChar(string str, int n)
    {
        bool[] prime = new bool[n + 1];
        for (int i = 0; i < n + 1; i++)
            prime[i] = true;

        // Function to create Sieve to check primes
        SieveOfEratosthenes(prime, str.Length + 1);

        // To store the frequency of each of
        // the character of the string
        int[] freq = new int[SIZE];

        // Initialize all elements of freq[] to 0
        for (int i = 0; i < SIZE; i++)
            freq[i] = 0;

        // Update the frequency of each character
        for (int i = 0; i < n; i++)
            freq[str[i] - 'a']++;

        // Traverse str character by character
        for (int i = 0; i < n; i++)
        {

            // If frequency of current character is prime
            if (prime[freq[str[i] - 'a']])
            {
                Console.Write(str[i]);
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "geeksforgeeks";
        int n = str.Length;

        printChar(str, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## java 描述语言

```
<script>
// javaScript implementation of the approach
let SIZE = 26;

// Function to create Sieve to check primes
// Function to create Sieve to check primes
function SieveOfEratosthenes(prime, p_size){
    // False here indicates
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
    return prime;
}

// Function to print the prime frequency characters
// in the order of their occurrence
function printChar(str, n){
    let prime = [];
    for(let i = 0; i<n+1; i++){
        prime.push(true);
    }

    // Function to create Sieve to check primes
    prime = SieveOfEratosthenes(prime, str.length + 1);

    // To store the frequency of each of
    // the character of the string
    let freq = [];
    for(let i = 0; i<26; i++){
        freq.push(0);
    }

    // Update the frequency of each character
    for (let i = 0; i < n; i++)
        freq[str.charCodeAt(i) - 97]++;

    // Traverse str character by character
    for (let i = 0; i < n; i++) {

        // If frequency of current character is prime
        if (prime[freq[str.charCodeAt(i) - 97]]) {
            document.write(str[i]);
        }
    }
}

// Driver code
let str = "geeksforgeeks";
let n = str.length;
printChar(str, n);
</script>
```

**Output**

```
gksgks
```

#### 方法 2:使用内置函数:

**进场:**

我们将扫描字符串，并使用内置的 Counter()函数计算所有字符的出现次数，然后遍历字符串并检查出现次数是否为质数，如果有任何质数频率，则打印它。

注意:该方法适用于所有类型的字符

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to check primes
static boolean prime(int n)
{
    if (n <= 1)
        return false;

    int max_div = (int)Math.floor(Math.sqrt(n));
    for(int i = 2; i < 1 + max_div; i++)
    {
        if (n % i == 0)
            return false;
    }
    return true;
}

static void checkString(String s)
{

    // Counting the frequency of all
    // character using Counter function
    Map<Character, Integer> freq = new HashMap<Character, Integer>();
    for(int i = 0; i < s.length(); i++)
    {
        if (!freq.containsKey(s.charAt(i)))
            freq.put(s.charAt(i),0);

        freq.put(s.charAt(i),freq.get(s.charAt(i))+1);
    }

    // Traversing string
    for(int i = 0; i < s.length(); i++)
    {
        if (prime(freq.get(s.charAt(i))))
            System.out.print(s.charAt(i));
    }
}

// Driver code

    public static void main (String[] args) {
        String s = "geeksforgeeks";

    // Passing string to checkString function
    checkString(s);
    }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python code for the above approach

# importing Counter function
from collections import Counter
import math

# Function to check primes
def prime(n):
    if n <= 1:
        return False
    max_div = math.floor(math.sqrt(n))
    for i in range(2, 1 + max_div):
        if n % i == 0:
            return False
    return True

def checkString(s):

    # Counting the frequency of all
    # character using Counter function
    freq = Counter(s)

    # Traversing string
    for i in range(len(s)):
        if prime(freq[s[i]]):
            print(s[i], end="")

# Driver code
s = "geeksforgeeks"
# passing string to checkString function
checkString(s)

# This code is contributed by vikkycirus
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check primes
static bool prime(int n)
{
    if (n <= 1)
        return false;

    int max_div = (int)Math.Floor(Math.Sqrt(n));
    for(int i = 2; i < 1 + max_div; i++)
    {
        if (n % i == 0)
            return false;
    }
    return true;
}

static void checkString(string s)
{

    // Counting the frequency of all
    // character using Counter function
    Dictionary<char,
               int> freq = new Dictionary<char,
                                          int>();
    for(int i = 0; i < s.Length; i++)
    {
        if (!freq.ContainsKey(s[i]))
            freq[s[i]] = 0;

        freq[s[i]] += 1;
    }

    // Traversing string
    for(int i = 0; i < s.Length; i++)
    {
        if (prime(freq[s[i]]))
            Console.Write(s[i]);
    }
}

// Driver code
public static void Main()
{
    string s = "geeksforgeeks";

    // Passing string to checkString function
    checkString(s);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript code for the above approach

// Function to check primes
function prime(n)
{
    if (n <= 1)
        return false;

    let max_div = Math.floor(Math.sqrt(n));
    for(let i = 2; i < 1 + max_div; i++)
    {
        if (n % i == 0)
            return false;
    }
    return true;
}

function checkString(s)
{

    // Counting the frequency of all
    // character using Counter function
    let freq = new Map();
    for(let i = 0; i < s.length; i++)
    {
        if (!freq.has(s[i]))
            freq.set(s[i], 0);

        freq.set(s[i], freq.get(s[i]) + 1);
    }

    // Traversing string
    for(let i = 0; i < s.length; i++)
    {
        if (prime(freq.get(s[i])))
            document.write(s[i]);
    }
}

// Driver code
let s = "geeksforgeeks";

// Passing string to checkString function
checkString(s);

// This code is contributed by rag2127

</script>
```

**Output**

```
gksgks
```