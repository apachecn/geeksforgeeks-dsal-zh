# 从给定的字符串中准确使用 P 辅音和 Q 元音可以组成的单词数

> 原文:[https://www . geeksforgeeks . org/使用给定字符串中的精确 p 辅音和 q 元音可以生成的单词数/](https://www.geeksforgeeks.org/number-of-words-that-can-be-made-using-exactly-p-consonants-and-q-vowels-from-the-given-string/)

给定一个字符串**字符串**和两个整数 **P** 和 **Q** 。任务是从给定的字符串中精确选择 **P** 辅音和 **Q** 元音，找到可以组成的单词总数。
**举例:**

> **输入:** str = "geek "，P = 1，Q = 1
> **输出:**8
> “ge”、“ge”、“eg”、“ek”、“eg”、“ek”、
> “ke”和“ke”是可能的单词。
> **输入:** str = "crackathon "，P = 4，Q = 3
> **输出:** 176400

**方法:**因为 **P** 辅音和 **Q** 元音必须从给定字符串中辅音和元音的原始计数中选择。因此，[二项式系数](https://www.geeksforgeeks.org/dynamic-programming-set-9-binomial-coefficient/)可用于计算选择这些字符的组合，并且所选择的字符可使用其计数的[因子](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)自行排列。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define lli long long int

// Function to return the value of nCk
lli binomialCoeff(lli n, lli k)
{
    if (k == 0 || k == n)
        return 1;

    return binomialCoeff(n - 1, k - 1)
           + binomialCoeff(n - 1, k);
}

// Function to return the factorial of n
lli fact(lli n)
{
    if (n >= 1)
        return n * fact(n - 1);
    else
        return 1;
}

// Function that returns true if ch is a vowel
bool isVowel(char ch)
{
    if (ch == 'a' || ch == 'e' || ch == 'i'
        || ch == 'o' || ch == 'u') {
        return true;
    }

    return false;
}

// Function to return the number of words possible
lli countWords(string s, int p, int q)
{

    // To store the count of vowels and
    // consonanats in the given string
    lli countc = 0, countv = 0;
    for (int i = 0; i < s.length(); i++) {

        // If current character is a vowel
        if (isVowel(s[i]))
            countv++;
        else
            countc++;
    }

    // Find the total possible words
    lli a = binomialCoeff(countc, p);
    lli b = binomialCoeff(countv, q);
    lli c = fact(p + q);
    lli ans = (a * b) * c;
    return ans;
}

// Driver code
int main()
{
    string s = "crackathon";
    int p = 4, q = 3;

    cout << countWords(s, p, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to return the value of nCk
    static long binomialCoeff(long n, long k)
    {
        if (k == 0 || k == n)
            return 1;

        return binomialCoeff(n - 1, k - 1) +
               binomialCoeff(n - 1, k);
    }

    // Function to return the factorial of n
    static long fact(long n)
    {
        if (n >= 1)
            return n * fact(n - 1);
        else
            return 1;
    }

    // Function that returns true if ch is a vowel
    static boolean isVowel(char ch)
    {
        if (ch == 'a' || ch == 'e' || ch == 'i' ||
                         ch == 'o' || ch == 'u')
        {
            return true;
        }

        return false;
    }

    // Function to return the number of words possible
    static long countWords(String s, int p, int q)
    {

        // To store the count of vowels and
        // consonanats in the given string
        long countc = 0, countv = 0;
        for (int i = 0; i < s.length(); i++)
        {

            // If current character is a vowel
            if (isVowel(s.charAt(i)))
                countv++;
            else
                countc++;
        }

        // Find the total possible words
        long a = binomialCoeff(countc, p);
        long b = binomialCoeff(countv, q);
        long c = fact(p + q);
        long ans = (a * b) * c;
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        String s = "crackathon";
        int p = 4, q = 3;

        System.out.println(countWords(s, p, q));
    }
}

// This Code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the value of nCk
def binomialCoeff(n, k):
    if (k == 0 or k == n):
        return 1

    return binomialCoeff(n - 1, k - 1) + \
           binomialCoeff(n - 1, k)

# Function to return the factorial of n
def fact(n):
    if (n >= 1):
        return n * fact(n - 1)
    else:
        return 1

# Function that returns true if ch is a vowel
def isVowel(ch):

    if (ch == 'a' or ch == 'e' or
        ch == 'i' or ch == 'o' or ch == 'u'):
        return True

    return False

# Function to return the number of words possible
def countWords(s, p, q):

    # To store the count of vowels and
    # consonanats in the given string
    countc = 0
    countv = 0
    for i in range(len(s)):

        # If current character is a vowel
        if (isVowel(s[i])):
            countv += 1
        else:
            countc += 1

    # Find the total possible words
    a = binomialCoeff(countc, p)
    b = binomialCoeff(countv, q)
    c = fact(p + q)
    ans = (a * b) * c
    return ans

# Driver code
s = "crackathon"
p = 4
q = 3

print(countWords(s, p, q))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the value of nCk
    static long binomialCoeff(long n, long k)
    {
        if (k == 0 || k == n)
            return 1;

        return binomialCoeff(n - 1, k - 1) +
               binomialCoeff(n - 1, k);
    }

    // Function to return the factorial of n
    static long fact(long n)
    {
        if (n >= 1)
            return n * fact(n - 1);
        else
            return 1;
    }

    // Function that returns true if ch is a vowel
    static bool isVowel(char ch)
    {
        if (ch == 'a' || ch == 'e' || ch == 'i' ||
                         ch == 'o' || ch == 'u')
        {
            return true;
        }
        return false;
    }

    // Function to return the number of words possible
    static long countWords(String s, int p, int q)
    {

        // To store the count of vowels and
        // consonanats in the given string
        long countc = 0, countv = 0;
        for (int i = 0; i < s.Length; i++)
        {

            // If current character is a vowel
            if (isVowel(s[i]))
                countv++;
            else
                countc++;
        }

        // Find the total possible words
        long a = binomialCoeff(countc, p);
        long b = binomialCoeff(countv, q);
        long c = fact(p + q);
        long ans = (a * b) * c;
        return ans;
    }

    // Driver code
    public static void Main (String[] args)
    {
        String s = "crackathon";
        int p = 4, q = 3;

        Console.WriteLine(countWords(s, p, q));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the value of nCk
function binomialCoeff(n, k)
{
    if (k == 0 || k == n)
        return 1;

    return binomialCoeff(n - 1, k - 1)
           + binomialCoeff(n - 1, k);
}

// Function to return the factorial of n
function fact(n)
{
    if (n >= 1)
        return n * fact(n - 1);
    else
        return 1;
}

// Function that returns true if ch is a vowel

function isVowel(ch)
{
    if (ch == 'a' || ch == 'e' || ch == 'i'
        || ch == 'o' || ch == 'u') {
        return true;
    }

    return false;
}

// Function to return the number of words possible

function countWords(s, p, q)
{

    // To store the count of vowels and
    // consonanats in the given string
    var countc = 0, countv = 0;
    for (var i = 0; i < s.length; i++) {

        // If current character is a vowel
        if (isVowel(s[i]))
            countv++;
        else
            countc++;
    }

    // Find the total possible words
    var a = binomialCoeff(countc, p);
    var b = binomialCoeff(countv, q);
    var c = fact(p + q);
    var ans = (a * b) * c;
    return ans;
}

// Driver code
var s = "crackathon";
var p = 4, q = 3;
document.write(countWords(s, p, q));

</script>
```

**Output:** 

```
176400
```