# 从两个不同的集合中选择一对或多对的方法

> 原文:[https://www . geesforgeks . org/从两个不同的集合中选择一对或多对的方法/](https://www.geeksforgeeks.org/ways-to-select-one-or-more-pairs-from-two-different-sets/)

给定两个正数‘n’和‘m’(n<= m) which represent total number of items of first and second type of sets respectively. Find total number of ways to select at-least one pair by picking one item from first type(I) and another item from second type(II). In any arrangement, an item should not be common between any two pairs.
**注:**由于答案可以很大，以模 **1000000007** 输出。

```
Input: 2 2
Output: 6
Explanation
Let's denote the items of I type
as a, b and II type as c, d i.e,
Type I -  a, b
Type II - c, d
Ways to arrange one pair at a time
1\. a --- c
2\. a --- d
3\. b --- c
4\. b --- d
Ways to arrange two pairs at a time
5\. a --- c, b --- d
6\. a --- d, b --- c

Input: 2 3
Output: 12

Input: 1 2
Output: 2

```

方法很简单，我们只需要从“ **n** 型中选择“ **i** 项”和从“ **m** 型中选择“ **i** 项”并将它们相乘([积法则](https://en.wikipedia.org/wiki/Rule_of_product))的组合，其中“ **i** 从 **1** 变化到“ **n** ”。但是我们也可以用“I”的方式排列结果，因此我们需要乘以 **i！**。然后取所有结果乘积的和([求和规则](https://en.wikipedia.org/wiki/Rule_of_sum))得到最终答案。

## C++

```
// C++ program to find total no. of ways
// to form a pair in two different set
#include <bits/stdc++.h>
using namespace std;

// initialize global variable so that
// it can access by preCalculate() and
// nCr() function
int* fact, *inverseMod;
const int mod = 1e9 + 7;

/* Iterative Function to calculate (x^y)%p in O(log y) */
int power(int x, int y, int p)
{
    int res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
               // equal to p

    while (y) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (1LL * res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (1LL * x * x) % p;
    } // trace(res);

    return res;
}

// Pre-calculate factorial and
// Inverse of number
void preCalculate(int n)
{
    fact[0] = inverseMod[0] = 1;
    for (int i = 1; i <= n; ++i) {

        fact[i] = (1LL * fact[i - 1] * i) % mod;
        inverseMod[i] = power(fact[i], mod - 2, mod);
    }
}

// utility function to calculate nCr
int nPr(int a, int b)
{
    return (1LL * fact[a] * inverseMod[a - b]) % mod;
}

int countWays(int n, int m)
{
    fact = new int[m + 1];
    inverseMod = new int[m + 1];

    // Pre-calculate factorial and
    // inverse of number
    preCalculate(m);

    // Initialize answer
    int ans = 0;
    for (int i = 1; i <= n; ++i) {

        ans += (1LL * ((1LL * nPr(n, i) 
                * nPr(m, i)) % mod)
                * inverseMod[i]) % mod;
        if (ans >= mod)
            ans %= mod;
    }

    return ans;
}

// Driver program
int main()
{
    int n = 2, m = 2;

    cout << countWays(n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find total
// no. of ways to form a pair
// in two different set

public class Test
{
    static long[] fact;
    static long[] inverseMod;
    static int mod=1000000007;

    /* Iterative Function to calculate 
       (x^y)%p in O(log y) */

    static long power(long x, int y, int p)
    {
        // Initialize result
        long res = 1; 

        // Update x if it is more than or
        // equal to p
        x = x % p; 

        while (y!=0)
        {

            // If y is odd, multiply 
            // x with result
            if ((y & 1)!=0)
                res = (1 * res * x) % p;
            }
            // y must be even now
            y = y >> 1; 

            x = (1 * x * x) % p;
        } 

        return res;
    }

    // Pre-calculate factorial and
    // Inverse of number
    public static void preCalculate(int n)
    {
        //int fact[]=new long[n];
        // int inverseMod[]=new long[n];
        fact[0] = 1;
        inverseMod[0] = 1;

        for (int i = 1; i <= n; i++) 
        {

                fact[i] = (1 * fact[i - 1] * i)
                                          % mod;

                inverseMod[i] = power(fact[i], 
                                  mod - 2, mod);

        }
    }

    // utility function to calculate nCr
    public static long nPr(int a, int b)
    {

        return (1 * fact[a] * inverseMod[a - b])
                                    % (long)mod;
    }

    public static int countWays(int n, int m)
    {

        fact = new long[m + 1];
        inverseMod = new long[m + 1];

        // Pre-calculate factorial and
        // inverse of number
        preCalculate(m);

        // Initialize answer
        long ans = 0;

        for (int i = 1; i <= n; i++) {

            ans = ans+(1 * ((1 * nPr(n, i)* 
                                nPr(m, i)) % mod)*
                                (inverseMod[i])) % mod;

            if (ans >= mod)
                ans %= mod;
        }

        return (int)ans;
     } 

    /* Driver program */
    public static void main(String[] args) 
    {
        int n = 2, m = 2;

        System.out.println(countWays(n, m));
    }
}

// This code is contributed by Gitanjali
```

**Output:**

```
6

```

**时间复杂度:** O(m*log(mod))
**辅助空间:** O(m)

本文由 [Shubham Bansal](https://www.quora.com/profile/Shubham-Bansal-209) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。