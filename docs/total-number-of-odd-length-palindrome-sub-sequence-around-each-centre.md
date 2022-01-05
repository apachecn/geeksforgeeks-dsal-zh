# 每个中心周围奇数长度回文子序列总数

> 原文:[https://www . geesforgeks . org/total-奇数长度回文-子序列-围绕每个中心/](https://www.geeksforgeeks.org/total-number-of-odd-length-palindrome-sub-sequence-around-each-centre/)

给定一个字符串 **str** ，任务是找到以**str【I】**为中心的 str 周围的奇数长度回文子序列的个数，即每个索引将被逐个视为中心。

**示例:**

> **输入:** str = "xyzx"
> **输出:** 1 2 2 1
> 对于索引 0:可能只有单个子序列，即“x”
> 对于索引 1:可能有两个子序列，即“y”和“xyx”
> 对于索引 2:“z”和“xzx”
> 对于索引 3:“x”
> 
> **输入:**str = " AAAA "
> T3】输出: 1 3 3 1

**方法:**我们将用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来解决这个问题。让我们表示弦**弦**的长度为 **N** 。现在，让 **dp[i][j]** 表示从 **0** 到**I–1**的回文子序列数和从 **j** 到**N–1**的回文子序列数。
让**透镜**成为 **i** 和 **j** 之间的距离。对于每一个长度**的镜头**，我们将固定我们的 **i** 和 **j** ，并检查字符**str【I】**和**str【j】**是否相等。然后根据它，我们将进行 dp 过渡。

> 如果**串【I】！= str[j]** 然后**DP[I][j]= DP[I–1][j]+DP[I][j+1]–DP[I–1][j+1]**
> 如果 **str[i] == str[j]** 那么**DP[I–1][j]+DP[I][j+1]**
> 基本情况:
> 如果 **i == 0** 和【

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the total palindromic
// odd length sub-sequences
void solve(string& s)
{
    int n = s.length();

    // dp array to store the number of palindromic
    // subsequences for 0 to i-1 and j+1 to n-1
    int dp[n][n];
    memset(dp, 0, sizeof dp);

    // We will start with the largest
    // distance between i and j
    for (int len = n - 1; len >= 0; --len) {

        // For each len, we fix our i
        for (int i = 0; i + len < n; ++i) {

            // For this i we will find our j
            int j = i + len;

            // Base cases
            if (i == 0 and j == n - 1) {
                if (s[i] == s[j])
                    dp[i][j] = 2;
                else if (s[i] != s[j])
                    dp[i][j] = 1;
            }
            else {
                if (s[i] == s[j]) {

                    // If the characters are equal
                    // then look for out of bound index
                    if (i - 1 >= 0) {
                        dp[i][j] += dp[i - 1][j];
                    }
                    if (j + 1 <= n - 1) {
                        dp[i][j] += dp[i][j + 1];
                    }
                    if (i - 1 < 0 or j + 1 >= n) {

                        // We have only 1 way that is to
                        // just pick these characters
                        dp[i][j] += 1;
                    }
                }
                else if (s[i] != s[j]) {

                    // If the characters are not equal
                    if (i - 1 >= 0) {
                        dp[i][j] += dp[i - 1][j];
                    }
                    if (j + 1 <= n - 1) {
                        dp[i][j] += dp[i][j + 1];
                    }
                    if (i - 1 >= 0 and j + 1 <= n - 1) {

                        // Subtract it as we have
                        // counted it twice
                        dp[i][j] -= dp[i - 1][j + 1];
                    }
                }
            }
        }
    }
    vector<int> ways;
    for (int i = 0; i < n; ++i) {
        if (i == 0 or i == n - 1) {

            // We have just 1 palindrome
            // sequence of length 1
            ways.push_back(1);
        }
        else {

            // Else total ways would be sum of dp[i-1][i+1],
            // that is number of palindrome sub-sequences
            // from 1 to i-1 + number of palindrome
            // sub-sequences from i+1 to n-1
            int total = dp[i - 1][i + 1];
            ways.push_back(total);
        }
    }
    for (int i = 0; i < ways.size(); ++i) {
        cout << ways[i] << " ";
    }
}

// Driver code
int main()
{
    string s = "xyxyx";
    solve(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{

// Function to find the total palindromic
// odd length sub-sequences
static void solve(char[] s)
{
    int n = s.length;

    // dp array to store the number of palindromic
    // subsequences for 0 to i-1 and j+1 to n-1
    int [][]dp = new int[n][n];

    // We will start with the largest
    // distance between i and j
    for (int len = n - 1; len >= 0; --len)
    {

        // For each len, we fix our i
        for (int i = 0; i + len < n; ++i)
        {

            // For this i we will find our j
            int j = i + len;

            // Base cases
            if (i == 0 && j == n - 1)
            {
                if (s[i] == s[j])
                    dp[i][j] = 2;
                else if (s[i] != s[j])
                    dp[i][j] = 1;
            }
            else
            {
                if (s[i] == s[j])
                {

                    // If the characters are equal
                    // then look for out of bound index
                    if (i - 1 >= 0)
                    {
                        dp[i][j] += dp[i - 1][j];
                    }
                    if (j + 1 <= n - 1)
                    {
                        dp[i][j] += dp[i][j + 1];
                    }
                    if (i - 1 < 0 || j + 1 >= n)
                    {

                        // We have only 1 way that is to
                        // just pick these characters
                        dp[i][j] += 1;
                    }
                }
                else if (s[i] != s[j])
                {

                    // If the characters are not equal
                    if (i - 1 >= 0)
                    {
                        dp[i][j] += dp[i - 1][j];
                    }
                    if (j + 1 <= n - 1)
                    {
                        dp[i][j] += dp[i][j + 1];
                    }
                    if (i - 1 >= 0 && j + 1 <= n - 1)
                    {

                        // Subtract it as we have
                        // counted it twice
                        dp[i][j] -= dp[i - 1][j + 1];
                    }
                }
            }
        }
    }

    Vector<Integer> ways = new Vector<>();
    for (int i = 0; i < n; ++i)
    {
        if (i == 0 || i == n - 1)
        {

            // We have just 1 palindrome
            // sequence of length 1
            ways.add(1);
        }
        else
        {

            // Else total ways would be sum of dp[i-1][i+1],
            // that is number of palindrome sub-sequences
            // from 1 to i-1 + number of palindrome
            // sub-sequences from i+1 to n-1
            int total = dp[i - 1][i + 1];
            ways.add(total);
        }
    }
    for (int i = 0; i < ways.size(); ++i)
    {
        System.out.print(ways.get(i) + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    char[] s = "xyxyx".toCharArray();
    solve(s);
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Function to find the total palindromic
# odd Length sub-sequences
def solve(s):
    n = len(s)

    # dp array to store the number of palindromic
    # subsequences for 0 to i-1 and j+1 to n-1
    dp=[[0 for i in range(n)] for i in range(n)]

    # We will start with the largest
    # distance between i and j
    for Len in range(n-1,-1,-1):

        # For each Len, we fix our i
        for i in range(n):

            if i + Len >= n:
                break

            # For this i we will find our j
            j = i + Len

            # Base cases
            if (i == 0 and j == n - 1):
                if (s[i] == s[j]):
                    dp[i][j] = 2
                elif (s[i] != s[j]):
                    dp[i][j] = 1
            else:
                if (s[i] == s[j]):
                    # If the characters are equal
                    # then look for out of bound index
                    if (i - 1 >= 0):
                        dp[i][j] += dp[i - 1][j]

                    if (j + 1 <= n - 1):
                        dp[i][j] += dp[i][j + 1]

                    if (i - 1 < 0 or j + 1 >= n):

                        # We have only 1 way that is to
                        # just pick these characters
                        dp[i][j] += 1

                elif (s[i] != s[j]):

                    # If the characters are not equal
                    if (i - 1 >= 0):
                        dp[i][j] += dp[i - 1][j]

                    if (j + 1 <= n - 1):
                        dp[i][j] += dp[i][j + 1]

                    if (i - 1 >= 0 and j + 1 <= n - 1):

                        # Subtract it as we have
                        # counted it twice
                        dp[i][j] -= dp[i - 1][j + 1]

    ways = []
    for i in range(n):
        if (i == 0 or i == n - 1):

            # We have just 1 palindrome
            # sequence of Length 1
            ways.append(1)
        else:

            # Else total ways would be sum of dp[i-1][i+1],
            # that is number of palindrome sub-sequences
            # from 1 to i-1 + number of palindrome
            # sub-sequences from i+1 to n-1
            total = dp[i - 1][i + 1]
            ways.append(total)

    for i in ways:
        print(i,end=" ")

# Driver code

s = "xyxyx"
solve(s)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find the total palindromic
    // odd length sub-sequences
    static void solve(char[] s)
    {
        int n = s.Length;

        // dp array to store the number of palindromic
        // subsequences for 0 to i-1 and j+1 to n-1
        int [,]dp = new int[n, n];

        // We will start with the largest
        // distance between i and j
        for (int len = n - 1; len >= 0; --len)
        {

            // For each len, we fix our i
            for (int i = 0; i + len < n; ++i)
            {

                // For this i we will find our j
                int j = i + len;

                // Base cases
                if (i == 0 && j == n - 1)
                {
                    if (s[i] == s[j])
                        dp[i, j] = 2;
                    else if (s[i] != s[j])
                        dp[i, j] = 1;
                }
                else
                {
                    if (s[i] == s[j])
                    {

                        // If the characters are equal
                        // then look for out of bound index
                        if (i - 1 >= 0)
                        {
                            dp[i, j] += dp[i - 1, j];
                        }
                        if (j + 1 <= n - 1)
                        {
                            dp[i, j] += dp[i, j + 1];
                        }
                        if (i - 1 < 0 || j + 1 >= n)
                        {

                            // We have only 1 way that is to
                            // just pick these characters
                            dp[i, j] += 1;
                        }
                    }
                    else if (s[i] != s[j])
                    {

                        // If the characters are not equal
                        if (i - 1 >= 0)
                        {
                            dp[i, j] += dp[i - 1, j];
                        }
                        if (j + 1 <= n - 1)
                        {
                            dp[i, j] += dp[i, j + 1];
                        }
                        if (i - 1 >= 0 && j + 1 <= n - 1)
                        {

                            // Subtract it as we have
                            // counted it twice
                            dp[i, j] -= dp[i - 1, j + 1];
                        }
                    }
                }
            }
        }

        List<int> ways = new List<int>();

        for (int i = 0; i < n; ++i)
        {
            if (i == 0 || i == n - 1)
            {

                // We have just 1 palindrome
                // sequence of length 1
                ways.Add(1);
            }
            else
            {

                // Else total ways would be sum of dp[i-1][i+1],
                // that is number of palindrome sub-sequences
                // from 1 to i-1 + number of palindrome
                // sub-sequences from i+1 to n-1
                int total = dp[i - 1,i + 1];
                ways.Add(total);
            }
        }
        for (int i = 0; i < ways.Capacity; ++i)
        {
            Console.Write(ways[i] + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        char[] s = "xyxyx".ToCharArray();
        solve(s);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to find the total palindromic
// odd length sub-sequences
function solve(s)
{
    n = s.length;

    // dp array to store the number of palindromic
    // subsequences for 0 to i-1 and j+1 to n-1
    let dp = new Array(n);
    for(let i=0;i<n;i++)
    {
        dp[i]=new Array(n);
        for(let j=0;j<n;j++)
            dp[i][j]=0;
    }

    // We will start with the largest
    // distance between i and j
    for (let len = n - 1; len >= 0; --len)
    {

        // For each len, we fix our i
        for (let i = 0; i + len < n; ++i)
        {

            // For this i we will find our j
            let j = i + len;

            // Base cases
            if (i == 0 && j == n - 1)
            {
                if (s[i] == s[j])
                    dp[i][j] = 2;
                else if (s[i] != s[j])
                    dp[i][j] = 1;
            }
            else
            {
                if (s[i] == s[j])
                {

                    // If the characters are equal
                    // then look for out of bound index
                    if (i - 1 >= 0)
                    {
                        dp[i][j] += dp[i - 1][j];
                    }
                    if (j + 1 <= n - 1)
                    {
                        dp[i][j] += dp[i][j + 1];
                    }
                    if (i - 1 < 0 || j + 1 >= n)
                    {

                        // We have only 1 way that is to
                        // just pick these characters
                        dp[i][j] += 1;
                    }
                }
                else if (s[i] != s[j])
                {

                    // If the characters are not equal
                    if (i - 1 >= 0)
                    {
                        dp[i][j] += dp[i - 1][j];
                    }
                    if (j + 1 <= n - 1)
                    {
                        dp[i][j] += dp[i][j + 1];
                    }
                    if (i - 1 >= 0 && j + 1 <= n - 1)
                    {

                        // Subtract it as we have
                        // counted it twice
                        dp[i][j] -= dp[i - 1][j + 1];
                    }
                }
            }
        }
    }

    let ways = [];
    for (let i = 0; i < n; ++i)
    {
        if (i == 0 || i == n - 1)
        {

            // We have just 1 palindrome
            // sequence of length 1
            ways.push(1);
        }
        else
        {

            // Else total ways would be sum of dp[i-1][i+1],
            // that is number of palindrome sub-sequences
            // from 1 to i-1 + number of palindrome
            // sub-sequences from i+1 to n-1
            let total = dp[i - 1][i + 1];
            ways.push(total);
        }
    }
    for (let i = 0; i < ways.length; ++i)
    {
        document.write(ways[i] + " ");
    }
}

// Driver code
let s = "xyxyx".split("");
solve(s);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
1 3 4 3 1
```