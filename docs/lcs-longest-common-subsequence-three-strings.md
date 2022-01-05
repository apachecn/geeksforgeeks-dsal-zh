# 三个字符串的 LCS(最长公共子序列)

> 原文:[https://www . geesforgeks . org/LCS-最长-公共-子序列-三个字符串/](https://www.geeksforgeeks.org/lcs-longest-common-subsequence-three-strings/)

给定 3 根长度均为< 100,the task is to find the longest common sub-sequence in all three given sequences.
**的弦，例如:**

```
Input : str1 = "geeks"  
        str2 = "geeksfor"  
        str3 = "geeksforgeeks"
Output : 5
Longest common subsequence is "geeks"
i.e., length = 5

Input : str1 = "abcd1e2"  
        str2 = "bc12ea"  
        str3 = "bd1ea"
Output : 3
Longest common subsequence is "b1e" 
i.e. length = 3.
```

这个问题只是[LCS](https://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/)T2 的一个扩展让输入序列为 X[0..m-1]，Y[0..n-1]和 Z[0..长度分别为 m、n 和 o 的 o-1]。并让 L(X[0..m-1]，Y[0..n-1]，Z[0..o-1])是三个序列 X、Y 和 z 的 LCS 长度。下面是实现:

```
The idea is to take a 3D array to store the 
length of common subsequence in all 3 given 
sequences i. e., L[m + 1][n + 1][o + 1]

1- If any of the string is empty then there
   is no common subsequence at all then
           L[i][j][k] = 0

2- If the characters of all sequences match
   (or X[i] == Y[j] ==Z[k]) then
        L[i][j][k] = 1 + L[i-1][j-1][k-1]

3- If the characters of both sequences do 
   not match (or X[i] != Y[j] || X[i] != Z[k] 
   || Y[j] !=Z[k]) then
        L[i][j][k] = max(L[i-1][j][k], 
                         L[i][j-1][k], 
                         L[i][j][k-1])
```

下面是上述想法的实现。

## C++

```
// C++ program to find LCS of three strings
#include<bits/stdc++.h>
using namespace std;

/* Returns length of LCS for X[0..m-1], Y[0..n-1]
   and Z[0..o-1] */
int lcsOf3( string X, string Y, string Z, int m,
                               int n, int o)
{
    int L[m+1][n+1][o+1];

    /* Following steps build L[m+1][n+1][o+1] in
       bottom up fashion. Note that L[i][j][k]
       contains length of LCS of X[0..i-1] and
       Y[0..j-1]  and Z[0.....k-1]*/
    for (int i=0; i<=m; i++)
    {
        for (int j=0; j<=n; j++)
        {
            for (int k=0; k<=o; k++)
            {
                if (i == 0 || j == 0||k==0)
                    L[i][j][k] = 0;

                else if (X[i-1] == Y[j-1] && X[i-1]==Z[k-1])
                    L[i][j][k] = L[i-1][j-1][k-1] + 1;

                else
                    L[i][j][k] = max(max(L[i-1][j][k],
                                         L[i][j-1][k]),
                                     L[i][j][k-1]);
            }
        }
    }

    /* L[m][n][o] contains length of LCS for
      X[0..n-1] and Y[0..m-1] and Z[0..o-1]*/
    return L[m][n][o];
}

/* Driver program to test above function */
int main()
{
    string X = "AGGT12";
    string Y = "12TXAYB";
    string Z = "12XBA";

    int m = X.length();
    int n = Y.length();
    int o = Z.length();

    cout << "Length of LCS is " << lcsOf3(X, Y,
                                    Z, m, n, o);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find LCS of three strings
public class LCS_3Strings {

    /* Returns length of LCS for X[0..m-1], Y[0..n-1]
       and Z[0..o-1] */
    static int lcsOf3(String X, String Y, String Z, int m,
                                   int n, int o)
    {
        int[][][] L = new int[m+1][n+1][o+1];

        /* Following steps build L[m+1][n+1][o+1] in
           bottom up fashion. Note that L[i][j][k]
           contains length of LCS of X[0..i-1] and
           Y[0..j-1]  and Z[0.....k-1]*/
        for (int i=0; i<=m; i++)
        {
            for (int j=0; j<=n; j++)
            {
                for (int k=0; k<=o; k++)
                {
                    if (i == 0 || j == 0||k==0)
                        L[i][j][k] = 0;

                    else if (X.charAt(i - 1) == Y.charAt(j - 1)
                                && X.charAt(i - 1)==Z.charAt(k - 1))
                        L[i][j][k] = L[i-1][j-1][k-1] + 1;

                    else
                        L[i][j][k] = Math.max(Math.max(L[i-1][j][k],
                                             L[i][j-1][k]),
                                         L[i][j][k-1]);
                }
            }
        }

        /* L[m][n][o] contains length of LCS for
          X[0..n-1] and Y[0..m-1] and Z[0..o-1]*/
        return L[m][n][o];
    }

    /* Driver program to test above function */
    public static void main(String args[])
    {
        String X = "AGGT12";
        String Y = "12TXAYB";
        String Z = "12XBA";

        int m = X.length();
        int n = Y.length();
        int o = Z.length();

        System.out.println("Length of LCS is " +
                                lcsOf3(X, Y,Z, m, n, o));

    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python program to find
# LCS of three strings

# Returns length of LCS
# for X[0..m-1], Y[0..n-1]
# and Z[0..o-1]
def lcsOf3(X, Y, Z, m, n, o):

    L = [[[0 for i in range(o+1)] for j in range(n+1)]
         for k in range(m+1)]

    ''' Following steps build L[m+1][n+1][o+1] in
    bottom up fashion. Note that L[i][j][k]
    contains length of LCS of X[0..i-1] and
    Y[0..j-1] and Z[0.....k-1] '''
    for i in range(m+1):
        for j in range(n+1):
            for k in range(o+1):
                if (i == 0 or j == 0 or k == 0):
                    L[i][j][k] = 0

                elif (X[i-1] == Y[j-1] and
                      X[i-1] == Z[k-1]):
                    L[i][j][k] = L[i-1][j-1][k-1] + 1

                else:
                    L[i][j][k] = max(max(L[i-1][j][k],
                    L[i][j-1][k]),
                                    L[i][j][k-1])

    # L[m][n][o] contains length of LCS for
    # X[0..n-1] and Y[0..m-1] and Z[0..o-1]
    return L[m][n][o]

# Driver program to test above function

X = 'AGGT12'
Y = '12TXAYB'
Z = '12XBA'

m = len(X)
n = len(Y)
o = len(Z)

print('Length of LCS is', lcsOf3(X, Y, Z, m, n, o))

# This code is contributed by Soumen Ghosh.                   
```

## C#

```
// C# program to find
// LCS of three strings
using System;

class GFG
{

    /* Returns length of LCS
    for X[0..m-1], Y[0..n-1]
    and Z[0..o-1] */
    static int lcsOf3(String X, String Y,
                      String Z, int m,
                      int n, int o)
    {
        int [,,]L = new int[m + 1,
                            n + 1, o + 1];

        /* Following steps build
        L[m+1][n+1][o+1] in bottom
        up fashion. Note that
        L[i][j][k] contains length
        of LCS of X[0..i-1] and
        Y[0..j-1] and Z[0.....k-1]*/
        for (int i = 0; i <= m; i++)
        {
            for (int j = 0; j <= n; j++)
            {
                for (int k = 0; k <= o; k++)
                {
                    if (i == 0 ||
                        j == 0 || k == 0)
                        L[i, j, k] = 0;

                    else if (X[i - 1] == Y[j - 1] &&
                             X[i - 1] == Z[k - 1])
                        L[i, j, k] = L[i - 1,
                                       j - 1,
                                       k - 1] + 1;

                    else
                        L[i, j, k] = Math.Max(Math.Max(L[i - 1, j, k],
                                                       L[i, j - 1, k]),
                                                       L[i, j, k - 1]);
                }
            }
        }

        /* L[m][n][o] contains length
        of LCS for X[0..n-1] and
        Y[0..m-1] and Z[0..o-1]*/
        return L[m, n, o];
    }

    // Driver Code
    public static void Main()
    {
        string X = "AGGT12";
        string Y = "12TXAYB";
        string Z = "12XBA";

        int m = X.Length;
        int n = Y.Length;
        int o = Z.Length;

        Console.Write("Length of LCS is " +
                       lcsOf3(X, Y, Z, m, n, o));
    }
}

// This code is contributed
// by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// LCS of three strings

/* Returns length of LCS for
X[0..m-1], Y[0..n-1] and Z[0..o-1] */
function lcsOf3($X, $Y, $Z,
                $m, $n, $o)
{
    $L[$m + 1][$n + 1][$o + 1] = array(array(array()));

    /* Following steps build
    L[m+1][n+1][o+1] in bottom
    up fashion. Note that
    L[i][j][k] contains length
    of LCS of X[0..i-1] and
    Y[0..j-1] and Z[0.....k-1]*/
    for ($i = 0; $i <= $m; $i++)
    {
        for ($j = 0; $j <= $n; $j++)
        {
            for ($k = 0; $k <= $o; $k++)
            {
                if ($i == 0 || $j == 0||$k == 0)
                    $L[$i][$j][$k] = 0;

                else if ($X[$i - 1] == $Y[$j - 1] &&
                         $X[$i - 1] == $Z[$k - 1])
                    $L[$i][$j][$k] = $L[$i - 1][$j - 1][$k - 1] + 1;

                else
                    $L[$i][$j][$k] = max(max($L[$i - 1][$j][$k],
                                              $L[$i][$j - 1][$k]),
                                             $L[$i][$j][$k - 1]);
            }
        }
    }

    /* L[m][n][o] contains length
    of LCS for X[0..n-1] and
    Y[0..m-1] and Z[0..o-1]*/
    return $L[$m][$n][$o];
}

// Driver code
$X = "AGGT12";
$Y = "12TXAYB";
$Z = "12XBA";

$m = strlen($X);
$n = strlen($Y);
$o = strlen($Z);

echo "Length of LCS is " .
      lcsOf3($X, $Y, $Z,
             $m, $n, $o);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript program to find LCS of three strings   

    /* Returns length of LCS for X[0..m-1], Y[0..n-1]
       and Z[0..o-1] */
    function lcsOf3(X,Y,Z,m,n,o)
    {
        let L = new Array(m + 1);
        for(let i = 0; i < m + 1; i++)
        {
            L[i] = new Array(n + 1);
            for(let j = 0; j < n + 1; j++)
            {
                L[i][j] = new Array(o + 1);
                for(let k = 0; k < o + 1; k++)
                {
                    L[i][j][k] = 0;
                }
            }
        }

        /* Following steps build L[m+1][n+1][o+1] in
           bottom up fashion. Note that L[i][j][k]
           contains length of LCS of X[0..i-1] and
           Y[0..j-1]  and Z[0.....k-1]*/
        for (let i = 0; i <= m; i++)
        {
            for (let j = 0; j <= n; j++)
            {
                for (let k = 0; k <= o; k++)
                {
                    if (i == 0 || j == 0 || k == 0)
                        L[i][j][k] = 0;

                    else if (X[i - 1] == Y[j - 1]
                                && X[i - 1] == Z[k - 1])
                        L[i][j][k] = L[i - 1][j - 1][k - 1] + 1;

                    else
                        L[i][j][k] = Math.max(Math.max(L[i - 1][j][k],
                                             L[i][j - 1][k]),
                                         L[i][j][k - 1]);
                }
            }
        }

        /* L[m][n][o] contains length of LCS for
          X[0..n-1] and Y[0..m-1] and Z[0..o-1]*/
        return L[m][n][o];
    }

     /* Driver program to test above function */
     let X = "AGGT12";
     let Y = "12TXAYB";
     let Z = "12XBA";
     let m = X.length;
    let n = Y.length;
    let o = Z.length;

    document.write("Length of LCS is " +
                            lcsOf3(X, Y,Z, m, n, o));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Length of LCS is 2
```

**另一种方法:**(使用递归)

## C++

```
// C++ program to find LCS of three strings
#include<bits/stdc++.h>
using namespace std;

    string X = "AGGT12";
    string Y = "12TXAYB";
    string Z = "12XBA";

int dp[100][100][100];

/* Returns length of LCS for X[0..m-1], Y[0..n-1]
and Z[0..o-1] */
int lcsOf3(int i, int j,int k)
{
    if(i==-1||j==-1||k==-1)
        return 0;
    if(dp[i][j][k]!=-1)
        return dp[i][j][k];

    if(X[i]==Y[j] && Y[j]==Z[k])
        return dp[i][j][k] = 1+lcsOf3(i-1,j-1,k-1);
    else
        return dp[i][j][k] = max(max(lcsOf3(i-1,j,k),
                            lcsOf3(i,j-1,k)),lcsOf3(i,j,k-1));
}

// Driver code
int main()
{
    memset(dp, -1,sizeof(dp));
    int m = X.length();
    int n = Y.length();
    int o = Z.length();

    cout << "Length of LCS is " << lcsOf3(m-1,n-1,o-1);
// this code is contributed by Kushdeep Mittal
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find LCS of three strings
class GFG
{

    static String X = "AGGT12";
    static String Y = "12TXAYB";
    static String Z = "12XBA";

    static int[][][] dp = new int[100][100][100];

    /* Returns length of LCS for X[0..m-1],
    Y[0..n-1] and Z[0..o-1] */
    static int lcsOf3(int i, int j, int k)
    {
        if (i == -1 || j == -1 || k == -1)
        {
            return 0;
        }
        if (dp[i][j][k] != -1)
        {
            return dp[i][j][k];
        }

        if (X.charAt(i) == Y.charAt(j) &&
            Y.charAt(j) == Z.charAt(k))
        {
            return dp[i][j][k] = 1 + lcsOf3(i - 1, j - 1, k - 1);
        } else {
            return dp[i][j][k] = Math.max(Math.max(lcsOf3(i - 1, j, k),
                                lcsOf3(i, j - 1, k)),
                                lcsOf3(i, j, k - 1));
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        for (int i = 0; i < 100; i++)
        {
            for (int j = 0; j < 100; j++)
            {
                for (int k = 0; k < 100; k++)
                {
                    dp[i][j][k] = -1;
                }
            }
        }
        int m = X.length();
        int n = Y.length();
        int o = Z.length();

        System.out.print("Length of LCS is "
                + lcsOf3(m - 1, n - 1, o - 1));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find LCS of
# three strings
X = "AGGT12"
Y = "12TXAYB"
Z = "12XBA"

dp = [[[-1 for i in range(100)]
           for j in range(100)]
           for k in range(100)]

# Returns length of LCS for
# X[0..m-1], Y[0..n-1] and Z[0..o-1]
def lcsOf3(i, j, k) :

    if(i == -1 or j == -1 or k == -1) :
        return 0

    if(dp[i][j][k] != -1) :
        return dp[i][j][k]

    if(X[i] == Y[j] and Y[j] == Z[k]) :
        dp[i][j][k] = 1 + lcsOf3(i - 1,
                                 j - 1, k - 1)
        return dp[i][j][k]

    else :
        dp[i][j][k] = max(max(lcsOf3(i - 1, j, k),
                              lcsOf3(i, j - 1, k)),
                              lcsOf3(i, j, k - 1))

        return dp[i][j][k]

# Driver code
if __name__ == "__main__" :
    m = len(X)
    n = len(Y)
    o = len(Z)

    print("Length of LCS is",
           lcsOf3(m - 1, n - 1, o - 1))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find LCS of three strings
using System;

class GFG
{
static string X = "AGGT12";
static string Y = "12TXAYB";
static string Z = "12XBA";

static int[,,] dp = new int[100, 100, 100];

/* Returns length of LCS for X[0..m-1],
Y[0..n-1] and Z[0..o-1] */
static int lcsOf3(int i, int j, int k)
{
    if(i == -1 || j == -1 || k == -1)
        return 0;
    if(dp[i, j, k] != -1)
        return dp[i, j, k];

    if(X[i] == Y[j] && Y[j] == Z[k])
        return dp[i, j, k] = 1 + lcsOf3(i - 1, j - 1, k - 1);
    else
        return dp[i, j, k] = Math.Max(Math.Max(lcsOf3(i - 1, j, k),
                                               lcsOf3(i, j - 1, k)),
                                               lcsOf3(i, j, k - 1));
}

// Driver code
static void Main()
{
    for(int i = 0; i < 100; i++)
        for(int j = 0; j < 100; j++)
            for(int k = 0; k < 100; k++)
                dp[i, j, k] = -1;
    int m = X.Length;
    int n = Y.Length;
    int o = Z.Length;

    Console.Write("Length of LCS is " +
                   lcsOf3(m - 1, n - 1, o - 1));
}
}

// This code is contributed by DrRoot_
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find LCS of three strings

    $X = "AGGT12";
    $Y = "12TXAYB";
    $Z = "12XBA";

    $dp=array_fill(0, 100, array_fill(0, 100, array_fill(0, 100, -1)));

/* Returns length of LCS for X[0..m-1], Y[0..n-1]
and Z[0..o-1] */
function lcsOf3($i, $j, $k)
{
    global $dp, $X, $Y, $Z;
    if($i == -1 || $j == -1 || $k == -1)
        return 0;
    if($dp[$i][$j][$k] != -1)
        return $dp[$i][$j][$k];

    if($X[$i] == $Y[$j] && $Y[$j] == $Z[$k])
        return $dp[$i][$j][$k] = 1+lcsOf3($i - 1, $j - 1, $k - 1);
    else
        return $dp[$i][$j][$k] = max(max(lcsOf3($i - 1, $j, $k),
                            lcsOf3($i, $j - 1, $k)), lcsOf3($i, $j, $k - 1));
}

// Driver code
    $m = strlen($X);
    $n = strlen($Y);
    $o = strlen($Z);

    echo "Length of LCS is ".lcsOf3($m - 1, $n - 1, $o - 1);

// This code is contributed by mits

?>
```

## java 描述语言

```
<script>
// Java program to find LCS of three strings

let X = "AGGT12";
let Y = "12TXAYB";
let Z = "12XBA";

let dp = new Array(100);
for(let i=0;i<100;i++)
{
    dp[i]=new Array(100);
    for(let j=0;j<100;j++)
    {
        dp[i][j]=new Array(100);
        for(let k=0;k<100;k++)
        {
            dp[i][j][k]=-1;
        }
    }
}

/* Returns length of LCS for X[0..m-1],
    Y[0..n-1] and Z[0..o-1] */
function lcsOf3(i,j,k)
{
     if (i == -1 || j == -1 || k == -1)
        {
            return 0;
        }
        if (dp[i][j][k] != -1)
        {
            return dp[i][j][k];
        }

        if (X[i] == Y[j] &&
            Y[j] == Z[k])
        {
            return dp[i][j][k] = 1 + lcsOf3(i - 1, j - 1, k - 1);
        } else {
            return dp[i][j][k] = Math.max(Math.max(lcsOf3(i - 1, j, k),
                                lcsOf3(i, j - 1, k)),
                                lcsOf3(i, j, k - 1));
        }
}

// Driver code

        let m = X.length;
        let n = Y.length;
        let o = Z.length;

        document.write("Length of LCS is "
                + lcsOf3(m - 1, n - 1, o - 1));

// This code is contributed by rag2127
</script>
```

**输出:**

```
Length of LCS is 2
```

本文由 [**萨希尔·查布拉(akku)**](https://practice.geeksforgeeks.org/user-profile.php?user=sahil_coder) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。