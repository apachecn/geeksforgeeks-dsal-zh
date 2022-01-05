# 具有主频的阵列元件

> 原文:[https://www . geeksforgeeks . org/prime-frequency 数组元素/](https://www.geeksforgeeks.org/array-elements-with-prime-frequencies/)

给定一个字符串。任务是找出出现次数为质数的字符数。
**例** :

```
Input : str = "geeksforgeeks"
Output : 3
Count of occurrences of characters are:
g -> 2
e -> 4
k -> 2
s -> 2
f -> 1
o -> 1
r -> 1
So, g, k and s occurs prime number of times i.e. 2

Input : str = "aabbcc"
Output : 3
```

开始遍历字符串，使用 C++中的[映射计算每个字符的出现次数](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，并检查出现次数[是否为质数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。如果是质数，则增加计数，否则不增加。
以下是上述方法的实施:

## C++

```
// C++ program to find count of numbers
// with prime frequencies

#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// number is prime
bool check_prime(int n)
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

// Function to find count of numbers
// with prime frequencies
int countPrimeFrequent(string s)
{
    int count = 0;

    // create a map to store
    // frequency of each character
    unordered_map<char, int> mp;

    // Store frequency of each character
    // in the map
    for (int i = 0; i < s.length(); i++)
        mp[s[i]]++;

    // now iterate the map and characters
    // with prime occurrences
    for (auto it = mp.begin(); it != mp.end(); it++) {

        // if prime then increment count
        if (check_prime(it->second))
            count++;
    }

    return count;
}

// Driver Code
int main()
{
    string s = "geeksforgeeks";

    cout << countPrimeFrequent(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of numbers
// with prime frequencies

import java.util.*;

class GFG
{

    // Function to check if a
    // number is prime
    static boolean check_prime(int n)
    {
        // Corner cases
        if (n <= 1)
        {
            return false;
        }
        if (n <= 3)
        {
            return true;
        }

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
        {
            return false;
        }

        for (int i = 5; i * i <= n; i = i + 6)
        {
            if (n % i == 0 || n % (i + 2) == 0)
            {
                return false;
            }
        }

        return true;
    }

    // Function to find count of numbers
    // with prime frequencies
    static int countPrimeFrequent(String s)
    {
        int count = 0;

        // create a map to store
        // frequency of each character
        Map<Character, Integer> mp = new HashMap<>();

        // Store frequency of each character
        // in the map
        for (int i = 0; i < s.length(); i++)
        {
            if (mp.containsKey(s.charAt(i)))
            {
                mp.put(s.charAt(i), mp.get(s.charAt(i)) + 1);
            }
            else
            {
                mp.put(s.charAt(i), 1);
            }
        }

        // now iterate the map and characters
        // with prime occurrences
        for (Map.Entry<Character, Integer> entry : mp.entrySet())
        {

            // if prime then increment count
            if (check_prime(entry.getValue()))
            {
                count++;
            }
        }

        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "geeksforgeeks";

        System.out.println(countPrimeFrequent(s));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python3 program to find count of numbers
# with prime frequencies

# Function to check if a
# number is prime

def check_prime(n):
    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

     # This is checked so that we can skip
     # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False

    for i in range(5,n+1,6):
        if (n % i == 0 or n % (i + 2) == 0):
            return False
    return True

# Function to find count of numbers
# with prime frequencies
def countPrimeFrequent(s):
    count = 0
    # create a map to store
    # frequency of each character
    mp={}

    # Store frequency of each character
    # in the mp
    for i in range(0,len(s)):
        mp.setdefault(s[i],0)
        mp[s[i]]+=1

    # now iterate the map and characters
    # with prime occurrences
    for i in mp.keys():
        # if prime then increment count
        if (check_prime(mp[i])):
            count+=1
    return count;

# Driver Code
s = "geeksforgeeks"
print(countPrimeFrequent(s))
# This code is improved by sahilshelangia
```

## C#

```
// C# program to find count of numbers
// with prime frequencies
using System;
using System.Collections.Generic;

class GFG
{

    // Function to check if a
    // number is prime
    static Boolean check_prime(int n)
    {
        // Corner cases
        if (n <= 1)
        {
            return false;
        }
        if (n <= 3)
        {
            return true;
        }

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
        {
            return false;
        }

        for (int i = 5; i * i <= n; i = i + 6)
        {
            if (n % i == 0 || n % (i + 2) == 0)
            {
                return false;
            }
        }

        return true;
    }

    // Function to find count of numbers
    // with prime frequencies
    static int countPrimeFrequent(String s)
    {
        int count = 0;

        // create a map to store
        // frequency of each character
        Dictionary<char, int> mp = new Dictionary<char,int>();

        // Store frequency of each character
        // in the map
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

        // now iterate the map and characters
        // with prime occurrences
        foreach(KeyValuePair<char, int> entry in mp)
        {
            // if prime then increment count
            if (check_prime(entry.Value))
            {
                count++;        
            }
        }
        return count;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String s = "geeksforgeeks";

        Console.WriteLine(countPrimeFrequent(s));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to find count of numbers
// with prime frequencies

// Function to check if a
// number is prime
function check_prime(n) {
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

// Function to find count of numbers
// with prime frequencies
function countPrimeFrequent(s) {
    let count = 0;

    // create a map to store
    // frequency of each character
    let mp = new Map();

    // Store frequency of each character
    // in the map
    for (let i = 0; i < s.length; i++) {
        if (mp.has(s[i])) {
            mp.set(s[i], mp.get(s[i]) + 1);
        }
        else {
            mp.set(s[i], 1);
        }
    }

    // now iterate the map and characters
    // with prime occurrences
    for (let it of mp) {

        // if prime then increment count
        if (check_prime(it[1]))
            count++;
    }

    return count;
}

// Driver Code

let s = "geeksforgeeks";

document.write(countPrimeFrequent(s));

// This code is contributed by Saurabh Jaiswal
</script>
```

**Output:** 

```
3
```