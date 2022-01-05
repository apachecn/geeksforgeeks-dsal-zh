# 莱蒙诺的猜想

> 哎哎哎:# t0]https://www . geeksforgeeks . org/lemoines-猜想/

任何大于 5 的奇数都可以表示为奇数[素数](https://www.geeksforgeeks.org/prime-numbers/)(除 2 以外的所有素数都是奇数)和偶数半素数的和。一个[半素](https://www.geeksforgeeks.org/check-whether-number-semiprime-not/)数是两个素数的乘积。这叫做[勒莫因猜想](https://en.wikipedia.org/wiki/Lemoine%27s_conjecture)。
**举例:**

> 7 = 3 + (2 × 2)，
> 其中 3 是素数(不是 2)，4 (= 2 × 2)是半素数。
> 11 = 5 + (2 × 3)
> 其中 5 是素数，6(= 2 × 3)是半素数。
> 9 = 3 + (2 × 3)或 9 = 5+(2×2)
> 47 = 13+2×17 = 37+2×5 = 41+2×3 = 43+2×2

## C++

```
// C++ code to verify Lemoine's Conjecture
// for any odd number >= 7
#include<bits/stdc++.h>
using namespace std;

// Function to check if a number is
// prime or not
bool isPrime(int n)
{
    if (n < 2)
        return false;

    for (int i = 2; i <= sqrt(n); i++) {
        if (n % i == 0)
            return false;
    }
    return true;
}

// Representing n as p + (2 * q) to satisfy
// lemoine's conjecture
void lemoine(int n)
{
    // Declaring a map to hold pairs (p, q)
    map<int, int> pr;

    // Declaring an iterator for map
    map<int, int>::iterator it;
    it = pr.begin();

    // Finding various values of p for each q
    // to satisfy n = p + (2 * q)
    for (int q = 1; q <= n / 2; q++)
    {
        int p = n - 2 * q;

        // After finding a pair that satisfies the
        // equation, check if both p and q are
        // prime or not
        if (isPrime(p) && isPrime(q))

            // If both p and q are prime, store
            // them in the map
            pr.insert(it, pair<int, int>(p, q));
    }

    // Displaying all pairs (p, q) that satisfy
    // lemoine's conjecture for the number 'n'
    for (it = pr.begin(); it != pr.end(); ++it)
        cout << n << " = " << it->first
             << " + (2 * " << it->second << ")\n";
}

// Driver Function
int main()
{
    int n = 39;
    cout << n << " can be expressed as " << endl;

    // Function calling
    lemoine(n);

    return 0;
}

// This code is contributed by Saagnik Adhikary
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to verify Lemoine's Conjecture
// for any odd number >= 7

import java.util.*;

class GFG {
    static class pair {
        int first, second;

        public pair(int first, int second) {
            this.first = first;
            this.second = second;
        }
    }

    // Function to check if a number is
    // prime or not
    static boolean isPrime(int n) {
        if (n < 2)
            return false;

        for (int i = 2; i <= Math.sqrt(n); i++) {
            if (n % i == 0)
                return false;
        }
        return true;
    }

    // Representing n as p + (2 * q) to satisfy
    // lemoine's conjecture
    static void lemoine(int n) {
        // Declaring a map to hold pairs (p, q)
        HashMap<Integer, pair> pr = new HashMap<>();

        // Declaring an iterator for map
        // HashMap<Integer,Integer>::iterator it;
        // it = pr.begin();
        int i = 0;
        // Finding various values of p for each q
        // to satisfy n = p + (2 * q)
        for (int q = 1; q <= n / 2; q++) {
            int p = n - 2 * q;

            // After finding a pair that satisfies the
            // equation, check if both p and q are
            // prime or not
            if (isPrime(p) && isPrime(q))

                // If both p and q are prime, store
                // them in the map
                pr.put(i, new pair(p, q));
            i++;
        }

        // Displaying all pairs (p, q) that satisfy
        // lemoine's conjecture for the number 'n'
        for (Map.Entry<Integer, pair> it : pr.entrySet())
            System.out.print(n + " = " + it.getValue().first + " + (2 * " + it.getValue().second + ")\n");
    }

    // Driver Function
    public static void main(String[] args) {
        int n = 39;
        System.out.print(n + " can be expressed as " + "\n");

        // Function calling
        lemoine(n);

    }
}

// This code contributed by aashish1995
```

## 蟒蛇 3

```
# Python code to verify Lemoine's Conjecture
# for any odd number >= 7
from math import sqrt

# Function to check if a number is
# prime or not
def isPrime(n: int) -> bool:
    if n < 2:
        return False

    for i in range(2, int(sqrt(n)) + 1):
        if n % i == 0:
            return False

    return True

# Representing n as p + (2 * q) to satisfy
# lemoine's conjecture
def lemoine(n: int) -> None:

    # Declaring a map to hold pairs (p, q)
    pr = dict()

    # Finding various values of p for each q
    # to satisfy n = p + (2 * q)
    for q in range(1, n // 2 + 1):
        p = n - 2 * q

        # After finding a pair that satisfies the
        # equation, check if both p and q are
        # prime or not
        if isPrime(p) and isPrime(q):

            # If both p and q are prime, store
            # them in the map
            if p not in pr:
                pr[p] = q

    # Displaying all pairs (p, q) that satisfy
    # lemoine's conjecture for the number 'n'
    for it in pr:
        print("%d = %d + (2 * %d)" % (n, it, pr[it]))

# Driver Code
if __name__ == "__main__":
    n = 39
    print(n, "can be expressed as ")

    # Function calling
    lemoine(n)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# code to verify Lemoine's Conjecture
// for any odd number >= 7
using System;
using System.Collections.Generic;

class GFG
{
    public
   class pair
   {
         public
           int first, second;

          public pair(int first, int second)
          {
              this.first = first;
              this.second = second;
          }
      }

      // Function to check if a number is
      // prime or not
      static bool isPrime(int n)
      {
          if (n < 2)
              return false;

          for (int i = 2; i <= Math.Sqrt(n); i++)
          {
              if (n % i == 0)
                  return false;
          }
          return true;
      }

      // Representing n as p + (2 * q) to satisfy
      // lemoine's conjecture
      static void lemoine(int n)
      {

          // Declaring a map to hold pairs (p, q)
          Dictionary<int, pair> pr = new Dictionary<int, pair>();

          // Declaring an iterator for map
          // Dictionary<int,int>::iterator it;
          // it = pr.begin();
          int i = 0;

          // Finding various values of p for each q
          // to satisfy n = p + (2 * q)
          for (int q = 1; q <= n / 2; q++)
          {
              int p = n - 2 * q;

              // After finding a pair that satisfies the
              // equation, check if both p and q are
              // prime or not
              if (isPrime(p) && isPrime(q))

                  // If both p and q are prime, store
                  // them in the map
                  pr.Add(i, new pair(p, q));
              i++;
          }

          // Displaying all pairs (p, q) that satisfy
          // lemoine's conjecture for the number 'n'
          foreach (KeyValuePair<int, pair> it in pr)
              Console.Write(n + " = " + it.Value.first +
                            " + (2 * " + it.Value.second + ")\n");
      }

      // Driver code
      public static void Main(String[] args)
      {
          int n = 39;
          Console.Write(n + " can be expressed as " + "\n");

          // Function calling
          lemoine(n);
      }
  }

  // This code is contributed by aashish1995
```

**输出:**

```
39 can be expressed as :
39 = 5 + (2 * 17)
39 = 13 + (2 * 13)
39 = 17 + (2 * 11)
39 = 29 + (2 * 5)
```