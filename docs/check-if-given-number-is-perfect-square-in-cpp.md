# 检查给定的数字是否是完美的正方形

> 原文:[https://www . geesforgeks . org/check-如果给定的数字是完美平方英寸 cpp/](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)

给定一个数字，检查它是否是一个完美的正方形。

**例:**

```
Input : 2500
Output : Yes
Explanation:
2500 is a perfect square.
50 * 50 = 2500

Input  : 2555
Output : No
```

**逼近:**

1.  Take the square root of the number.
2.  Multiply the square root twice
3.  Use Boolean equality operator to verify whether the product of square root is equal to a given number.

## c++

```
// CPP program to find if x is a
// perfect square.
#include <bits/stdc++.h>
using namespace std;

bool isPerfectSquare(long double x)
{
    // Find floating point value of
    // square root of x.
    if (x >= 0) {

        long long sr = sqrt(x);

        // if product of square root
        //is equal, then
        // return T/F
        return (sr * sr == x);
    }
    // else return false if n<0
    return false;
}

int main()
{
    long long x = 2502;
    if (isPerfectSquare(x))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java

```
// Java program to find if x is a
// perfect square.
class GFG {

    static boolean isPerfectSquare(int x)
    {
        if (x >= 0) {

            // Find floating point value of
            // square root of x.
            int sr = (int)Math.sqrt(x);

            // if product of square root
            // is equal, then
            // return T/F

            return ((sr * sr) == x);
        }
        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        int x = 2502;

        if (isPerfectSquare(x))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}

// This code is contributed by Anant Agarwal.
```

## python 3

```
# Python program to find if x is a
# perfect square.

import math

def isPerfectSquare(x):

    #if x >= 0,
    if(x >= 0):
        sr = math.sqrt(x)
        # sqrt function returns floating value so we have to convert it into integer
        #return boolean T/F
        return ((sr*sr) == float(x))
    return false

# Driver code

x = 2502
if (isPerfectSquare(x)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Anant Agarwal.
```

T29】c#T3T33】PHPT4T37】JavascriptT5T41】T42**输出**

```
No
```