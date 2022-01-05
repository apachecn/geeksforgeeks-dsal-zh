# 求位计数的幂次加到幂次 B 的和

> 原文:[https://www . geeksforgeeks . org/find-位计数的幂之和-升至 b 的幂/](https://www.geeksforgeeks.org/find-the-sum-of-power-of-bit-count-raised-to-the-power-b/)

给定一个整数，数组 A .求 A[i]中每个元素的集合位的和，其幂为 A[i]。
**例:**

```
Input: N = 3, A[] = {1, 2, 3}
Output: 10
Explanation:
Set bit of each array element is
1 = 1 set bit, 
2 = 1 set bit, 
3 = 2 set bit 
store each set bit in b[i].
Compute sum of power(b[i], i) 
where i is ranging from 1 to n.
that is sum = power(1, 1)+
power(1, 2)+power(2, 3) = 10

Input: N = 4, A[] = {2, 4, 5, 3}
Output: 42
```

**方法:**
我们可以使用[模幂](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)方法来计算 mod m 下的 a^b，并内置 __builtin_popcount 函数来计算 A[i]的二进制表示中的设置位数。
以下是上述办法的实施情况。

## C++

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate a^b mod m
// using fast-exponentiation method
int fastmod(int base, int exp, int mod)
{
    if (exp == 0)
      return 1;
    else if (exp % 2 == 0) {
      int ans = fastmod(base, exp / 2, mod);
      return (ans % mod * ans % mod) % mod;
    }
    else
      return (fastmod(base, exp - 1, mod) % mod * base % mod) % mod;
}

// Function to
// calculate sum
int findPowerSum(int n, int ar[])
{

    const int mod = 1e9 + 7;
    int sum = 0;

    // Iterate for all
    // values of array A
    for (int i = 0; i < n; i++) {
        int base = __builtin_popcount(ar[i]);
        int exp = ar[i];
        // Calling fast-exponentiation and
        // appending ans to sum
        sum += fastmod(base, exp, mod);
        sum %= mod;
    }

    return sum;
}

// Driver code.
int main()
{
    int n = 3;
    int ar[] = { 1, 2, 3 };
    cout << findPowerSum(n, ar);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

    // Function to calculate a^b mod m
    // using fast-exponentiation method
    static int fastmod(int base, int exp, int mod)
    {
        if (exp == 0)
        return 1;
        else if (exp % 2 == 0)
        {
            int ans = fastmod(base, exp / 2, mod);
            return (ans % mod * ans % mod) % mod;
        }
        else
            return (fastmod(base, exp - 1, mod) %
                        mod * base % mod) % mod;
    }

    /* Function to get no of set
    bits in binary representation
    of positive integer n */
    static int countSetBits(int n)
    {
        int count = 0;
        while (n > 0)
        {
            count += n & 1;
            n >>= 1;
        }
        return count;
    }

    // Function to calculate sum
    static int findPowerSum(int n, int ar[])
    {

        final int mod = (int)1e9 + 7;
        int sum = 0;

        // Iterate for all
        // values of array A
        for (int i = 0; i < n; i++)
        {
            int base = countSetBits(ar[i]);
            int exp = ar[i];

            // Calling fast-exponentiation and
            // appending ans to sum
            sum += fastmod(base, exp, mod);
            sum %= mod;
        }

        return sum;
    }

    // Driver code.
    public static void main (String[] args)
    {
        int n = 3;
        int ar[] = { 1, 2, 3 };
        System.out.println(findPowerSum(n, ar));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate a^b mod m
# using fast-exponentiation method
def fastmod(base, exp, mod) :

    if (exp == 0) :
        return 1;

    elif (exp % 2 == 0) :
        ans = fastmod(base, exp / 2, mod);

        return (ans % mod * ans % mod) % mod;

    else :
        return (fastmod(base, exp - 1, mod)
                % mod * base % mod) % mod;

# Function to
# calculate sum
def findPowerSum(n, ar) :

    mod = int(1e9) + 7;
    sum = 0;

    # Iterate for all values of array A
    for i in range(n) :
        base = bin(ar[i]).count('1');
        exp = ar[i];

        # Calling fast-exponentiation and
        # appending ans to sum
        sum += fastmod(base, exp, mod);
        sum %= mod;

    return sum;

# Driver code.
if __name__ == "__main__" :

    n = 3;
    ar = [ 1, 2, 3 ];

    print(findPowerSum(n, ar));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function to calculate a^b mod m
    // using fast-exponentiation method
    static int fastmod(int baseval, int exp, int mod)
    {
        if (exp == 0)
            return 1;
        else if (exp % 2 == 0)
        {
            int ans = fastmod(baseval, exp / 2, mod);
            return (ans % mod * ans % mod) % mod;
        }
        else
            return (fastmod(baseval, exp - 1, mod) %
                        mod * baseval % mod) % mod;
    }

    /* Function to get no of set
    bits in binary representation
    of positive integer n */
    static int countSetBits(int n)
    {
        int count = 0;
        while (n > 0)
        {
            count += n & 1;
            n >>= 1;
        }
        return count;
    }

    // Function to calculate sum
    static int findPowerSum(int n, int []ar)
    {

        int mod = (int)1e9 + 7;
        int sum = 0;

        // Iterate for all
        // values of array A
        for (int i = 0; i < n; i++)
        {
            int baseval = countSetBits(ar[i]);
            int exp = ar[i];

            // Calling fast-exponentiation and
            // appending ans to sum
            sum += fastmod(baseval, exp, mod);
            sum %= mod;
        }

        return sum;
    }

    // Driver code.
    public static void Main ()
    {
        int n = 3;
        int []ar = { 1, 2, 3 };
        Console.WriteLine(findPowerSum(n, ar));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript program for the above approach    
// Function to calculate a^b mod m
    // using fast-exponentiation method
    function fastmod(base , exp , mod)
    {
        if (exp == 0)
            return 1;
        else if (exp % 2 == 0)
        {
            var ans = fastmod(base, exp / 2, mod);
            return (ans % mod * ans % mod) % mod;
        } else
            return (fastmod(base, exp - 1, mod) % mod * base % mod) % mod;
    }

    /*
     * Function to get no of set bits in binary representation of positive integer n
     */
    function countSetBits(n)
    {
        var count = 0;
        while (n > 0)
        {
            count += n & 1;
            n >>= 1;
        }
        return count;
    }

    // Function to calculate sum
    function findPowerSum(n , ar)
    {

         var mod = parseInt( 1e9 + 7);
        var sum = 0;

        // Iterate for all
        // values of array A
        for (i = 0; i < n; i++) {
            var base = countSetBits(ar[i]);
            var exp = ar[i];

            // Calling fast-exponentiation and
            // appending ans to sum
            sum += fastmod(base, exp, mod);
            sum %= mod;
        }

        return sum;
    }

    // Driver code
        var n = 3;
        var ar = [ 1, 2, 3 ];
        document.write(findPowerSum(n, ar));

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
10
```

**时间复杂度:** O(n*log(n))
**辅助空间:** O(1)