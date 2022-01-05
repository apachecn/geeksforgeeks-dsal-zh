# 基数 B 的最大偶数和奇数 N 位数

> 原文:[https://www . geeksforgeeks . org/最大偶数和奇数 n 位数基数-b/](https://www.geeksforgeeks.org/largest-even-and-odd-n-digit-numbers-of-base-b/)

给定一个整数 **N** 和基数 **B** ，任务是找出十进制形式的基数 B 的最大偶数和奇数 **N 位数**。

**示例:**

> **输入:** N = 2，B = 5
> **输出:**
> 偶数= 24
> 奇数= 23
> **说明:**
> 基数为 5 的 2 位数最大偶数= 44，也就是十进制的 24。
> 基数为 5 的 2 位数最大奇数= 43，十进制为 23。
> 
> **输入:** N = 2，B = 10
> T3】输出:T5】偶数= 98
> 奇数= 99

**方法:**
以十进制形式得到基 B 的最大偶数和奇数 **N 位数**由下式给出:

1.  如果基数 B 是偶数，那么:
    *   最大的 N 位偶数是**(B<sup>N</sup>–2)**。
    *   最大 N 位奇数为**(B<sup>N</sup>–1)**。
2.  如果基数 B 是奇数，那么:
    *   最大 N 位偶数为**(B<sup>N</sup>–1)**。
    *   最大 N 位奇数为**(B<sup>N</sup>–2)**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the largest
// N-digit even and odd numbers
// of base B
void findNumbers(int n, int b)
{
    // Initialise the Number
    int even = 0, odd = 0;

    // If Base B is even, then
    // B^n will give largest
    // Even number of N+1 digit
    if (b % 2 == 0) {

        // To get even number of
        // N digit subtract 2 from
        // B^n
        even = pow(b, n) - 2;

        // To get odd number of
        // N digit subtract 1 from
        // B^n
        odd = pow(b, n) - 1;
    }

    // If Base B is odd, then
    // B^n will give largest
    // Odd number of N+1 digit
    else {

        // To get even number of
        // N digit subtract 1 from
        // B^n
        even = pow(b, n) - 1;

        // To get odd number of
        // N digit subtract 2 from
        // B^n
        odd = pow(b, n) - 2;
    }
    cout << "Even Number = " << even << '\n';
    cout << "Odd Number = " << odd;
}

// Driver's Code
int main()
{
    int N = 2, B = 5;

    // Function to find the
    // numbers
    findNumbers(N, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;

class GFG{

// Function to print the largest
// N-digit even and odd numbers
// of base B
static void findNumbers(int n, int b)
{
    // Initialise the Number
    double even = 0, odd = 0;

    // If Base B is even, then
    // B^n will give largest
    // Even number of N+1 digit
    if (b % 2 == 0) {

        // To get even number of
        // N digit subtract 2 from
        // B^n
        even = Math.pow(b, n) - 2;

        // To get odd number of
        // N digit subtract 1 from
        // B^n
        odd = Math.pow(b, n) - 1;
    }

    // If Base B is odd, then
    // B^n will give largest
    // Odd number of N+1 digit
    else {

        // To get even number of
        // N digit subtract 1 from
        // B^n
        even = Math.pow(b, n) - 1;

        // To get odd number of
        // N digit subtract 2 from
        // B^n
        odd = Math.pow(b, n) - 2;
    }
    System.out.println("Even Number = " +  (int)even );
    System.out.print("Odd Number = " +  (int)odd);
}

// Driver's Code
public static void main(String[] args)
{
    int N = 2, B = 5;

    // Function to find the
    // numbers
    findNumbers(N, B);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation of the
# above approach

# Function to print the largest
# N-digit even and odd numbers
# of base B
def findNumbers(n, b):
    # Initialise the Number
    even = 0;
    odd = 0;

    # If Base B is even, then
    # B^n will give largest
    # Even number of N+1 digit
    if (b % 2 == 0):

        # To get even number of
        # N digit subtract 2 from
        # B^n
        even = pow(b, n) - 2;

        # To get odd number of
        # N digit subtract 1 from
        # B^n
        odd = pow(b, n) - 1;

    # If Base B is odd, then
    # B^n will give largest
    # Odd number of N+1 digit
    else:

        # To get even number of
        # N digit subtract 1 from
        # B^n
        even = pow(b, n) - 1;

        # To get odd number of
        # N digit subtract 2 from
        # B^n
        odd = pow(b, n) - 2;

    print("Even Number = ",int(even));
    print("Odd Number = ", int(odd));

# Driver's Code
if __name__ == '__main__':
    N = 2;
    B = 5;

    # Function to find the
    # numbers
    findNumbers(N, B);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG{

// Function to print the largest
// N-digit even and odd numbers
// of base B
static void findNumbers(int n, int b)
{
    // Initialise the Number
    double even = 0, odd = 0;

    // If Base B is even, then
    // B^n will give largest
    // Even number of N+1 digit
    if (b % 2 == 0) {

        // To get even number of
        // N digit subtract 2 from
        // B^n
        even = Math.Pow(b, n) - 2;

        // To get odd number of
        // N digit subtract 1 from
        // B^n
        odd = Math.Pow(b, n) - 1;
    }

    // If Base B is odd, then
    // B^n will give largest
    // Odd number of N+1 digit
    else {

        // To get even number of
        // N digit subtract 1 from
        // B^n
        even = Math.Pow(b, n) - 1;

        // To get odd number of
        // N digit subtract 2 from
        // B^n
        odd = Math.Pow(b, n) - 2;
    }
    Console.WriteLine("Even Number = " +  (int)even );
    Console.Write("Odd Number = " +  (int)odd);
}

// Driver's Code
public static void Main(String[] args)
{
    int N = 2, B = 5;

    // Function to find the
    // numbers
    findNumbers(N, B);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the
// above approach

// Function to print the largest
// N-digit even and odd numbers
// of base B
function findNumbers(n, b)
{

    // Initialise the Number
    var even = 0, odd = 0;

    // If Base B is even, then
    // B^n will give largest
    // Even number of N+1 digit
    if (b % 2 == 0) {

        // To get even number of
        // N digit subtract 2 from
        // B^n
        even = Math.pow(b, n) - 2;

        // To get odd number of
        // N digit subtract 1 from
        // B^n
        odd = Math.pow(b, n) - 1;
    }

    // If Base B is odd, then
    // B^n will give largest
    // Odd number of N+1 digit
    else {

        // To get even number of
        // N digit subtract 1 from
        // B^n
        even = Math.pow(b, n) - 1;

        // To get odd number of
        // N digit subtract 2 from
        // B^n
        odd = Math.pow(b, n) - 2;
    }
    document.write("Even Number = " + even + "<br>");
    document.write("Odd Number = " + odd);
}

// Driver's Code
var N = 2, B = 5;

// Function to find the
// numbers
findNumbers(N, B);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
Even Number = 24
Odd Number = 23
```