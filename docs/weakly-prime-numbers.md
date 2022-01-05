# 弱质数

> 原文:[https://www.geeksforgeeks.org/weakly-prime-numbers/](https://www.geeksforgeeks.org/weakly-prime-numbers/)

给定一个整数 **N** ，任务是检查 **N** 是否是弱质数。

> 弱素数是不能通过改变一个位数变成素数的素数。

**例:**

> **输入:** N = 294001
> **输出:**是
> **输入:** N = 30
> **输出:**否

**解决方法:**如果数字是复合返回 false 否则我们将对每个位置用 0 到 9 的所有可能的数字逐一替换数字的每个数字，如果由此形成的数字是质数则返回 false。

## C++

```
// C++ Program to check if n
// is Weakly Prime Number

#include <bits/stdc++.h>
using namespace std;

// function to check if N is prime
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0
        || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0
            || n % (i + 2) == 0)
            return false;

    return true;
}

// function to check if n
// is a Weakly Prime Number
bool isWeaklyPrimeNum(int N)
{
    // number should be prime
    if (!isPrime(N))
        return false;

    // converting N to string
    string s = to_string(N);

    // loop to change digit
    // at every character
    // one by one.
    for (int j = 0; j < s.length(); j++) {

        string str = s;

        // loop to store every
        // digit one by one
        // at index j
        for (int i = 0; i <= 9; i++) {

            char c = '0' + i;
            str[j] = c;
            int Num = stoi(str);
            if (str[j] != s[j]
                && isPrime(Num)) {
                return false;
            }
        }
    }
    return true;
}

// Driver code
int main()
{
    int n = 294001;
    if (isWeaklyPrimeNum(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if n
// is Weakly Prime Number
class GFG{

// Function to check if N is prime
static boolean isPrime(int n)
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

    for(int i = 5; i * i <= n; i = i + 6)
       if (n % i == 0 || n % (i + 2) == 0)
           return false;

    return true;
}

// Function to check if n
// is a Weakly Prime Number
static boolean isWeaklyPrimeNum(int N)
{

    // Number should be prime
    if (!isPrime(N))
        return false;

    // Converting N to String
    String s = String.valueOf(N);

    // Loop to change digit
    // at every character
    // one by one.
    for(int j = 0; j < s.length(); j++)
    {
       char []str = s.toCharArray();

       // Loop to store every
       // digit one by one
       // at index j
       for(int i = 0; i <= 9; i++)
       {
          char c = (char)('0' + i);
          str[j] = c;
          int Num = Integer.valueOf(
                    String.valueOf(str));

          if (str[j] != s.charAt(j) &&
              isPrime(Num))
          {
              return false;
          }
       }
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    int n = 294001;

    if (isWeaklyPrimeNum(n))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 Program to check if n
# is weakly prime Number

# function to check if N is prime
def isPrime(n):

    # Corner cases
    if (n <= 1) :
        return False
    if (n <= 3) :
        return True

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False

    for i in range(5, int(n**0.5) + 1, 6):
        if (n % i == 0 or n % (i + 2) == 0):
            return False

    return True

# function to check if n
# is a weakly prime Number
def isWeaklyPrimeNum(N):

    # number should be prime
    if (isPrime(N)==False) :
        return False

    # converting N to string
    s = str(N)

    # loop to change digit at every character
    # one by one.
    for  j in range(len(s)):
        str1 = s

        # loop to store every digit one by one
        # at index j
        for i in range(10):
            c = str(i)
            str1 = str1[ : j] + c + str1[j + 1 : ]
            Num = int(str1)
            if (str1[j] != s[j] and isPrime(Num)) :
                return False

    return True

# Driver code
n = 294001
if (isWeaklyPrimeNum(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by Vishal Maurya.
```

## C#

```
// C# program to check if n
// is Weakly Prime Number
using System;
class GFG{

// Function to check if N is prime
static bool isPrime(int n)
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

    for(int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check if n
// is a Weakly Prime Number
static bool isWeaklyPrimeNum(int N)
{

    // Number should be prime
    if (!isPrime(N))
        return false;

    // Converting N to String
    String s = String.Join("", N);

    // Loop to change digit
    // at every character
    // one by one.
    for(int j = 0; j < s.Length; j++)
    {
        char []str = s.ToCharArray();

        // Loop to store every
        // digit one by one
        // at index j
        for(int i = 0; i <= 9; i++)
        {
            char c = (char)('0' + i);
            str[j] = c;
            int Num = Int32.Parse(String.Join("", str));

            if (str[j] != s[j] && isPrime(Num))
            {
                return false;
            }
        }
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{
    int n = 294001;

    if (isWeaklyPrimeNum(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation

// function to check if N is prime
function isPrime(n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0
        || n % 3 == 0)
        return false;

    for (var i = 5; i * i <= n; i = i + 6)
        if (n % i == 0
            || n % (i + 2) == 0)
            return false;

    return true;
}

// function to check if n
// is a Weakly Prime Number
function isWeaklyPrimeNum(N)
{
    // number should be prime
    if (!isPrime(N))
        return false;

    // converting N to string
    var s = N.toString();

    // loop to change digit
    // at every character
    // one by one.
    for (var j = 0; j < s.length; j++) {

        var str = s;

        // loop to store every
        // digit one by one
        // at index j
        for (var i = 0; i <= 9; i++) {

            var c = '0' + i.toString();
            str[j] = c;
            var Num = parseInt(str);
            if (str[j] != s[j]
                && isPrime(Num)) {
                return false;
            }
        }
    }
    return true;
}

// Driver Code
// Given Number N
var N = 294001;

// Function Call
if (isWeaklyPrimeNum(N))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by shubhamsingh10
</script>
```

**Output:** 

```
Yes
```

参考文献:[http://oeis.org/A050249](http://oeis.org/A050249)T2】