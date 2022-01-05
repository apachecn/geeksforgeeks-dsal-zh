# 检查字符串的任何排列是否为 K 次重复字符串

> 原文:[https://www . geesforgeks . org/check-if-any-arrange-of-string-is-a-k-times-repeated-string/](https://www.geeksforgeeks.org/check-if-any-permutation-of-string-is-a-k-times-repeated-string/)

给定一个字符串 **S** 和一个整数 **K** ，任务是检查该字符串的任何排列是否可以通过 **K** 次重复任何其他字符串来形成。
**举例:**

> **输入:**S =“ABBA”，K = 2
> **输出:**是
> **解释:**
> 给定字符串的排列–
> {“AABB”“abab”“ABBA”“baab”“Baba”“bbaa”}
> As“abab”是“ab”+“ab”=“abab”的重复字符串，也是字符串的排列。
> **输入:**S =“ABC Abd”，K = 2
> **输出:**否
> **说明:**
> 给定字符串的所有排列中都没有这样的重复字符串。

**方法:**思路是找出字符串中每个字符的[频率，并检查该字符的频率是否为给定整数 **K** 的倍数。如果字符串中所有字符的频率都可以被 **K** 整除，那么就有一个字符串是给定字符串的排列，也是一个 K 倍重复字符串。
以下是上述方法的实施:](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/) 

## C++

```
// C++ implementation to check that
// the permutation of the given string
// is K times repeated string

#include <bits/stdc++.h>

using namespace std;

// Function to check that permutation
// of the given string is a
// K times repeating String
bool repeatingString(string s,
                 int n, int k)
{
    // if length of string is
    // not divisible by K
    if (n % k != 0) {
        return false;
    }

    // Frequency Array
    int frequency[123];

    // Initially frequency of each
    // character is 0
    for (int i = 0; i < 123; i++) {
        frequency[i] = 0;
    }

    // Computing the frequency of
    // each character in the string
    for (int i = 0; i < n; i++) {
        frequency[s[i]]++;
    }

    int repeat = n / k;

    // Loop to check that frequency of
    // every character of the string
    // is divisible by K
    for (int i = 0; i < 123; i++) {

        if (frequency[i] % repeat != 0) {
            return false;
        }
    }

    return true;
}

// Driver Code
int main()
{
    string s = "abcdcba";
    int n = s.size();
    int k = 3;

    if (repeatingString(s, n, k)) {
        cout << "Yes" << endl;
    }
    else {
        cout << "No" << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check that
// the permutation of the given String
// is K times repeated String
class GFG{

// Function to check that permutation
// of the given String is a
// K times repeating String
static boolean repeatingString(String s,
                int n, int k)
{
    // if length of String is
    // not divisible by K
    if (n % k != 0) {
        return false;
    }

    // Frequency Array
    int []frequency = new int[123];

    // Initially frequency of each
    // character is 0
    for (int i = 0; i < 123; i++) {
        frequency[i] = 0;
    }

    // Computing the frequency of
    // each character in the String
    for (int i = 0; i < n; i++) {
        frequency[s.charAt(i)]++;
    }

    int repeat = n / k;

    // Loop to check that frequency of
    // every character of the String
    // is divisible by K
    for (int i = 0; i < 123; i++) {

        if (frequency[i] % repeat != 0) {
            return false;
        }
    }

    return true;
}

// Driver Code
public static void main(String[] args)
{
    String s = "abcdcba";
    int n = s.length();
    int k = 3;

    if (repeatingString(s, n, k)) {
        System.out.print("Yes" +"\n");
    }
    else {
        System.out.print("No" +"\n");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation to check that
# the permutation of the given string
# is K times repeated string

# Function to check that permutation
# of the given string is a
# K times repeating String
def repeatingString(s, n, k):

    # If length of string is
    # not divisible by K
    if (n % k != 0):
        return False

    # Frequency Array
    frequency = [0 for i in range(123)]

    # Initially frequency of each
    # character is 0
    for i in range(123):
        frequency[i] = 0

    # Computing the frequency of
    # each character in the string
    for i in range(n):
        frequency[s[i]] += 1

    repeat = n // k

    # Loop to check that frequency of
    # every character of the string
    # is divisible by K
    for i in range(123):
        if (frequency[i] % repeat != 0):
            return False

    return True

# Driver Code
if __name__ == '__main__':

    s = "abcdcba"
    n = len(s)
    k = 3

    if (repeatingString(s, n, k)):
        print("Yes")
    else:
        print("No")

# This code is contributed by Samarth
```

## C#

```
// C# implementation to check that
// the permutation of the given String
// is K times repeated String
using System;

class GFG{

// Function to check that permutation
// of the given String is a
// K times repeating String
static bool repeatingString(String s,
                int n, int k)
{
    // if length of String is
    // not divisible by K
    if (n % k != 0) {
        return false;
    }

    // Frequency Array
    int []frequency = new int[123];

    // Initially frequency of each
    // character is 0
    for (int i = 0; i < 123; i++) {
        frequency[i] = 0;
    }

    // Computing the frequency of
    // each character in the String
    for (int i = 0; i < n; i++) {
        frequency[s[i]]++;
    }

    int repeat = n / k;

    // Loop to check that frequency of
    // every character of the String
    // is divisible by K
    for (int i = 0; i < 123; i++) {

        if (frequency[i] % repeat != 0) {
            return false;
        }
    }

    return true;
}

// Driver Code
public static void Main(String[] args)
{
    String s = "abcdcba";
    int n = s.Length;
    int k = 3;

    if (repeatingString(s, n, k)) {
        Console.Write("Yes" +"\n");
    }
    else {
        Console.Write("No" +"\n");
    }
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation to check that
// the permutation of the given string
// is K times repeated string

// Function to check that permutation
// of the given string is a
// K times repeating String
function repeatingString( s, n, k)
{
    // if length of string is
    // not divisible by K
    if (n % k != 0) {
        return false;
    }

    // Frequency Array
    var frequency = new Array(123);

    // Initially frequency of each
    // character is 0
    for (let i = 0; i < 123; i++) {
        frequency[i] = 0;
    }

    // Computing the frequency of
    // each character in the string
    for (let i = 0; i < n; i++) {
        frequency[s[i]]++;
    }

    var repeat = n / k;

    // Loop to check that frequency of
    // every character of the string
    // is divisible by K
    for (let i = 0; i < 123; i++) {

        if (frequency[i] % repeat != 0) {
            return false;
        }
    }

    return true;
}

// Driver Code

var s = "abcdcba";
var n = s.length;
var k = 3;

if (repeatingString(s, n, k)) {
    console.log("Yes");
}
else {
    console.log("No" );
}

// This code is contributed by ukasp.

</script>
```

**Output:** 

```
No
```

**性能分析:**
**时间复杂度** O(N)
**辅助空间:** O(1)