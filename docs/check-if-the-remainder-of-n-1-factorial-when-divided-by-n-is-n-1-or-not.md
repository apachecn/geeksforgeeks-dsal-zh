# 检查 N-1 阶乘除以 N 的余数是否为 N-1

> 原文:[https://www . geesforgeks . org/check-n-1 的余数除以 n-is-n-1-or-not/](https://www.geeksforgeeks.org/check-if-the-remainder-of-n-1-factorial-when-divided-by-n-is-n-1-or-not/)

给定一个整数 **N** ，其中**1≤N≤10<sup>5</sup>T5】，任务是查找 **(N-1)！% N = N–1**与否。
**示例:****

> **输入:** N = 3
> **输出:**是
> **说明:**
> 这里 N = 3 so(3–1)！= 2!= 2
> = > 2 % 3 = 2 也就是 N–1 本身
> **输入:** N = 4
> **输出:** No
> **说明:**
> 这里 N = 4 so(4–1)！= 3!= 6
> = > 6 % 3 = 0，不是 N–1。

**天真法:**解决上面提到的问题，天真法就是找(N–1)！并检查是否(N-1)！% N = N–1 或不是。但是这种方法会导致溢出，因为 **1 ≤ N ≤ 10 <sup>5</sup>**
**有效方法:**为了以最佳方式解决上述问题，我们将使用 [**威尔逊定理**](https://www.geeksforgeeks.org/wilsons-theorem/) ，该定理指出自然数 p > 1 是素数的当且仅当

> (p–1)！≦-1 mod p
> 或；(p–1)！(p-1)国防部

所以，现在我们只需要检查 N 是否是素数(包括 1)。

下面是上述方法的实现:

## C++

```
// C++ implementation to check
// the following expression for
// an integer N is valid or not
#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// holds the condition
// (N-1)! % N = N - 1
bool isPrime(int n)
{
    // Corner cases
    if (n == 1)
        return true;
    if (n <= 3)
        return true;

    // Number divisible by 2
    // or 3 are not prime
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Iterate from 5 and keep
    // checking for prime
    for (int i = 5; i * i <= n; i = i + 6)

        if (n % i == 0
            || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check the
// expression for the value N
void checkExpression(int n)
{
    if (isPrime(n))
        cout << "Yes";
    else
        cout << "No";
}

// Driver Program
int main()
{
    int N = 3;
    checkExpression(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// the following expression for
// an integer N is valid or not
class GFG{

// Function to check if a number
// holds the condition
// (N-1)! % N = N - 1
static boolean isPrime(int n)
{

    // Corner cases
    if (n == 1)
        return true;
    if (n <= 3)
        return true;

    // Number divisible by 2
    // or 3 are not prime
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Iterate from 5 and keep
    // checking for prime
    for(int i = 5; i * i <= n; i = i + 6)
       if (n % i == 0 || n % (i + 2) == 0)
           return false;

    return true;
}

// Function to check the
// expression for the value N
static void checkExpression(int n)
{
    if (isPrime(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver code
public static void main(String[] args)
{
    int N = 3;

    checkExpression(N);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 implementation to check
# the following expression for
# an integer N is valid or not

# Function to check if a number
# holds the condition
# (N-1)! % N = N - 1
def isPrime(n):

    # Corner cases
    if (n == 1):
        return True
    if (n <= 3):
        return True

    # Number divisible by 2
    # or 3 are not prime
    if ((n % 2 == 0) or (n % 3 == 0)):
        return False

    # Iterate from 5 and keep
    # checking for prime
    i = 5
    while (i * i <= n):
        if ((n % i == 0) or
            (n % (i + 2) == 0)):
            return False;
            i += 6

    return true;

# Function to check the
# expression for the value N
def checkExpression(n):

    if (isPrime(n)):
        print("Yes")
    else:
        print("No")

# Driver code
if __name__ == '__main__':

    N = 3

    checkExpression(N)

# This code is contributed by jana_sayantan
```

## C#

```
// C# implementation to check
// the following expression for
// an integer N is valid or not
using System;
class GFG{

// Function to check if a number
// holds the condition
// (N-1)! % N = N - 1
static bool isPrime(int n)
{

    // Corner cases
    if (n == 1)
        return true;
    if (n <= 3)
        return true;

    // Number divisible by 2
    // or 3 are not prime
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Iterate from 5 and keep
    // checking for prime
    for(int i = 5; i * i <= n; i = i + 6)
       if (n % i == 0 || n % (i + 2) == 0)
           return false;

    return true;
}

// Function to check the
// expression for the value N
static void checkExpression(int n)
{
    if (isPrime(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver code
public static void Main()
{
    int N = 3;

    checkExpression(N);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

    // Javascript implementation to check
    // the following expression for
    // an integer N is valid or not

    // Function to check if a number
    // holds the condition
    // (N-1)! % N = N - 1
    function isPrime(n)
    {
        // Corner cases
        if (n == 1)
            return true;
        if (n <= 3)
            return true;

        // Number divisible by 2
        // or 3 are not prime
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        // Iterate from 5 and keep
        // checking for prime
        for (let i = 5; i * i <= n; i = i + 6)

            if (n % i == 0
                || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Function to check the
    // expression for the value N
    function checkExpression(n)
    {
        if (isPrime(n))
            document.write("Yes");
        else
            document.write("No");
    }

    let N = 3;
    checkExpression(N);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(sqrt(N))*