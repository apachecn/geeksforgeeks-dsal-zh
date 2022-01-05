# 一个数的回文除数

> 原文:[https://www . geeksforgeeks . org/a-number 的回文除数/](https://www.geeksforgeeks.org/palindromic-divisors-of-a-number/)

**先决条件:** [找到一个自然数的所有约数](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)
给定一个数 **N** 。任务是找到 **N** 的所有回文除数。

**示例:**

> **输入:**N = 66
> T3】输出: 1 2 3 6 11 22 33 66
> 
> **输入:**N = 808
> T3】输出: 1 2 4 8 101 202 404 808

**进场:**

*   使用在[这篇](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)文章中讨论的方法找到 **N** 的所有因子。
*   对于每个除数 D，检查 D 是否是回文。
*   对所有除数重复上述步骤。

下面是上述方法的实现:

## C++14

```
// C++ program to find all the palindromic
// divisors of a number
#include "bits/stdc++.h"
using namespace std;

// Function to check is num is palindromic
// or not
bool isPalindrome(int n)
{
    // Convert n to string str
    string str = to_string(n);

    // Starting and ending index of
    // string str
    int s = 0, e = str.length() - 1;
    while (s < e) {

        // If char at s and e are
        // not equals then return
        // false
        if (str[s] != str[e]) {
            return false;
        }
        s++;
        e--;
    }
    return true;
}

// Function to find  palindromic divisors
void palindromicDivisors(int n)
{
    // To sore the palindromic divisors of
    // number n
    vector<int> PalindromDivisors;

    for (int i = 1; i <= sqrt(n); i++) {

        // If n is divisible by i
        if (n % i == 0) {

            // Check if number is a perfect square
            if (n / i == i) {

                // Check divisor is palindromic,
                // then store it
                if (isPalindrome(i)) {
                    PalindromDivisors.push_back(i);
                }
            }
            else {

                // Check if divisors are palindrome
                if (isPalindrome(i)) {
                    PalindromDivisors.push_back(i);
                }

                // Check if n / divisors is palindromic
                // or not
                if (isPalindrome(n / i)) {
                    PalindromDivisors.push_back(n / i);
                }
            }
        }
    }

    // Print all palindromic divisors in sorted order
    sort(PalindromDivisors.begin(),
         PalindromDivisors.end());

    for (int i = 0; i < PalindromDivisors.size();
         i++) {
        cout << PalindromDivisors[i] << " ";
    }
}

// Driver code
int main()
{
    int n = 66;

    // Function call to find all palindromic
    // divisors
    palindromicDivisors(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all the palindromic
// divisors of a number
import java.util.*;

class GFG
{

// Function to check is num is palindromic
// or not
static boolean isPalindrome(int n)
{
    // Convert n to String str
    String str = String.valueOf(n);

    // Starting and ending index of
    // String str
    int s = 0, e = str.length() - 1;
    while (s < e) {

        // If char at s and e are
        // not equals then return
        // false
        if (str.charAt(s) != str.charAt(e)) {
            return false;
        }
        s++;
        e--;
    }
    return true;
}

// Function to find palindromic divisors
static void palindromicDivisors(int n)
{
    // To sore the palindromic divisors of
    // number n
    Vector<Integer> PalindromDivisors = new Vector<Integer>();

    for (int i = 1; i <= Math.sqrt(n); i++) {

        // If n is divisible by i
        if (n % i == 0) {

            // Check if number is a perfect square
            if (n / i == i) {

                // Check divisor is palindromic,
                // then store it
                if (isPalindrome(i)) {
                    PalindromDivisors.add(i);
                }
            }
            else {

                // Check if divisors are palindrome
                if (isPalindrome(i)) {
                    PalindromDivisors.add(i);
                }

                // Check if n / divisors is palindromic
                // or not
                if (isPalindrome(n / i)) {
                    PalindromDivisors.add(n / i);
                }
            }
        }
    }

    // Print all palindromic divisors in sorted order
    Collections.sort(PalindromDivisors);

    for (int i = 0; i < PalindromDivisors.size();
        i++) {
        System.out.print(PalindromDivisors.get(i)+ " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 66;

    // Function call to find all palindromic
    // divisors
    palindromicDivisors(n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find all the palindromic
# divisors of a number
from math import sqrt;

# Function to check is num is palindromic
# or not
def isPalindrome(n) :

    # Convert n to string str
    string = str(n);

    # Starting and ending index of
    # string str
    s = 0; e = len(string) - 1;
    while (s < e) :

        # If char at s and e are
        # not equals then return
        # false
        if (string[s] != string[e]) :
            return False;

        s += 1;
        e -= 1;

    return True;

# Function to find palindromic divisors
def palindromicDivisors(n) :

    # To sore the palindromic divisors of
    # number n
    PalindromDivisors = [];

    for i in range(1, int(sqrt(n))) :

        # If n is divisible by i
        if (n % i == 0) :

            # Check if number is a perfect square
            if (n // i == i) :

                # Check divisor is palindromic,
                # then store it
                if (isPalindrome(i)) :
                    PalindromDivisors.append(i);

            else :

                # Check if divisors are palindrome
                if (isPalindrome(i)) :
                    PalindromDivisors.append(i);

                # Check if n / divisors is palindromic
                # or not
                if (isPalindrome(n // i)) :
                    PalindromDivisors.append(n // i);

    # Print all palindromic divisors in sorted order
    PalindromDivisors.sort();

    for i in range(len( PalindromDivisors)) :
        print(PalindromDivisors[i] ,end=" ");

# Driver code
if __name__ == "__main__" :

    n = 66;

    # Function call to find all palindromic
    # divisors
    palindromicDivisors(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find all the palindromic
// divisors of a number
using System;
using System.Collections.Generic;

class GFG
{

// Function to check is num is palindromic
// or not
static bool isPalindrome(int n)
{
    // Convert n to String str
    String str = String.Join("",n);

    // Starting and ending index of
    // String str
    int s = 0, e = str.Length - 1;
    while (s < e)
    {

        // If char at s and e are
        // not equals then return
        // false
        if (str[s] != str[e])
        {
            return false;
        }
        s++;
        e--;
    }
    return true;
}

// Function to find palindromic divisors
static void palindromicDivisors(int n)
{
    // To sore the palindromic divisors of
    // number n
    List<int> PalindromDivisors = new List<int>();

    for (int i = 1; i <= Math.Sqrt(n); i++)
    {

        // If n is divisible by i
        if (n % i == 0)
        {

            // Check if number is a perfect square
            if (n / i == i)
            {

                // Check divisor is palindromic,
                // then store it
                if (isPalindrome(i))
                {
                    PalindromDivisors.Add(i);
                }
            }
            else
            {

                // Check if divisors are palindrome
                if (isPalindrome(i))
                {
                    PalindromDivisors.Add(i);
                }

                // Check if n / divisors is palindromic
                // or not
                if (isPalindrome(n / i))
                {
                    PalindromDivisors.Add(n / i);
                }
            }
        }
    }

    // Print all palindromic divisors in sorted order
    PalindromDivisors.Sort();

    for (int i = 0; i < PalindromDivisors.Count;
        i++)
    {
        Console.Write(PalindromDivisors[i]+ " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 66;

    // Function call to find all palindromic
    // divisors
    palindromicDivisors(n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find all the palindromic
// divisors of a number

// Function to check is num is palindromic
// or not
function isPalindrome(n)
{

    // Convert n to string str
    var str = (n.toString());

    // Starting and ending index of
    // string str
    var s = 0, e = str.length - 1;

    while (s < e)
    {

        // If char at s and e are
        // not equals then return
        // false
        if (str[s] != str[e])
        {
            return false;
        }
        s++;
        e--;
    }
    return true;
}

// Function to find  palindromic divisors
function palindromicDivisors(n)
{

    // To sore the palindromic divisors of
    // number n
    var PalindromDivisors = [];

    for(var i = 1; i <= parseInt(Math.sqrt(n)); i++)
    {

        // If n is divisible by i
        if (n % i == 0)
        {

            // Check if number is a perfect square
            if (n / i == i)
            {

                // Check divisor is palindromic,
                // then store it
                if (isPalindrome(i))
                {
                    PalindromDivisors.push(i);
                }
            }
            else
            {

                // Check if divisors are palindrome
                if (isPalindrome(i))
                {
                    PalindromDivisors.push(i);
                }

                // Check if n / divisors is palindromic
                // or not
                if (isPalindrome(n / i))
                {
                    PalindromDivisors.push(n / i);
                }
            }
        }
    }

    // Print all palindromic divisors in sorted order
    PalindromDivisors.sort((a, b) => a - b)

    for(var i = 0;
            i < PalindromDivisors.length; i++)
    {
        document.write( PalindromDivisors[i] + " ");
    }
}

// Driver code
var n = 66;

// Function call to find all palindromic
// divisors
palindromicDivisors(n);

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
1 2 3 6 11 22 33 66
```

**时间复杂度:** O(N*log N)