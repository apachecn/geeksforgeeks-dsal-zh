# 计算一个数 N 的所有除数对，该数 N 的和与 N 同素

> 原文:[https://www . geesforgeks . org/count-all-对-数-n-的除数，其和是-n 的互素/](https://www.geeksforgeeks.org/count-all-pairs-of-divisors-of-a-number-n-whose-sum-is-coprime-with-n/)

给定一个整数 **N** ，任务是对 **N** 的所有除数对进行计数，使得每对之和与 **N** 互素。
**举例:**

> **输入:** N = 24
> **输出:** 2
> **解释:**
> 有 2 对(1，24)和(2，3)和 24
> **输入:** 105
> **输出:** 4
> **解释:**
> 有 4 对(1，105)、(3，35)、(5，5)

**方法:**
解决上述问题，我们可以通过 **√N** 复杂度中 [**求所有除数**](https://contribute.geeksforgeeks.org/geek/count-the-number-of-ordered-sets-not-containing-consecutive-numbers-3/) 轻松计算出结果，并检查每一对的和是否与 **N** 同素。
以下是上述方法的实施:

## C++

```
// C++ program to count all pairs
// of divisors such that their sum
// is coprime with N
#include <bits/stdc++.h>
using namespace std;

// Function to calculate GCD
int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return (gcd(b, a % b));
}

// Function to count all valid pairs
int CountPairs(int n)
{

    // Initialize count
    int cnt = 0;

    for (int i = 1; i * i <= n; i++) {
        if (n % i == 0) {
            int div1 = i;

            int div2 = n / i;

            int sum = div1 + div2;

            // Check if sum of pair
            // and n are coprime
            if (gcd(sum, n) == 1)

                cnt += 1;
        }
    }

    // Return the result
    return cnt;
}

// Driver code
int main()
{

    int n = 24;

    cout << CountPairs(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all pairs
// of divisors such that their sum
// is coprime with N
import java.util.*;

class GFG{

// Function to calculate GCD
public static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return (gcd(b, a % b));
}

// Function to count all valid pairs
public static int CountPairs(int n)
{

    // Initialize count
    int cnt = 0;

    for(int i = 1; i * i <= n; i++)
    {
       if (n % i == 0)
       {
           int div1 = i;
           int div2 = n / i;
           int sum = div1 + div2;

           // Check if sum of pair
           // and n are coprime
           if (gcd(sum, n) == 1)
               cnt += 1;
       }
    }

    // Return the result
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int n = 24;

    System.out.println(CountPairs(n));
}
}

// This code is contributed by equbalzeeshan
```

## 蟒蛇 3

```
# Python3 program to count all pairs
# of divisors such that their sum
# is coprime with N
import math as m

# Function to count all valid pairs
def CountPairs(n):

    # initialize count
    cnt = 0

    i = 1

    while i * i <= n :

        if(n % i == 0):

            div1 = i
            div2 = n//i

            sum = div1 + div2;

            # Check if sum of pair
            # and n are coprime
            if( m.gcd(sum, n) == 1):
                cnt += 1

        i += 1

    # Return the result
    return cnt

# Driver code
n = 24

print(CountPairs(n))
```

## C#

```
// C# program to count all pairs of
// divisors such that their sum
// is coprime with N
using System;

class GFG {

    // Function to find gcd of a and b
    static int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function to count all valid pairs
    static int CountPairs(int n)
    {

        // Initialize count
        int cnt = 0;

        for (int i = 1; i * i <= n; i++) {
            if (n % i == 0) {
                int div1 = i;

                int div2 = n / i;

                int sum = div1 + div2;

                // Check if sum of pair
                // and n are coprime
                if (gcd(sum, n) == 1)
                    cnt += 1;
            }
        }
        // Return the result
        return cnt;
    }

    // Driver method
    public static void Main()
    {
        int n = 24;

        Console.WriteLine(CountPairs(n));
    }
}
```

## java 描述语言

```
<script>

// JavaScript program to count all pairs
// of divisors such that their sum
// is coprime with N

// Function to calculate GCD
function gcd(a, b)
{
    if (b == 0)
        return a;

    return (gcd(b, a % b));
}

// Function to count all valid pairs
function CountPairs(n)
{

    // Initialize count
    let cnt = 0;

    for (let i = 1; i * i <= n; i++) {
        if (n % i == 0) {
            let div1 = i;

            let div2 = Math.floor(n / i);

            let sum = div1 + div2;

            // Check if sum of pair
            // and n are coprime
            if (gcd(sum, n) == 1)

                cnt += 1;
        }
    }

    // Return the result
    return cnt;
}

// Driver code
    let n = 24;

    document.write(CountPairs(n) + "<br>");

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(√N * log(N))*