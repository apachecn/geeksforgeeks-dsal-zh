# 最短公共超序列

> 原文:[https://www . geesforgeks . org/short-common-super quence/](https://www.geeksforgeeks.org/shortest-common-supersequence/)

给定两个字符串 str1 和 str2，任务是找到以 str1 和 str2 作为子序列的最短字符串的长度。

**示例:**

```
Input:   str1 = "geek",  str2 = "eke"
Output: 5
Explanation: 
String "geeke" has both string "geek" 
and "eke" as subsequences.

Input:   str1 = "AGGTAB",  str2 = "GXTXAYB"
Output:  9
Explanation: 
String "AGXGTXAYB" has both string 
"AGGTAB" and "GXTXAYB" as subsequences.
```

这个问题与[最长公共子序列问题](https://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/)密切相关。以下是步骤。
**1)** 找到两个给定字符串的最长公共子序列。比如“极客”和“eke”的 lcs 就是“ek”。
**2)** 将非 lcs 字符(以字符串中的原始顺序)插入到上面找到的 lcs 中，并返回结果。所以“ek”变成了最短的公共超序列“geeke”。
我们再考虑一个例子，str 1 =“AGGTAB”和 str 2 =“GXTXAYB”。str1 和 str2 中的 LCS 是“GTAB”。一旦我们找到 LCS，我们按顺序插入两个字符串的字符，我们得到“AGXGTXAYB”
**这是如何工作的？**
我们需要找到一个既有字符串作为子序列，又是最短的这样的字符串。如果两个字符串的所有字符都不同，那么结果就是两个给定字符串的长度之和。如果有共同的字符，那么我们不希望他们多次，因为任务是最小化长度。因此，我们首先找到最长的公共子序列，取该子序列的一次出现，并添加额外的字符。

```
Length of the shortest supersequence  
= (Sum of lengths of given two strings) 
- (Length of LCS of two given strings) 
```

以下是上述想法的实现。下面的实现只找到最短超序列的长度。

## C++

```
// C++ program to find length of the
// shortest supersequence
#include <bits/stdc++.h>
using namespace std;

// Utility function to get max
// of 2 integers
int max(int a, int b) { return (a > b) ? a : b; }

// Returns length of LCS for
// X[0..m - 1], Y[0..n - 1]
int lcs(char* X, char* Y, int m, int n);

// Function to find length of the
// shortest supersequence of X and Y.
int shortestSuperSequence(char* X, char* Y)
{
    int m = strlen(X), n = strlen(Y);

    // find lcs
    int l = lcs(X, Y, m, n);

    // Result is sum of input string
    // lengths - length of lcs
    return (m + n - l);
}

// Returns length of LCS
// for X[0..m - 1], Y[0..n - 1]
int lcs(char* X, char* Y, int m, int n)
{
    int L[m + 1][n + 1];
    int i, j;

    // Following steps build L[m + 1][n + 1]
    // in bottom up fashion. Note that
    // L[i][j] contains length of LCS of
    // X[0..i - 1] and Y[0..j - 1]
    for (i = 0; i <= m; i++) {
        for (j = 0; j <= n; j++) {
            if (i == 0 || j == 0)
                L[i][j] = 0;

            else if (X[i - 1] == Y[j - 1])
                L[i][j] = L[i - 1][j - 1] + 1;

            else
                L[i][j] = max(L[i - 1][j], L[i][j - 1]);
        }
    }

    // L[m][n] contains length of LCS
    // for X[0..n - 1] and Y[0..m - 1]
    return L[m][n];
}

// Driver code
int main()
{
    char X[] = "AGGTAB";
    char Y[] = "GXTXAYB";

    cout << "Length of the shortest supersequence is "
         << shortestSuperSequence(X, Y) << endl;

    return 0;
}

// This code is contributed by Akanksha Rai
```

## C

```
// C program to find length of
// the shortest supersequence
#include <stdio.h>
#include <string.h>

// Utility function to get
// max of 2 integers
int max(int a, int b) { return (a > b) ? a : b; }

// Returns length of LCS for
// X[0..m - 1], Y[0..n - 1]
int lcs(char* X, char* Y, int m, int n);

// Function to find length of the
// shortest supersequence of X and Y.
int shortestSuperSequence(char* X, char* Y)
{
    int m = strlen(X), n = strlen(Y);

    // find lcs
    int l = lcs(X, Y, m, n);

    // Result is sum of input string
    // lengths - length of lcs
    return (m + n - l);
}

// Returns length of LCS
// for X[0..m - 1], Y[0..n - 1]
int lcs(char* X, char* Y, int m, int n)
{
    int L[m + 1][n + 1];
    int i, j;

    // Following steps build L[m + 1][n + 1]
    // in bottom up fashion. Note that
    // L[i][j] contains length of LCS of
    // X[0..i - 1] and Y[0..j - 1]
    for (i = 0; i <= m; i++) {
        for (j = 0; j <= n; j++) {
            if (i == 0 || j == 0)
                L[i][j] = 0;

            else if (X[i - 1] == Y[j - 1])
                L[i][j] = L[i - 1][j - 1] + 1;

            else
                L[i][j] = max(L[i - 1][j], L[i][j - 1]);
        }
    }

    // L[m][n] contains length of LCS
    // for X[0..n - 1] and Y[0..m - 1]
    return L[m][n];
}

// Driver code
int main()
{
    char X[] = "AGGTAB";
    char Y[] = "GXTXAYB";

    printf("Length of the shortest supersequence is %d\n",
           shortestSuperSequence(X, Y));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length of
// the shortest supersequence
class GFG {

    // Function to find length of the
    // shortest supersequence of X and Y.
    static int shortestSuperSequence(String X, String Y)
    {
        int m = X.length();
        int n = Y.length();

        // find lcs
        int l = lcs(X, Y, m, n);

        // Result is sum of input string
        // lengths - length of lcs
        return (m + n - l);
    }

    // Returns length of LCS
    // for X[0..m - 1], Y[0..n - 1]
    static int lcs(String X, String Y, int m, int n)
    {
        int[][] L = new int[m + 1][n + 1];
        int i, j;

        // Following steps build L[m + 1][n + 1]
        // in bottom up fashion. Note that
        // L[i][j] contains length of LCS
        // of X[0..i - 1]and Y[0..j - 1]
        for (i = 0; i <= m; i++) {
            for (j = 0; j <= n; j++) {
                if (i == 0 || j == 0)
                    L[i][j] = 0;

                else if (X.charAt(i - 1) == Y.charAt(j - 1))
                    L[i][j] = L[i - 1][j - 1] + 1;

                else
                    L[i][j] = Math.max(L[i - 1][j],
                                       L[i][j - 1]);
            }
        }

        // L[m][n] contains length of LCS
        // for X[0..n - 1] and Y[0..m - 1]
        return L[m][n];
    }

    // Driver code
    public static void main(String args[])
    {
        String X = "AGGTAB";
        String Y = "GXTXAYB";

        System.out.println("Length of the shortest "
                           + "supersequence is "
                           + shortestSuperSequence(X, Y));
    }
}

// This article is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to find length
# of the shortest supersequence

# Function to find length of the
# shortest supersequence of X and Y.

def shortestSuperSequence(X, Y):
    m = len(X)
    n = len(Y)
    l = lcs(X, Y, m, n)

    # Result is sum of input string
    # lengths - length of lcs
    return (m + n - l)

# Returns length of LCS for
# X[0..m - 1], Y[0..n - 1]

def lcs(X, Y, m, n):
    L = [[0] * (n + 2) for i in
         range(m + 2)]

    # Following steps build L[m + 1][n + 1]
    # in bottom up fashion. Note that L[i][j]
    # contains length of LCS of X[0..i - 1]
    # and Y[0..j - 1]
    for i in range(m + 1):

        for j in range(n + 1):

            if (i == 0 or j == 0):
                L[i][j] = 0

            elif (X[i - 1] == Y[j - 1]):
                L[i][j] = L[i - 1][j - 1] + 1

            else:
                L[i][j] = max(L[i - 1][j],
                              L[i][j - 1])

    # L[m][n] contains length of
    # LCS for X[0..n - 1] and Y[0..m - 1]
    return L[m][n]

# Driver code
X = "AGGTAB"
Y = "GXTXAYB"

print("Length of the shortest supersequence is %d"
      % shortestSuperSequence(X, Y))

# This code is contributed by Ansu Kumari
```

## C#

```
// C# program to find length of
// the shortest supersequence
using System;

class GFG {
    // Function to find length of the
    // shortest supersequence of X and Y.
    static int shortestSuperSequence(String X, String Y)
    {
        int m = X.Length;
        int n = Y.Length;

        // find lcs
        int l = lcs(X, Y, m, n);

        // Result is sum of input string
        // lengths - length of lcs
        return (m + n - l);
    }

    // Returns length of LCS for
    // X[0..m - 1], Y[0..n - 1]
    static int lcs(String X, String Y, int m, int n)
    {
        int[, ] L = new int[m + 1, n + 1];
        int i, j;

        // Following steps build L[m + 1][n + 1]
        // in bottom up fashion.Note that
        // L[i][j] contains length of LCS of
        // X[0..i - 1] and Y[0..j - 1]
        for (i = 0; i <= m; i++) {
            for (j = 0; j <= n; j++) {
                if (i == 0 || j == 0)
                    L[i, j] = 0;

                else if (X[i - 1] == Y[j - 1])
                    L[i, j] = L[i - 1, j - 1] + 1;

                else
                    L[i, j] = Math.Max(L[i - 1, j],
                                       L[i, j - 1]);
            }
        }

        // L[m][n] contains length of LCS
        // for X[0..n - 1] and Y[0..m - 1]
        return L[m, n];
    }

    // Driver code
    public static void Main()
    {
        String X = "AGGTAB";
        String Y = "GXTXAYB";

        Console.WriteLine("Length of the shortest"
                          + "supersequence is "
                          + shortestSuperSequence(X, Y));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find length of the
// shortest supersequence

// Function to find length of the
// shortest supersequence of X and Y.
function shortestSuperSequence($X, $Y)
{
    $m = strlen($X);
    $n = strlen($Y);

    // find lcs
    $l = lcs($X, $Y, $m, $n);

    // Result is sum of input string
    // lengths - length of lcs
    return ($m + $n - $l);
}

// Returns length of LCS
// for X[0..m - 1], Y[0..n - 1]
function lcs( $X, $Y, $m, $n)
{
    $L=array_fill(0, $m + 1, array_fill(0, $n + 1, 0));

    // Following steps build $L[m + 1][n + 1]
    // in bottom up fashion. Note that
    // $L[i][j] contains length of LCS of
    // X[0..i - 1] and Y[0..j - 1]
    for ($i = 0; $i <= $m; $i++)
    {
        for ($j = 0; $j <= $n; $j++)
        {
            if ($i == 0 || $j == 0)
                $L[$i][$j] = 0;

            else if ($X[$i - 1] == $Y[$j - 1])
                $L[$i][$j] = $L[$i - 1][$j - 1] + 1;

            else
                $L[$i][$j] = max($L[$i - 1][$j],
                            $L[$i][$j - 1]);
        }
    }

    // $L[m][n] contains length of LCS
    // for X[0..n - 1] and Y[0..m - 1]
    return $L[$m][$n];
}

    // Driver code
    $X = "AGGTAB";
    $Y = "GXTXAYB";

    echo "Length of the shortest supersequence is ".
                shortestSuperSequence($X, $Y)."\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to find length of
// the shortest supersequence   // Function to find length of the
// shortest supersequence of X and Y.
function shortestSuperSequence(X, Y)
{
    var m = X.length;
    var n = Y.length;

    // find lcs
    var l = lcs(X, Y, m, n);

    // Result is sum of input string
    // lengths - length of lcs
    return (m + n - l);
}

// Returns length of LCS
// for X[0..m - 1], Y[0..n - 1]
function lcs(X, Y , m , n)
{
    var L = Array(m+1).fill(0).map(x => Array(n+1).fill(0));
    var i, j;

    // Following steps build L[m + 1][n + 1]
    // in bottom up fashion. Note that
    // L[i][j] contains length of LCS
    // of X[0..i - 1]and Y[0..j - 1]
    for (i = 0; i <= m; i++) {
        for (j = 0; j <= n; j++) {
            if (i == 0 || j == 0)
                L[i][j] = 0;

            else if (X.charAt(i - 1) == Y.charAt(j - 1))
                L[i][j] = L[i - 1][j - 1] + 1;

            else
                L[i][j] = Math.max(L[i - 1][j],
                                   L[i][j - 1]);
        }
    }

    // L[m][n] contains length of LCS
    // for X[0..n - 1] and Y[0..m - 1]
    return L[m][n];
}

// Driver code
var X = "AGGTAB";
var Y = "GXTXAYB";

document.write("Length of the shortest "
                   + "supersequence is "
                   + shortestSuperSequence(X, Y));

// This code contributed by shikhasingrajput
</script>
```

**输出:**

```
Length of the shortest supersequence is 9
```

下面是**解决上述问题的另一种方法**。
一个简单的分析产生以下简单的递归解。

```
Let X[0..m - 1] and Y[0..n - 1] be two 
strings and m and n be respective
lengths.

  if (m == 0) return n;
  if (n == 0) return m;

  // If last characters are same, then 
  // add 1 to result and
  // recur for X[]
  if (X[m - 1] == Y[n - 1])
     return 1 + SCS(X, Y, m - 1, n - 1);

  // Else find shortest of following two
  //  a) Remove last character from X and recur
  //  b) Remove last character from Y and recur
  else 
    return 1 + min( SCS(X, Y, m - 1, n), SCS(X, Y, m, n - 1) );
```

下面是基于上述递归公式的简单朴素递归解法。

## C++

```
// A Naive recursive C++ program to find
// length of the shortest supersequence
#include <bits/stdc++.h>
using namespace std;

int superSeq(char* X, char* Y, int m, int n)
{
    if (!m)
        return n;
    if (!n)
        return m;

    if (X[m - 1] == Y[n - 1])
        return 1 + superSeq(X, Y, m - 1, n - 1);

    return 1
           + min(superSeq(X, Y, m - 1, n),
                 superSeq(X, Y, m, n - 1));
}

// Driver Code
int main()
{
    char X[] = "AGGTAB";
    char Y[] = "GXTXAYB";
    cout << "Length of the shortest supersequence is "
         << superSeq(X, Y, strlen(X), strlen(Y));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Naive recursive Java program to find
// length of the shortest supersequence
class GFG {
    static int superSeq(String X, String Y, int m, int n)
    {
        if (m == 0)
            return n;
        if (n == 0)
            return m;

        if (X.charAt(m - 1) == Y.charAt(n - 1))
            return 1 + superSeq(X, Y, m - 1, n - 1);

        return 1
            + Math.min(superSeq(X, Y, m - 1, n),
                       superSeq(X, Y, m, n - 1));
    }

    // Driver code
    public static void main(String args[])
    {
        String X = "AGGTAB";
        String Y = "GXTXAYB";
        System.out.println(
            "Length of the shortest"
            + "supersequence is: "
            + superSeq(X, Y, X.length(), Y.length()));
    }
}

// This article is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# A Naive recursive python program to find
# length of the shortest supersequence

def superSeq(X, Y, m, n):
    if (not m):
        return n
    if (not n):
        return m

    if (X[m - 1] == Y[n - 1]):
        return 1 + superSeq(X, Y, m - 1, n - 1)

    return 1 + min(superSeq(X, Y, m - 1, n),
                   superSeq(X, Y, m, n - 1))

# Driver Code
X = "AGGTAB"
Y = "GXTXAYB"
print("Length of the shortest supersequence is %d"
      % superSeq(X, Y, len(X), len(Y)))

# This code is contributed by Ansu Kumari
```

## C#

```
// A Naive recursive C# program to find
// length of the shortest supersequence
using System;

class GFG {
    static int superSeq(String X, String Y, int m, int n)
    {
        if (m == 0)
            return n;
        if (n == 0)
            return m;

        if (X[m - 1] == Y[n - 1])
            return 1 + superSeq(X, Y, m - 1, n - 1);

        return 1
            + Math.Min(superSeq(X, Y, m - 1, n),
                       superSeq(X, Y, m, n - 1));
    }

    // Driver Code
    public static void Main()
    {
        String X = "AGGTAB";
        String Y = "GXTXAYB";
        Console.WriteLine(
            "Length of the shortest supersequence is: "
            + superSeq(X, Y, X.Length, Y.Length));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Naive recursive PHP program to find
// length of the shortest supersequence

function superSeq($X, $Y, $m, $n)
{
    if (!$m)
        return $n;
    if (!$n)
        return $m;

    if ($X[$m - 1] == $Y[$n - 1])
        return 1 + superSeq($X, $Y, $m - 1, $n - 1);

    return 1 + min(superSeq($X, $Y, $m - 1, $n),
                   superSeq($X, $Y, $m, $n - 1));
}

// Driver Code
$X = "AGGTAB";
$Y = "GXTXAYB";
echo "Length of the shortest supersequence is ",
       superSeq($X, $Y, strlen($X), strlen($Y));

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// A Naive recursive javascript program to find
// length of the shortest supersequence

function superSeq(X, Y , m , n)
{
    if (m == 0)
        return n;
    if (n == 0)
        return m;

    if (X.charAt(m - 1) == Y.charAt(n - 1))
        return 1 + superSeq(X, Y, m - 1, n - 1);

    return 1
        + Math.min(superSeq(X, Y, m - 1, n),
                   superSeq(X, Y, m, n - 1));
}

// Driver code
var X = "AGGTAB";
var Y = "GXTXAYB";
document.write(
    "Length of the shortest"
    + "supersequence is "
    + superSeq(X, Y, X.length, Y.length));

// This code contributed by Princi Singh

</script>
```

**输出:**

```
Length of the shortest supersequence is 9
```

上述解的时间复杂度指数 O(2 <sup>min(m，n)</sup> )。由于存在[重叠子问题](https://www.geeksforgeeks.org/dynamic-programming-set-1/)，我们可以使用动态规划有效地解决这个递归问题。下面是基于动态编程的实现。这个解决方案的时间复杂度是 O(mn)。

## C++

```
// A dynamic programming based C program to
// find length of the shortest supersequence
#include <bits/stdc++.h>
using namespace std;

// Returns length of the shortest
// supersequence of X and Y
int superSeq(char* X, char* Y, int m, int n)
{
    int dp[m + 1][n + 1];

    // Fill table in bottom up manner
    for (int i = 0; i <= m; i++) {
        for (int j = 0; j <= n; j++) {
            // Below steps follow above recurrence
            if (!i)
                dp[i][j] = j;
            else if (!j)
                dp[i][j] = i;
            else if (X[i - 1] == Y[j - 1])
                dp[i][j] = 1 + dp[i - 1][j - 1];
            else
                dp[i][j]
                    = 1 + min(dp[i - 1][j], dp[i][j - 1]);
        }
    }

    return dp[m][n];
}

// Driver Code
int main()
{
    char X[] = "AGGTAB";
    char Y[] = "GXTXAYB";
    cout << "Length of the shortest supersequence is "
         << superSeq(X, Y, strlen(X), strlen(Y));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A dynamic programming based Java program to
// find length of the shortest supersequence
class GFG {

    // Returns length of the shortest
    // supersequence of X and Y
    static int superSeq(String X, String Y, int m, int n)
    {
        int[][] dp = new int[m + 1][n + 1];

        // Fill table in bottom up manner
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                // Below steps follow above recurrence
                if (i == 0)
                    dp[i][j] = j;
                else if (j == 0)
                    dp[i][j] = i;
                else if (X.charAt(i - 1) == Y.charAt(j - 1))
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                else
                    dp[i][j] = 1
                               + Math.min(dp[i - 1][j],
                                          dp[i][j - 1]);
            }
        }

        return dp[m][n];
    }

    // Driver Code
    public static void main(String args[])
    {
        String X = "AGGTAB";
        String Y = "GXTXAYB";
        System.out.println(
            "Length of the shortest supersequence is "
            + superSeq(X, Y, X.length(), Y.length()));
    }
}

// This article is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# A dynamic programming based python program
# to find length of the shortest supersequence

# Returns length of the shortest supersequence of X and Y

def superSeq(X, Y, m, n):
    dp = [[0] * (n + 2) for i in range(m + 2)]

    # Fill table in bottom up manner
    for i in range(m + 1):
        for j in range(n + 1):

            # Below steps follow above recurrence
            if (not i):
                dp[i][j] = j
            elif (not j):
                dp[i][j] = i

            elif (X[i - 1] == Y[j - 1]):
                dp[i][j] = 1 + dp[i - 1][j - 1]

            else:
                dp[i][j] = 1 + min(dp[i - 1][j],
                                   dp[i][j - 1])

    return dp[m][n]

# Driver Code
X = "AGGTAB"
Y = "GXTXAYB"
print("Length of the shortest supersequence is %d"
      % superSeq(X, Y, len(X), len(Y)))

# This code is contributed by Ansu Kumari
```

## C#

```
// A dynamic programming based C# program to
// find length of the shortest supersequence
using System;

class GFG {
    // Returns length of the shortest
    // supersequence of X and Y
    static int superSeq(String X, String Y, int m, int n)
    {
        int[, ] dp = new int[m + 1, n + 1];

        // Fill table in bottom up manner
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                // Below steps follow above recurrence
                if (i == 0)
                    dp[i, j] = j;
                else if (j == 0)
                    dp[i, j] = i;
                else if (X[i - 1] == Y[j - 1])
                    dp[i, j] = 1 + dp[i - 1, j - 1];
                else
                    dp[i, j] = 1
                               + Math.Min(dp[i - 1, j],
                                          dp[i, j - 1]);
            }
        }

        return dp[m, n];
    }

    // Driver code
    public static void Main()
    {
        String X = "AGGTAB";
        String Y = "GXTXAYB";
        Console.WriteLine(
            "Length of the shortest supersequence is "
            + superSeq(X, Y, X.Length, Y.Length));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A dynamic programming based PHP program to
// find length of the shortest supersequence

// Returns length of the shortest
// supersequence of X and Y
function superSeq($X, $Y, $m, $n)
{
    $dp = array_fill(0, $m + 1,
          array_fill(0, $n + 1, 0));

    // Fill table in bottom up manner
    for ($i = 0; $i <= $m; $i++)
    {
        for ($j = 0; $j <= $n; $j++)
        {

            // Below steps follow above recurrence
            if (!$i)
                $dp[$i][$j] = $j;
            else if (!$j)
                $dp[$i][$j] = $i;
            else if ($X[$i - 1] == $Y[$j - 1])
                    $dp[$i][$j] = 1 + $dp[$i - 1][$j - 1];
            else
                    $dp[$i][$j] = 1 + min($dp[$i - 1][$j],
                                          $dp[$i][$j - 1]);
        }
    }

    return $dp[$m][$n];
}

// Driver Code
$X = "AGGTAB";
$Y = "GXTXAYB";
echo "Length of the shortest supersequence is " .
      superSeq($X, $Y, strlen($X), strlen($Y));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// A dynamic programming based javascript program to
// find length of the shortest supersequence  
// Returns length of the shortest
    // supersequence of X and Y
    function superSeq(X, Y, m, n)
    {
        var dp = Array(m+1).fill(0).map(x => Array(n+1).fill(0));

        // Fill table in bottom up manner
        for (var i = 0; i <= m; i++)
        {
            for (var j = 0; j <= n; j++)
            {

                // Below steps follow above recurrence
                if (i == 0)
                    dp[i][j] = j;
                else if (j == 0)
                    dp[i][j] = i;
                else if (X.charAt(i - 1) == Y.charAt(j - 1))
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                else
                    dp[i][j] = 1
                               + Math.min(dp[i - 1][j],
                                          dp[i][j - 1]);
            }
        }
        return dp[m][n];
    }

    // Driver Code
    var X = "AGGTAB";
    var Y = "GXTXAYB";
    document.write(
        "Length of the shortest supersequence is "
        + superSeq(X, Y, X.length, Y.length));

// This code is contributed by 29AjayKumar
</script>
```

**输出:**

```
Length of the shortest supersequence is 9
```

感谢[高拉夫·阿希瓦尔](https://www.facebook.com/COOL.DUDE.BORN.NUD3?fref=ts)提出这个解决方案。

**自上而下的记忆方法:**
这个想法是遵循简单的递归解决方案，使用查找表来避免重新计算。在计算输入的结果之前，我们检查结果是否已经计算。如果已经计算过，我们就返回那个结果。

## C++

```
// A dynamic programming based python program
// to find length of the shortest supersequence

// Returns length of the
// shortest supersequence of X and Y
#include <bits/stdc++.h>
using namespace std;

int superSeq(string X, string Y, int n, int m,
             vector<vector<int> > lookup)
{

    if (m == 0 || n == 0) {
        lookup[n][m] = n + m;
    }

    if (lookup[n][m] == 0)
        if (X[n - 1] == Y[m - 1]) {
            lookup[n][m]
                = superSeq(X, Y, n - 1, m - 1, lookup) + 1;
        }

        else {
            lookup[n][m]
                = min(superSeq(X, Y, n - 1, m, lookup) + 1,
                      superSeq(X, Y, n, m - 1, lookup) + 1);
        }

    return lookup[n][m];
}

// Driver Code
int main()
{
    string X = "AGGTB";
    string Y = "GXTXAYB";

    vector<vector<int> > lookup(
        X.size() + 1, vector<int>(Y.size() + 1, 0));

    cout << "Length of the shortest supersequence is "
         << superSeq(X, Y, X.size(), Y.size(), lookup)
         << endl;

    return 0;
}

    // This code is contributed by niraj gusain
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A dynamic programming based python program
// to find length of the shortest supersequence

// Returns length of the
// shortest supersequence of X and Y
import java.util.*;

class GFG {

    static int superSeq(String X, String Y, int n, int m,
                        int[][] lookup)
    {

        if (m == 0 || n == 0) {
            lookup[n][m] = n + m;
        }

        if (lookup[n][m] == 0)
            if (X.charAt(n - 1) == Y.charAt(m - 1)) {
                lookup[n][m]
                    = superSeq(X, Y, n - 1, m - 1, lookup)
                      + 1;
            }

            else {
                lookup[n][m] = Math.min(
                    superSeq(X, Y, n - 1, m, lookup) + 1,
                    superSeq(X, Y, n, m - 1, lookup) + 1);
            }

        return lookup[n][m];
    }

    // Driver Code
    public static void main(String[] args)
    {
        String X = "AGGTB";
        String Y = "GXTXAYB";

        int[][] lookup
            = new int[X.length() + 1][Y.length() + 1];

        System.out.print(
            "Length of the shortest supersequence is "
            + superSeq(X, Y, X.length(), Y.length(), lookup)
            + "\n");
    }
}

// This code contributed by umadevi9616
```

## 蟒蛇 3

```
# A dynamic programming based python program
# to find length of the shortest supersequence

# Returns length of the
# shortest supersequence of X and Y

import numpy as np
def superSeq(X,Y,n,m,lookup):

    if m==0 or n==0:
        lookup[n][m] = n+m

    if (lookup[n][m] == 0):    
        if X[n-1]==Y[m-1]:
            lookup[n][m] = superSeq(X,Y,n-1,m-1,lookup)+1

        else:
            lookup[n][m] = min(superSeq(X,Y,n-1,m,lookup)+1,
                               superSeq(X,Y,n,m-1,lookup)+1)

    return lookup[n][m]

# Driver Code
X = "AGGTAB"
Y = "GXTXAYB"

lookup = np.zeros([len(X)+1,len(Y)+1])
print("Length of the shortest supersequence is {}"
      .format(superSeq(X,Y,len(X),len(Y),lookup)))

# This code is contributed by Tanmay Ambadkar
```

## C#

```
// A dynamic programming based python program
// to find length of the shortest supersequence

// Returns length of the
// shortest supersequence of X and Y
using System;

public class GFG {

    static int superSeq(String X, String Y, int n,
                        int m, int[,] lookup)
    {

        if (m == 0 || n == 0) {
            lookup[n, m] = n + m;
        }

        if (lookup[n, m] == 0)
            if (X[n - 1] == Y[m - 1]) {
                lookup[n, m] = superSeq(X, Y, n - 1,
                                       m - 1, lookup) + 1;
            }

            else {
                lookup[n, m] = Math.Min(superSeq(X, Y, n - 1, m, lookup) +
                                       1, superSeq(X, Y, n, m - 1, lookup) +
                                       1);
            }

        return lookup[n, m];
    }

    // Driver Code
    public static void Main(String[] args) {
        String X = "AGGTB";
        String Y = "GXTXAYB";

        int[,] lookup = new int[X.Length + 1,Y.Length + 1];

        Console.Write(
                "Length of the shortest supersequence is " +
          superSeq(X, Y, X.Length, Y.Length, lookup) + "\n");
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// A dynamic programming based python program
// to find length of the shortest supersequence

// Returns length of the
// shortest supersequence of X and Y

    function superSeq( X,  Y , n , m,  lookup) {

        if (m == 0 || n == 0) {
            lookup[n][m] = n + m;
        }

        if (lookup[n][m] == 0)
            if (X.charAt(n - 1) == Y.charAt(m - 1)) {
                lookup[n][m] = superSeq(X, Y, n - 1, m - 1, lookup) + 1;
            }

            else {
                lookup[n][m] = Math.min(superSeq(X, Y, n - 1, m, lookup) + 1, superSeq(X, Y, n, m - 1, lookup) + 1);
            }

        return lookup[n][m];
    }

    // Driver Code

        var X = "AGGTB";
        var Y = "GXTXAYB";

        var lookup = Array(X.length + 1).fill().map(()=>Array(Y.length + 1).fill(0));

        document.write(
                "Length of the shortest supersequence is "
                + superSeq(X, Y, X.length, Y.length, lookup) + "\n");

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
Length of the shortest supersequence is 9.0
```

**练习:**
扩展上述程序打印最短超序列，也使用[功能打印 LCS](https://www.geeksforgeeks.org/printing-longest-common-subsequence/) 。
[解决方案请参考打印最短公共超序列](https://www.geeksforgeeks.org/shortest-possible-combination-two-strings/)
**参考:**
[https://en.wikipedia.org/wiki/Shortest_common_supersequence](https://en.wikipedia.org/wiki/Shortest_common_supersequence)
如有不正确的地方请写评论，或者想分享更多以上讨论话题的信息