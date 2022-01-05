# 检查给定的一对号码是否为订婚号码

> 原文:[https://www . geesforgeks . org/check-如果给定的一对号码是订婚号码或不订婚号码/](https://www.geeksforgeeks.org/check-if-a-given-pair-of-numbers-are-betrothed-numbers-or-not/)

给定两个正数 **N** 和 **M** ，任务是检查给定的数对 **(N，M)** 是否形成一个[许配数](https://www.geeksforgeeks.org/betrothed-numbers/)。
**举例:**

> **输入:** N = 48，M = 75
> **输出:**是
> **说明:**
> 48 的定数是 1，2，3，4，6，8，12，16，24
> 48 的定数之和是 75(**Sum 1**)
> 75 的定数是 1，3，5，15，25
> 的定数之和
> **输入:** N = 95，M = 55
> **输出:**否
> **说明:**
> 95 的真约数是 1，5，19
> 48 的真约数之和是 25(**Sum 1**)
> 55 的真约数是 1，5，11
> 48 的真约数之和是 17(

**进场:**

1.  求给定数 **N 和 M** 的适当因子的[和。](https://www.geeksforgeeks.org/sum-of-all-proper-divisors-of-a-natural-number/)
2.  如果 **N** 的定数之和等于 **M + 1** 或者 **M** 的定数之和等于 **N + 1** ，那么给定的对形成一个[定数](https://www.geeksforgeeks.org/betrothed-numbers/)。
3.  否则它不会形成一对订婚号码。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether N is
// Perfect Square or not
bool isPerfectSquare(int N)
{

    // Find sqrt
    double sr = sqrt(N);

    return (sr - floor(sr)) == 0;
}

// Function to check whether the given
// pairs of numbers is Betrothed Numbers
// or not
void BetrothedNumbers(int n, int m)
{
    int Sum1 = 1;
    int Sum2 = 1;

    // For finding the sum of all the
    // divisors of first number n
    for (int i = 2; i <= sqrt(n); i++) {
        if (n % i == 0) {
            Sum1 += i
                    + (isPerfectSquare(n)
                           ? 0
                           : n / i);
        }
    }

    // For finding the sum of all the
    // divisors of second number m
    for (int i = 2; i <= sqrt(m); i++) {
        if (m % i == 0) {
            Sum2 += i
                    + (isPerfectSquare(m)
                           ? 0
                           : m / i);
        }
    }

    if ((n + 1 == Sum2)
        && (m + 1 == Sum1)) {
        cout << "YES" << endl;
    }
    else {
        cout << "NO" << endl;
    }
}

// Driver Code
int main()
{
    int N = 9504;
    int M = 20734;

    // Function Call
    BetrothedNumbers(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check whether N is
// Perfect Square or not
static boolean isPerfectSquare(int N)
{

    // Find sqrt
    double sr = Math.sqrt(N);

    return (sr - Math.floor(sr)) == 0;
}

// Function to check whether the given
// pairs of numbers is Betrothed Numbers
// or not
static void BetrothedNumbers(int n, int m)
{
    int Sum1 = 1;
    int Sum2 = 1;

    // For finding the sum of all the
    // divisors of first number n
    for (int i = 2; i <= Math.sqrt(n); i++) {
        if (n % i == 0) {
            Sum1 += i
                    + (isPerfectSquare(n)
                           ? 0
                           : n / i);
        }
    }

    // For finding the sum of all the
    // divisors of second number m
    for (int i = 2; i <= Math.sqrt(m); i++) {
        if (m % i == 0) {
            Sum2 += i
                    + (isPerfectSquare(m)
                           ? 0
                           : m / i);
        }
    }

    if ((n + 1 == Sum2)
        && (m + 1 == Sum1)) {
        System.out.print("YES" +"\n");
    }
    else {
        System.out.print("NO" +"\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 9504;
    int M = 20734;

    // Function Call
    BetrothedNumbers(N, M);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt,floor

# Function to check whether N is
# Perfect Square or not
def isPerfectSquare(N):
    # Find sqrt
    sr = sqrt(N)

    return (sr - floor(sr)) == 0

# Function to check whether the given
# pairs of numbers is Betrothed Numbers
# or not
def BetrothedNumbers(n,m):
    Sum1 = 1
    Sum2 = 1

    # For finding the sum of all the
    # divisors of first number n
    for i in range(2,int(sqrt(n))+1,1):
        if (n % i == 0):
            if (isPerfectSquare(n)):
                Sum1 += i
            else:
                Sum1 += i + n/i

    # For finding the sum of all the
    # divisors of second number m
    for i in range(2,int(sqrt(m))+1,1):
        if (m % i == 0):
            if (isPerfectSquare(m)):
                Sum2 += i
            else:
                Sum2 += i + (m / i)

    if ((n + 1 == Sum2) and (m + 1 == Sum1)):
        print("YES")   
    else:
        print("NO")

# Driver Code
if __name__ == '__main__':
    N = 9504
    M = 20734

    # Function Call
    BetrothedNumbers(N, M)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check whether N is
// perfect square or not
static bool isPerfectSquare(int N)
{

    // Find sqrt
    double sr = Math.Sqrt(N);

    return (sr - Math.Floor(sr)) == 0;
}

// Function to check whether the given
// pairs of numbers is Betrothed numbers
// or not
static void BetrothedNumbers(int n, int m)
{
    int Sum1 = 1;
    int Sum2 = 1;

    // For finding the sum of all the
    // divisors of first number n
    for(int i = 2; i <= Math.Sqrt(n); i++)
    {
       if (n % i == 0)
       {
           Sum1 += i + (isPerfectSquare(n) ?
                                 0 : n / i);
       }
    }

    // For finding the sum of all the
    // divisors of second number m
    for(int i = 2; i <= Math.Sqrt(m); i++)
    {
       if (m % i == 0)
       {
           Sum2 += i + (isPerfectSquare(m) ?
                                 0 : m / i);
       }
    }

    if ((n + 1 == Sum2) && (m + 1 == Sum1))
    {
        Console.Write("YES" + "\n");
    }
    else
    {
        Console.Write("NO" + "\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 9504;
    int M = 20734;

    // Function Call
    BetrothedNumbers(N, M);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check whether N is
// Perfect Square or not
function isPerfectSquare(N)
{

    // Find sqrt
    let sr = Math.sqrt(N);

    return (sr - Math.floor(sr)) == 0;
}

// Function to check whether the given
// pairs of numbers is Betrothed Numbers
// or not
function BetrothedNumbers(n, m)
{
    let Sum1 = 1;
    let Sum2 = 1;

    // For finding the sum of all the
    // divisors of first number n
    for (let i = 2; i <= Math.sqrt(n); i++) {
        if (n % i == 0) {
            Sum1 += i
                    + (isPerfectSquare(n)
                           ? 0
                           : parseInt(n / i));
        }
    }

    // For finding the sum of all the
    // divisors of second number m
    for (let i = 2; i <= Math.sqrt(m); i++) {
        if (m % i == 0) {
            Sum2 += i
                    + (isPerfectSquare(m)
                           ? 0
                           : parseInt(m / i));
        }
    }

    if ((n + 1 == Sum2)
        && (m + 1 == Sum1)) {
        document.write("YES");
    }
    else {
        document.write("NO");
    }
}

// Driver Code
    let N = 9504;
    let M = 20734;

    // Function Call
    BetrothedNumbers(N, M);

// This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
NO
```

***时间复杂度:** O(√N + √M)*