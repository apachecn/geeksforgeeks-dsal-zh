# 用 GCD 1 计数子序列数量

> 原文:[https://www . geesforgeks . org/count-子序列数-with-gcd-1/](https://www.geeksforgeeks.org/count-number-of-sub-sequences-with-gcd-1/)

给定一个 N 个数的数组，任务是计算 gcd 等于 1 的子序列的个数。

**例:**

```
Input: a[] = {3, 4, 8, 16} 
Output: 7
The subsequences are:  
{3, 4}, {3, 8}, {3, 16}, {3, 4, 8},
{3, 4, 16}, {3, 8, 16}, {3, 4, 8, 16}

Input: a[] = {1, 2, 4}
Output: 4
```

一个**简单的解决方案**是生成所有[子序列](https://www.geeksforgeeks.org/print-subsequences-string/)或[子集](https://www.geeksforgeeks.org/recursive-program-to-generate-power-set/)。对于每个子序列，检查其 GCD 是否为 1。如果为 1，则递增结果。

**当我们在数组中有值时(假设都小于 1000)，我们可以优化上面的解决方案**，因为我们知道可能的 gcd 数量会很少。我们修改了递归子集生成算法，其中考虑每个元素的两种情况，我们要么包含它，要么排除它。我们跟踪当前的 GCD，如果我们已经为这个 GCD 进行了计数，我们将返回计数。因此，当我们考虑一个子集时，一些 gcd 会一次又一次地出现。因此这个问题可以用[动态规划来解决。](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)下面给出了解决上述问题的步骤:

*   从每个索引开始，通过获取索引元素调用递归函数。
*   在递归函数中，我们迭代直到到达 n
*   这两个递归调用将基于我们是否接受索引元素。
*   基本情况是返回 1，如果我们已经到达终点，gcd 到目前为止是 1。
*   两个递归调用将是 func(ind+1，gcd(a[i]，prevgcd))和 func(ind+1，prevgcd)
*   使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)技术可以避免重叠子问题。

下面是上述方法的实现:

## c++

```
// C++ program to find the number
// of subsequences with gcd 1
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Recursive function to calculate the number
// of subsequences with gcd 1 starting with
// particular index
int func(int ind, int g, int dp[][MAX], int n, int a[])
{

    // Base case
    if (ind == n) {
        if (g == 1)
            return 1;
        else
            return 0;
    }

    // If already visited
    if (dp[ind][g] != -1)
        return dp[ind][g];

    // Either we take or we do not
    int ans = func(ind + 1, g, dp, n, a)
              + func(ind + 1, gcd(a[ind], g), dp, n, a);

    // Return the answer
    return dp[ind][g] = ans;
}

// Function to return the number of subsequences
int countSubsequences(int a[], int n)
{

    // Hash table to memoize
    int dp[n][MAX];
    memset(dp, -1, sizeof dp);

    // Count the number of subsequences
    int count = 0;

    // Count for every subsequence
    for (int i = 0; i < n; i++)
        count += func(i + 1, a[i], dp, n, a);

    return count;
}

// Driver Code
int main()
{
    int a[] = { 3, 4, 8, 16 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << countSubsequences(a, n);
    return 0;
}
```

## Java

```
// Java program to find the number
// of subsequences with gcd 1
class GFG
{

static final int MAX = 1000;
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Recursive function to calculate the number
// of subsequences with gcd 1 starting with
// particular index
static int func(int ind, int g, int dp[][],
                int n, int a[])
{

    // Base case
    if (ind == n)
    {
        if (g == 1)
            return 1;
        else
            return 0;
    }

    // If already visited
    if (dp[ind][g] != -1)
        return dp[ind][g];

    // Either we take or we do not
    int ans = func(ind + 1, g, dp, n, a)
            + func(ind + 1, gcd(a[ind], g), dp, n, a);

    // Return the answer
    return dp[ind][g] = ans;
}

// Function to return the
// number of subsequences
static int countSubsequences(int a[], int n)
{

    // Hash table to memoize
    int dp[][] = new int[n][MAX];
    for(int i = 0; i < n; i++)
        for(int j = 0; j < MAX; j++)
            dp[i][j] = -1;

    // Count the number of subsequences
    int count = 0;

    // Count for every subsequence
    for (int i = 0; i < n; i++)
        count += func(i + 1, a[i], dp, n, a);

    return count;
}

// Driver Code
public static void main(String args[])
{
    int a[] = { 3, 4, 8, 16 };
    int n = a.length;
    System.out.println(countSubsequences(a, n));
}
}

// This code is contributed by Arnab Kundu
```

## python 3

T2T20】c#T3T24】PHPT4

## Javascript

T5T32T34】输出

**备选方案:** [计算 GCD 等于给定数的集合的子集数](https://www.geeksforgeeks.org/count-number-of-subsets-of-a-set-with-gcd-equal-to-a-given-number/)

**动态规划法**到**这个问题没有记忆:**

基本上，该方法将制作一个 2d 矩阵，其中 I 坐标将是给定数组元素的位置，j 坐标将是从 0 到 100 ie 的数字。如果数组元素不够大，gcd 可以从 0 到 100 不等。我们将在给定的数组上迭代，2d 矩阵将存储信息，直到有多少子序列具有从 1 到 100 不等的 gcd。稍后，我们将添加 dp[i][1]以获得 gcd 为 1 的所有子序列。

下面是上述方法的实现:

## c++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// This function calculates
// gcd of two number
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// This function will return total
// subsequences
int countSubsequences(int arr[], int n)
{

   // Declare a dp 2d array
   long long int dp[n][101] = {0};

   // Iterate i from 0 to n - 1
   for(int i = 0; i < n; i++)
   {

       dp[i][arr[i]] = 1;

       // Iterate j from i - 1 to 0
       for(int j = i - 1; j >= 0; j--)
       {
           if(arr[j] < arr[i])
           {

              // Iterate k from 0 to 100
              for(int k = 0; k <= 100; k++)
              {

                 // Find gcd of two number
                 int GCD = gcd(arr[i], k);

                 // dp[i][GCD] is summation of
                 // dp[i][GCD] and dp[j][k]
                 dp[i][GCD] = dp[i][GCD] +
                                    dp[j][k];
              }
           }
       }
   }

    // Add all elements of dp[i][1]
    long long int sum = 0;
    for(int i = 0; i < n; i++)
    {
       sum=(sum + dp[i][1]);
    }

    // Return sum
    return sum;
}

// Driver code
int main()
{
    int a[] = { 3, 4, 8, 16 };
    int n = sizeof(a) / sizeof(a[0]);

    // Function Call
    cout << countSubsequences(a, n);
    return 0;
}
```

## Java

```
// Java program for the
// above approach
import java.util.*;

class GFG{

// This function calculates
// gcd of two number
static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// This function will return total
// subsequences
static long countSubsequences(int arr[],
                              int n)
{

    // Declare a dp 2d array
    long  dp[][] = new long[n][101];

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < 101; j++)
        {
            dp[i][j] = 0;
        }
    }   

    // Iterate i from 0 to n - 1
    for(int i = 0; i < n; i++)
    {

        dp[i][arr[i]] = 1;

        // Iterate j from i - 1 to 0
        for(int j = i - 1; j >= 0; j--)
        {
            if (arr[j] < arr[i])
            {

                // Iterate k from 0 to 100
                for(int k = 0; k <= 100; k++)
                {

                    // Find gcd of two number
                    int GCD = gcd(arr[i], k);

                    // dp[i][GCD] is summation of
                    // dp[i][GCD] and dp[j][k]
                    dp[i][GCD] = dp[i][GCD] +
                                 dp[j][k];
                }
            }
        }
    }

    // Add all elements of dp[i][1]
    long sum = 0;
    for(int i = 0; i < n; i++)
    {
        sum = (sum + dp[i][1]);
    }

    // Return sum
    return sum;
}

// Driver code
public static void main(String args[])
{
    int a[] = { 3, 4, 8, 16 };
    int n = a.length;

    // Function Call
    System.out.println(countSubsequences(a, n));
}
}

// This code is contributed by bolliranadheer
```

## python 3

```
# Python3 program for the
# above approach

# This function calculates
# gcd of two number
def gcd(a, b):
    if (b == 0):
        return a;        
    return gcd(b, a % b);

# This function will return total
# subsequences
def countSubsequences(arr, n):

    # Declare a dp 2d array
    dp = [[0 for i in range(101)] for j in range(n)]

    # Iterate i from 0 to n - 1
    for i in range(n):    
        dp[i][arr[i]] = 1;

        # Iterate j from i - 1 to 0
        for j in range(i - 1, -1, -1):       
            if (arr[j] < arr[i]):

                # Iterate k from 0 to 100
                for k in range(101):

                    # Find gcd of two number
                    GCD = gcd(arr[i], k);

                    # dp[i][GCD] is summation of
                    # dp[i][GCD] and dp[j][k]
                    dp[i][GCD] = dp[i][GCD] + dp[j][k];

    # Add all elements of dp[i][1]
    sum = 0;  
    for i in range(n):  
        sum = (sum + dp[i][1]);

    # Return sum
    return sum;

# Driver code
if __name__=='__main__':

    a = [ 3, 4, 8, 16 ]
    n = len(a)

    # Function Call
    print(countSubsequences(a,n))

# This code is contributed by Pratham76
```

## c#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// This function calculates
// gcd of two number
static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// This function will return total
// subsequences
static long countSubsequences(int []arr,
                              int n)
{

    // Declare a dp 2d array
    long  [,]dp = new long[n, 101];

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < 101; j++)
        {
            dp[i, j] = 0;
        }
    }   

    // Iterate i from 0 to n - 1
    for(int i = 0; i < n; i++)
    {

        dp[i, arr[i]] = 1;

        // Iterate j from i - 1 to 0
        for(int j = i - 1; j >= 0; j--)
        {
            if (arr[j] < arr[i])
            {

                // Iterate k from 0 to 100
                for(int k = 0; k <= 100; k++)
                {

                    // Find gcd of two number
                    int GCD = gcd(arr[i], k);

                    // dp[i,GCD] is summation of
                    // dp[i,GCD] and dp[j,k]
                    dp[i, GCD] = dp[i, GCD] +
                                 dp[j, k];
                }
            }
        }
    }

    // Add all elements of dp[i,1]
    long sum = 0;
    for(int i = 0; i < n; i++)
    {
        sum = (sum + dp[i, 1]);
    }

    // Return sum
    return sum;
}

// Driver code
public static void Main(string []args)
{
    int []a = { 3, 4, 8, 16 };
    int n = a.Length;

    // Function Call
    Console.WriteLine(countSubsequences(a, n));
}
}

// This code is contributed by rutvik_56
```

## Javascript

```
<script>
// javascript program for the
// above approach

    // This function calculates
    // gcd of two number
    function gcd(a , b) {
        if (b == 0)
            return a;

        return gcd(b, a % b);
    }

    // This function will return total
    // subsequences
    function countSubsequences(arr , n) {

        // Declare a dp 2d array
        var dp = Array(n).fill().map(()=>Array(101).fill(0));

        for (i = 0; i < n; i++) {
            for (j = 0; j < 101; j++) {
                dp[i][j] = 0;
            }
        }

        // Iterate i from 0 to n - 1
        for (i = 0; i < n; i++) {

            dp[i][arr[i]] = 1;

            // Iterate j from i - 1 to 0
            for (j = i - 1; j >= 0; j--) {
                if (arr[j] < arr[i]) {

                    // Iterate k from 0 to 100
                    for (k = 0; k <= 100; k++) {

                        // Find gcd of two number
                        var GCD = gcd(arr[i], k);

                        // dp[i][GCD] is summation of
                        // dp[i][GCD] and dp[j][k]
                        dp[i][GCD] = dp[i][GCD] + dp[j][k];
                    }
                }
            }
        }

        // Add all elements of dp[i][1]
        var sum = 0;
        for (i = 0; i < n; i++) {
            sum = (sum + dp[i][1]);
        }

        // Return sum
        return sum;
    }

    // Driver code

        var a = [ 3, 4, 8, 16 ];
        var n = a.length;

        // Function Call
        document.write(countSubsequences(a, n));

// This code contributed by aashish1995
</script>
```

**输出**