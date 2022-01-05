# 下一个最小质数回文

> 原文:[https://www . geesforgeks . org/next-minist-prime-回文/](https://www.geeksforgeeks.org/next-smallest-prime-palindrome/)

给定一个正整数 **N** 其中![1 \leq N \leq 10^{9}  ](img/94574f3aa690fdd95cc1d3808d2fb474.png "Rendered by QuickLaTeX.com")。任务是找到大于或等于 n 的最小质数回文
**示例:**

```
Input: 8
Output: 11

Input: 7000000000
Output: 10000500001
```

**进场:**

**天真的**方法是从 **N + 1** 循环，直到我们找到下一个**最小的质数回文**大于或等于 **N** 。
**高效方法:**
假设 **P = R** 是一个大于或等于 **N** 的下一个**最小素回文**。
现在由于 **R** 是回文， **R** 的前半部分数字最多可以用来确定 **R** 两种可能性。让 **k** 为 **R** 中数字的前半部分。例如，如果 **k = 123** ，则 **R = 12321** 或 **R = 123321** 。
因此，我们遍历每个 **k** 直到 **10 <sup>5</sup>** 并创建关联回文 **R** ，并检查 **R** 是否为**质数**。
同样，我们会分别处理奇数和偶数回文，当我们找到结果时，我们会将它们打破。
**以下是以上办法的实施:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

#define ll long long int

// Function to check whether
// a number is prime
bool isPrime(ll n)
{
    if (n < 2) return false;

    for (ll i = 2; i <= sqrt(n); i++)
    {
        if (n % i == 0) return false;
    }
    return true;
}

// function to generate next
// smallest prime palindrome
ll nextPrimePalindrome(ll N)
{
for (ll k = 1; k < 1000000; k++)
{

    // Check for odd-length palindromes
    string s = to_string(k);
    string z(s.begin(), s.end());
    reverse(z.begin(), z.end());

    // eg. s = '1234' to x = int('1234321')
    ll x = stoll(s + z.substr(1));

    if (x >= N and isPrime(x)) return x;

    // Check for even-length palindromes
    s = to_string(k);
    z = string(s.begin(), s.end());
    reverse(z.begin(), z.end());

    // eg. s = '1234' to x = int('12344321')
    x = stoll(s + z);

    if (x >= N and isPrime(x)) return x;
}
}

// Driver Code
int main()
{
    ll N = 7000000000;

    // Function call to print answer
    cout << nextPrimePalindrome(N) << endl;

    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

// Function to check whether
// a number is prime
static boolean isPrime(long n)
{
    if (n < 2) return false;

    for (long i = 2; i <= Math.sqrt(n); i++)
    {
        if (n % i == 0) return false;
    }
    return true;
}

// reverse the String
static String reverse(String s)
{
    String s1 = "";
    for(int i = s.length() - 1; i >= 0; i--)
        s1 += s.charAt(i);

    return s1;
}

// function to generate next
// smalongest prime palindrome
static long nextPrimePalindrome(long N)
{
    for (long k = 1; k < 1000000l; k++)
    {

        // Check for odd-length palindromes
        String s = ""+k;
        String z;
        z = reverse(s);

        // eg. s = '1234' to x = int('1234321')
        long x = Long.parseLong(s + z.substring(1, z.length()));

        if (x >= N && isPrime(x))
            return x;

        // Check for even-length palindromes
        s = ""+(k);
        z = s;
        z = reverse(z);

        // eg. s = '1234' to x = int('12344321')
        x = Long.parseLong(s + z);

        if (x >= N && isPrime(x)) return x;
    }
    return -1;
}

// Driver Code
public static void main(String args[])
{
    long N = 7000000000l;

    // Function calong to print answer
    System.out.println( nextPrimePalindrome(N) );
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of above approach
import math

# Function to check whether a number is prime
def is_prime(n):
    return n > 1 and all(n % d for d in range(2, int(math.sqrt(n)) + 1))

# function to generate next smallest prime palindrome
def NextprimePalindrome(N):

    for k in range(1, 10**6):

        # Check for odd-length palindromes
        s = str(k)
        x = int(s + s[-2::-1])  # eg. s = '1234' to x = int('1234321')

        if x >= N and is_prime(x):
            return x

        # Check for even-length palindromes
        s = str(k)
        x = int(s + s[-1::-1])  # eg. s = '1234' to x = int('12344321')

        if x >= N and is_prime(x):
            return x

# Driver code
N = 7000000000

# Function call to print answer
print(NextprimePalindrome(N))

# This code is written by
# Sanjit_Prasad
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to check whether
// a number is prime
static bool isPrime(long n)
{
    if (n < 2) return false;

    for (long i = 2; i <= Math.Sqrt(n); i++)
    {
        if (n % i == 0) return false;
    }
    return true;
}

// reverse the String
static String reverse(String s)
{
    String s1 = "";
    for(int i = s.Length - 1; i >= 0; i--)
        s1 += s[i];

    return s1;
}

// function to generate next
// smalongest prime palindrome
static long nextPrimePalindrome(long N)
{
    for (long k = 1; k < 1000000; k++)
    {

        // Check for odd-length palindromes
        String s = ""+k;
        String z;
        z = reverse(s);

        // eg. s = '1234' to x = int('1234321')
        long x = long.Parse(s + z.Substring(1, z.Length - 1));

        if (x >= N && isPrime(x))
            return x;

        // Check for even-length palindromes
        s = ""+(k);
        z = s;
        z = reverse(z);

        // eg. s = '1234' to x = int('12344321')
        x = long.Parse(s + z);

        if (x >= N && isPrime(x)) return x;
    }
    return -1;
}

// Driver Code
public static void Main(String []args)
{
    long N = 7000000000;

    // Function calong to print answer
    Console.WriteLine( nextPrimePalindrome(N) );
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript  implementation of above approach

// Function to check whether
// a number is prime
function isPrime( n)
{
    if (n < 2) return false;

    for (var i = 2; i <= Math.sqrt(n); i++)
    {
        if (n % i == 0) return false;
    }
    return true;
}

// function to generate next
// smallest prime palindrome

function reverse( s)
{
    var s1 = "";
    for(var i = s.length - 1; i >= 0; i--)
        s1 += s[i];

    return s1;
}

function nextPrimePalindrome( N)
{
for (var k = 1; k < 1000000; k++)
{

    // Check for odd-length palindromes
    var s = ""+k;
    var z;
    z=reverse(s);

    // eg. s = '1234' to x = int('1234321')
    var x = Number(s + z.substring(1,z.length));

    if (x >= N && isPrime(x)) return x;

    // Check for even-length palindromes
    s =  ""+k;
    z = s;
     z=reverse(z);

    // eg. s = '1234' to x = int('12344321')
    x = Number(s + z);

    if (x >= N && isPrime(x)) return x;
}
}

var N = 7000000000;
// Function call to find maximum value
document.write(nextPrimePalindrome(N) + "<br>");

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
10000500001
```

时间复杂度:O(N*sqrt(N))，其中 N 是上限，sqrt(N)项来自检查候选项是否为素数。