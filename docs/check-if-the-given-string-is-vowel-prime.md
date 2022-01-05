# 检查给定的字符串是否是元音质数

> 原文:[https://www . geesforgeks . org/check-if-the-given-string-is-元音-prime/](https://www.geeksforgeeks.org/check-if-the-given-string-is-vowel-prime/)

给定一个由小写英文字母组成的字符串 **str** ，任务是检查该字符串是否是元音质数。如果一个字符串中的所有元音只出现在素数索引处，那么这个字符串被称为元音素数。
**例:**

> **输入:**str =“geeksforgeeks”
> T3】输出:否
> str[1]=“e”是元音，但 1 不是素数。
> **输入:** str = "bcae"
> **输出:**是
> 所有元音都在质数索引处，即 2 和 3。

**方法:**使用厄拉多塞的[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)找到所有小于 N 的素数，这样就可以检查字符串的每个索引的素性。现在，如果有一些非质数索引，使得在那个位置的字符是元音，那么字符串不是元音质数，否则它是。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if c is a vowel
bool isVowel(char c)
{
    if (c == 'a' || c == 'e' || c == 'i'
        || c == 'o' || c == 'u')
        return true;
    return false;
}

// Function that returns true if all the vowels in
// the given string are only at prime indices
bool isVowelPrime(string str, int n)
{
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    bool prime[n];
    memset(prime, true, sizeof(prime));

    // 0 and 1 are not prime
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p < n; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < n; i += p)
                prime[i] = false;
        }
    }

    // For every character of the given string
    for (int i = 0; i < n; i++) {

        // If current character is vowel
        // and the index is not prime
        if (isVowel(str[i]) && !prime[i])
            return false;
    }
    return true;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int n = str.length();

    if (isVowelPrime(str, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true
// if c is a vowel
static boolean isVowel(char c)
{
    if (c == 'a' || c == 'e' ||
        c == 'i' || c == 'o' ||
        c == 'u')
        return true;
    return false;
}

// Function that returns true if all the vowels in
// the given string are only at prime indices
static boolean isVowelPrime(String str, int n)
{

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true.
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    boolean []prime = new boolean[n];
    Arrays.fill(prime, true);

    // 0 and 1 are not prime
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p < n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < n; i += p)
                prime[i] = false;
        }
    }

    // For every character of the given string
    for (int i = 0; i < n; i++)
    {

        // If current character is vowel
        // and the index is not prime
        if (isVowel(str.charAt(i)) && !prime[i])
            return false;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    int n = str.length();

    if (isVowelPrime(str, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if c is a vowel
def isVowel(c):
    if (c == 'a' or c == 'e' or
        c == 'i' or c == 'o' or
        c == 'u'):
        return True
    return False

# Function that returns true if
# all the vowels in the given string
# are only at prime indices
def isVowelPrime(Str, n):

    # Create a boolean array "prime[0..n]"
    # and initialize all entries in it as true.
    # A value in prime[i] will finally be false
    # if i is Not a prime, else true.
    prime = [True for i in range(n)]

    # 0 and 1 are not prime
    prime[0] = False
    prime[1] = False
    for p in range(2, n):
        if p * p > n:
            break

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p greater than or
            # equal to the square of it
            # numbers which are multiple of p and are
            # less than p^2 are already been marked.
            for i in range(2 * p, n, p):
                prime[i] = False

    # For every character of the given String
    for i in range(n):

        # If current character is vowel
        # and the index is not prime
        if (isVowel(Str[i]) and
            prime[i] == False):
            return False
    return True

# Driver code
Str= "geeksforgeeks";
n = len(Str)

if (isVowelPrime(Str, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true
// if c is a vowel
static Boolean isVowel(char c)
{
    if (c == 'a' || c == 'e' ||
        c == 'i' || c == 'o' ||
        c == 'u')
        return true;
    return false;
}

// Function that returns true if all the vowels in
// the given string are only at prime indices
static Boolean isVowelPrime(String str, int n)
{

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true.
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    Boolean []prime = new Boolean[n];
    for(int i = 0; i < n; i++)
        prime[i] = true;

    // 0 and 1 are not prime
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p < n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p greater than
            // or equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < n; i += p)
                prime[i] = false;
        }
    }

    // For every character of the given string
    for (int i = 0; i < n; i++)
    {

        // If current character is vowel
        // and the index is not prime
        if (isVowel(str[i]) && !prime[i])
            return false;
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    int n = str.Length;

    if (isVowelPrime(str, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if c is a vowel
function isVowel(c)
{
    if (c == 'a' || c == 'e' || c == 'i'
        || c == 'o' || c == 'u')
        return true;
    return false;
}

// Function that returns true if all the vowels in
// the given string are only at prime indices
function isVowelPrime(str, n)
{
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    var prime = Array(n).fill(true);

    // 0 and 1 are not prime
    prime[0] = false;
    prime[1] = false;
    for (var p = 2; p * p < n; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (var i = p * p; i < n; i += p)
                prime[i] = false;
        }
    }

    // For every character of the given string
    for (var i = 0; i < n; i++) {

        // If current character is vowel
        // and the index is not prime
        if (isVowel(str[i]) && !prime[i])
            return false;
    }
    return true;
}

// Driver code
var str = "geeksforgeeks";
var n = str.length;
if (isVowelPrime(str, n))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
No
```