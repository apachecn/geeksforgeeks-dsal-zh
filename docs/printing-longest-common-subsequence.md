# 打印最长公共子序列

> 原文:[https://www . geesforgeks . org/printing-最长-公共-子序列/](https://www.geeksforgeeks.org/printing-longest-common-subsequence/)

给定两个序列，打印两个序列中最长的子序列。
**例:**
LCS 对于输入序列“ABCDGH”和“AEDFHR”是长度为 3 的“ADH”。
LCS 对于输入序列“AGGTAB”和“GXTXAYB”是长度为 4 的“GTAB”。
我们在[之前的帖子](https://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/)中讨论了[最长公共子序列(LCS)](https://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/) 的问题。那里讨论的函数主要是求 LCS 的长度。为了求出 LCS 的长度，构造了一个 2D 表 L[][]。在这篇文章中，讨论了构建和打印 LCS 的功能。
以下是打印 LCS 的详细算法。它使用相同的 2D 表 L[][]。
**1)** 使用[上一篇文章](https://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence)中讨论的步骤构建 L[m+1][n+1]。
**2)** 值 L[m][n]包含 LCS 长度。创建一个长度等于 lcs 加 1 的字符数组 lcs[](多一个存储\0)。
**2)** 从 L[m][n]开始遍历 2D 阵。对每个单元格 L[i][j]
执行以下操作….. **a)** 如果对应于 L[i][j]的字符(在 X 和 Y 中)相同(或 X[i-1] == Y[j-1])，则包括该字符作为 LCS 的一部分。
….. **b)** 否则比较 L[i-1][j]和 L[i][j-1]的值，向更大的值的方向走。
下表(取自[维基](http://en.wikipedia.org/wiki/Longest_common_subsequence_problem))显示了上述算法遵循的步骤(高亮显示)。

<figure class="table">

|   | Zero | one | Two | three | four | five | six | seven |
| 一座岛 | M | Z | J | A | W | X | U |
| Zero | 一座岛 | **0** | Zero | Zero | Zero | Zero | Zero | Zero | Zero |
| one | X | Zero | Zero | Zero | Zero | Zero | Zero | one | one |
| Two | M | Zero | **1** | one | one | one | one | one | one |
| three | J | Zero | one | one | **2** | Two | Two | Two | Two |
| four | Y | Zero | one | one | Two | Two | Two | Two | Two |
| five | A | Zero | one | one | Two | **3** | three | three | three |
| six | U | Zero | one | one | Two | three | three | three | **4** |
| seven | Z | Zero | one | Two | Two | three | three | three | four |

下面是上述方法的实现。

## C++

```
/* Dynamic Programming implementation of LCS problem */
#include<iostream>
#include<cstring>
#include<cstdlib>
using namespace std;

/* Returns length of LCS for X[0..m-1], Y[0..n-1] */
void lcs( char *X, char *Y, int m, int n )
{
  int L[m+1][n+1];

  /* Following steps build L[m+1][n+1] in bottom up fashion. Note
    that L[i][j] contains length of LCS of X[0..i-1] and Y[0..j-1] */
  for (int i=0; i<=m; i++)
  {
    for (int j=0; j<=n; j++)
    {
      if (i == 0 || j == 0)
        L[i][j] = 0;
      else if (X[i-1] == Y[j-1])
        L[i][j] = L[i-1][j-1] + 1;
      else
        L[i][j] = max(L[i-1][j], L[i][j-1]);
    }
  }

  // Following code is used to print LCS
  int index = L[m][n];

  // Create a character array to store the lcs string
  char lcs[index+1];
  lcs[index] = '\0'; // Set the terminating character

  // Start from the right-most-bottom-most corner and
  // one by one store characters in lcs[]
  int i = m, j = n;
  while (i > 0 && j > 0)
  {
    // If current character in X[] and Y are same, then
    // current character is part of LCS
    if (X[i-1] == Y[j-1])
    {
      lcs[index-1] = X[i-1]; // Put current character in result
      i--; j--; index--;     // reduce values of i, j and index
    }

    // If not same, then find the larger of two and
    // go in the direction of larger value
    else if (L[i-1][j] > L[i][j-1])
      i--;
    else
      j--;
  }

  // Print the lcs
  cout << "LCS of " << X << " and " << Y << " is " << lcs;
}

/* Driver program to test above function */
int main()
{
  char X[] = "AGGTAB";
  char Y[] = "GXTXAYB";
  int m = strlen(X);
  int n = strlen(Y);
  lcs(X, Y, m, n);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Dynamic Programming implementation of LCS problem in Java
import java.io.*;

class  LongestCommonSubsequence
{
    // Returns length of LCS for X[0..m-1], Y[0..n-1]
    static void lcs(String X, String Y, int m, int n)
    {
        int[][] L = new int[m+1][n+1];

        // Following steps build L[m+1][n+1] in bottom up fashion. Note
        // that L[i][j] contains length of LCS of X[0..i-1] and Y[0..j-1]
        for (int i=0; i<=m; i++)
        {
            for (int j=0; j<=n; j++)
            {
                if (i == 0 || j == 0)
                    L[i][j] = 0;
                else if (X.charAt(i-1) == Y.charAt(j-1))
                    L[i][j] = L[i-1][j-1] + 1;
                else
                    L[i][j] = Math.max(L[i-1][j], L[i][j-1]);
            }
        }

        // Following code is used to print LCS
        int index = L[m][n];
        int temp = index;

        // Create a character array to store the lcs string
        char[] lcs = new char[index+1];
        lcs[index] = '\u0000'; // Set the terminating character

        // Start from the right-most-bottom-most corner and
        // one by one store characters in lcs[]
        int i = m;
        int j = n;
        while (i > 0 && j > 0)
        {
            // If current character in X[] and Y are same, then
            // current character is part of LCS
            if (X.charAt(i-1) == Y.charAt(j-1))
            {
                // Put current character in result
                lcs[index-1] = X.charAt(i-1);

                // reduce values of i, j and index
                i--;
                j--;
                index--;    
            }

            // If not same, then find the larger of two and
            // go in the direction of larger value
            else if (L[i-1][j] > L[i][j-1])
                i--;
            else
                j--;
        }

        // Print the lcs
        System.out.print("LCS of "+X+" and "+Y+" is ");
        for(int k=0;k<=temp;k++)
            System.out.print(lcs[k]);
    }

    // driver program
    public static void main (String[] args)
    {
        String X = "AGGTAB";
        String Y = "GXTXAYB";
        int m = X.length();
        int n = Y.length();
        lcs(X, Y, m, n);
    }
}

// Contributed by Pramod Kumar
```

## 计算机编程语言

```
# Dynamic programming implementation of LCS problem

# Returns length of LCS for X[0..m-1], Y[0..n-1]
def lcs(X, Y, m, n):
    L = [[0 for x in xrange(n+1)] for x in xrange(m+1)]

    # Following steps build L[m+1][n+1] in bottom up fashion. Note
    # that L[i][j] contains length of LCS of X[0..i-1] and Y[0..j-1]
    for i in xrange(m+1):
        for j in xrange(n+1):
            if i == 0 or j == 0:
                L[i][j] = 0
            elif X[i-1] == Y[j-1]:
                L[i][j] = L[i-1][j-1] + 1
            else:
                L[i][j] = max(L[i-1][j], L[i][j-1])

    # Following code is used to print LCS
    index = L[m][n]

    # Create a character array to store the lcs string
    lcs = [""] * (index+1)
    lcs[index] = ""

    # Start from the right-most-bottom-most corner and
    # one by one store characters in lcs[]
    i = m
    j = n
    while i > 0 and j > 0:

        # If current character in X[] and Y are same, then
        # current character is part of LCS
        if X[i-1] == Y[j-1]:
            lcs[index-1] = X[i-1]
            i-=1
            j-=1
            index-=1

        # If not same, then find the larger of two and
        # go in the direction of larger value
        elif L[i-1][j] > L[i][j-1]:
            i-=1
        else:
            j-=1

    print "LCS of " + X + " and " + Y + " is " + "".join(lcs)

# Driver program
X = "AGGTAB"
Y = "GXTXAYB"
m = len(X)
n = len(Y)
lcs(X, Y, m, n)

# This code is contributed by BHAVYA JAIN
```

## C#

```
// Dynamic Programming implementation
// of LCS problem in C#
using System;

class GFG
{
    // Returns length of LCS for X[0..m-1], Y[0..n-1]
    static void lcs(String X, String Y, int m, int n)
    {
        int[,] L = new int[m+1, n+1];

        // Following steps build L[m+1][n+1] in
        // bottom up fashion. Note that L[i][j]
        // contains length of LCS of X[0..i-1]
        // and Y[0..j-1]
        for (int i = 0; i <= m; i++)
        {
            for (int j = 0; j <= n; j++)
            {
                if (i == 0 || j == 0)
                    L[i, j] = 0;
                else if (X[i-1] == Y[j-1])
                    L[i, j] = L[i-1, j-1] + 1;
                else
                    L[i, j] = Math.Max(L[i-1, j], L[i, j-1]);
            }
        }

        // Following code is used to print LCS
        int index = L[m, n];
        int temp = index;

        // Create a character array
        // to store the lcs string
        char[] lcs = new char[index+1];

        // Set the terminating character
        lcs[index] = '\0';

        // Start from the right-most-bottom-most corner
        // and one by one store characters in lcs[]
        int k = m, l = n;
        while (k > 0 && l > 0)
        {
            // If current character in X[] and Y
            // are same, then current character
            // is part of LCS
            if (X[k-1] == Y[l-1])
            {
                // Put current character in result
                lcs[index-1] = X[k-1];

                // reduce values of i, j and index
                k--;
                l--;
                index--;    
            }

            // If not same, then find the larger of two and
            // go in the direction of larger value
            else if (L[k-1, l] > L[k, l-1])
                k--;
            else
                l--;
        }

        // Print the lcs
        Console.Write("LCS of " + X + " and " + Y + " is ");
        for(int q = 0; q <= temp; q++)
            Console.Write(lcs[q]);
    }

    // Driver program
    public static void Main ()
    {
        String X = "AGGTAB";
        String Y = "GXTXAYB";
        int m = X.Length;
        int n = Y.Length;
        lcs(X, Y, m, n);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Dynamic Programming implementation of LCS problem

// Returns length of LCS for X[0..m-1], Y[0..n-1]
function lcs( $X, $Y, $m, $n )
{
    $L = array_fill(0, $m + 1,
         array_fill(0, $n + 1, NULL));

    /* Following steps build L[m+1][n+1] in bottom
       up fashion. Note that L[i][j] contains length
       of LCS of X[0..i-1] and Y[0..j-1] */
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

    // Following code is used to print LCS
    $index = $L[$m][$n];
    $temp = $index;

    // Create a character array to store the lcs string
    $lcs = array_fill(0, $index + 1, NULL);
    $lcs[$index] = ''; // Set the terminating character

    // Start from the right-most-bottom-most corner
    // and one by one store characters in lcs[]
    $i = $m;
    $j = $n;
    while ($i > 0 && $j > 0)
    {
        // If current character in X[] and Y are same,
        // then current character is part of LCS
        if ($X[$i - 1] == $Y[$j - 1])
        {
            // Put current character in result
            $lcs[$index - 1] = $X[$i - 1];
            $i--;
            $j--;
            $index--;    // reduce values of i, j and index
        }

        // If not same, then find the larger of two
        // and go in the direction of larger value
        else if ($L[$i - 1][$j] > $L[$i][$j - 1])
            $i--;
        else
            $j--;
    }

    // Print the lcs
    echo "LCS of " . $X . " and " . $Y . " is ";
    for($k = 0; $k < $temp; $k++)
        echo $lcs[$k];
}

// Driver Code
$X = "AGGTAB";
$Y = "GXTXAYB";
$m = strlen($X);
$n = strlen($Y);
lcs($X, $Y, $m, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
function ReverseString(str) {
   return str.split('').reverse().join('')
}

function max(a, b)
{
    if (a > b)
        return a;
    else
        return b;
}
function printLCS(str1, str2) {
    var len1 = str1.length;
    var len2 = str2.length;
    var lcs = new Array(len1 + 1);
    for (var i = 0; i <= len1; i++) {
        lcs[i] = new Array(len2 + 1)
    }
    for (var i = 0; i <= len1; i++) {
        for (var j = 0; j <= len2; j++) {
            if (i == 0 || j == 0) {
                lcs[i][j] = 0;
            }
            else {
                if (str1[i - 1] == str2[j - 1]) {
                    lcs[i][j] = 1 + lcs[i - 1][j - 1];
                }
                else {
                    lcs[i][j] = max(lcs[i][j - 1], lcs[i - 1][j]);
                }
            }
        }}

        var n = lcs[len1][len2];
         document.write("Length of common subsequence is: " +
         n + "<br>" + "The subsequence is : ");
        var str="";
       var i = len1;
       var j = len2;
       while(i>0&&j>0)
       {
            if(str1[i - 1] == str2[j - 1])
            {
                str += str1[i - 1];
                i--;
                j--;
            }
            else{
            if(lcs[i][j-1]>lcs[i-1][j])
            {
                j--;
            }
            else
            {
                i--;
            }
            }
        }
       return ReverseString(str);
    }
    var str1 = "AGGTAB";
    var str2 = "GXTXAYB";
    document.write(printLCS(str1, str2));

    // This code is contributed by akshitsaxenaa09
</script>
```

**输出:**

```
LCS of AGGTAB and GXTXAYB is GTAB
```

**参考文献:**
[http://en . Wikipedia . org/wiki/long _ common _ subsequence _ problem](http://en.wikipedia.org/wiki/Longest_common_subsequence_problem)
如发现有不正确的地方，或想分享以上讨论话题的更多信息，请写评论

</figure>