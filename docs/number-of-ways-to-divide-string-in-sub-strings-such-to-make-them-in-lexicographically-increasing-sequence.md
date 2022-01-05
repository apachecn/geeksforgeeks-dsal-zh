# 将字符串划分为子字符串的方法数量，以使它们按照字典顺序递增

> 原文:[https://www . geeksforgeeks . org/子串中的串的划分方法数-这样就可以按字典顺序增加它们的顺序/](https://www.geeksforgeeks.org/number-of-ways-to-divide-string-in-sub-strings-such-to-make-them-in-lexicographically-increasing-sequence/)

给定一个字符串 **S** ，任务是找到在子字符串 **S1、S2、S3、…、Sk** 中划分/划分给定字符串的方法的数量，使得**S1<S2<S3<…<Sk**(按字典顺序)。

**示例:**

> **输入:** S = "aabc"
> **输出:** 6
> 以下是允许的分区:
> {“aabc”}、{“aa”、“BC”}、{“aab”、“c”}、{“a”、“ABC”}、
> {“a”、“ab”、“c”}和{“aa”、“b”、“c”}。
> 
> **输入:**S = " za "
> T3】输出: 1
> 唯一可能的分区是{“za”}。

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。

*   将 **DP[i][j]** 定义为子串 **S[0…j]** 的划分方式数，使得 **S[i，j]** 为最后一个划分。
*   现在，递归关系将是 **DP[i][j] =所有 **k ≥ 0** 和**I≤N–1**的(DP[k][I–1])**之和，其中 **N** 是字符串的长度。
*   最终答案将是在 **0** 到**N–1**之间的所有 **i** 的**(DP[I][N–1])**的总和，因为这些子串将以某种可能的划分方式成为最后的划分。
*   因此，在这里，对于所有子串 **S[i][j]** ，找到子串**S[k][I–1]**，使得**S[k][I–1]**在词典上小于 **S[i][j]** ，并在 **DP[i][j]** 中添加**DP[k][I–1]**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of
// ways of partitioning
int ways(string s, int n)
{

    int dp[n][n];

    // Initialize DP table
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++) {
            dp[i][j] = 0;
        }

    // Base Case
    for (int i = 0; i < n; i++)
        dp[0][i] = 1;

    for (int i = 1; i < n; i++) {

        // To store sub-string S[i][j]
        string temp;
        for (int j = i; j < n; j++) {
            temp += s[j];

            // To store sub-string S[k][i-1]
            string test;
            for (int k = i - 1; k >= 0; k--) {
                test += s[k];
                if (test < temp) {
                    dp[i][j] += dp[k][i - 1];
                }
            }
        }
    }

    int ans = 0;
    for (int i = 0; i < n; i++) {
        // Add all the ways where S[i][n-1]
        // will be the last partition
        ans += dp[i][n - 1];
    }

    return ans;
}

// Driver code
int main()
{
    string s = "aabc";
    int n = s.length();

    cout << ways(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{
    // Function to return the number of
    // ways of partitioning
    static int ways(String s, int n)
    {
        int dp[][] = new int[n][n];

        // Initialize DP table
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
            {
                dp[i][j] = 0;
            }

        // Base Case
        for (int i = 0; i < n; i++)
            dp[0][i] = 1;

        for (int i = 1; i < n; i++)
        {

            // To store sub-string S[i][j]
            String temp = "";
            for (int j = i; j < n; j++)
            {
                temp += s.charAt(j);

                // To store sub-string S[k][i-1]
                String test = "";
                for (int k = i - 1; k >= 0; k--)
                {
                    test += s.charAt(k);
                    if (test.compareTo(temp) < 0)
                    {
                        dp[i][j] += dp[k][i - 1];
                    }
                }
            }
        }

        int ans = 0;
        for (int i = 0; i < n; i++)
        {
            // Add all the ways where S[i][n-1]
            // will be the last partition
            ans += dp[i][n - 1];
        }
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        String s = "aabc";
        int n = s.length();

        System.out.println(ways(s, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number of
# ways of partitioning
def ways(s, n):

    dp = [[0 for i in range(n)]
             for i in range(n)]

    # Base Case
    for i in range(n):
        dp[0][i] = 1

    for i in range(1, n):

        # To store sub-S[i][j]
        temp = ""
        for j in range(i, n):
            temp += s[j]

            # To store sub-S[k][i-1]
            test = ""
            for k in range(i - 1, -1, -1):
                test += s[k]
                if (test < temp):
                    dp[i][j] += dp[k][i - 1]

    ans = 0
    for i in range(n):

        # Add all the ways where S[i][n-1]
        # will be the last partition
        ans += dp[i][n - 1]

    return ans

# Driver code
s = "aabc"
n = len(s)

print(ways(s, n))

# This code is contributed by Mohit Kumarv
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    // Function to return the number of
    // ways of partitioning
    static int ways(String s, int n)
    {
        int [,]dp = new int[n, n];

        // Initialize DP table
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
            {
                dp[i, j] = 0;
            }

        // Base Case
        for (int i = 0; i < n; i++)
            dp[0, i] = 1;

        for (int i = 1; i < n; i++)
        {

            // To store sub-string S[i,j]
            String temp = "";
            for (int j = i; j < n; j++)
            {
                temp += s[j];

                // To store sub-string S[k,i-1]
                String test = "";
                for (int k = i - 1; k >= 0; k--)
                {
                    test += s[k];
                    if (test.CompareTo(temp) < 0)
                    {
                        dp[i, j] += dp[k, i - 1];
                    }
                }
            }
        }

        int ans = 0;
        for (int i = 0; i < n; i++)
        {
            // Add all the ways where S[i,n-1]
            // will be the last partition
            ans += dp[i, n - 1];
        }
        return ans;
    }

    // Driver code
    public static void Main (String[] args)
    {
        String s = "aabc";
        int n = s.Length;

        Console.WriteLine(ways(s, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the number of
// ways of partitioning
function ways(s, n)
{

    var dp = Array.from(Array(n), ()=> Array(n).fill(0));

    // Base Case
    for (var i = 0; i < n; i++)
        dp[0][i] = 1;

    for (var i = 1; i < n; i++) {

        // To store sub-string S[i][j]
        var temp;
        for (var j = i; j < n; j++) {
            temp += s[j];

            // To store sub-string S[k][i-1]
            var test;
            for (var k = i - 1; k >= 0; k--) {
                test += s[k];
                if (test < temp) {
                    dp[i][j] += dp[k][i - 1];
                }
            }
        }
    }

    var ans = 0;
    for (var i = 0; i < n; i++) {
        // Add all the ways where S[i][n-1]
        // will be the last partition
        ans += dp[i][n - 1];
    }

    return ans;
}

// Driver code
var s = "aabc";
var n = s.length;
document.write( ways(s, n));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
6
```