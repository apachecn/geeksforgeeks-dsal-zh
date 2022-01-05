# 给定数组所有子集的平方和

> 原文:[https://www . geesforgeks . org/给定数组所有子集的平方和/](https://www.geeksforgeeks.org/sum-of-squares-of-all-subsets-of-given-array/)

给定数组 **arr[]** 。数组子集 **A** 的值定义为该子集中所有数字的平方和。任务是计算给定数组的所有可能的非空子集的值的总和。
自，答案可以是大号打印 val **mod** 1000000007。
**示例:**

> **输入:**arr[]=【3，7】
> **输出:**116
> val({ 3 })= 3<sup>2</sup>= 9
> val({ 7 })= 7<sup>2</sup>

**天真的方法:**一个简单的方法是找到所有的子集，然后对该子集中的每个元素进行平方，并将其添加到结果中。这种方法的时间复杂度将是 **O(2 <sup>N</sup> )**
**高效方法:**可以观察到，在给定数组的所有可能子集中，每个元素都将出现**2<sup>N–1</sup>**次，其中 **N** 是数组的大小。
所以任何元素 **X** 在总和中的贡献将是**2<sup>N–1</sup>* X<sup>2</sup>**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int mod = 1e9 + 7;

// Function to return (2^P % mod)
long long power(int p)
{
    long long res = 1;
    for (int i = 1; i <= p; ++i) {
        res *= 2;
        res %= mod;
    }
    return res % mod;
}

// Function to return the sum of squares of subsets
long long subset_square_sum(vector<int>& A)
{

    int n = (int)A.size();

    long long ans = 0;

    // Sqauaring the elements
    // and adding it to ans
    for (int i : A) {
        ans += (1LL * i * i) % mod;
        ans %= mod;
    }

    return (1LL * ans * power(n - 1)) % mod;
}

// Driver code
int main()
{
    vector<int> A = { 3, 7 };

    cout << subset_square_sum(A);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static final int mod = (int)(1e9 + 7);

    // Function to return (2^P % mod)
    static long power(int p)
    {
        long res = 1;
        for (int i = 1; i <= p; ++i)
        {
            res *= 2;
            res %= mod;
        }
        return res % mod;
    }

    // Function to return the sum of squares of subsets
    static long subset_square_sum(int A[])
    {
        int n = A.length;

        long ans = 0;

        // Sqauaring the elements
        // and adding it to ans
        for (int i : A)
        {
            ans += (1 * i * i) % mod;
            ans %= mod;
        }
        return (1 * ans * power(n - 1)) % mod;
    }

    // Driver code
    public static void main (String[] args)
    {
        int A[] = { 3, 7 };

        System.out.println(subset_square_sum(A));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
mod = 10**9 + 7

# Function to return (2^P % mod)
def power(p):

    res = 1
    for i in range(1, p + 1):
        res *= 2
        res %= mod

    return res % mod

# Function to return the sum of
# squares of subsets
def subset_square_sum(A):

    n = len(A)

    ans = 0

    # Squaring the elements
    # and adding it to ans
    for i in A:
        ans += i * i % mod
        ans %= mod

    return ans * power(n - 1) % mod

# Driver code
A = [3, 7]

print(subset_square_sum(A))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static readonly int mod = (int)(1e9 + 7);

    // Function to return (2^P % mod)
    static long power(int p)
    {
        long res = 1;
        for (int i = 1; i <= p; ++i)
        {
            res *= 2;
            res %= mod;
        }
        return res % mod;
    }

    // Function to return the sum of squares of subsets
    static long subset_square_sum(int []A)
    {
        int n = A.Length;

        long ans = 0;

        // Sqauaring the elements
        // and adding it to ans
        foreach (int i in A)
        {
            ans += (1 * i * i) % mod;
            ans %= mod;
        }
        return (1 * ans * power(n - 1)) % mod;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []A = { 3, 7 };

        Console.WriteLine(subset_square_sum(A));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

const mod = 1000000000 + 7;

// Function to return (2^P % mod)
function power(p)
{
    let res = 1;
    for (let i = 1; i <= p; ++i) {
        res *= 2;
        res %= mod;
    }
    return res % mod;
}

// Function to return the sum of squares of subsets
function subset_square_sum(A)
{

    let n = A.length;

    let ans = 0;

    // Sqauaring the elements
    // and adding it to ans
    for (let i = 0; i < n; i++) {
        ans += (A[i] * A[i]) % mod;
        ans %= mod;
    }

    return (ans * power(n - 1)) % mod;
}

// Driver code
    let A = [ 3, 7 ];

    document.write(subset_square_sum(A));
</script>
```

**Output:** 

```
116
```

**时间复杂度:** O(N)