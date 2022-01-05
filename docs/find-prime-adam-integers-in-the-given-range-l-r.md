# 求给定范围内的素数亚当整数[L，R]

> 原文:[https://www . geesforgeks . org/find-prime-Adam-给定范围内的整数-l-r/](https://www.geeksforgeeks.org/find-prime-adam-integers-in-the-given-range-l-r/)

给定两个数字 **L** 和 **R** ，表示一个范围**【L，R】**，任务是打印该范围内的所有[质数](https://www.geeksforgeeks.org/prime-numbers/) [亚当](https://www.geeksforgeeks.org/adam-number/)整数。
**注:**既有[素数](https://www.geeksforgeeks.org/prime-numbers/)又有[亚当](https://www.geeksforgeeks.org/adam-number/)的数称为素数亚当数。
**举例:**

> **输入:** L = 5，R = 100
> **输出:** 11 13 31
> **说明:**
> 三个数字 11，13，31 是质数。它们也是亚当数字。
> **输入:** L = 70，R = 50
> **输出:**无效输入

**做法:**这道题用的思路是先检查一个数是不是质数。如果它是质数，那么检查它是否不是亚当数:

*   迭代给定的范围**【L，R】**。
*   对于每个数字，[检查该数字是否为质数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。
*   如果是质数，则检查该数是否为[亚当数](https://www.geeksforgeeks.org/adam-number/)。
*   如果一个数既是素数又是亚当，那么就打印这个数。

以下是上述方法的实现:

## C++

```
// C++ program to find all prime
// adam numbers in the given range
#include <bits/stdc++.h>
using namespace std;

int reverse(int a)
{
    int rev = 0;
    while (a != 0)
    {
        int r = a % 10;

        // Reversing a number by taking
        // remainder at a time
        rev = rev * 10 + r;
        a = a / 10;
    }
    return (rev);
}

// Function to check if a number
// is a prime or not
int prime(int a)
{
    int k = 0;

    // Iterating till the number
    for(int i = 2; i < a; i++)
    {

       // Checking for factors
       if (a % i == 0)
       {
           k = 1;
           break;
       }
    }

    // Returning 1 if the there are
    // no factors of the number other
    // than 1 or itself
    if (k == 1)
    {
        return (0);
    }
    else
    {
        return (1);
    }
}

// Function to check whether a number
// is an adam number or not
int adam(int a)
{

    // Reversing given number
    int r1 = reverse(a);

    // Squaring given number
    int s1 = a * a;

    // Squaring reversed number
    int s2 = r1 * r1;

    // Reversing the square of the
    // reversed number
    int r2 = reverse(s2);

    // Checking if the square of the
    // number and the square of its
    // reverse are equal or not
    if (s1 == r2)
    {
        return (1);
    }
    else
    {
        return (0);
    }
}

// Function to find all the prime
// adam numbers in the given range
void find(int m, int n)
{

    // If the first number is greater
    // than the second number,
    // print invalid
    if (m > n)
    {
        cout << " INVALID INPUT " << endl;
    }
    else
    {
        int c = 0;

        // Iterating through all the
        // numbers in the given range
        for(int i = m; i <= n; i++)
        {

           // Checking for prime number
           int l = prime(i);
           // Checking for Adam number
           int k = adam(i);
           if ((l == 1) && (k == 1))
           {
               cout << i << "\t";
           }
        }
    }
}

// Driver code
int main()
{
    int L = 5, R = 100;

    find(L, R);
    return 0;
}

// This code is contributed by Amit Katiyar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all prime
// adam numbers in the given range
import java.io.*;

class GFG {

    public static int reverse(int a)
    {
        int rev = 0;
        while (a != 0) {
            int r = a % 10;

            // reversing a number by taking
            // remainder at a time
            rev = rev * 10 + r;
            a = a / 10;
        }
        return (rev);
    }

    // Function to check if a number
    // is a prime or not
    public static int prime(int a)
    {
        int k = 0;

        // Iterating till the number
        for (int i = 2; i < a; i++) {

            // Checking for factors
            if (a % i == 0) {
                k = 1;
                break;
            }
        }

        // Returning 1 if the there are no factors
        // of the number other than 1 or itself
        if (k == 1) {
            return (0);
        }
        else {
            return (1);
        }
    }

    // Function to check whether a number
    // is an adam number or not
    public static int adam(int a)
    {
        // Reversing given number
        int r1 = reverse(a);

        // Squaring given number
        int s1 = a * a;

        // Squaring reversed number
        int s2 = r1 * r1;

        // Reversing the square of the
        // reversed number
        int r2 = reverse(s2);

        // Checking if the square of the number
        // and the square of its reverse
        // are equal or not
        if (s1 == r2) {
            return (1);
        }
        else {
            return (0);
        }
    }
    // Function to find all the prime
    // adam numbers in the given range
    public static void find(int m, int n)
    {

        // If the first number is greater
        // than the second number,
        // print invalid
        if (m > n) {
            System.out.println(" INVALID INPUT ");
        }
        else {

            int c = 0;

            // Iterating through all the numbers
            // in the given range
            for (int i = m; i <= n; i++) {

                // Checking for prime number
                int l = prime(i);

                // Checking for Adam number
                int k = adam(i);
                if ((l == 1) && (k == 1)) {
                    System.out.print(i + "\t");
                }
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        int L = 5, R = 100;
        find(L, R);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find all prime
# adam numbers in the given range

def reverse(a):

    rev = 0;
    while (a != 0):

        r = a % 10;

        # Reversing a number by taking
        # remainder at a time
        rev = rev * 10 + r;
        a = a // 10;

    return(rev);

# Function to check if a number
# is a prime or not
def prime(a):

    k = 0;

    # Iterating till the number
    for i in range(2, a):

        # Checking for factors
        if (a % i == 0):
            k = 1;
            break;

    # Returning 1 if the there are
    # no factors of the number other
    # than 1 or itself
    if (k == 1):
        return (0);
    else:
        return (1);

# Function to check whether a number
# is an adam number or not
def adam(a):

    # Reversing given number
    r1 = reverse(a);

    # Squaring given number
    s1 = a * a;

    # Squaring reversed number
    s2 = r1 * r1;

    # Reversing the square of the
    # reversed number
    r2 = reverse(s2);

    # Checking if the square of the
    # number and the square of its
    # reverse are equal or not
    if (s1 == r2):
        return (1);
    else:
        return (0);

# Function to find all the prime
# adam numbers in the given range
def find(m, n):

    # If the first number is greater
    # than the second number,
    # print invalid
    if (m > n):
        print("INVALID INPUT\n");
    else:
        c = 0;

    # Iterating through all the
    # numbers in the given range
    for i in range(m, n):

        # Checking for prime number
        l = prime(i);

        # Checking for Adam number
        k = adam(i);
        if ((l == 1) and (k == 1)):
            print(i, "\t", end = " ");

# Driver code
L = 5; R = 100;
find(L, R);

# This code is contributed by Code_Mech
```

## C#

```
// C# program to find all prime
// adam numbers in the given range
using System;

class GFG{

public static int reverse(int a)
{
    int rev = 0;
    while (a != 0)
    {
        int r = a % 10;

        // Reversing a number by taking
        // remainder at a time
        rev = rev * 10 + r;
        a = a / 10;
    }
    return (rev);
}

// Function to check if a number
// is a prime or not
public static int prime(int a)
{
    int k = 0;

    // Iterating till the number
    for(int i = 2; i < a; i++)
    {

       // Checking for factors
       if (a % i == 0)
       {
           k = 1;
           break;
       }
    }

    // Returning 1 if the there are no factors
    // of the number other than 1 or itself
    if (k == 1)
    {
        return (0);
    }
    else
    {
        return (1);
    }
}

// Function to check whether a number
// is an adam number or not
public static int adam(int a)
{

    // Reversing given number
    int r1 = reverse(a);

    // Squaring given number
    int s1 = a * a;

    // Squaring reversed number
    int s2 = r1 * r1;

    // Reversing the square of the
    // reversed number
    int r2 = reverse(s2);

    // Checking if the square of the
    // number and the square of its
    // reverse are equal or not
    if (s1 == r2)
    {
        return (1);
    }
    else
    {
        return (0);
    }
}

// Function to find all the prime
// adam numbers in the given range
public static void find(int m, int n)
{

    // If the first number is greater
    // than the second number,
    // print invalid
    if (m > n)
    {
        Console.WriteLine("INVALID INPUT");
    }
    else
    {

        // Iterating through all the numbers
        // in the given range
        for(int i = m; i <= n; i++)
        {

           // Checking for prime number
           int l = prime(i);

           // Checking for Adam number
           int k = adam(i);
           if ((l == 1) && (k == 1))
           {
               Console.Write(i + "\t");
           }
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    int L = 5, R = 100;
    find(L, R);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

    // JavaScript program to find all prime
    // adam numbers in the given range

    function reverse(a)
    {
        let rev = 0;
        while (a != 0) {
            let r = a % 10;

            // reversing a number by taking
            // remainder at a time
            rev = rev * 10 + r;
            a = parseInt(a / 10, 10);
        }
        return (rev);
    }

    // Function to check if a number
    // is a prime or not
    function prime(a)
    {
        let k = 0;

        // Iterating till the number
        for (let i = 2; i < a; i++) {

            // Checking for factors
            if (a % i == 0) {
                k = 1;
                break;
            }
        }

        // Returning 1 if the there are no factors
        // of the number other than 1 or itself
        if (k == 1) {
            return (0);
        }
        else {
            return (1);
        }
    }

    // Function to check whether a number
    // is an adam number or not
    function adam(a)
    {
        // Reversing given number
        let r1 = reverse(a);

        // Squaring given number
        let s1 = a * a;

        // Squaring reversed number
        let s2 = r1 * r1;

        // Reversing the square of the
        // reversed number
        let r2 = reverse(s2);

        // Checking if the square of the number
        // and the square of its reverse
        // are equal or not
        if (s1 == r2) {
            return (1);
        }
        else {
            return (0);
        }
    }
    // Function to find all the prime
    // adam numbers in the given range
    function find(m, n)
    {

        // If the first number is greater
        // than the second number,
        // print invalid
        if (m > n) {
            document.write(" INVALID INPUT " + "</br>");
        }
        else {

            let c = 0;

            // Iterating through all the numbers
            // in the given range
            for (let i = m; i <= n; i++) {

                // Checking for prime number
                let l = prime(i);

                // Checking for Adam number
                let k = adam(i);
                if ((l == 1) && (k == 1)) {
                    document.write(i + " ");
                }
            }
        }
    }

    let L = 5, R = 100;
      find(L, R);

</script>
```

**Output:** 11    13    31 

**时间复杂度:** *O(N <sup>2</sup> )* ，其中 N 为最大数 r

**辅助空间:** O(1)