# 长度为 K 的子序列 X，使得 gcd(X[0]，X[1]) + (X[2]，X[3]) + …最大化

> 原文:[https://www . geesforgeks . org/subsequel-x-of-length-k-so-gcdx0-x1-x2-x3-is-maximized/](https://www.geeksforgeeks.org/subsequence-x-of-length-k-such-that-gcdx0-x1-x2-x3-is-maximized/)

给定一个大小为 **N** 的数组**。任务是找到长度为 **K** 的子序列 **X** ，使得 **gcd(X[0]，X[1]) + (X[2]，X[3]) + …** 最大。
**注** : **K** 为偶数。
**举例:**** 

> ****输入:** a[] = {4，5，3，7，8，10，9，8}，k = 4
> **输出:** 9
> 子序列{4，7，8，8}给出最大值= 9。
> 其他子序列如{ 5，3，8，8}也给出 9。
> **输入:** a[] = {5，8，16，20}，K = 2
> **输出:**
> 子序列{8，16}给出最大值。**

****天真方法**:天真方法是使用[递归](https://www.geeksforgeeks.org/recursion/)生成长度为 K 的所有子序列，并找到可能的最大值。
**高效方法**:一种高效的方法是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来解决上述问题。如果将**第 I 个**指标元素作为**第 j 个**元素，则让 **dp[i][j]** 表示对 gcd 和的值。递归生成所有可能的子序列。如果所取元素的 **cnt** 为**奇数**，则将[**【gcd】**](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)**(a【prev】，a【current】)**相加，因为这个数字将是该对中的第二个，并对下一个元素重复出现。如果 **cnt** 是**甚至**，那么只需重复设置 **a[i]** 作为前一个元素。[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)已经被用来避免相同循环的重新计算。所有生成总和的最大值将是答案。
以下是上述方法的实施:** 

## **C++**

```
// C++ program to find the sum of
// the addition of all possible subsets
#include <bits/stdc++.h>
using namespace std;
const int MAX = 100;

// Recursive function to find the maximum value of
// the given recurrence
int recur(int ind, int cnt, int last, int a[],
          int n, int k, int dp[][MAX])
{

    // If we get K elements
    if (cnt == k)
        return 0;

    // If we have reached the end
    // and K elements are not there
    if (ind == n)
        return -1e9;

    // If the state has been visited
    if (dp[ind][cnt] != -1)
        return dp[ind][cnt];
    int ans = 0;

    // Iterate for every element as the
    // next possible element
    // and take the element which gives
    // the maximum answer
    for (int i = ind; i < n; i++)
    {
        // If this element is the first element
        // in the individual pair in the subsequence
        // then simply recurrence with the last
        // element as i-th index
        if (cnt % 2 == 0)
         ans=max(ans,recur(i + 1, cnt + 1, i, a, n, k, dp));

        // If this element is the second element in
        // the individual pair, the find gcd with
        // the previous element and add to the answer
        // and recur for the next element
        else
            ans = max(ans, __gcd(a[last], a[i]) +
                recur(i + 1, cnt + 1, 0, a, n, k, dp));
    }

    return dp[ind][cnt] = ans;
}

// Driver Code
int main()
{
    int a[] = { 4, 5, 3, 7, 8, 10, 9, 8 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 4;
    int dp[n][MAX];
    memset(dp, -1, sizeof dp);

    cout << recur(0, 0, 0, a, n, k, dp);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find the sum of
// the addition of all possible subsets
import java.util.*;

class GFG
{

static int MAX = 100;

// Recursive function to find the maximum value of
// the given recurrence
static int recur(int ind, int cnt, int last, int a[],
                            int n, int k, int dp[][])
{

    // If we get K elements
    if (cnt == k)
        return 0;

    // If we have reached the end
    // and K elements are not there
    if (ind == n)
        return (int) -1e9;

    // If the state has been visited
    if (dp[ind][cnt] != -1)
        return dp[ind][cnt];
    int ans = 0;

    // Iterate for every element as the
    // next possible element
    // and take the element which gives
    // the maximum answer
    for (int i = ind; i < n; i++)
    {
        // If this element is the first element
        // in the individual pair in the subsequence
        // then simply recurrence with the last
        // element as i-th index
        if (cnt % 2 == 0)
            ans = Math.max(ans,recur(i + 1, cnt + 1, i, a, n, k, dp));

        // If this element is the second element in
        // the individual pair, the find gcd with
        // the previous element and add to the answer
        // and recur for the next element
        else
            ans = Math.max(ans, __gcd(a[last], a[i]) +
                recur(i + 1, cnt + 1, 0, a, n, k, dp));
    }

    return dp[ind][cnt] = ans;
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 4, 5, 3, 7, 8, 10, 9, 8 };
    int n = a.length;
    int k = 4;
    int [][]dp = new int[n][MAX];
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < MAX; j++)
        {
            dp[i][j] = -1;
        }
    }
    System.out.println(recur(0, 0, 0, a, n, k, dp));
    }
}

// This code is contributed by Rajput-Ji
```

## **蟒蛇 3**

```
# Python3 program to find the sum of
# the addition of all possible subsets
from math import gcd as __gcd
MAX = 100

# Recursive function to find the
# maximum value of the given recurrence
def recur(ind, cnt, last, a, n, k, dp):

    # If we get K elements
    if (cnt == k):
        return 0

    # If we have reached the end
    # and K elements are not there
    if (ind == n):
        return -10**9

    # If the state has been visited
    if (dp[ind][cnt] != -1):
        return dp[ind][cnt]
    ans = 0

    # Iterate for every element as the
    # next possible element
    # and take the element which gives
    # the maximum answer
    for i in range(ind, n):

        # If this element is the first element
        # in the individual pair in the subsequence
        # then simply recurrence with the last
        # element as i-th index
        if (cnt % 2 == 0):
            ans = max(ans, recur(i + 1, cnt + 1,
                                 i, a, n, k, dp))

        # If this element is the second element in
        # the individual pair, the find gcd with
        # the previous element and add to the answer
        # and recur for the next element
        else:
            ans = max(ans, __gcd(a[last], a[i]) +
                      recur(i + 1, cnt + 1, 0, a, n, k, dp))

    dp[ind][cnt] = ans
    return ans

# Driver Code
a = [4, 5, 3, 7, 8, 10, 9, 8 ]

n = len(a)
k = 4;
dp = [[-1 for i in range(MAX)]
          for i in range(n)]

print(recur(0, 0, 0, a, n, k, dp))

# This code is contributed by Mohit Kumar
```

## **C#**

```
// C# program to find the sum of
// the addition of all possible subsets
using System;

class GFG
{

static int MAX = 100;

// Recursive function to find the maximum value of
// the given recurrence
static int recur(int ind, int cnt, int last, int []a,
                            int n, int k, int [,]dp)
{

    // If we get K elements
    if (cnt == k)
        return 0;

    // If we have reached the end
    // and K elements are not there
    if (ind == n)
        return (int) -1e9;

    // If the state has been visited
    if (dp[ind,cnt] != -1)
        return dp[ind,cnt];
    int ans = 0;

    // Iterate for every element as the
    // next possible element
    // and take the element which gives
    // the maximum answer
    for (int i = ind; i < n; i++)
    {
        // If this element is the first element
        // in the individual pair in the subsequence
        // then simply recurrence with the last
        // element as i-th index
        if (cnt % 2 == 0)
            ans = Math.Max(ans,recur(i + 1, cnt + 1, i, a, n, k, dp));

        // If this element is the second element in
        // the individual pair, the find gcd with
        // the previous element and add to the answer
        // and recur for the next element
        else
            ans = Math.Max(ans, __gcd(a[last], a[i]) +
                recur(i + 1, cnt + 1, 0, a, n, k, dp));
    }

    return dp[ind,cnt] = ans;
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 4, 5, 3, 7, 8, 10, 9, 8 };
    int n = a.Length;
    int k = 4;
    int [,]dp = new int[n,MAX];
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < MAX; j++)
        {
            dp[i,j] = -1;
        }
    }
    Console.WriteLine(recur(0, 0, 0, a, n, k, dp));
}
}

// This code is contributed by Princi Singh
```

## **java 描述语言**

```
<script>
// Javascript program to find the sum of
// the addition of all possible subsets

let MAX = 100;

// Recursive function to find the maximum value of
// the given recurrence
function recur(ind,cnt,last,a,n,k,dp)
{
    // If we get K elements
    if (cnt == k)
        return 0;

    // If we have reached the end
    // and K elements are not there
    if (ind == n)
        return -1e9;

    // If the state has been visited
    if (dp[ind][cnt] != -1)
        return dp[ind][cnt];
    let ans = 0;

    // Iterate for every element as the
    // next possible element
    // and take the element which gives
    // the maximum answer
    for (let i = ind; i < n; i++)
    {
        // If this element is the first element
        // in the individual pair in the subsequence
        // then simply recurrence with the last
        // element as i-th index
        if (cnt % 2 == 0)
            ans = Math.max(ans,recur(i + 1, cnt + 1, i, a, n, k, dp));

        // If this element is the second element in
        // the individual pair, the find gcd with
        // the previous element and add to the answer
        // and recur for the next element
        else
            ans = Math.max(ans, __gcd(a[last], a[i]) +
                recur(i + 1, cnt + 1, 0, a, n, k, dp));
    }

    return dp[ind][cnt] = ans;
}

function __gcd(a,b)
{
     if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Driver Code
let a=[4, 5, 3, 7, 8, 10, 9, 8];
let n = a.length;
let k = 4;
let dp = new Array(n);
for(let i=0;i<n;i++)
{
    dp[i]=new Array(MAX);
    for(let j = 0; j < MAX; j++)
    {
        dp[i][j] = -1;
    }
}
document.write(recur(0, 0, 0, a, n, k, dp));

// This code is contributed by unknown2108
</script>
```

****Output:** 

```
9
```**