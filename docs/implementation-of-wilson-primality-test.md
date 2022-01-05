# 威尔逊素性检验的实现

> 原文:[https://www . geeksforgeeks . org/implementation-of-Wilson-primality-test/](https://www.geeksforgeeks.org/implementation-of-wilson-primality-test/)

给定一个数字 N，任务是使用[威尔逊素性测试](https://www.geeksforgeeks.org/wilsons-theorem/)检查它是否是素的。如果数字是质数，则打印“1”，否则打印“0”。
威尔逊定理指出自然数 p > 1 是素数的当且仅当

```
    (p - 1) ! ≡  -1   mod p 
OR  (p - 1) ! ≡  (p-1) mod p
```

**示例:**

```
Input: p = 5
Output: Yes
(p - 1)! = 24
24 % 5  = 4

Input: p = 7
Output: Yes
(p-1)! = 6! = 720
720 % 7  = 6
```

下面是威尔逊素性检验的实现

## C++

```
// C++ implementation to check if a number is
// prime or not using Wilson Primality Test
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the factorial
long fact(const int& p)
{
    if (p <= 1)
        return 1;
    return p * fact(p - 1);
}

// Function to check if the
// number is prime or not
bool isPrime(const int& p)
{
    if (p == 4)
        return false;
    return bool(fact(p >> 1) % p);
}

// Driver code
int main()
{
    cout << isPrime(127);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if a number is 
// prime or not using Wilson Primality Test
public class Main
{
    // Function to calculate the factorial
    public static long fact(int p)
    {
        if (p <= 1)
            return 1;
        return p * fact(p - 1);
    }

    // Function to check if the
    // number is prime or not
    public static long isPrime(int p)
    {
        if (p == 4)
            return 0;
        return (fact(p >> 1) % p);
    }

    public static void main(String[] args) {
        if(isPrime(127) == 0)
        {
            System.out.println(0);
        }
        else{
            System.out.println(1);
        }
    }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 implementation to check if a number is
# prime or not using Wilson Primality Test

# Function to calculate the factorial
def fact(p):

    if (p <= 1):
        return 1

    return p * fact(p - 1)

# Function to check if the
# number is prime or not
def isPrime(p):

    if (p == 4):
        return 0

    return (fact(p >> 1) % p)

# Driver code
if (isPrime(127) == 0):
    print(0)
else:
    print(1)

# This code is contributed by rag2127
```

## C#

```
// C# implementation to check if a number is 
// prime or not using Wilson Primality Test
using System;
class GFG {

    // Function to calculate the factorial
    static long fact(int p)
    {
        if (p <= 1)
            return 1;
        return p * fact(p - 1);
    }

    // Function to check if the
    // number is prime or not
    static long isPrime(int p)
    {
        if (p == 4)
            return 0;
        return (fact(p >> 1) % p);
    }

  static void Main() {
    if(isPrime(127) == 0)
    {
        Console.WriteLine(0);
    }
    else{
        Console.WriteLine(1);
    }
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
    // Javascript implementation to check if a number is
    // prime or not using Wilson Primality Test

    // Function to calculate the factorial
    function fact(p)
    {
        if (p <= 1)
            return 1;
        return p * fact(p - 1);
    }

    // Function to check if the
    // number is prime or not
    function isPrime(p)
    {
        if (p == 4)
            return false;

          if(fact(p >> 1) % p == 0)
        {
            return 0;
        }

        return 1;
    }

    document.write(isPrime(127));

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
1
```

**它是如何工作的？**

1.  我们可以快速检查 p = 2 或 p = 3 的结果。
2.  对于 p > 3:如果 p 是复合的，那么它的正整数除数在整数 1，2，3，4，…，p-1 之间，很明显 **gcd((p-1)！，p) > 1** ，所以我们可以没有(p-1)！= -1 (mod p)。
3.  现在让我们看看当 p 是素数时，它是如何精确地为-1 的。如果 p 是素数，那么[1，p-1]中的所有数相对于 p 都是素数，并且对于范围[2，p-2]中的每个数 x，必须存在一对 y，使得(x*y)%p = 1。因此

```
    [1 * 2 * 3 * ... (p-1)]%p 
 =  [1 * 1 * 1 ... (p-1)] // Group all x and y in [2..p-2] 
                          // such that (x*y)%p = 1
 = (p-1)
```