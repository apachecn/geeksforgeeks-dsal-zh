# 求给定数阶乘的最后两位数字

> 原文:[https://www . geeksforgeeks . org/find-给定数字的因子的最后两位数/](https://www.geeksforgeeks.org/find-the-last-two-digits-of-factorial-of-a-given-number/)

给定一个整数 **N** ，任务是找到一个数的[阶乘的最后两位数字。
**例:**](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/) 

> **输入:**N = 7
> T3】输出:40
> T6】说明: 7！= 5040
> **输入:** N = 11
> **输出:** 00

**方法:**我们可以观察到对于 **N > = 10** ，其阶乘的最后两个位置将只包含 0。遂 **N！任何 **N > = 10** 的% 100** 将始终为 0。所以我们只计算阶乘 if **N < 10** 并提取最后两位数。
以下是上述方法的实施:

## C++

```
// C++ implementation to
// find last two digits
// factorial of a given number

#include <bits/stdc++.h>
using namespace std;

// Function to print the
// last two digits of N!
void lastTwoDigits(long long N)
{

    // For N >= 10, N! % 100
    // will always be 0
    if (N >= 10) {
        cout << "00";
        return;
    }

    long long fac = 1;
    // Calculating N! % 100
    for (int i = 1; i <= N; i++)
        fac = (fac * i) % 100;

    cout << fac;
}

// Driver code
int main()
{
    int N = 7;
    lastTwoDigits(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// find last two digits
// factorial of a given number
import java.util.*;
class GFG{

// Function to print the
// last two digits of N!
static void lastTwoDigits(double N)
{

    // For N >= 10, N! % 100
    // will always be 0
    if (N >= 10)
    {
        System.out.print("00");
        return;
    }

    double fac = 1;

    // Calculating N! % 100
    for (int i = 1; i <= N; i++)
        fac = (fac * i) % 100;

    System.out.print(fac);
}

// Driver code
public static void main(String args[])
{
    int N = 7;
    lastTwoDigits(N);
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation to
# find last two digits
# factorial of a given number

# Function to print the
# last two digits of N!
def lastTwoDigits(N):

    # For N >= 10, N! % 100
    # will always be 0
    if (N >= 10):
        print("00", end = "")
        return

    fac = 1

    # Calculating N! % 100
    for i in range(1, N + 1):
        fac = (fac * i) % 100

    print(fac)

# Driver code
if __name__ == '__main__':
    N = 7
    lastTwoDigits(N)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation to
// find last two digits
// factorial of a given number
using System;
class GFG{

// Function to print the
// last two digits of N!
static void lastTwoDigits(double N)
{

    // For N >= 10, N! % 100
    // will always be 0
    if (N >= 10)
    {
        Console.Write("00");
        return;
    }

    double fac = 1;

    // Calculating N! % 100
    for (int i = 1; i <= N; i++)
        fac = (fac * i) % 100;

    Console.Write(fac);
}

// Driver code
public static void Main()
{
    int N = 7;
    lastTwoDigits(N);
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>

// JavaScript implementation to
// find last two digits of
// factorial of a given number

// Function to print the
// last two digits of N!
function lastTwoDigits(N)
{

    // For N >= 10, N! % 100
    // will always be 0
    if (N >= 10) {
        cout << "00";
        return;
    }

    let fac = 1;
    // Calculating N! % 100
    for (let i = 1; i <= N; i++)
        fac = (fac * i) % 100;

    document.write(fac);
}

// Driver code
    let N = 7;
    lastTwoDigits(N);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
40
```