# 求出现在质数位置的字符的 ascii 值之和

> 原文:[https://www . geeksforgeeks . org/find-字符的 ascii 值之和-出现在素数位置/](https://www.geeksforgeeks.org/find-the-sum-of-the-ascii-values-of-characters-which-are-present-at-prime-positions/)

给定大小为 **N** 的字符串 **str** ，任务是找出出现在质数位置的字符的所有 ASCII 值的总和。
**例:**

> **输入:** str = "abcdef"
> **输出:**298
> “b”、“c”和“e”是仅有的位于质数位置即分别为 2、3 和 5 的
> 字符。
> 它们的 ASCII 值之和为 298。
> **输入:**str = " geeks forgeeks "
> **输出:** 644

**方法:**一种有效的方法是遍历整个字符串，找出特定位置是否是质数。如果当前字符的位置是质数，则将该字符的 ASCII 值添加到答案中。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true
// if n is prime
bool isPrime(int n)
{
    if (n == 0 || n == 1)
        return false;
    for (int i = 2; i * i <= n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function to return the sum
// of the ascii values of the characters
// which are present at prime positions
int sumAscii(string str, int n)
{
    // To store the sum
    int sum = 0;

    // For every character
    for (int i = 0; i < n; i++) {

        // If current position is prime
        // then add the ASCII value of the
        // character at the current position
        if (isPrime(i + 1))
            sum += (int)(str[i]);
    }

    return sum;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int n = str.size();

    cout << sumAscii(str, n);

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
    // if n is prime
    static boolean isPrime(int n)
    {
        if (n == 0 || n == 1)
        {
            return false;
        }
        for (int i = 2; i * i <= n; i++)
        {
            if (n % i == 0)
            {
                return false;
            }
        }

        return true;
    }

    // Function to return the sum
    // of the ascii values of the characters
    // which are present at prime positions
    static int sumAscii(String str, int n)
    {
        // To store the sum
        int sum = 0;

        // For every character
        for (int i = 0; i < n; i++)
        {

            // If current position is prime
            // then add the ASCII value of the
            // character at the current position
            if (isPrime(i + 1))
            {
                sum += (int) (str.charAt(i));
            }
        }

        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        int n = str.length();

        System.out.println(sumAscii(str, n));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

from math import sqrt

# Function that returns true
# if n is prime
def isPrime(n) :

    if (n == 0 or n == 1) :
        return False;

    for i in range(2, int(sqrt(n)) + 1) :
        if (n % i == 0):
            return False;

    return True;

# Function to return the sum
# of the ascii values of the characters
# which are present at prime positions
def sumAscii(string, n) :

    # To store the sum
    sum = 0;

    # For every character
    for i in range(n) :

        # If current position is prime
        # then add the ASCII value of the
        # character at the current position
        if (isPrime(i + 1)) :
            sum += ord(string[i]);

    return sum;

# Driver code
if __name__ == "__main__" :

    string = "geeksforgeeks";
    n = len(string);

    print(sumAscii(string, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true
    // if n is prime
    static bool isPrime(int n)
    {
        if (n == 0 || n == 1)
        {
            return false;
        }

        for (int i = 2; i * i <= n; i++)
        {
            if (n % i == 0)
            {
                return false;
            }
        }

        return true;
    }

    // Function to return the sum
    // of the ascii values of the characters
    // which are present at prime positions
    static int sumAscii(string str, int n)
    {
        // To store the sum
        int sum = 0;

        // For every character
        for (int i = 0; i < n; i++)
        {

            // If current position is prime
            // then add the ASCII value of the
            // character at the current position
            if (isPrime(i + 1))
            {
                sum += (int) (str[i]);
            }
        }

        return sum;
    }

    // Driver code
    public static void Main()
    {
        string str = "geeksforgeeks";
        int n = str.Length;

        Console.WriteLine(sumAscii(str, n));
    }
}

// This code contributed by anuj_67..
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true
// if n is prime
function isPrime(n)
{
    if (n == 0 || n == 1)
        return false;
    for (let i = 2; i * i <= n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function to return the sum
// of the ascii values of the characters
// which are present at prime positions
function sumAscii(str, n)
{
    // To store the sum
    let sum = 0;

    // For every character
    for (let i = 0; i < n; i++) {

        // If current position is prime
        // then add the ASCII value of the
        // character at the current position
        if (isPrime(i + 1))
            sum += str.charCodeAt(i);
    }

    return sum;
}

// Driver code
    let str = "geeksforgeeks";
    let n = str.length;

    document.write(sumAscii(str, n));

</script>
```

**Output:** 

```
644
```