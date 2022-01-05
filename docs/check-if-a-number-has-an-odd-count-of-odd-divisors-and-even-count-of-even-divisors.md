# 检查一个数是否有奇数除数和偶数除数

> 原文:[https://www . geesforgeks . org/check-如果一个数有奇数除数和偶数除数/](https://www.geeksforgeeks.org/check-if-a-number-has-an-odd-count-of-odd-divisors-and-even-count-of-even-divisors/)

给定一个整数 **N** ，任务是检查 **N** 是否有奇数个奇数除数和偶数个偶数除数。

**示例**:

> **输入:** N = 36
> **输出:**是
> **解释:**
> 36 的除数= 1、2、3、4、6、9、12、18、36
> 奇数除数(1、3、9) = 3【奇数】
> 偶数除数(2、4、6、12、18、36) = 6【偶数】
> 
> **输入:**N = 28
> T3】输出:否

**天真的做法**:思路是找到 N 个数的因子，统计 N 的奇数因子和 N 的偶数因子，最后检查奇数因子的计数是否为奇数，偶数因子的计数是否为偶数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;

#define lli long long int

// Function to find the count
// of even and odd factors of N
void checkFactors(lli N)
{
    lli ev_count = 0, od_count = 0;

    // Loop runs till square root
    for (lli i = 1;
         i <= sqrt(N) + 1; i++) {
        if (N % i == 0) {
            if (i == N / i) {
                if (i % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
            }
            else {
                if (i % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
                if ((N / i) % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
            }
        }
    }

    // Condition to check if the even
    // factors of the number N is
    // is even and count of
    // odd factors is odd
    if (ev_count % 2 == 0
        && od_count % 2 == 1)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}

// Driver Code
int main()
{
    lli N = 36;
    checkFactors(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;

class GFG{

// Function to find the count
// of even and odd factors of N
static void checkFactors(long N)
{
    long ev_count = 0, od_count = 0;

    // Loop runs till square root
    for(long i = 1;
             i <= Math.sqrt(N) + 1; i++)
    {
        if (N % i == 0)
        {
            if (i == N / i)
            {
                if (i % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
            }
            else
            {
                if (i % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
                if ((N / i) % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
            }
        }
    }

    // Condition to check if the even
    // factors of the number N is
    // is even and count of
    // odd factors is odd
    if (ev_count % 2 == 0 && od_count % 2 == 1)
        System.out.print("Yes" + "\n");
    else
        System.out.print("No" + "\n");
}

// Driver Code
public static void main(String[] args)
{
    long N = 36;

    checkFactors(N);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to find the count
# of even and odd factors of N
def checkFactors(N):

    ev_count = 0; od_count = 0;

    # Loop runs till square root
    for i in range(1, int(pow(N, 1 / 2)) + 1):
        if (N % i == 0):
            if (i == N / i):

                if (i % 2 == 0):
                    ev_count += 1;
                else:
                    od_count += 1;

            else:
                if (i % 2 == 0):
                    ev_count += 1;
                else:
                    od_count += 1;
                if ((N / i) % 2 == 0):
                    ev_count += 1;
                else:
                    od_count += 1;

    # Condition to check if the even
    # factors of the number N is
    # is even and count of
    # odd factors is odd
    if (ev_count % 2 == 0 and
        od_count % 2 == 1):
        print("Yes" + "");
    else:
        print("No" + "");

# Driver Code
if __name__ == '__main__':

    N = 36;

    checkFactors(N);

# This code is contributed by Princi Singh
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG{

// Function to find the count
// of even and odd factors of N
static void checkFactors(long N)
{
    long ev_count = 0, od_count = 0;

    // Loop runs till square root
    for(long i = 1;
             i <= Math.Sqrt(N) + 1; i++)
    {
        if (N % i == 0)
        {
            if (i == N / i)
            {
                if (i % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
            }
            else
            {
                if (i % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
                if ((N / i) % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
            }
        }
    }

    // Condition to check if the even
    // factors of the number N is
    // is even and count of
    // odd factors is odd
    if (ev_count % 2 == 0 && od_count % 2 == 1)
        Console.Write("Yes" + "\n");
    else
        Console.Write("No" + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    long N = 36;

    checkFactors(N);
}
}

// This code is contributed by Amit Katiyar 
```

## java 描述语言

```
<script>

// JavaScript implementation of the
// above approach

// Function to find the count
// of even and odd factors of N
function checkFactors(N)
{
    let ev_count = 0, od_count = 0;

    // Loop runs till square root
    for (let i = 1;
        i <= Math.sqrt(N) + 1; i++) {
        if (N % i == 0) {
            if (i == Math.floor(N / i)) {
                if (i % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
            }
            else {
                if (i % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
                if (Math.floor(N / i) % 2 == 0)
                    ev_count += 1;
                else
                    od_count += 1;
            }
        }
    }

    // Condition to check if the even
    // factors of the number N is
    // is even and count of
    // odd factors is odd
    if (ev_count % 2 == 0
        && od_count % 2 == 1)
        document.write("Yes" + "<br>");
    else
        document.write("No" + "<br>");
}

// Driver Code

    let N = 36;
    checkFactors(N);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
Yes
```

**高效逼近**:问题中的关键观察是，只有在完美平方的情况下，奇数除数为奇数，偶数除数为偶数。因此，最好的解决办法是[检查给定的数字是否是一个完美的正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。如果是完美的正方形，那么打印“是”，否则打印“否”。

以下是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;

#define lli long long int

// Function to check if the
// number is a perfect square
bool isPerfectSquare(long double x)
{
    long double sr = sqrt(x);

    // If square root is an integer
    return ((sr - floor(sr)) == 0);
}

// Function to check
// if count of even divisors is even
// and count of odd divisors is odd
void checkFactors(lli N)
{
    if (isPerfectSquare(N))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}

// Driver Code
int main()
{
    lli N = 36;

    checkFactors(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to check if the
// number is a perfect square
static boolean isPerfectSquare(double x)
{

    // Find floating point value of
    // square root of x.
    double sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0);
}

// Function to check if count of
// even divisors is even and count
// of odd divisors is odd
static void checkFactors(int x)
{
    if (isPerfectSquare(x))
        System.out.print("Yes");
    else
        System.out.print("No");
}

// Driver code
public static void main(String[] args)
{
    int N = 36;

    checkFactors(N);
}
}

// This code is contributed by dewantipandeydp
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import math

# Function to check if the
# number is a perfect square
def isPerfectSquare(x):

    # Find floating povalue of
    # square root of x.
    sr = pow(x, 1 / 2);

    # If square root is an integer
    return ((sr - math.floor(sr)) == 0);

# Function to check if count of
# even divisors is even and count
# of odd divisors is odd
def checkFactors(x):
    if (isPerfectSquare(x)):
        print("Yes");
    else:
        print("No");

# Driver code
if __name__ == '__main__':
    N = 36;

    checkFactors(N);

# This code is contributed by sapnasingh4991
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to check if the
// number is a perfect square
static bool isPerfectSquare(double x)
{

    // Find floating point value of
    // square root of x.
    double sr = Math.Sqrt(x);

    // If square root is an integer
    return ((sr - Math.Floor(sr)) == 0);
}

// Function to check if count of
// even divisors is even and count
// of odd divisors is odd
static void checkFactors(int x)
{
    if (isPerfectSquare(x))
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver code
public static void Main(String[] args)
{
    int N = 36;

    checkFactors(N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript implementation of the
// above approach

// Function to check if the
// number is a perfect square
function isPerfectSquare(x)
{
    sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0);
}

// Function to check
// if count of even divisors is even
// and count of odd divisors is odd
function checkFactors(N)
{
    if (isPerfectSquare(N))
        document.write("Yes" + "<br>");
    else
        document.write("No" + "<br>");
}

// Driver Code

    N = 36;

    checkFactors(N);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
Yes
```