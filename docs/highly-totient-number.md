# 全能型号码

> 原文:[https://www.geeksforgeeks.org/highly-totient-number/](https://www.geeksforgeeks.org/highly-totient-number/)

高度全能数 k 是对方程φ(x) = k 有更多解的整数，其中φ是[欧拉全能函数](https://www.geeksforgeeks.org/eulers-totient-function/)
**顺序:**

> 1、2、4、8、12、24、48、72、144、240、432、480、576、720、1152、1440、2880、4320、5760、8640

**说明:**

*   1 有 2 个解决方案
*   2 有 3 个解决方案
*   4 有 4 个解决方案
*   8 有 5 个解决方案
*   12 有 6 个解决方案
*   24 有 10 个解决方案

对于给定的 **N** ，任务是首先打印 **N** 个全能型数字。
**例:**

> **输入:** N = 10
> **输出:** 1、2、4、8、12、24、48、72、144、240
> **输入:** N = 20
> **输出:** 1、2、4、8、12、24、48、72、144、240、432、480、576、720、1152、115

**方法:**
一种有效的方法是将 **φ(x)** 直到 **10 <sup>5</sup>** 的所有值连同它们的频率一起存储在地图中，然后从 **1** 运行一个循环，直到高全能数的计数小于 **N** 。对于每个 **i** 我们将检查 **i** 的频率是否大于前一个元素，如果是，则打印数字并增加计数，否则增加数字。
以下是上述方法的实施:

## C++

```
// CPP program to find highly totient numbers
#include <bits/stdc++.h>
using namespace std;

// Function to find euler totient number
int phi(int n)
{
    int result = n; // Initialize result as n

    // Consider all prime factors of n and
    // subtract their multiples from result
    for (int p = 2; p * p <= n; ++p) {

        // Check if p is a prime factor.
        if (n % p == 0) {

            // If yes, then update n and result
            while (n % p == 0)
                n /= p;
            result -= result / p;
        }
    }

    // If n has a prime factor greater than sqrt(n)
    // (There can be at-most one such prime factor)
    if (n > 1)
        result -= result / n;
    return result;
}

// Function to find first n highly totient numbers
void Highly_Totient(int n)
{
    // Count of Highly totient numbers
    // and value of count of phi of previous numbers
    int count = 0, p_count = -1, i = 1;

    // Store all the values of phi(x) upto
    // 10^5 with frequencies
    map<int, int> mp;

    for (int i = 1; i < 100000; i++)
        mp[phi(i)]++;

    while (count < n) {

        // If count is greater than count of
        // previous element
        if (mp[i] > p_count)
        {
            // Display the number
            cout << i;

            if(count < n-1)
                cout << ", ";

            // Store the value of phi
            p_count = mp[i];
            count++;
        }
        i++;
    }
}

// Driver code
int main()
{
    int n = 20;

    // Function call
    Highly_Totient(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find highly totient numbers
import java.util.*;

class GFG
{

// Function to find euler totient number
static int phi(int n)
{
    int result = n; // Initialize result as n

    // Consider all prime factors of n and
    // subtract their multiples from result
    for (int p = 2; p * p <= n; ++p)
    {

        // Check if p is a prime factor.
        if (n % p == 0)
        {

            // If yes, then update n and result
            while (n % p == 0)
                n /= p;
            result -= result / p;
        }
    }

    // If n has a prime factor greater than sqrt(n)
    // (There can be at-most one such prime factor)
    if (n > 1)
        result -= result / n;
    return result;
}

// Function to find first n highly totient numbers
static void Highly_Totient(int n)
{
    // Count of Highly totient numbers
    // and value of count of phi of previous numbers
    int count = 0, p_count = -1;

    // Store all the values of phi(x) upto
    // 10^5 with frequencies
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    for (int i = 1; i < 100000; i++)
    {
        if(mp.containsKey(phi(i)))
        {
            mp.put(phi(i), mp.get(phi(i)) + 1);
        }
        else
        {
            mp.put(phi(i), 1);
        }
    }

    int i = 1;
    while (count < n)
    {

        // If count is greater than count of
        // previous element
        if (mp.containsKey(i)&&mp.get(i) > p_count)
        {
            // Display the number
            System.out.print(i);

            if(count < n - 1)
                System.out.print(", ");

            // Store the value of phi
            p_count = mp.get(i);
            count++;
        }
        i++;
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 20;

    // Function call
    Highly_Totient(n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find highly totient numbers

# Function to find euler totient number
def phi(n):

    result = n; # Initialize result as n

    # Consider all prime factors of n and
    # subtract their multiples from result
    p = 2

    while(p*p <= n):

        # Check if p is a prime factor.
        if (n % p == 0):

            # If yes, then update n and result
            while (n % p == 0):
                n //= p;
            result -= (result // p);
        p += 1

    # If n has a prime factor greater than sqrt(n)
    # (There can be at-most one such prime factor)
    if (n > 1):
        result -= (result // n);
    return result;

# Function to find first n highly totient numbers
def Highly_Totient(n):

    # Count of Highly totient numbers
    # and value of count of phi of previous numbers
    count = 0
    p_count = -1

    # Store all the values of phi(x) upto
    # 10^5 with frequencies
    mp = dict()
    i = 1

    while i < 100000:

        tmp = phi(i)

        if tmp not in mp:
            mp[tmp] = 0
        mp[tmp] += 1;
        i += 1
    i = 1

    while (count < n):

        # If count is greater than count of
        # previous element
        if ((i in mp) and  mp[i] > p_count):

            # Display the number
            print(i, end = '');

            if(count < n - 1):
                print(", ", end = '');

            # Store the value of phi
            p_count = mp[i];
            count += 1
        i += 1

# Driver code
if __name__=='__main__':

    n = 20;

    # Function call
    Highly_Totient(n);

    # This code is contributed by rutvik_56
```

## C#

```
// C# program to find highly totient numbers
using System;
using System.Collections.Generic;

class GFG
{

// Function to find euler totient number
static int phi(int n)
{
    int result = n; // Initialize result as n

    // Consider all prime factors of n and
    // subtract their multiples from result
    for (int p = 2; p * p <= n; ++p)
    {

        // Check if p is a prime factor.
        if (n % p == 0)
        {

            // If yes, then update n and result
            while (n % p == 0)
                n /= p;
            result -= result / p;
        }
    }

    // If n has a prime factor greater than sqrt(n)
    // (There can be at-most one such prime factor)
    if (n > 1)
        result -= result / n;
    return result;
}

// Function to find first n highly totient numbers
static void Highly_Totient(int n)
{
    // Count of Highly totient numbers
    // and value of count of phi of
    // previous numbers
    int count = 0, p_count = -1, i;

    // Store all the values of phi(x) upto
    // 10^5 with frequencies
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();
    for (i = 1; i < 100000; i++)
    {
        if(mp.ContainsKey(phi(i)))
        {
            mp[phi(i)] = mp[phi(i)] + 1;
        }
        else
        {
            mp.Add(phi(i), 1);
        }
    }

    i = 1;
    while (count < n)
    {

        // If count is greater than count of
        // previous element
        if (mp.ContainsKey(i)&&mp[i] > p_count)
        {
            // Display the number
            Console.Write(i);

            if(count < n - 1)
                Console.Write(", ");

            // Store the value of phi
            p_count = mp[i];
            count++;
        }
        i++;
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 20;

    // Function call
    Highly_Totient(n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program to find highly totient numbers

    // Function to find euler totient number
    function phi(n) {
        var result = n; // Initialize result as n

        // Consider all prime factors of n and
        // subtract their multiples from result
        for (var p = 2; p * p <= n; ++p) {

            // Check if p is a prime factor.
            if (n % p == 0) {

                // If yes, then update n and result
                while (n % p == 0)
                    n /= p;
                result -= result / p;
            }
        }

        // If n has a prime factor greater than sqrt(n)
        // (There can be at-most one such prime factor)
        if (n > 1)
            result -= result / n;
        return result;
    }

    // Function to find first n highly totient numbers
    function Highly_Totient(n)
    {

        // Count of Highly totient numbers
        // and value of count of phi of previous numbers
        var count = 0, p_count = -1;

        // Store all the values of phi(x) upto
        // 10^5 with frequencies
        var mp = new Map();

        for (i = 1; i < 100000; i++) {
            if (mp.has(phi(i))) {
                mp.set(phi(i), mp.get(phi(i)) + 1);
            } else {
                mp.set(phi(i), 1);
            }
        }

        var i = 1;
        while (count < n) {

            // If count is greater than count of
            // previous element
            if (mp.has(i) && mp.get(i) > p_count)
            {

                // Display the number
                document.write(i);

                if (count < n - 1)
                    document.write(", ");

                // Store the value of phi
                p_count = mp.get(i);
                count++;
            }
            i++;
        }
    }

    // Driver code
        var n = 20;

        // Function call
        Highly_Totient(n);

// This code is contributed by gauravrajput1
</script>
```

**输出:**

> 1、2、4、8、12、24、48、72、144、240、432、480、576、720、1152、1440、2880、4320、5760、8640

**该方法不能用于查找 1000 个以上的高度全能数。**