# 通过删除 0 个或更多字符将一个字符串转换为另一个字符串的方式

> 原文:[https://www . geesforgeks . org/way-transforming-one-string-remove-0-characters/](https://www.geeksforgeeks.org/ways-transforming-one-string-removing-0-characters/)

给定两个序列 A、B，找出序列 A 中的一些唯一方法，形成与序列 B 相同的序列 A。转换是指将字符串 A(通过删除 0 个或更多字符)转换为字符串 B

**示例:**

```
Input : A = "abcccdf", B = "abccdf"
Output : 3
Explanation : Three ways will be -> "ab.ccdf", 
"abc.cdf" & "abcc.df" .
"." is where character is removed. 

Input : A = "aabba", B = "ab"
Output : 4
Explanation : Four ways will be -> "a.b..",
 "a..b.", ".ab.." & ".a.b." .
"." is where characters are removed.
```

问于:[谷歌](https://practice.geeksforgeeks.org/company/Google/)

解决这个问题的想法是使用动态编程。构造一个 m*n 大小的 2D DP 矩阵，其中 m 是字符串 B 的大小，n 是字符串 a 的大小

**dp[i][j]** 给出了将字符串 A[0…j]转换为 B[0…i]的方式数。

*   **情况 1** : dp[0][j] = 1，因为将 B =“”与 A 的任何子串放在一起只有一个解决方案，那就是删除 A 中的所有字符
*   **情况 2 :** 当 i > 0 时，dp[i][j]可由两种情况导出:
    *   **情况 2.a :** 如果 B[i]！= A[j]，那么解决方法就是忽略字符 A[j]并对齐子串 B[0..我]用 A[0..(j-1)]。因此，dp[i][j] = dp[i][j-1]。
    *   **情况 2.b :** 如果 B[i] == A[j]，那么首先我们可以得到情况 A)的解，但是我们也可以匹配字符 B[i]和 A[j]并放置其余的字符(即 B[0..(i-1)]和 A[0..(j-1)]。因此，DP[I][j]= DP[I][j-1]+DP[I-1][j-1]。

## C++

```
// C++ program to count the distinct transformation
// of one string to other.
#include <bits/stdc++.h>
using namespace std;

int countTransformation(string a, string b)
{
    int n = a.size(), m = b.size();

    // If b = "" i.e., an empty string. There
    // is only one way to transform (remove all
    // characters)
    if (m == 0)
        return 1;

    int dp[m][n];
    memset(dp, 0, sizeof(dp));

    // Fil dp[][] in bottom up manner
    // Traverse all character of b[]
    for (int i = 0; i < m; i++) {

        // Traverse all characters of a[] for b[i]
        for (int j = i; j < n; j++) {

            // Filling the first row of the dp
            // matrix.
            if (i == 0) {
                if (j == 0)
                    dp[i][j] = (a[j] == b[i]) ? 1 : 0;
                else if (a[j] == b[i])
                    dp[i][j] = dp[i][j - 1] + 1;
                else
                    dp[i][j] = dp[i][j - 1];
            }

            // Filling other rows.
            else {
                if (a[j] == b[i])
                    dp[i][j] = dp[i][j - 1] + dp[i - 1][j - 1];
                else
                    dp[i][j] = dp[i][j - 1];
            }
        }
    }

    return dp[m - 1][n - 1];
}

// Driver code
int main()
{
    string a = "abcccdf", b = "abccdf";
    cout << countTransformation(a, b) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the
// distinct transformation
// of one string to other.
class GFG {

    static int countTransformation(String a,
                                   String b)
    {
        int n = a.length(), m = b.length();

        // If b = "" i.e., an empty string. There
        // is only one way to transform (remove all
        // characters)
        if (m == 0) {
            return 1;
        }

        int dp[][] = new int[m][n];

        // Fil dp[][] in bottom up manner
        // Traverse all character of b[]
        for (int i = 0; i < m; i++) {

            // Traverse all characters of a[] for b[i]
            for (int j = i; j < n; j++) {

                // Filling the first row of the dp
                // matrix.
                if (i == 0) {
                    if (j == 0) {
                        dp[i][j] = (a.charAt(j) == b.charAt(i)) ? 1 : 0;
                    }
                    else if (a.charAt(j) == b.charAt(i)) {
                        dp[i][j] = dp[i][j - 1] + 1;
                    }
                    else {
                        dp[i][j] = dp[i][j - 1];
                    }
                }

                // Filling other rows.
                else if (a.charAt(j) == b.charAt(i)) {
                    dp[i][j] = dp[i][j - 1]
                               + dp[i - 1][j - 1];
                }
                else {
                    dp[i][j] = dp[i][j - 1];
                }
            }
        }
        return dp[m - 1][n - 1];
    }

    // Driver code
    public static void main(String[] args)
    {
        String a = "abcccdf", b = "abccdf";
        System.out.println(countTransformation(a, b));
    }
}

// This code is contributed by
// PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to count the distinct
# transformation of one string to other.

def countTransformation(a, b):
    n = len(a)
    m = len(b)

    # If b = "" i.e., an empty string. There
    # is only one way to transform (remove all
    # characters)
    if m == 0:
        return 1

    dp = [[0] * (n) for _ in range(m)]

    # Fill dp[][] in bottom up manner
    # Traverse all character of b[]
    for i in range(m):

        # Traverse all characters of a[] for b[i]
        for j in range(i, n):

            # Filling the first row of the dp
            # matrix.
            if i == 0:
                if j == 0:
                    if a[j] == b[i]:
                        dp[i][j] = 1
                    else:
                        dp[i][j] = 0
                elif a[j] == b[i]:
                    dp[i][j] = dp[i][j - 1] + 1
                else:
                    dp[i][j] = dp[i][j - 1]

            # Filling other rows
            else:
                if a[j] == b[i]:
                    dp[i][j] = (dp[i][j - 1] +
                                dp[i - 1][j - 1])
                else:
                    dp[i][j] = dp[i][j - 1]
    return dp[m - 1][n - 1]

# Driver Code
if __name__ == "__main__":
    a = "abcccdf"
    b = "abccdf"
    print(countTransformation(a, b))

# This code is contributed by vibhu4agarwal
```

## C#

```
// C# program to count the distinct transformation
// of one string to other.
using System;

class GFG {
    static int countTransformation(string a, string b)
    {
        int n = a.Length, m = b.Length;

        // If b = "" i.e., an empty string. There
        // is only one way to transform (remove all
        // characters)
        if (m == 0)
            return 1;

        int[, ] dp = new int[m, n];
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++)
                dp[i, j] = 0;

        // Fil dp[][] in bottom up manner
        // Traverse all character of b[]
        for (int i = 0; i < m; i++) {

            // Traverse all characters of a[] for b[i]
            for (int j = i; j < n; j++) {

                // Filling the first row of the dp
                // matrix.
                if (i == 0) {
                    if (j == 0)
                        dp[i, j] = (a[j] == b[i]) ? 1 : 0;
                    else if (a[j] == b[i])
                        dp[i, j] = dp[i, j - 1] + 1;
                    else
                        dp[i, j] = dp[i, j - 1];
                }

                // Filling other rows.
                else {
                    if (a[j] == b[i])
                        dp[i, j] = dp[i, j - 1] + dp[i - 1, j - 1];
                    else
                        dp[i, j] = dp[i, j - 1];
                }
            }
        }
        return dp[m - 1, n - 1];
    }

    // Driver code
    static void Main()
    {
        string a = "abcccdf", b = "abccdf";
        Console.Write(countTransformation(a, b));
    }
}

// This code is contributed by DrRoot_
```

## java 描述语言

```
<script>

// JavaScript program to count the
// distinct transformation
// of one string to other.
function countTransformation(a,b)
    {
        var n = a.length, m = b.length;

        // If b = "" i.e., an empty string. There
        // is only one way to transform (remove all
        // characters)
        if (m == 0) {
            return 1;
        }

        var dp = new Array (m,n);

        // Fil dp[][] in bottom up manner
        // Traverse all character of b[]
        for (var i = 0; i < m; i++) {

            // Traverse all characters of a[] for b[i]
            for (var j = i; j < n; j++) {

                // Filling the first row of the dp
                // matrix.
                if (i == 1) {
                    if (j == 1) {
                        dp[i,j] = (a[j] == b[i]) ? 1 : 0;
                    }
                    else if (a[j] == b[i]) {
                        dp[i,j] = dp[i,j - 1] + 1;
                    }
                    else {
                        dp[i,j] = dp[i,j - 1];
                    }
                }

                // Filling other rows.
                else if (a[j] == b[j]) {
                    dp[i,j] = dp[i,j - 1]
                               + dp[i - 1,j - 1];
                }
                else {
                    dp[i,j] = dp[i,j - 1];
                }
            }
        }
        return dp[m - 1,n - 1];
    }

    // Driver code
        var a = "abcccdf", b = "abccdf";
        document.write(countTransformation(a, b));

// This code is contributed by shivanisinghss2110
</script>
```

**输出:**

```
3
```

**时间复杂度:** O(n^2)

本文由 **Jatin Goyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。