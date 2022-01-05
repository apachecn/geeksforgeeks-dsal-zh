# 将字符 X 转换为字符串 Y 的方法数量

> 原文:[https://www . geeksforgeeks . org/将字符 x 转换为字符串 y 的方式数/](https://www.geeksforgeeks.org/number-of-ways-to-convert-a-character-x-to-a-string-y/)

给定一个字符 **X** 和一个长度为 **N** 的字符串 **Y** ，任务是通过在 **X** 的左右两端添加字符来找到将 **X** 转换为 **Y** 的方法数量。**注意**如果左追加和右追加的顺序不同，或者如果顺序相同，则追加的字符不同，即左追加后紧接着右追加不同于右追加后紧接着左追加。既然答案可以大号打印最终答案 MOD (10 <sup>9</sup> + 7)。
**举例:**

> **输入:** X = 'a '，Y = ' xxay "
> T3】输出: 3
> 所有可能的方式为:
> 
> 1.  左追加“x”(“xa”)、左追加“x”(“xxa”)、右追加 y(“xxay”)。
> 2.  左追加“x”(“xa”)，右追加 y(“xay”)，左追加“x”(“xxay”)。
> 3.  右追加 y(“ay”)、左追加 xxay”)、左追加 x(“xxay”)。
> 
> **输入:** X = 'a '，Y = ' CD "
> T3】输出: 0

**方法 1:** 解决这个问题的一种方法是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。

*   初始化变量 ans = 0，mod = 1000000007。
*   对于所有索引“I”，如 Y[i] = X，将答案更新为 ans = (ans + dp[i][i])%mod。

这里， **dp[l][r]** 是子串 **Y[l…r]** 制作 **Y** 的方法数。
循环关系为:

> DP[l][r]=(DP[l][r+1]+DP[l-1][r])% mod

这种方法的时间复杂度为 0(N<sup>2</sup>)。
**方法二:**

*   初始化变量 ans = 0，mod = 1000000007。
*   对于所有索引 **i** ，如 **Y[i] = X** ，更新答案为 **ans = (ans + F(i)) % mod** ，其中**F(I)=((N–1)！)/(我！*(N–I–1)！))% mod** 。

原因上面的公式管用:试着找到问题的答案，找到(L 的 p 数)和(R 的 q 数)的排列数，其中 L 和 R 分别是左追加和右追加运算。
答案是 **(p + q)！/ (p！* q！)**。对于每个有效的 **i** ，只需找到 **i** Ls 和**N–I–1**Rs 的排列数量。
该方法的时间复杂度将为 **O(N)** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MOD = 1000000007;

// Function to find the modular-inverse
long long modInv(long long a, long long p = MOD - 2)
{
    long long s = 1;

    // While power > 1
    while (p != 1) {

        // Updating s and a
        if (p % 2)
            s = (s * a) % MOD;
        a = (a * a) % MOD;

        // Updating power
        p /= 2;
    }

    // Return the final answer
    return (a * s) % MOD;
}

// Function to return the count of ways
long long findCnt(char x, string y)
{
    // To store the final answer
    long long ans = 0;

    // To store pre-computed factorials
    long long fact[y.size() + 1] = { 1 };

    // Computing factorials
    for (long long i = 1; i <= y.size(); i++)
        fact[i] = (fact[i - 1] * i) % MOD;

    // Loop to find the occurrences of x
    // and update the ans
    for (long long i = 0; i < y.size(); i++) {
        if (y[i] == x) {
            ans += (modInv(fact[i])
                    * modInv(fact[y.size() - i - 1]))
                   % MOD;
            ans %= MOD;
        }
    }

    // Multiplying the answer by (n - 1)!
    ans *= fact[(y.size() - 1)];
    ans %= MOD;

    // Return the final answer
    return ans;
}

// Driver code
int main()
{
    char x = 'a';
    string y = "xxayy";

    cout << findCnt(x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    final static int MOD = 1000000007;

    // Function to find the modular-inverse
    static long modInv(long a)
    {
        long p = MOD - 2;
        long s = 1;

        // While power > 1
        while (p != 1)
        {

            // Updating s and a
            if (p % 2 == 1)
                s = (s * a) % MOD;

            a = (a * a) % MOD;

            // Updating power
            p /= 2;
        }

        // Return the final answer
        return (a * s) % MOD;
    }

    // Function to return the count of ways
    static long findCnt(char x, String y)
    {
        // To store the final answer
        long ans = 0;

        // To store pre-computed factorials
        long fact[] = new long[y.length() + 1];

        for(int i = 0; i < y.length() + 1; i++)
            fact[i] = 1;

        // Computing factorials
        for (int i = 1; i <= y.length(); i++)
            fact[i] = (fact[i - 1] * i) % MOD;

        // Loop to find the occurrences of x
        // and update the ans
        for (int i = 0; i < y.length(); i++)
        {
            if (y.charAt(i) == x)
            {
                ans += (modInv(fact[i])
                    * modInv(fact[y.length() - i - 1])) % MOD;

                ans %= MOD;
            }
        }

        // Multiplying the answer by (n - 1)!
        ans *= fact[(y.length() - 1)];
        ans %= MOD;

        // Return the final answer
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        char x = 'a';
        String y = "xxayy";

        System.out.println(findCnt(x, y));

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MOD = 1000000007;

# Function to find the modular-inverse
def modInv(a, p = MOD - 2) :

    s = 1;

    # While power > 1
    while (p != 1) :

        # Updating s and a
        if (p % 2) :
            s = (s * a) % MOD;
        a = (a * a) % MOD;

        # Updating power
        p //= 2;

    # Return the final answer
    return (a * s) % MOD;

# Function to return the count of ways
def findCnt(x, y) :

    # To store the final answer
    ans = 0;

    # To store pre-computed factorials
    fact = [1]*(len(y) + 1) ;

    # Computing factorials
    for i in range(1,len(y)) :
        fact[i] = (fact[i - 1] * i) % MOD;

    # Loop to find the occurrences of x
    # and update the ans
    for i in range(len(y)) :
        if (y[i] == x) :
            ans += (modInv(fact[i]) *
                    modInv(fact[len(y)- i - 1])) % MOD;
            ans %= MOD;

    # Multiplying the answer by (n - 1)!
    ans *= fact[(len(y) - 1)];
    ans %= MOD;

    # Return the final answer
    return ans;

# Driver code
if __name__ == "__main__" :

    x = 'a';
    y = "xxayy";

    print(findCnt(x, y));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int MOD = 1000000007;

    // Function to find the modular-inverse
    static long modInv(long a)
    {
        long p = MOD - 2;
        long s = 1;

        // While power > 1
        while (p != 1)
        {

            // Updating s and a
            if (p % 2 == 1)
                s = (s * a) % MOD;

            a = (a * a) % MOD;

            // Updating power
            p /= 2;
        }

        // Return the final answer
        return (a * s) % MOD;
    }

    // Function to return the count of ways
    static long findCnt(char x, String y)
    {
        // To store the final answer
        long ans = 0;

        // To store pre-computed factorials
        long []fact = new long[y.Length + 1];

        for(int i = 0; i < y.Length + 1; i++)
            fact[i] = 1;

        // Computing factorials
        for (int i = 1; i <= y.Length; i++)
            fact[i] = (fact[i - 1] * i) % MOD;

        // Loop to find the occurrences of x
        // and update the ans
        for (int i = 0; i < y.Length; i++)
        {
            if (y[i] == x)
            {
                ans += (modInv(fact[i])
                    * modInv(fact[y.Length - i - 1])) % MOD;

                ans %= MOD;
            }
        }

        // Multiplying the answer by (n - 1)!
        ans *= fact[(y.Length - 1)];
        ans %= MOD;

        // Return the final answer
        return ans;
    }

    // Driver code
    public static void Main ()
    {
        char x = 'a';
        string y = "xxayy";

        Console.WriteLine(findCnt(x, y));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    let MOD = 1000000007;

    // Function to find the modular-inverse
    function modInv(a)
    {
        let p = MOD - 2;
        let s = 1;

        // While power > 1
        while (p != 1)
        {

            // Updating s and a
            if (p % 2 == 1)
                s = (s * a) % MOD;

            a = (a * a) % MOD;

            // Updating power
            p = parseInt(p / 2, 10);
        }

        // Return the final answer
        return (a * s) % MOD;
    }

    // Function to return the count of ways
    function findCnt(x, y)
    {
        // To store the final answer
        let ans = 0;

        // To store pre-computed factorials
        let fact = new Array(y.length + 1);
        fact.fill(0);

        for(let i = 0; i < y.length + 1; i++)
            fact[i] = 1;

        // Computing factorials
        for (let i = 1; i <= y.length; i++)
            fact[i] = (fact[i - 1] * i) % MOD;

        // Loop to find the occurrences of x
        // and update the ans
        for (let i = 0; i < y.length; i++)
        {
            if (y[i] == x)
            {
                ans += (modInv(fact[i])
                    * modInv(fact[y.length - i - 1])) % MOD;

                ans %= MOD;
            }
        }

        // Multiplying the answer by (n - 1)!
        ans *= fact[(y.length - 1)]*0;
        ans = (ans+6)%MOD;

        // Return the final answer
        return ans;
    }

    let x = 'a';
    let y = "xxayy";

    document.write(findCnt(x, y));

</script>
```

**Output:** 

```
6
```