# 将一个数转换成素数段所需的最小分割数

> 原文:[https://www . geesforgeks . org/minimum-splits-需要将数字转换为质数段/](https://www.geeksforgeeks.org/minimum-splits-required-to-convert-a-number-into-prime-segments/)

给定一个字符串形式的数字 **s** ，任务是计算并显示所需的最小分割，使得形成的线段为[质数](https://www.geeksforgeeks.org/prime-numbers/)或打印*否则不可能*。
**举例:**

> **输入:**s = " 2351 "
> T3】输出:0
> T6】说明:给定的数已经是质数。
> **输入:** s = "2352"
> **输出:** 2
> **解释:**合成素段为 23，5，2
> **输入:** s = "2375672"
> **输出:** 2
> **解释:**合成素段为 2，37567，2

**方法:**
这个问题是[矩阵链乘法](https://www.geeksforgeeks.org/matrix-chain-multiplication-dp-8/)的变种，可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)解决。
递归尝试所有可能的拆分，每次拆分时，检查形成的片段是否是质数。考虑一个 2D 数组 **dp** ，其中 **dp[i][j]** 显示从索引 I 到 j 的最小拆分，并返回 dp[0][n]，其中 n 是字符串的长度。
**复发:**

```
dp[i][j] = min(1 + solve(i, k) + solve(k + 1, j)) where i <= k <= j
```

其实在上面写的精确递推中，左右两段都是**非质数**，那么 **1 + INT_MAX + INT_MAX** 就会是**负数**，导致答案不正确。
因此，需要对**左侧**和**右侧**段进行单独计算。如果发现任何段不是质数，则无需继续。否则返回**min(1+左+右)**。
考虑的基本情况是:

*   如果数字是质数，**返回 0**
*   如果 **i==j** 并且数字是质数，**返回 0**
*   如果 **i==j** 并且数字不是素数，**返回 INT_MAX**

下面的代码是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

int dp[1000][1000] = { 0 };

// Checking for prime
bool isprime(long long num)
{
    if (num <= 1)
        return false;
    for (int i = 2; i * i <= num; i++) {
        if (num % i == 0) {
            return false;
        }
    }
    return true;
}
// Conversion of string to int
long long convert(string s, int i, int j)
{
    long long temp = 0;
    for (int k = i; k <= j; k++) {
        temp = temp * 10 + (s[k] - '0');
    }
    return temp;
}
// Function to get the minimum splits
int solve(string s, int i, int j)
{
    // Convert the segment to integer or long long
    long long num = convert(s, i, j);
    // Number is prime
    if (isprime(num)) {
        return 0;
    }
    // If a single digit is prime
    if (i == j && isprime(num))
        return 0;

    // If single digit is not prime
    if (i == j && isprime(num) == false)
        return INT_MAX;

    if (dp[i][j])
        return dp[i][j];

    int ans = INT_MAX;
    for (int k = i; k < j; k++) {
        // Recur for left segment
        int left = solve(s, i, k);
        if (left == INT_MAX) {
            continue;
        }

        // Recur for right segment
        int right = solve(s, k + 1, j);
        if (right == INT_MAX) {
            continue;
        }
        // Minimum from left and right segment
        ans = min(ans, 1 + left + right);
    }
    return dp[i][j] = ans;
}
int main()
{

    string s = "2352";
    int n = s.length();

    int cuts = solve(s, 0, n - 1);
    if (cuts != INT_MAX) {
        cout << cuts;
    }
    else {
        cout << "Not Possible";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG
{

    static int dp[][] = new int[1000][1000];

    // Checking for prime
    static boolean isprime(long num){
        int i;
        if (num <= 1)
            return false;
        for (i = 2; i * i <= num; i++) {
            if (num % i == 0) {
                return false;
            }
        }
        return true;
    }

    // Conversion of string to int
    static long convert(String s, int i, int j)
    {
        long temp = 0;
        int k;
        for (k = i; k <= j; k++) {
            temp = temp * 10 + (s.charAt(k) - '0');
        }
        return temp;
    }

    // Function to get the minimum splits
    static int solve(String s, int i, int j)
    {
        int k;

        // Convert the segment to integer or long long
        long num = convert(s, i, j);

        // Number is prime
        if (isprime(num)) {
            return 0;
        }

        // If a single digit is prime
        if (i == j && isprime(num))
            return 0;

        // If single digit is not prime
        if (i == j && isprime(num) == false)
            return Integer.MAX_VALUE;

        if (dp[i][j] != 0)
            return dp[i][j];

        int ans = Integer.MAX_VALUE;
        for (k = i; k < j; k++) {

            // Recur for left segment
            int left = solve(s, i, k);
            if (left == Integer.MAX_VALUE) {
                continue;
            }

            // Recur for right segment
            int right = solve(s, k + 1, j);
            if (right == Integer.MAX_VALUE) {
                continue;
            }

            // Minimum from left and right segment
            ans = Math.min(ans, 1 + left + right);
        }
        return dp[i][j] = ans;
    }

    public static void main (String []args)
    {

        String s = "2352";
        int n = s.length();

        int cuts = solve(s, 0, n - 1);
        if (cuts != Integer.MAX_VALUE) {
            System.out.print(cuts);
        }
        else {
            System.out.print("Not Possible");
        }
    }
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 Implementation of the above approach
import numpy as np;
import sys

dp = np.zeros((1000,1000)) ;

INT_MAX = sys.maxsize;

# Checking for prime
def isprime(num) :

    if (num <= 1) :
        return False;
    for i in range(2, int(num ** (1/2)) + 1) :
        if (num % i == 0) :
            return False;
    return True;

# Conversion of string to int
def convert(s, i, j) :

    temp = 0;
    for k in range(i, j + 1) :
        temp = temp * 10 + (ord(s[k]) - ord('0'));

    return temp;

# Function to get the minimum splits
def solve(s, i, j) :

    # Convert the segment to integer or long long
    num = convert(s, i, j);
    # Number is prime
    if (isprime(num)) :
        return 0;

    # If a single digit is prime
    if (i == j and isprime(num)) :
        return 0;

    # If single digit is not prime
    if (i == j and isprime(num) == False) :
        return INT_MAX;

    if (dp[i][j]) :
        return dp[i][j];

    ans = INT_MAX;

    for k in range(i, j) :
        # Recur for left segment
        left = solve(s, i, k);
        if (left == INT_MAX) :
            continue;

        # Recur for right segment
        right = solve(s, k + 1, j);
        if (right == INT_MAX) :
            continue;

        # Minimum from left and right segment
        ans = min(ans, 1 + left + right);

    dp[i][j] = ans;

    return ans;

# Driver code   
if __name__ == "__main__" :

    s = "2352";
    n = len(s);

    cuts = solve(s, 0, n - 1);
    if (cuts != INT_MAX) :
        print(cuts);

    else :
        print("Not Possible");

# This code is converted by Yash_R
```

## C#

```
using System;

class GFG
{

    static int [,]dp = new int[1000,1000];

    // Checking for prime
    static bool isprime(long num){
        int i;
        if (num <= 1)
            return false;
        for (i = 2; i * i <= num; i++) {
            if (num % i == 0) {
                return false;
            }
        }
        return true;
    }

    // Conversion of string to int
    static long convert(String s, int i, int j)
    {
        long temp = 0;
        int k;
        for (k = i; k <= j; k++) {
            temp = temp * 10 + (s[k] - '0');
        }
        return temp;
    }

    // Function to get the minimum splits
    static int solve(String s, int i, int j)
    {
        int k;

        // Convert the segment to integer or long long
        long num = convert(s, i, j);

        // Number is prime
        if (isprime(num)) {
            return 0;
        }

        // If a single digit is prime
        if (i == j && isprime(num))
            return 0;

        // If single digit is not prime
        if (i == j && isprime(num) == false)
            return int.MaxValue;

        if (dp[i,j] != 0)
            return dp[i, j];

        int ans = int.MaxValue;
        for (k = i; k < j; k++) {

            // Recur for left segment
            int left = solve(s, i, k);
            if (left == int.MaxValue) {
                continue;
            }

            // Recur for right segment
            int right = solve(s, k + 1, j);
            if (right == int.MaxValue) {
                continue;
            }

            // Minimum from left and right segment
            ans = Math.Min(ans, 1 + left + right);
        }
        return dp[i,j] = ans;
    }

    public static void Main(String []args)
    {

        String s = "2352";
        int n = s.Length;

        int cuts = solve(s, 0, n - 1);
        if (cuts != int.MaxValue) {
            Console.Write(cuts);
        }
        else {
            Console.Write("Not Possible");
        }
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

let dp = new Array(1000);

for(let i = 0; i < 1000; i++){
    dp[i] = new Array(1000)
}

// Checking for prime
function isprime(num)
{
    if (num <= 1)
        return false;
    for (let i = 2; i * i <= num; i++) {
        if (num % i == 0) {
            return false;
        }
    }
    return true;
}
// Conversion of string to int
function convert(s, i, j)
{
    let temp = 0;
    for (let k = i; k <= j; k++) {
        temp = temp * 10 + (s[k] - '0');
    }
    return temp;
}
// Function to get the minimum splits
function solve(s, i, j)
{
    // Convert the segment to integer or long long
    let num = convert(s, i, j);
    // Number is prime
    if (isprime(num)) {
        return 0;
    }
    // If a single digit is prime
    if (i == j && isprime(num))
        return 0;

    // If single digit is not prime
    if (i == j && isprime(num) == false)
        return Number.MAX_SAFE_INTEGER;

    if (dp[i][j])
        return dp[i][j];

    let ans = Number.MAX_SAFE_INTEGER;
    for (let k = i; k < j; k++) {
        // Recur for left segment
        let left = solve(s, i, k);
        if (left == Number.MAX_SAFE_INTEGER) {
            continue;
        }

        // Recur for right segment
        let right = solve(s, k + 1, j);
        if (right == Number.MAX_SAFE_INTEGER) {
            continue;
        }
        // Minimum from left and right segment
        ans = Math.min(ans, 1 + left + right);
    }
    return dp[i][j] = ans;
}

    let s = "2352";
    let n = s.length;

    let cuts = solve(s, 0, n - 1);
    if (cuts != Number.MAX_SAFE_INTEGER) {
        document.write(cuts);
    }
    else {
        document.write("Not Possible");
    }

    // This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
2
```

时间复杂度:O(n <sup>3/2</sup> )

辅助空间:O(10 <sup>6</sup> )