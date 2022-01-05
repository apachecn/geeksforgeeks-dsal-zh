# 统计所有质数长度回文子串

> 原文:[https://www . geesforgeks . org/count-all-prime-length-回文-substrings/](https://www.geeksforgeeks.org/count-all-prime-length-palindromic-substrings/)

给定字符串 **str** ，任务是统计 **str** 的所有子串，这些子串都是回文，长度都是质数。

**示例:**

> **输入:** str = "geeksforgeeks"
> **输出:**2
> “ee”和“ee”是唯一有效的子字符串。
> 
> **输入:**str = " abccc "
> T3】输出: 3

**方法:**使用厄拉多塞的[筛，找到所有的素数直到**串**的长度，因为那是**串**的**子串**所能拥有的最大长度。现在从最小素数开始，即 **j = 2** 到 **j ≤ len(str)** 。如果 **j 为质数**，则统计**串**中**长度= j** 的所有回文子串。打印最后的总计数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if sub-string
// starting at i and ending at j in str is a palindrome
bool isPalindrome(string str, int i, int j)
{
    while (i < j) {
        if (str[i] != str[j])
            return false;
        i++;
        j--;
    }

    return true;
}

// Function to count all palindromic substring
// whose length is a prime number
int countPrimePalindrome(string str, int len)
{

    bool prime[len + 1];
    memset(prime, true, sizeof(prime));

    // 0 and 1 are non-primes
    prime[0] = prime[1] = false;
    for (int p = 2; p * p <= len; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p]) {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= len; i += p)
                prime[i] = false;
        }
    }

    // To store the required number of sub-strings
    int count = 0;

    // Starting from the smallest prime till
    // the largest length of the sub-string possible
    for (int j = 2; j <= len; j++) {

        // If j is prime
        if (prime[j]) {

            // Check all the sub-strings of length j
            for (int i = 0; i + j - 1 < len; i++) {

                // If current sub-string is a palindrome
                if (isPalindrome(str, i, i + j - 1))
                    count++;
            }
        }
    }

    return count;
}

// Driver Code
int main()
{
    string s = "geeksforgeeks";
    int len = s.length();

    cout << countPrimePalindrome(s, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GfG
{

    // Function that returns true if
    // sub-string starting at i and
    // ending at j in str is a palindrome
    static boolean isPalindrome(String str, int i, int j)
    {
        while (i < j)
        {
            if (str.charAt(i) != str.charAt(j))
                return false;
            i++;
            j--;
        }

        return true;
    }

    // Function to count all palindromic substring
    // whose length is a prime number
    static int countPrimePalindrome(String str, int len)
    {

        boolean[] prime = new boolean[len + 1];
        Arrays.fill(prime, true);

        // 0 and 1 are non-primes
        prime[0] = prime[1] = false;
        for (int p = 2; p * p <= len; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p])
            {

                // Update all multiples of p greater than or
                // equal to the square of it
                // numbers which are multiple of p and are
                // less than p^2 are already been marked.
                for (int i = p * p; i <= len; i += p)
                    prime[i] = false;
            }
        }

        // To store the required number of sub-strings
        int count = 0;

        // Starting from the smallest prime till
        // the largest length of the sub-string possible
        for (int j = 2; j <= len; j++)
        {

            // If j is prime
            if (prime[j])
            {

                // Check all the sub-strings of length j
                for (int i = 0; i + j - 1 < len; i++)
                {

                    // If current sub-string is a palindrome
                    if (isPalindrome(str, i, i + j - 1))
                        count++;
                }
            }
        }
        return count;
    }

    // Driver code
    public static void main(String []args)
    {
        String s = "geeksforgeeks";
        int len = s.length();

        System.out.println(countPrimePalindrome(s, len));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math as mt

# Function that returns True if sub-str1ing
# starting at i and ending at j in str1
# is a palindrome
def isPalindrome(str1, i, j):

    while (i < j):
        if (str1[i] != str1[j]):
            return False
        i += 1
        j -= 1

    return True

# Function to count all palindromic substr1ing
# whose length is a prime number
def countPrimePalindrome(str1, Len):

    prime = [True for i in range(Len + 1)]

    # 0 and 1 are non-primes
    prime[0], prime[1] = False, False
    for p in range(2, mt.ceil(mt.sqrt(Len + 1))):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]):

            # Update all multiples of p greater
            # than or equal to the square of it
            # numbers which are multiple of p
            # and are less than p^2 are already
            # been marked.
            for i in range(2 * p, Len + 1, p):
                prime[i] = False

    # To store the required number
    # of sub-str1ings
    count = 0

    # Starting from the smallest prime
    # till the largest Length of the
    # sub-str1ing possible
    for j in range(2, Len + 1):

        # If j is prime
        if (prime[j]):

            # Check all the sub-str1ings of
            # Length j
            for i in range(Len + 1 - j):

                # If current sub-str1ing is a palindrome
                if (isPalindrome(str1, i, i + j - 1)):
                    count += 1

    return count

# Driver Code
s = "geeksforgeeks"
Len = len(s)

print( countPrimePalindrome(s, Len))

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

// Function that returns true if
// sub-string starting at i and
// ending at j in str is a palindrome
static bool isPalindrome(string str,
                         int i, int j)
{
    while (i < j)
    {
        if (str[i] != str[j])
            return false;
        i++;
        j--;
    }

    return true;
}

// Function to count all palindromic
// substring whose length is a prime number
static int countPrimePalindrome(string str,
                                int len)
{

    bool[] prime = new bool[len + 1];
    Array.Fill(prime, true);

    // 0 and 1 are non-primes
    prime[0] = prime[1] = false;
    for (int p = 2; p * p <= len; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p])
        {

            // Update all multiples of p greater
            // than or equal to the square of it
            // numbers which are multiple of p
            // and are less than p^2 are already
            // been marked.
            for (int i = p * p; i <= len; i += p)
                prime[i] = false;
        }
    }

    // To store the required number
    // of sub-strings
    int count = 0;

    // Starting from the smallest prime
    // till the largest length of the
    // sub-string possible
    for (int j = 2; j <= len; j++)
    {

        // If j is prime
        if (prime[j])
        {

            // Check all the sub-strings of
            // length j
            for (int i = 0;
                     i + j - 1 < len; i++)
            {

                // If current sub-string is a
                // palindrome
                if (isPalindrome(str, i, i + j - 1))
                    count++;
            }
        }
    }
    return count;
}

// Driver code
public static void Main()
{
    string s = "geeksforgeeks";
    int len = s.Length;

    Console.WriteLine(countPrimePalindrome(s, len));
}
}

// This code is contributed by Code_Mech
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if sub-string
// starting at i and ending at j in str is
// a palindrome
function isPalindrome($str, $i, $j)
{
    while ($i < $j)
    {
        if ($str[$i] != $str[$j])
            return false;
        $i++;
        $j--;
    }

    return true;
}

// Function to count all palindromic substring
// whose length is a prime number
function countPrimePalindrome($str, $len)
{
    $prime = array_fill(0, $len + 1, true);

    // 0 and 1 are non-primes
    $prime[0] = false ;
    $prime[1] = false;
    for ($p = 2; $p * $p <= $len; $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p])
        {

            // Update all multiples of p greater
            // than or equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for ($i = $p * $p; $i <= $len; $i += $p)
                $prime[$i] = false;
        }
    }

    // To store the required number
    // of sub-strings
    $count = 0;

    // Starting from the smallest prime till
    // the largest length of the sub-string possible
    for ($j = 2; $j <= $len; $j++)
    {

        // If j is prime
        if ($prime[$j])
        {

            // Check all the sub-strings of length j
            for ($i = 0; $i + $j - 1 < $len; $i++)
            {

                // If current sub-string is a palindrome
                if (isPalindrome($str, $i, $i + $j - 1))
                    $count++;
            }
        }
    }

    return $count;
}

// Driver Code
$s = "geeksforgeeks";
$len = strlen($s);

echo countPrimePalindrome($s, $len);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if sub-string
// starting at i and ending at j in str is a palindrome
function isPalindrome(str, i, j)
{
    while (i < j) {
        if (str[i] != str[j])
            return false;
        i++;
        j--;
    }

    return true;
}

// Function to count all palindromic substring
// whose length is a prime number
function countPrimePalindrome(str, len)
{

    var prime = Array(len + 1).fill(true);

    // 0 and 1 are non-primes
    prime[0] = prime[1] = false;
    for (var p = 2; p * p <= len; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p]) {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (var i = p * p; i <= len; i += p)
                prime[i] = false;
        }
    }

    // To store the required number of sub-strings
    var count = 0;

    // Starting from the smallest prime till
    // the largest length of the sub-string possible
    for (var j = 2; j <= len; j++) {

        // If j is prime
        if (prime[j]) {

            // Check all the sub-strings of length j
            for (var i = 0; i + j - 1 < len; i++) {

                // If current sub-string is a palindrome
                if (isPalindrome(str, i, i + j - 1))
                    count++;
            }
        }
    }

    return count;
}

// Driver Code
var s = "geeksforgeeks";
var len = s.length;
document.write( countPrimePalindrome(s, len));

</script>
```

**Output:** 

```
2
```