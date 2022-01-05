# 从给定的频率为质数的字符串中删除字符

> 原文:[https://www . geesforgeks . org/remove-characters-from-给定字符串-其频率为质数/](https://www.geeksforgeeks.org/remove-characters-from-given-string-whose-frequencies-are-a-prime-number/)

给定长度为 **N** 的字符串 **str** ，任务是从频率为质数的字符串中移除所有字符。

**示例:**

> **输入:**str = " geeks forgeeks "
> T3】输出: eeforee
> **解释:**
> 字符的频率为:{ g=2，e=4，k=2，s=2，f=1，o=1，r=1}
> 所以，g，k 和 s 是素数频率的字符，所以从字符串中删除。
> 结果字符串为“eeforee”
> 
> **输入:** str = "abcdef"
> **输出:** abcdef
> **解释:**
> 由于所有字符都是唯一的，频率为 1，因此没有字符被删除。

**天真法:**解决这个问题最简单的方法是找出字符串中每个不同字符 的[**频率，对于每个字符，检查其频率是否为**](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/) **[**质数**](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/) 。如果发现频率是质数，跳过那个字符。否则，将其追加到新形成的字符串中。**

***时间复杂度:**O(N<sup>3/2</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以通过使用厄拉多塞的[筛预计算](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[素数](https://www.geeksforgeeks.org/prime-numbers/)来优化。按照以下步骤解决问题:

*   使用厄拉多塞的**筛，生成直到 **N** 的所有质数，并将其存储在数组**质数[]** 中。**
*   初始化一张 [**地图**](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) ，存储每个角色的[频率。](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)
*   然后，[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，借助地图和质数[]数组，找出哪些字符有**质数频率**。
*   忽略所有具有质数频率的字符，并将其余字符存储在一个新的字符串中。
*   完成上述步骤后，打印新字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform the seive of
// eratosthenes algorithm
void SieveOfEratosthenes(bool* prime, int n)
{
    // Initialize all entries in
    // prime[] as true
    for (int i = 0; i <= n; i++) {
        prime[i] = true;
    }

    // Initialize 0 and 1 as non prime
    prime[0] = prime[1] = false;

    // Traversing the prime array
    for (int i = 2; i * i <= n; i++) {

        // If i is prime
        if (prime[i] == true) {

            // All multiples of i must
            // be marked false as they
            // are non prime
            for (int j = 2; i * j <= n; j++) {
                prime[i * j] = false;
            }
        }
    }
}

// Function to remove characters which
// have prime frequency in the string
void removePrimeFrequencies(string s)
{
    // Length of the string
    int n = s.length();

    // Create a boolean array prime
    bool prime[n + 1];

    // Sieve of Eratosthenes
    SieveOfEratosthenes(prime, n);

    // Stores the frequency of character
    unordered_map<char, int> m;

    // Storing the frequencies
    for (int i = 0; i < s.length(); i++) {
        m[s[i]]++;
    }

    // New string that will be formed
    string new_string = "";

    // Removing the characters which
    // have prime frequencies
    for (int i = 0; i < s.length(); i++) {

        // If the character has
        // prime frequency then skip
        if (prime[m[s[i]]])
            continue;

        // Else concatenate the
        // character to the new string
        new_string += s[i];
    }

    // Print the modified string
    cout << new_string;
}

// Driver Code
int main()
{
    string str = "geeksforgeeks";

    // Function Call
    removePrimeFrequencies(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to perform the seive of
// eratosthenes algorithm
static void SieveOfEratosthenes(boolean[] prime,
                                int n)
{

    // Initialize all entries in
    // prime[] as true
    for(int i = 0; i <= n; i++)
    {
        prime[i] = true;
    }

    // Initialize 0 and 1 as non prime
    prime[0] = prime[1] = false;

    // Traversing the prime array
    for(int i = 2; i * i <= n; i++)
    {

        // If i is prime
        if (prime[i] == true)
        {

            // All multiples of i must
            // be marked false as they
            // are non prime
            for(int j = 2; i * j <= n; j++)
            {
                prime[i * j] = false;
            }
        }
    }
}

// Function to remove characters which
// have prime frequency in the String
static void removePrimeFrequencies(char[] s)
{

    // Length of the String
    int n = s.length;

    // Create a boolean array prime
    boolean []prime = new boolean[n + 1];

    // Sieve of Eratosthenes
    SieveOfEratosthenes(prime, n);

    // Stores the frequency of character
    HashMap<Character, Integer> m = new HashMap<>();

    // Storing the frequencies
    for(int i = 0; i < s.length; i++)
    {
        if (m.containsKey(s[i]))
        {
            m.put(s[i], m.get(s[i]) + 1);
        }
        else
        {
            m.put(s[i], 1);
        }
    }

    // New String that will be formed
    String new_String = "";

    // Removing the characters which
    // have prime frequencies
    for(int i = 0; i < s.length; i++)
    {

        // If the character has
        // prime frequency then skip
        if (prime[m.get(s[i])])
            continue;

        // Else concatenate the
        // character to the new String
        new_String += s[i];
    }

    // Print the modified String
    System.out.print(new_String);
}

// Driver Code
public static void main(String[] args)
{
    String str = "geeksforgeeks";

    // Function Call
    removePrimeFrequencies(str.toCharArray());
}
}

// This code is contributed by aashish1995
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to perform the seive of
# eratosthenes algorithm
def SieveOfEratosthenes(prime, n) :

    # Initialize all entries in
    # prime[] as true
    for i in range(n + 1) :   
        prime[i] = True

    # Initialize 0 and 1 as non prime
    prime[0] = prime[1] = False

    # Traversing the prime array
    i = 2
    while i*i <= n :

        # If i is prime
        if (prime[i] == True) :

            # All multiples of i must
            # be marked false as they
            # are non prime
            j = 2
            while i*j <= n :          
                prime[i * j] = False
                j += 1
        i += 1

# Function to remove characters which
# have prime frequency in the String
def removePrimeFrequencies(s) :

    # Length of the String
    n = len(s)

    # Create a bool array prime
    prime = [False] * (n + 1)

    # Sieve of Eratosthenes
    SieveOfEratosthenes(prime, n)

    # Stores the frequency of character
    m = {}

    # Storing the frequencies
    for i in range(len(s)) :   
        if s[i] in m :       
            m[s[i]]+= 1       
        else :      
            m[s[i]] = 1

    # New String that will be formed
    new_String = ""

    # Removing the characters which
    # have prime frequencies
    for i in range(len(s)) :

        # If the character has
        # prime frequency then skip
        if (prime[m[s[i]]]) :
            continue

        # Else concatenate the
        # character to the new String
        new_String += s[i]

    # Print the modified String
    print(new_String, end = "")

Str = "geeksforgeeks"

# Function Call
removePrimeFrequencies(list(Str))

# This code is contributed by divyesh072019
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to perform the seive of
// eratosthenes algorithm
static void SieveOfEratosthenes(bool[] prime,
                                int n)
{

    // Initialize all entries in
    // prime[] as true
    for(int i = 0; i <= n; i++)
    {
        prime[i] = true;
    }

    // Initialize 0 and 1 as non prime
    prime[0] = prime[1] = false;

    // Traversing the prime array
    for(int i = 2; i * i <= n; i++)
    {

        // If i is prime
        if (prime[i] == true)
        {

            // All multiples of i must
            // be marked false as they
            // are non prime
            for(int j = 2; i * j <= n; j++)
            {
                prime[i * j] = false;
            }
        }
    }
}

// Function to remove characters which
// have prime frequency in the String
static void removePrimeFrequencies(char[] s)
{

    // Length of the String
    int n = s.Length;

    // Create a bool array prime
    bool []prime = new bool[n + 1];

    // Sieve of Eratosthenes
    SieveOfEratosthenes(prime, n);

    // Stores the frequency of character
    Dictionary<char,
               int> m = new Dictionary<char,
                                       int>();

    // Storing the frequencies
    for(int i = 0; i < s.Length; i++)
    {
        if (m.ContainsKey(s[i]))
        {
            m[s[i]]++;
        }
        else
        {
            m.Add(s[i], 1);
        }
    }

    // New String that will be formed
    String new_String = "";

    // Removing the characters which
    // have prime frequencies
    for(int i = 0; i < s.Length; i++)
    {

        // If the character has
        // prime frequency then skip
        if (prime[m[s[i]]])
            continue;

        // Else concatenate the
        // character to the new String
        new_String += s[i];
    }

    // Print the modified String
    Console.Write(new_String);
}

// Driver Code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";

    // Function Call
    removePrimeFrequencies(str.ToCharArray());
}
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to perform the seive of
// eratosthenes algorithm
function SieveOfEratosthenes(prime, n)
{
    // Initialize all entries in
    // prime[] as true
    for (let i = 0; i <= n; i++) {
        prime[i] = true;
    }

    // Initialize 0 and 1 as non prime
    prime[0] = prime[1] = false;

    // Traversing the prime array
    for (let i = 2; i * i <= n; i++) {

        // If i is prime
        if (prime[i] == true) {

            // All multiples of i must
            // be marked false as they
            // are non prime
            for (let j = 2; i * j <= n; j++) {
                prime[i * j] = false;
            }
        }
    }
}

// Function to remove characters which
// have prime frequency in the string
function removePrimeFrequencies( s)
{
    // Length of the string
    var n = s.length;

    // Create a boolean array prime
    var prime = new Array(n + 1);

    // Sieve of Eratosthenes
    SieveOfEratosthenes(prime, n);

    // Stores the frequency of character
    var m = {};
    for(let i =0;i<s.length;i++)
      m[s[i]] = 0;

    // Storing the frequencies
    for (let i = 0; i < s.length; i++) {
        m[s[i]]++;
    }

    // New string that will be formed
    var new_string = "";

    // Removing the characters which
    // have prime frequencies
    for (let i = 0; i < s.length; i++) {

        // If the character has
        // prime frequency then skip
        if (prime[m[s[i]]])
            continue;

        // Else concatenate the
        // character to the new string
        new_string += s[i];

    }

    // Print the modified string
    console.log( new_string);
}

// Driver Code
str = "geeksforgeeks";

// Function Call
removePrimeFrequencies(str);

// This code is contributed by ukasp.   

</script>
```

**Output:** 

```
eeforee
```

***时间复杂度:**O(N * log(log N))*
***辅助空间:** O(N)*