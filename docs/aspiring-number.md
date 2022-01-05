# 有志号

> 原文:[https://www.geeksforgeeks.org/aspiring-number/](https://www.geeksforgeeks.org/aspiring-number/)

给定一个数字 n，我们需要检查 n 是否是一个有抱负的数字。如果数字 n 的[等份序列](https://www.geeksforgeeks.org/aliquot-sequence/)以[完全数](https://www.geeksforgeeks.org/perfect-number/)结尾，则该数字被称为有抱负的数字，并且它本身不是完全数。前几个有抱负的数字是:25，95，119，143，417，445，565，608，650，652…

**示例:**

```
Input : 25
Output : Yes.
Explanation : Terminating number of 
aliquot sequence of 25 is 6 which is 
perfect number.

Input :  24
Output : No.
Explanation : Terminating number of 
aliquot sequence of 24 is 0 which is 
not a perfect number.
```

**方法:**首先我们找到给定输入的等分序列的终止数，然后检查它是否是一个完全数(根据定义)。下面给出了检查一个有抱负的号码的实现。

## C++

```
// C++ implementation to check whether
// a number is aspiring or not
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of all proper
// divisors
int getSum(int n)
{
    int sum = 0; // 1 is a proper divisor

    // Note that this loop runs till square root
    // of n
    for (int i = 1; i <= sqrt(n); i++) {
        if (n % i == 0) {

            // If divisors are equal, take only one
            // of them
            if (n / i == i)
                sum = sum + i;

            else // Otherwise take both
            {
                sum = sum + i;
                sum = sum + (n / i);
            }
        }
    }

    // calculate sum of all proper divisors only
    return sum - n;
}

// Function to get last number of Aliquot Sequence.
int getAliquot(int n)
{
    unordered_set<int> s;
    s.insert(n);

    int next = 0;
    while (n > 0) {

        // Calculate next term from previous term
        n = getSum(n);

        if (s.find(n) != s.end())
            return n;       

        s.insert(n);
    }
    return 0;
}

// Returns true if n is perfect
bool isPerfect(int n)
{
    // To store sum of divisors
    long long int sum = 1;

    // Find all divisors and add them
    for (long long int i = 2; i * i <= n; i++)
        if (n % i == 0)
            sum = sum + i + n / i;

    // If sum of divisors is equal to
    // n, then n is a perfect number
    if (sum == n && n != 1)
        return true;

    return false;
}

// Returns true if n is aspiring
// else returns false
bool isAspiring(int n)
{
    // checking condition for aspiring
    int alq = getAliquot(n);
    if (isPerfect(alq) && !isPerfect(n))
        return true;
    else
        return false;
}

// Driver program
int main()
{
    int n = 25;
    if (isAspiring(n))
        cout << "Aspiring" << endl;
    else
        cout << "Not Aspiring" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether
// a number is aspiring or not
import java.util.*;

class GFG
{

    // Function to calculate sum of
    //  all proper divisors
    static int getSum(int n)
    {
        int sum = 0; // 1 is a proper divisor

        // Note that this loop runs till 
        // square root of n
        for (int i = 1; i <= Math.sqrt(n); i++)
        {
            if (n % i == 0)
            {

                // If divisors are equal,
                // take only one of them
                if (n / i == i)
                {
                    sum = sum + i;
                }
                else // Otherwise take both
                {
                    sum = sum + i;
                    sum = sum + (n / i);
                }
            }
        }

        // calculate sum of all
        // proper divisors only
        return sum - n;
    }

    // Function to get last number
    // of Aliquot Sequence.
    static int getAliquot(int n)
    {
        TreeSet<Integer> s = new TreeSet<Integer>();
        s.add(n);

        int next = 0;
        while (n > 0)
        {

            // Calculate next term from previous term
            n = getSum(n);

            if (s.contains(n) & n != s.last())
            {
                return n;
            }

            s.add(n);
        }
        return 0;
    }

    // Returns true if n is perfect
    static boolean isPerfect(int n)
    {
        // To store sum of divisors
        int sum = 1;

        // Find all divisors and add them
        for (int i = 2; i * i <= n; i++)
        {
            if (n % i == 0)
            {
                sum = sum + i + n / i;
            }
        }

        // If sum of divisors is equal to
        // n, then n is a perfect number
        if (sum == n && n != 1)
        {
            return true;
        }

        return false;
    }

    // Returns true if n is aspiring
    // else returns false
    static boolean isAspiring(int n)
    {

        // checking condition for aspiring
        int alq = getAliquot(n);
        if (isPerfect(alq) && !isPerfect(n))
        {
            return true;
        }
        else
        {
            return false;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 25;
        if (isAspiring(n))
        {
            System.out.println("Aspiring");
        }
        else
        {
            System.out.println("Not Aspiring");
        }
    }
}

/* This code has been contributed
by PrinciRaj1992*/
```

## 蟒蛇 3

```
# Python3 implementation to check whether
# a number is aspiring or not

# Function to calculate sum of all proper
# divisors
def getSum(n):

  # 1 is a proper divisor
  sum = 0

  # Note that this loop runs till
  # square root of n
  for i in range(1, int((n) ** (1 / 2)) + 1):
    if not n % i:

      # If divisors are equal, take
      # only one of them
      if n // i == i:
        sum += i

      # Otherwise take both
      else:
        sum += i
        sum += (n // i)

  # Calculate sum of all proper
  # divisors only
  return sum - n

# Function to get last number
# of Aliquot Sequence.
def getAliquot(n):

  s = set()
  s.add(n)
  next = 0

  while (n > 0):

    # Calculate next term from
    # previous term
    n = getSum(n)

    if n not in s:
      return n 

    s.add(n)

  return 0

# Returns true if n is perfect
def isPerfect(n):

  # To store sum of divisors
  sum = 1

  # Find all divisors and add them
  for i in range(2, int((n ** (1 / 2))) + 1):
    if not n % i:
      sum += (i + n // i)

  # If sum of divisors is equal to
  # n, then n is a perfect number
  if sum == n and n != 1:
    return True

  return False

# Returns true if n is aspiring
# else returns false
def isAspiring(n):

  # Checking condition for aspiring
  alq = getAliquot(n)

  if (isPerfect(alq) and not isPerfect(n)):
    return True
  else:
    return False

# Driver Code
n = 25

if (isAspiring(n)):
  print("Aspiring")
else:
  print("Not Aspiring")

# This code is contributed by rohitsingh07052
```

## C#

```
// C# implementation to check whether
// a number is aspiring or not
using System;
using System.Collections.Generic;
class GFG
{

    // Function to calculate sum of
    //  all proper divisors
    static int getSum(int n)
    {
        int sum = 0; // 1 is a proper divisor

        // Note that this loop runs till 
        // square root of n
        for (int i = 1; i <= (int)Math.Sqrt(n); i++)
        {
            if (n % i == 0)
            {

                // If divisors are equal,
                // take only one of them
                if (n / i == i)
                {
                    sum = sum + i;
                }
                else // Otherwise take both
                {
                    sum = sum + i;
                    sum = sum + (n / i);
                }
            }
        }

        // calculate sum of all
        // proper divisors only
        return sum - n;
    }

    // Function to get last number
    // of Aliquot Sequence.
    static int getAliquot(int n)
    {
        HashSet<int> s = new HashSet<int>();
        s.Add(n);
        while (n > 0)
        {

            // Calculate next term from previous term
            n = getSum(n);
            if (s.Contains(n))
            {
                return n;
            }
            s.Add(n);
        }
        return 0;
    }

    // Returns true if n is perfect
    static bool isPerfect(int n)
    {
        // To store sum of divisors
        int sum = 1;

        // Find all divisors and add them
        for (int i = 2; i * i <= n; i++)
        {
            if (n % i == 0)
            {
                sum = sum + i + n / i;
            }
        }

        // If sum of divisors is equal to
        // n, then n is a perfect number
        if (sum == n && n != 1)
        {
            return true;
        }

        return false;
    }

    // Returns true if n is aspiring
    // else returns false
    static bool isAspiring(int n)
    {

        // checking condition for aspiring
        int alq = getAliquot(n);
        if (isPerfect(alq) && !isPerfect(n))
        {
            return true;
        }
        else
        {
            return false;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 25;
        if (isAspiring(n))
        {
            Console.WriteLine("Aspiring");
        }
        else
        {
            Console.WriteLine("Not Aspiring");
        }
    }
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>
// javascript implementation to check whether
// a number is aspiring or not

    // Function to calculate sum of
    // all proper divisors
    function getSum(n) {
        var sum = 0; // 1 is a proper divisor

        // Note that this loop runs till
        // square root of n
        for (var i = 1; i <= Math.sqrt(n); i++) {
            if (n % i == 0) {

                // If divisors are equal,
                // take only one of them
                if (n / i == i) {
                    sum = sum + i;
                } else // Otherwise take both
                {
                    sum = sum + i;
                    sum = sum + (n / i);
                }
            }
        }

        // calculate sum of all
        // proper divisors only
        return sum - n;
    }

    // Function to get last number
    // of Aliquot Sequence.
    function getAliquot(n) {
        var s = new Set();
        s.add(n);

        var next = 0;
        while (n > 0) {

            // Calculate next term from previous term
            n = getSum(n);

            if (s.has(n) & n != s[s.length-1]) {
                return n;
            }

            s.add(n);
        }
        return 0;
    }

    // Returns true if n is perfect
    function isPerfect(n) {
        // To store sum of divisors
        var sum = 1;

        // Find all divisors and add them
        for (var i = 2; i * i <= n; i++) {
            if (n % i == 0) {
                sum = sum + i + n / i;
            }
        }

        // If sum of divisors is equal to
        // n, then n is a perfect number
        if (sum == n && n != 1) {
            return true;
        }

        return false;
    }

    // Returns true if n is aspiring
    // else returns false
    function isAspiring(n) {

        // checking condition for aspiring
        var alq = getAliquot(n);
        if (isPerfect(alq) && !isPerfect(n)) {
            return true;
        } else {
            return false;
        }
    }

    // Driver code

        var n = 25;
        if (isAspiring(n)) {
            document.write("Aspiring");
        } else {
            document.write("Not Aspiring");
        }

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
Aspiring
```

**时间复杂度:** O(n)