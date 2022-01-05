# 求一个自然数所有除数之和

> 原文:[https://www . geesforgeks . org/find-sum-除数-除数-自然数/](https://www.geeksforgeeks.org/find-sum-divisors-divisors-natural-number/)

给定一个自然数 **n** ，任务是求 n 的所有除数之和。

**示例:**

```
Input : n = 54
Output : 232
Divisors of 54 = 1, 2, 3, 6, 9, 18, 27, 54.
Sum of divisors of 1, 2, 3, 6, 9, 18, 27, 54 
are 1, 3, 4, 12, 13, 39, 40, 120 respectively.
Sum of divisors of all the divisors of 54 = 
1 + 3 + 4 + 12 + 13 + 39 + 40 + 120 = 232.

Input : n = 10
Output : 28
Divisors of 10 are 1, 2, 5, 10
Sums of divisors of divisors are 
1, 3, 6, 18.
Overall sum = 1 + 3 + 6 + 18 = 28
```

利用任意数 **n** 可以表示为质因数的乘积这一事实，**n**= p<sub>1</sub>T6】k1x p<sub>2</sub>T10】k2x…其中 p <sub>1</sub> ，p <sub>2</sub> ，…都是质数。
n 的所有除数可以表示为 p<sub>1</sub>T19】ax p<sub>2</sub>T23】bx…，其中 0 < = a < = k1，0 < = b < = k2。
现在除数之和将是 p<sub>1</sub>–p<sub>1</sub>T30】0，p<sub>1</sub>T34】1，…。，p<sub>1</sub>T38】k1 乘以 p<sub>2</sub>–p<sub>2</sub>T44】0，p<sub>2</sub>T48】1，…。，p<sub>2</sub>T52】k1T54】n
除数之和=(p<sub>1</sub>T58】0x p<sub>2</sub>T62】0)+(p<sub>1</sub>T66】1x p<sub>2</sub>T70】0)+…..+(p<sub>1</sub>T74】k1x p<sub>2</sub>T78】0)+…。+(p<sub>1</sub>T82】0x p<sub>2</sub>T86】1)+(p<sub>1</sub>T90】1x p<sub>2</sub>T94】1)+…..+(p<sub>1</sub><sup>k1</sup>x p<sub>2</sub><sup>1</sup>)+……..+
(p<sub>1</sub><sup>0</sup>x p<sub>2</sub><sup>k2</sup>)+(p<sub>1</sub>T115】1x p<sub>2</sub><sup>k2</sup>)+……+(p<sub>1</sub>T123】k1x p
=(p<sub>1</sub>T132】0+p<sub>1</sub>T136】1+…+p<sub>1</sub>T140】k1x p<sub>2</sub>T144】0+(p<sub>1</sub>T148】0+p+(p<sub>1</sub><sup>0</sup>+p<sub>1</sub><sup>1</sup>+…+p<sub>1</sub><sup>k1</sup>)x p<sub>2</sub><sup>k2</sup>。
=(p<sub>1</sub>T181】0+p<sub>1</sub>T185】1+…+p<sub>1</sub>T189】k1x(p<sub>2</sub>T193】0+p<sub>2</sub>T197】1

现在，任何 p <sup>a</sup> 的除数，对于 p 为素数，为 p <sup>0</sup> ，p <sup>1</sup> ，……，p <sup>a</sup> 。而除数之和将是(p<sup>(a+1)</sup>–1)/(p-1)，让它用 f(p)来定义。
那么，所有除数的除数之和将是，
=(f(p<sub>1</sub><sup>0</sup>)+f(p<sub>1</sub><sup>1</sup>)+…+f(p<sub>1</sub>T22】k1)x(f(p<sub>2</sub><sup>0</sup>)+f(p<sub>2</sub>T30

所以，给定一个数 n，通过质因数分解，我们可以求出所有除数的和。但是在这个问题中，我们得到 n 是数组元素的乘积。所以，找出每个元素的素因子分解，并利用事实 a<sup>b</sup>x a<sup>c</sup>= a<sup>b+ c</sup>。

下面是该方法的实现:

## C++

```
// C++ program to find sum of divisors of all
// the divisors of a natural number.
#include<bits/stdc++.h>
using namespace std;

// Returns sum of divisors of all the divisors
// of n
int sumDivisorsOfDivisors(int n)
{
    // Calculating powers of prime factors and
    // storing them in a map mp[].
    map<int, int> mp;
    for (int j=2; j<=sqrt(n); j++)
    {
        int count = 0;
        while (n%j == 0)
        {
            n /= j;
            count++;
        }

        if (count)
            mp[j] = count;
    }

    // If n is a prime number
    if (n != 1)
        mp[n] = 1;

    // For each prime factor, calculating (p^(a+1)-1)/(p-1)
    // and adding it to answer.
    int ans = 1;
    for (auto it : mp)
    {
        int pw = 1;
        int sum = 0;

        for (int i=it.second+1; i>=1; i--)
        {
            sum += (i*pw);
            pw *= it.first;
        }
        ans *= sum;
    }

    return ans;
}

// Driven Program
int main()
{
    int n = 10;
    cout << sumDivisorsOfDivisors(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of divisors of all
// the divisors of a natural number.
import java.util.HashMap;

class GFG
{

    // Returns sum of divisors of all the divisors
    // of n
    public static int sumDivisorsOfDivisors(int n)
    {

        // Calculating powers of prime factors and
        // storing them in a map mp[].
        HashMap<Integer, Integer> mp = new HashMap<>();
        for (int j = 2; j <= Math.sqrt(n); j++)
        {
            int count = 0;
            while (n % j == 0)
            {
                n /= j;
                count++;
            }
            if (count != 0)
                mp.put(j, count);
        }

        // If n is a prime number
        if (n != 1)
            mp.put(n, 1);

        // For each prime factor, calculating (p^(a+1)-1)/(p-1)
        // and adding it to answer.
        int ans = 1;

        for (HashMap.Entry<Integer, Integer> entry : mp.entrySet())
        {
            int pw = 1;
            int sum = 0;
            for (int i = entry.getValue() + 1; i >= 1; i--)
            {
                sum += (i * pw);
                pw = entry.getKey();
            }
            ans *= sum;
        }

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 10;
        System.out.println(sumDivisorsOfDivisors(n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find sum of divisors
# of all the divisors of a natural number.
import math as mt

# Returns sum of divisors of all
# the divisors of n
def sumDivisorsOfDivisors(n):

    # Calculating powers of prime factors
    # and storing them in a map mp[].
    mp = dict()
    for j in range(2, mt.ceil(mt.sqrt(n))):

        count = 0
        while (n % j == 0):
            n //= j
            count += 1

        if (count):
            mp[j] = count

    # If n is a prime number
    if (n != 1):
        mp[n] = 1

    # For each prime factor, calculating
    # (p^(a+1)-1)/(p-1) and adding it to answer.
    ans = 1
    for it in mp:
        pw = 1
        summ = 0

        for i in range(mp[it] + 1, 0, -1):
            summ += (i * pw)
            pw *= it

        ans *= summ

    return ans

# Driver Code
n = 10
print(sumDivisorsOfDivisors(n))

# This code is contributed
# by mohit kumar 29
```

## C#

```
// C# program to find sum of divisors of all
// the divisors of a natural number.
using System;
using System.Collections.Generic;

class GFG
{

    // Returns sum of divisors of
    // all the divisors of n
    public static int sumDivisorsOfDivisors(int n)
    {

        // Calculating powers of prime factors and
        // storing them in a map mp[].
        Dictionary<int,
                   int> mp = new Dictionary<int,
                                            int>();
        for (int j = 2; j <= Math.Sqrt(n); j++)
        {
            int count = 0;
            while (n % j == 0)
            {
                n /= j;
                count++;
            }
            if (count != 0)
                mp.Add(j, count);
        }

        // If n is a prime number
        if (n != 1)
            mp.Add(n, 1);

        // For each prime factor,
        // calculating (p^(a+1)-1)/(p-1)
        // and adding it to answer.
        int ans = 1;

        foreach(KeyValuePair<int, int> entry in mp)
        {
            int pw = 1;
            int sum = 0;
            for (int i = entry.Value + 1;
                     i >= 1; i--)
            {
                sum += (i * pw);
                pw = entry.Key;
            }
            ans *= sum;
        }

        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 10;
        Console.WriteLine(sumDivisorsOfDivisors(n));
    }
}

// This code is contributed
// by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program to find sum of divisors of all
// the divisors of a natural number.

     // Returns sum of divisors of all the divisors
    // of n
    function sumDivisorsOfDivisors(n)
    {
        // Calculating powers of prime factors and
        // storing them in a map mp[].
        let mp = new Map();
        for (let j = 2; j <= Math.sqrt(n); j++)
        {
            let count = 0;
            while (n % j == 0)
            {
                n = Math.floor(n/j);
                count++;
            }
            if (count != 0)
                mp.set(j, count);
        }

        // If n is a prime number
        if (n != 1)
            mp.set(n, 1);

        // For each prime factor, calculating (p^(a+1)-1)/(p-1)
        // and adding it to answer.
        let ans = 1;

        for (let [key, value] of mp.entries())
        {
            let pw = 1;
            let sum = 0;
            for (let i = value + 1; i >= 1; i--)
            {
                sum += (i * pw);
                pw = key;
            }
            ans *= sum;
        }

        return ans;
    }

    // Driver code
    let n = 10;
    document.write(sumDivisorsOfDivisors(n));

// This code is contributed by patel2127
</script>
```

**输出:**

```
28
```

**优化:**
对于有多个需要求值的输入的情况，可以使用本帖[中讨论的](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/)[厄拉多塞](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)筛。

本文由 [**Anuj Chauhan**](https://web.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。